##Looping through files

```bash`
for filepath in `find $1 -name "*.js"`;
do
    echo "$filepath"
done;
```
