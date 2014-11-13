Tool to backup RDS logs to S3 `{bucket_upload}{DB-name}/LOG_TYPE/YEAR/MONTH/DAY`

## REQUIREMENTS
ruby > 1.9.3

### jq http://stedolan.github.io/jq/
```
sudo yum install jq
sudo apt-get install jq
```

### aws-cli http://aws.amazon.com/cli/
well configured (either with IAM role or KEY/SECRET)

## INSTALL
adjust `@bucket_upload` and `@DBInstanceIdentifiers` variable in the script file
```
cp backup_rotated_logs /usr/bin/backup_rotated_logs
chmod +x /usr/bin/backup_rotated_logs
```
### with cron:
```
cp rds_backup.cron /etc/cron.hourly/rds_backup.cron
chmod +x /etc/cron.hourly/rds_backup.cron
```


reload cron (depends of your system)
`/etc/init.d/crond restart`
