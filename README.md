🔹 How to Use for backup and restore

Make it executable:

chmod +x jenkins_volume_manager.sh


Run the script:

./jenkins_volume_manager.sh


You’ll see a menu:

1) Backup Jenkins Volume
2) Restore Jenkins Volume
3) Exit


Choose 1 → creates a timestamped backup in ./backups/

Choose 2 → restores a selected backup file into your Jenkins container volume

Choose 3 → exits the script# jenkins-docker-demo
jenkins-docker-demo
