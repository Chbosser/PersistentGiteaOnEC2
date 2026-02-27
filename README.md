# PersistentGiteaOnEC2
Gitea on an AWS EC2 instance using Docker. All persistent application data is stored on a separate EBS volume. Includes a small S-3 backup and restore work that uses AWS CLI 

Commands for Formatting and Mounting EBS:
```
sudo lsblk
sudo mkfs.ext4 /dev/nvme1n1
mkdir -p ˜/data
sudo mount /dev/nvme1n1 ˜/data
df -h
sudo chown -R $USER:$USER /data // Command that makes me the owner of the newly mounted EBS volume
```

Commands to make the mount persistent
```
sudo nano /etc/fstab
# UUID: 05260b75-e275-42ad-9d9f-40e6ee78f5ec /home/ubuntu/data ext4 defaults,nofail 0 2
sudo mount -a
df -h

```

Commands to 
```

```
