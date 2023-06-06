reference artile:
    https://qiita.com/taiyaki8926/items/18bb7b8d0d8c2109dedc

1. update / upgrade apt
```
sudo apt -y update
sudo apt -y upgrade
sudo reboot -f
```

2. reinstall open-vm-tools-desktop & fuse
if you cannnot reinstall GUI options, please run
```
sudo apt install -y --reinstall open-vm-tools-desktop fuse3
```

3. make bash script

```bash
#!/bin/zsh

vmware-hgfsclient | while read folder; do
  mkdir -p "/mnt/hgfs/${folder}"
  umount -f "/mnt/hgfs/${folder}" 2>/dev/null
  vmhgfs-fuse -o allow_other -o auto_unmount ".host:/${folder}" "/mnt/hgfs/${folder}"
done

sleep 2s
```

4. automatically run above script
```
sudo su
crontab -e
```
add bottom line
```
@reboot /home/{username}/.mount-shared-folders.sh
```

you can access share host PC folder `/mnt/hgfs`
