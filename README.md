# PersistentGiteaOnEC2
Gitea on an AWS EC2 instance using Docker. All persistent application data is stored on a separate EBS volume. Includes a small S-3 backup and restore work that uses AWS CLI 

# Step By Step Deployment Instructions
---

First I started by making an EC2 Instance and installing Docker on it. Then I set up the EBS on AWS and mounted it using these commands:

Commands for Formatting and Mounting EBS:
```
sudo lsblk
sudo mkfs.ext4 /dev/nvme1n1
mkdir -p ˜/data
sudo mount /dev/nvme1n1 ˜/data
df -h
sudo chown -R $USER:$USER /data // Command that makes me the owner of the newly mounted EBS volume
```
In order for the EBS volume to stay mounted to the EC2 instance I used these commands

Commands to make the mount persistent
```
sudo nano /etc/fstab
# UUID: 05260b75-e275-42ad-9d9f-40e6ee78f5ec /home/ubuntu/data ext4 defaults,nofail 0 2
sudo mount -a
df -h

```
Then I set up a docker file and ran gitea on a container
Commands to run Docker
```
sudo docker build -t my-gitea .
sudo docker run -d -p 3000:3000 -v ~/data:/data --name gitea-container my-gitea
sudo docker start gitea-container
```

