# Hooks

[Send mail on error ref:](https://stackoverflow.com/a/32996815/116239)

```bash
# Compress Tar file
tar -czf logfiles.tar.gz *.log

TAR_EXIT_STATUS=$?

# Start service
service $SERVICE start

SERVICE_EXIT_STATUS=$?

# mail if failed
if [ $TAR_EXIT_STATUS -ne 0 ] || [ $SERVICE_EXIT_STATUS -ne 0 ];then
    mail -s "Task failed" | user@domain.com << "the task failed"
fi;
```

## Adding version number to constant in file

Put this in a file called `pre-commit` in `.git/hooks/`

```
#!/bin/sh
# To enable this hook, rename this file to "pre-commit".

sed -i.bak "s/export const VERSION = \".*\";/export const VERSION = \"`git describe --tags --long`\";/g" src/app/data.ts
```

Using Tags we will get the version number, the commits away from the tag and sha signature.  This is used on `src/app/data.ts` to substite the old value with a nnew one
Make sure the permissions on the file you created are the same as the samples in that directory. 

```javascript
// data.ts
// sed -i.bak "s/export const VERSION = \".*\";/export const VERSION = \"`git describe --tags --long`\";/g" src/app/data.ts

export const VERSION = "v1.1-0-gb8e3f21";
```
