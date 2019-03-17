
Building:
./compile.sh docker KERNEL_ONLY=yes KERNEL_CONFIGURE=no BOARD=helios4 BRANCH=next

https://docs.armbian.com/Developer-Guide_Building-with-Docker/

Changed kernel config:
Device Drivers
  Multimedia support (on)
    Analog TV Support (on)
    Media USB Adapters (on)
      Hauppage HD PVR support=M
Networking support
  Networking options
    IP: WireGuard secure network tunnel (off)

After build, copy config from output/config/ to userpatches/

Can diff user config vs. baseline:
diff config/kernel/linux-mvebu-default.config userpatches/linux-mvebu-default.config

Kernel config options:
VIDEO_HDPVR
  - depends on VIDEO_DEV && VIDEO_V4L2

VIDEO_DEV
  - depends on MEDIA_SUPPORT
  - depends on MEDIA_CAMERA_SUPPORT || MEDIA_ANALOG_TV_SUPPORT || MEDIA_RADIO_SUPPORT || MEDIA_SDR_SUPPORT

MEDIA_SUPPORT
MEDIA_ANALOG_TV_SUPPORT
MEDIA_USB_SUPPORT

Disabled wireguard due to warning as error failing build
