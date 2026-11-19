# WORKING WITH EBS
## NAME: Mohamed Mubeen A
## REG NO: 212225040241

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs
<img width="1112" height="956" alt="Screenshot 2026-11-18 150740" src="https://github.com/user-attachments/assets/1868dbdb-4e5b-473c-bda5-ea25e8d54537" />

<img width="1203" height="953" alt="Screenshot 2026-11-18 151037" src="https://github.com/user-attachments/assets/f765e001-f23a-4b4f-8ff8-19d4da84b8fc" />

<img width="1196" height="962" alt="Screenshot 2026-11-18 151245" src="https://github.com/user-attachments/assets/fc559873-01d8-4b54-96ea-eee6aee86701" />

<img width="1917" height="963" alt="Screenshot 2026-11-18 151517" src="https://github.com/user-attachments/assets/6fe302aa-b554-4047-abef-bdc172932f52" />

<img width="1202" height="952" alt="Screenshot 2026-11-18 151737" src="https://github.com/user-attachments/assets/a6ff7625-739b-42c5-8615-d339c9c69ddf" />

<img width="1917" height="960" alt="Screenshot 2026-11-18 151904" src="https://github.com/user-attachments/assets/f7eaf534-0549-4591-8666-d85ec2361eb6" />

<img width="1206" height="956" alt="Screenshot 2026-11-18 152310" src="https://github.com/user-attachments/assets/70baa310-d5ee-40cf-af03-af6a8b5d0840" />

<img width="1202" height="948" alt="Screenshot 2026-11-18 152458" src="https://github.com/user-attachments/assets/1c22b0f4-3db0-4b92-b2cc-aa017bf9b3fc" />

<img width="402" height="427" alt="Screenshot 2026-11-18 152651" src="https://github.com/user-attachments/assets/d6fa9f84-6367-475f-b556-e26c8c469709" />


## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
