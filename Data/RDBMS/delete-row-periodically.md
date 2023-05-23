---
title: Delete Row Periodically
description: 
published: true
date: 2023-05-23T07:00:18.993Z
tags: mysql, sql
editor: markdown
dateCreated: 2023-05-23T07:00:18.993Z
---

# Query
```sql
# RUN CRON or SCRIPT or ELSE ...
DELETE FROM table_name WHERE DATE_SUB(DATE(NOW()), INTERVAL 180 day) > DATE(date_column);
```