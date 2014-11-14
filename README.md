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
Create log folder for this one.
`mkdir /var/log/cron-log/`

Edit your crontab and add:
```
20 * * * */usr/bin/backup_rotated_logs >> /var/log/cron-log/rds_backup.log 2>&1
```

/!\ As AWS RDS don't write instantly logs, it is recommended to trigger the script after 15min of the hour otherwise
you could have double entry for a same log. (as the check is based on the last written information)
