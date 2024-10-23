## Create RAID0 array on 4 nvme drives

1. Format the 4 nvme drives
```bash
lsblk;
for drive in nvme0n1 nvme1n1 nvme2n1 nvme3n1;do sudo mkfs.ext4 /dev/"$drive";done
```

2. Install `mdadm`
```bash
sudo apt install mdadm;
mdadm --version;
```

3. Create RAID0 array
```bash
sudo mdadm --create --verbose /dev/md0 --level=0 --raid-devices=4 /dev/nvme0n1 /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1;
```

4. Check the array
```bash
cat /proc/mdstat;
sudo mdadm --detail /dev/md0;
```

5. Format the array
```bash
sudo mkfs.ext4 /dev/md0;
```

6. Mount the array
```
mount /dev/md0 /mydata;
```
