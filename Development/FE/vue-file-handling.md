---
title: Vue File Upload/Download
description: 
published: true
date: 2023-04-07T02:02:34.428Z
tags: development, front, fe, vue, file
editor: markdown
dateCreated: 2023-04-07T02:01:25.684Z
---

# File Handling
## File Upload
- script 
  - FormData에 Name/Data를 append 한다.
  - Header에 파일 형식에 맞는 Content-Type를 추가한다.

```js
// js func. (vue 1.5)
uploadFileHandler(){
  this.isSelecting = true;
  window.addEventListener('focus', () => {
    this.isSelecting = false
  }, { once: true });
  this.$refs.uploader.click();
},
uploadFile(ev){
  const file = ev.target.files[0]
  this.fileName = file.name // Change input state

  var frm = new FormData();
  frm.append("files", file, file.name)
  // append(name, value, filename) // filename is optional

  axios.post(`$(URL)/${this.restTargetNo}/file`, frm, {
    headers: {
      'Content-Type': 'multipart/form-data'
    }
  })
    .then((response) => {
    console.log(response)
    // TODO 응답 처리 (to. jy)
  })
    .catch((error) => {
    // TODO 예외 처리 (to. jy)
  }).finally(() => {
    this.getFileList()
    this.fileName = ""
  })
},
```

- template
```html
<!-- template -->
<v-layout row>
  <v-flex xs4>
    <v-text-field
      @click="uploadFileHandler"
      v-model="fileName"
      prepend-icon="attach_file">
      <v-icon>file_upload</v-icon>FILE
    </v-text-field>
    <input 
      ref="uploader" 
      class="d-none" 
      type="file"
      @change="uploadFile"
      accept="application/multipart/form-data"
    >
  </v-flex>
  <v-flex xs4></v-flex>
</v-layout>
```


## File Download
- script 
  - **responseType을 'blob'로 지정한다.**
  	- 지정하지 않을 경우, 다운로드 완료 후 파일 실행이 정상적으로 수행되지 않는다.

```js
downloadFile(fileNo, fileNm){
  axios.get(`$(URL)/${this.restTargetNo}/file/${fileNo}`,
        {headers: authHeader(), responseType: 'blob'}
    	).then(response => {
    
    // local에서 url을 생성하여 다운로드 실행
    console.log(response.data)
    const url = window.URL.createObjectURL(new Blob([response.data]));
    const link = document.createElement('a');
    link.href = url;
    link.setAttribute('download', fileNm); //or any other extension
    document.body.appendChild(link);
    link.click();
  })
},
```

- template
```html
<v-layout row>
  <v-flex xs12>
    <div>
      <v-sheet
         color="grey lighten-4"
         max-width="70%"
         style="padding:4px 8px 4px 8px;"
      >
        <v-chip
          v-for="upload in uploadList" v-bind:key="upload.fileNo"
          class="ma-2"
          color="gray"
          label
          outlined
        > <div @click="downloadFile(upload.fileNo, upload.fileNm)">{{ upload.fileNm }}</div>
          <v-icon small @click="deleteFile(upload.fileNo)" style="padding-left:12px">delete</v-icon>
        </v-chip>
      </v-sheet>
    </div>
  </v-flex>
</v-layout>
```