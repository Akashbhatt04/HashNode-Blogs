---
title: "Mini Project - To Automate the Backup of your Work in Shell Script"
seoTitle: "Mini Project - To Automate the Backup of your Work in Shell Script"
seoDescription: "Mini Project - To Automate the Backup of your Work in Shell Script"
datePublished: Wed Mar 29 2023 15:10:57 GMT+0000 (Coordinated Universal Time)
cuid: clfttqr6p000309lahqfj5c6c
slug: mini-project-to-automate-the-backup-of-your-work-in-shell-script
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680102575541/32551a8b-2524-4b85-aaa6-bd3d29fc0817.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1680102617509/d07ac6be-8247-4e47-a779-7fcd5ca61875.jpeg
tags: devops, cronjob, shell-script

---

One of the simplest ways to back up a system is using a shell script. For example, a script can be used to **configure which directories to back up and pass those directories as arguments to the tar utility, which creates an archive file**.

First, create a new file with a .sh extension, for example, "backup\_script.sh".

Open the file in your favourite text editor, and enter the following code:

```plaintext
#!/bin/bash
```

# Define variables

```plaintext
backup_dir="/path/to/backup/directory" 
```

```plaintext
backup_file="backup-$(date +%Y-%m-%d-%H-%M-%S).tar.gz" 
```

```plaintext
source_dir="/path/to/source/directory"
```

# Create the backup directory if it doesn't exist

```plaintext
mkdir -p "$backup_dir"
```

# Create backup file

```plaintext
tar -czvf "$backup_dir/$backup_file" "$source_dir"
```

# Remove old backups (keep only the last 7 days)

```plaintext
find "$backup_dir" -type f -mtime +7 -delete 
```

Save the file and exit the editor.

Make the script executable by running the following command in the terminal:

```plaintext
chmod +x backup_script.sh 
```

Now, you can schedule the script to run automatically using cron. Open the crontab file by running the following command:

```plaintext
crontab -e 
```

Add the following line at the end of the file to schedule the script to run every day at midnight

```plaintext
0 0 * * * /path/to/backup_script.sh 
```

Save the crontab file and exit the editor. That's it! Now the script will run every day at midnight and create a compressed backup of the specified directory. The script will also delete any backups older than 7 days to save disk space.