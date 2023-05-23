---
title: Python Function for Querying to Presto
description: 
published: true
date: 2023-05-23T06:56:45.039Z
tags: sql, presto
editor: markdown
dateCreated: 2023-05-23T06:56:45.039Z
---

# Python Connection & Querying with Pandas

```python
def presto_query(query):

     cursor = presto.connect(host='10.162.51.21', port='9088').cursor()

     # execute a query and get a result as a DataFrame

     cursor.execute(query)
     col_names = [ desc[0] for desc in cursor.description ]
     result = pd.DataFrame(cursor.fetchall(), columns=col_names)

     cursor.close()

     return result
```