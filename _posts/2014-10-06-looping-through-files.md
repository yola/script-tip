---
layout: post
title: "Looping through files"
---

##Looping through files


```bash
#!/bin/sh

for filepath in `find $1 -name "*.js"`;
do
    echo "$filepath"
done;
```
