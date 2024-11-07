# Backup-Script-Linux
# enter the code root mode 
cd /home/ranjeet/Desktop
ls
touch /home/ranjeet/Desktop/backup_prd.sh
vi /home/ranjeet/Desktop/backup_prd.sh

# go to backup_prd.sh file and save the code 
# enter the code

#!/bin/bash

# Variables
SOURCE_DIR="/home/ranjeet/Desktop/scripts"      # Path to the "scripts" folder on Desktop
BACKUP_DIR="/home/ranjeet/backups"              # Backup location in the home directory
DATE=$(date +'%Y-%m-%d_%H-%M-%S')            
BACKUP_FILE="$BACKUP_DIR/backup_$DATE.tar.gz"

# Create the backup directory if it doesn't exist
mkdir -p $BACKUP_DIR

# Exclude directories that shouldn't be backed up
EXCLUDE_DIRS=(
    --exclude=/proc
    --exclude=/sys
    --exclude=/dev
    --exclude=/run
    --exclude=/tmp
    --exclude=/mnt
    --exclude=/media
    --exclude=/lost+found
)

# Create the backup, excluding unnecessary directories
tar "${EXCLUDE_DIRS[@]}" -czf $BACKUP_FILE $SOURCE_DIR

# Optional: Keep only the last 7 backups (delete older ones)
find $BACKUP_DIR -type f -name "backup_*.tar.gz" -mtime +7 -exec rm {} \;

# Echo backup status
if [ $? -eq 0 ]; then
    echo "Backup successful: $BACKUP_FILE"
else
    echo "Backup failed!"
fi
# save the file and exit the backup_prd.sh file
# exit the file

chmod +x /home/ranjeet/Desktop/backup_prd.sh
cd /home/ranjeet/Desktop
./backup_prd.sh
sudo ./backup_prd.sh
ls /home/ranjeet/backups     



