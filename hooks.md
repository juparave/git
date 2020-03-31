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
