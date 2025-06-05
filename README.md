# Flash Raspberry Pi Pico with UF2

---

## Build the UF2 file with TinyGO

- Install TinyGO Extension in VSCode.
- Run `Command + Shit + P` and select the TinyGO target for PICO(or desired)
- Write the code
- Build the `UF2` export

```shell
tinygo build -o firmware.uf2 -target=pico main.go
```

---

- Enter Bootloader Mode

- Disconnect the Pico from USB.

- Hold the BOOTSEL button (keep it pressed).

- Plug the Pico into your Ubuntu machine via USB.

- Release BOOTSEL after connecting.

---

Check if Pico is Detected(No `/mnt/RPI-RP2` appears, but `/dev/sdb1` should be available)

```shell
lsblk -f
```

Then

```shell
sudo mkdir -p /mnt/RPI-RP2  # Create mount point
sudo mount /dev/sdb1 /mnt/RPI-RP2  # Replace `sda1` if different
```

- Check again the `lsblk -f`. The `/mnt/RPI-RP2` should be dispplayed in front of `/dev/sdb1`. 

- After that, copy the build `UF2` file to the mount volume(here `/mnt/RPI-RP2`).

- It will flash the the new `UF2` automatically.

```shell
sudo cp firmware.uf2 /mnt/RPI-RP2/
```

Finally, Safely unmount

```shell
sudo umount /mnt/RPI-RP2
```