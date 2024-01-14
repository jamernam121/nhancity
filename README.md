1: wget -O bios64.bin "https://github.com/BlankOn/ovmf-blobs/raw/master/bios64.bin"
2 : wget -O win.iso "https://go.microsoft.com/fwlink/p/?LinkID=2195443&clcid=0x409&culture=en-us&country=US"
3 : wget -O ngrok.tgz "https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz"
4 : tar -xf ngrok.tgz
5 : rm -rf ngrok.tgz
6 : ./ngrok config add-authtoken 2J9yysLsB8D6w1CHb3S3yiRD2KU_4zTNpGTNxH7HRFhwgeTzi
7 : ./ngrok tcp 5900
8 : sudo apt update
9 : sudo apt install qemu-kvm -y
10 : qemu-img create -f raw win.img
11 : qemu-img create -f raw win.img 64G
12 :sudo qemu-system-x86_64 -m 4G -cpu host -boot order=c -drive file=win.iso,media=cdrom -drive file=win.img,format=raw -device usb-ehci,id=usb,bus=pci.0,addr=0x4 -device usb-tablet -vnc :0 -smp cores=4 -device rtl8139,netdev=n0 -netdev user,id=n0 -vga qxl -accel kvm -bios bios64.bin
