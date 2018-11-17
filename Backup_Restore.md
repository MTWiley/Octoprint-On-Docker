## Backup

tar -zcvf $(date +%Y-%m-%d)-octoprint_data.tar.gz -C /docker/octoprint/data .

## Restore

tar -xvf YYYY-MM-DD-octoprint_data.tar.gz -C /docker/octoprint/data
