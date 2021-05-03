# frida-ios-dump

Pull a decrypted IPA from a jailbroken device.
Tested on iPhone 6S with iOS 14.4 and Taurine 1.0.4 (libhooker).

## Usage

1. Install [Frida](https://frida.re/docs/ios/) and [openssh-server](https://cydia.saurik.com/package/openssh/) on your device
2. Clone this repository, and inside its directory, run:
   ```bash
   pip install -r requirements.txt --upgrade
   ```
3. Example commands:
   ```bash
   ./dump.py --host 192.168.1.101 --port 22 com.test.app # uses bundle identifier
   ./dump.py --host 192.168.1.101 --port 22 "FaceTime" # uses display name
   ./dump.py --host 192.168.1.101 --port 22 --list # lists installed apps
   ./dump.py Aftenposten # uses local SSH tunnel (port 2222) and Frida over USB
   ```

You can use [OpenSSH Settings](http://cydia.saurik.com/package/u.blanxd.opensshport/) to easily control your SSH server through a graphical interface.

You can also use [usbmuxd](https://github.com/libimobiledevice/usbmuxd) or [iproxy](https://iphonedev.wiki/index.php/SSH_Over_USB) to forward local SSH over a USB tunnel for increased security.

Example workflow:

```
./dump.py Aftenposten
Start the target app Aftenposten
Dumping Aftenposten to /var/folders/wn/9v1hs8ds6nv_xj7g95zxyl140000gn/T
start dump /var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/AftenpostenApp
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/AFNetworking.framework/AFNetworking
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/ATInternet_iOS_ObjC_SDK.framework/ATInternet_iOS_ObjC_SDK
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/SPTEventCollector.framework/SPTEventCollector
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/SPiDSDK.framework/SPiDSDK
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCore.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreData.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreGraphics.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreImage.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreLocation.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftDarwin.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftDispatch.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftFoundation.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftObjectiveC.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftQuartzCore.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftUIKit.dylib
Generating Aftenposten.ipa

Done.
```

Congratulations! You've got a decrypted IPA file.

### Troubleshooting

If any of the following errors occur:

- Device reboots
- Lost connection
- Unexpected error while probing dyld of target process

Please open the application manually and keep it in the foreground before dumping.
