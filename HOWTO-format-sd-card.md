# How to format a SD card

If you want to format a SD card that was already flashed with a Raspberry Pi image on it you can do it with the following command:

## Mac OSX

```bash
df
diskutil eraseDisk FAT32 NEU MBRFormat /dev/disk2
```

## Windows

```cmd
diskpart
list disk
select disk 6
list partition
clean
create partition primary
select partition 1
format fs=fat32 label="neu" quick
exit
```
