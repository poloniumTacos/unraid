#!/bin/bash

# Define the directories to clean
MOVIES_DIR="/mnt/user/data/usenet/complete/movies"
SHOWS_DIR="/mnt/user/data/usenet/complete/shows"

# Initialize counters
movies_removed=0
shows_removed=0

# Find and delete files older than 1 hour in movies directory
while IFS= read -r folder; do
    ((movies_removed++))
    #rm -rf "$folder"
    echo "Removed movie folder: $folder"  # Echo the folder name
done < <(find "$MOVIES_DIR" -type d -mmin +60)

echo " "

# Find and delete files older than 1 hour in shows directory
while IFS= read -r folder; do
    ((shows_removed++))
    #rm -rf "$folder"
    echo "Removed show folder: $folder"  # Echo the folder name
done < <(find "$SHOWS_DIR" -type d -mmin +60)

# Notify the user
/usr/local/emhttp/plugins/dynamix/scripts/notify -e "User Scripts" -s "Usenet Cleanup Summary" -d "Movies removed: $movies_removed<br>Shows removed: $shows_removed"
