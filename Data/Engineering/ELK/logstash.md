---
title: Configuration of Logstash
description: 
published: true
date: 2023-04-24T00:27:05.419Z
tags: 
editor: markdown
dateCreated: 2023-03-31T06:29:13.444Z
---

# Logstash 설정하기
Logstash는 input / filter / output으로 구성되며, 각 데이터들의 변환 과정을 거쳐 ES 또는 사용자가 정의하는 저장소로 전송할 수 있도록 한다.

## Install Logstash
Logstash는 [링크](https://www.elastic.co/kr/downloads/logstash)에서 다운로드 받을 수 있다.
```shell
curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-8.7.0-linux-x86_64.tar.gz
tar xzvf logstash-8.7.0-linux-x86_64.tar.gz
```

## Config Format
```ruby
input {
	stdin {
  }
}
filter {
}
output {
}
```

## logstash.yml
```yml
# 자동 config 적용 설정
config.reload.automatic: true
# 자동 config 갱신 시간 설정
config.reload.interval: 3s
```

## pipelines.yml
```yml
- pipeline.id: $ID
  path.config: "$DIR"
```

## execute Logstash
```shell
./bin/logstash -f $CONFIG_FILE
./bin/logstash # logstash.yml | pipeline.yml 파일에서 설정 및 대상을 지정했을 경우
```

## Samples of Config
- [logstash-patterns-core](https://github.com/logstash-plugins/logstash-patterns-core)
  - grok patterns

1. `tcp.conf`
```ruby
input {
	tcp {
  	port => 9000
  }
}
filter {
	grok {
  	match => { "message" => "Hello %{WORD:name}" }
  }
}
output {
	stdout {
  	codec => rubydebug
  }
}
```

2. `weblog.conf`
```ruby
input {
	tcp {
  	port => 9000
    type => "apache"
  }
}
filter {
	if [type] == "apache" {
  	grok {
    	match => {
      	message => "%{COMBINEDAPACHELOG}"
        remove_field => "message"
      }
    }
    
    geoip {
    	source => "clientip"
      fields => ["city_name", "country_name", "location", "region_name"]
    }
    
    date {
    	match => ["timestamp", "dd/MMM/yyyy:HH:mm:ss Z"]
      remove_field => "timestamp"
    }
  }
}
output {
	elasticsearch {
  	hosts => ["localhost:9200"]
  }
}
```


3. `twitter`
```ruby
input {
	twitter {
  	consumer_key => ""
    consumer_secret => ""
    oauth_token => ""
    oauth_token_secret => ""
    keywords => ["elastic", "logstash"]
    full_tweet => true
    use_samples => true
  }
}
output {
	elasticsearch {
  	hosts => ["loaclhost:9200"]
  }
}
```

4. `beats`
```ruby
input {
	beats {
  	port => 5044
  }
}
filter {
	grok {
  	match => {
    	"message" => "%{COMBINEDAPACHELOG}"
    }
    geoip {
    	source => "clientip"
    }
  }
}
output {
	elasticsearch {
  	hosts => ["loaclhost:9200"]
  }
  
  s3 {
  	access_key_id => ""
    secret_access_key => ""
    region => "eu-west-1"
    bucket => "bucket"
    size_file => 2048
    time_file => 5
  }
}
```

5. `database`
```ruby
input {
	jdbc {
  	jdbc_user => "mysql"
    schedule => "* * * * *"
    parameters => { "company" => "elastic" }
    use_column_value => true
    tracking_column => id
    
    statement => "SELECT * FROM table WHERE id > :sql_last_value"
  }
}
output {
	elasticsearch {
  	hosts => ["loaclhost:9200"]
  }
}
```


## Logstash stats
```shell
curl localhost:9600/_node?pretty
curl localhost:9600/_node/stats?pretty
```


# auditbeat 로그 연동

<br>

## logstash 설정

```ruby
# vi ./config/auditbeat.conf
input {
  beats {
    port => 5044
  }
}

output {
  elasticsearch {
    hosts => "https://localhost:9200"
    user => "$ES_USER_ID"
    password => "$ES_USER_PASSWORD"
    # `OR` api_key => "xxxx:xxxx"
    data_stream => true
    ssl => true
    cacert => "$ES_CERTIFICATION_LOCATION"
  }
}
```

## auditbeat 설정
logstash의 ssl 설정이 있을 경우, 관련 설정 포함 필요
```yml
output.logstash:
  hosts: ["$HOST_IP:5044"]
```

```yml
# 다음 에러가 발생하는 경우, 아래 옵션을 disable 해줘야한다.
# index management requested but the Elasticsearch output is not configured/enabled 
# 추가로, auditbeat setup -e 로 실행할 경우 에러가 발생하는데, auditbeat -e 로 실행하면 정상적으로 스트림이 이동한다.
# 상기 에러는 추가 확인이 필요함
#
#
# ======================= Elasticsearch template setting =======================
#setup.template.settings:
#  index.number_of_shards: 1
```
