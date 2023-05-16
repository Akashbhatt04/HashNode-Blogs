---
title: "Shell Scripting Scenarion Based Question and Answer"
datePublished: Tue May 16 2023 21:03:41 GMT+0000 (Coordinated Universal Time)
cuid: clhqrh9qi00060al9dfixgbck
slug: shell-scripting-scenarion-based-question-and-answer
tags: devops, shell-script

---

**Q1: How can you write a shell script to check if a file exists and display its content if it does?**

Ans: You can achieve this using conditional statements and file handling in shell scripting. Here's an example:

```bash
#!/bin/bash

filename="example.txt"

if [ -e "$filename" ]; then
    echo "File exists. Content:"
    cat "$filename"
else
    echo "File does not exist."
fi
```

In this script, we set the filename variable to the name of the file we want to check. The -e flag is used within the conditional statement to check if the file exists. If it does, we print a message indicating that the file exists and then display its content using the cat command. Otherwise, we display an error message indicating that the file does not exist.

You can modify the value of the filename variable to match the file you want to check in your specific scenario.

**Q2: You have been tasked with automating a backup process on a Linux server. The backup should be taken daily at midnight and should include the contents of the /home directory. The backup should be stored in /backup directory with a filename that includes the current date and time. Write a shell script to automate this process.**

Answer:

Here is an example shell script that will automate the backup process:

```bash
#!/bin/bash

# Set the backup directory
backup_dir="/backup"

# Set the source directory
source_dir="/home"

# Set the backup file name with current date and time
backup_file="backup-$(date +%Y-%m-%d-%H-%M-%S).tar.gz"

# Create the backup directory if it doesn't exist
mkdir -p "$backup_dir"

# Create the backup archive
tar czf "$backup_dir/$backup_file" "$source_dir"

# Display a message indicating the backup is complete
echo "Backup completed successfully: $backup_dir/$backup_file"
```

Explanation:

The first line `#!/bin/bash` tells the system that this is a Bash shell script.

The next three lines define the backup directory, source directory, and backup file name. The `$(date +%Y-%m-%d-%H-%M-%S)` command is used to get the current date and time in the specified format.

The `mkdir -p "$backup_dir"` command creates the backup directory if it doesn't already exist.

The `tar czf "$backup_dir/$backup_file" "$source_dir"` command creates the backup archive. The `c` option tells tar to create a new archive, the `z` option tells tar to compress the archive using gzip, and the `f` option specifies the filename of the archive.

Finally, the `echo` command displays a message indicating that the backup is complete and specifies the location of the backup file.

To schedule the backup to run daily at midnight, you can use the `cron` scheduling tool. To edit the crontab for the current user, run `crontab -e` and add the following line:

```bash
0 0 * * * /path/to/backup-script.sh
```

This will run the backup script at midnight every day. Be sure to replace `/path/to/backup-script.sh` with the actual path to the script.

**Q3: Scenario: You are a system administrator responsible for automating routine tasks on a Linux server. One of your tasks is to write a shell script that checks the disk usage of a specified directory and sends an email notification if it exceeds a certain threshold.**

**Question: How would you write a shell script to monitor disk usage and send email notifications?**

Answer:

```bash
#!/bin/bash

# Set the directory to monitor and the threshold in percentage
directory="/path/to/directory"
threshold=90

# Get the current disk usage of the directory
usage=$(df -h "$directory" | awk 'NR==2{print $5}' | cut -d'%' -f1)

# Check if the usage exceeds the threshold
if [ "$usage" -gt "$threshold" ]; then
    # Send an email notification
    email_subject="Disk Usage Alert"
    email_body="The disk usage of directory $directory has exceeded the threshold. Current usage: $usage%."
    recipient="admin@example.com"
    echo "$email_body" | mail -s "$email_subject" "$recipient"
fi
```

In this script:

Specify the directory you want to monitor by assigning its path to the directory variable.

Set the threshold value as a percentage (e.g., 90%) by assigning it to the threshold variable.

Use the df command to get the disk usage of the specified directory. The output is piped to awk and cut to extract the percentage value.

Compare the current disk usage ($usage) with the threshold ($threshold) using an if condition.

If the usage exceeds the threshold, compose an email message with the relevant information and assign it to the email\_body variable.

Specify the email subject (email\_subject), recipient (recipient), and use the mail command to send the email with the subject, body, and recipient.

You can schedule this script to run periodically using tools like cron to automate the monitoring and email notifications for disk usage.