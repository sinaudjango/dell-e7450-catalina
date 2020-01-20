# dell-e7450-catalina
Dell e7450 i7 Clover Catalina

Specs
Dell e7450 
CPU : Intel Core i7 (5th Gen) 5600U / 2.6 GHz
RAM : 2 x 8 GB (1600 MHz)
WIFI: Intel Tri-Band Wireless-AC 1726 (replace with Atheros AR9565)
Graphic: Intel HD Graphics 5500

Instalation

make bootable installer using vanilla installer, download from apple store
mount EFI folder using CLover or another application mount EFI
replace with config from this repo

i suggest to bootable dual boot with windows, so please provice another partition for windows  system see this tutorial https://youtu.be/eFnZF3rgS0o
its importent to load bluetooth firmware Atheros AR9565 for pairing device

Install Wifi Kext
- open terminal : type
sudo mount -rw /
killall Finder
- go to System/Library/Extensions and delete IO80211Family.kext, IO80211FamilyV2.kext, corecapture.kext and CoreCaptureResponder.kext (Backup First to Another Folder before you delete it)
- Copy IO80211Family.kext, corecapture.kext and CoreCaptureResponder.kext
- Run Kext Utility to fix permissions and update kext cache
- reboot enjoy


Load Bluetooth Pairing
- After you success install catalina, install windows
- boot windows, install drivers, add bluetooth devices for testing
- reboot windows (dont shutdown) then boot to your hackintosh
- pair your bluetooth devices

Enable On/Off Bluetooth
- open terminal : type
sudo mount -rw /
killall Finder
- go to system report > Hardware > bluetooth
find vendorID and Product id,
for example with my bluetooth like this https://prnt.sc/qq37e3
then convert from hexa to decimal
  Vendor ID:	0x0CF3 = 3315
  Product ID:	0x3004 = 12292
  
 - Edit /System/Library/Extensions/IOBluetoothFamily.kext/Contents/PlugIns/BroadcomBluetoothHostControllerUSBTransport.kext/Contents/Info.plist
 <key>Broadcom2045FamilyUSBBluetoothHCIController_D</key>
		<dict>
			<key>CFBundleIdentifier</key>
			<string>com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport</string>
			<key>IOClass</key>
			<string>BroadcomBluetoothHostControllerUSBTransport</string>
			<key>IOProviderClass</key>
			<string>IOUSBHostDevice</string>
			<key>idProduct</key>
			<integer>xxxxxx</integer>
			<key>idVendor</key>
			<integer>xxxxxx</integer>
		</dict> 
    
    replace with config below
    
    <key>Broadcom2045FamilyUSBBluetoothHCIController_D</key>
		<dict>
			<key>CFBundleIdentifier</key>
			<string>com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport</string>
			<key>IOClass</key>
			<string>BroadcomBluetoothHostControllerUSBTransport</string>
			<key>IOProviderClass</key>
			<string>IOUSBHostDevice</string>
			<key>idProduct</key>
			<integer>12292</integer>
			<key>idVendor</key>
			<integer>3315</integer>
		</dict>
    
    
 if you cant save directly, first copy Info.plist to Desktop after edited replace to origin source path
