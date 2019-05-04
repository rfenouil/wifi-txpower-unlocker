# wifi-txpower-unlocker

A bash script that generates a modified regulatory.bin from [Central Regulatory Domain Agent](https://wireless.wiki.kernel.org/en/developers/regulatory/crda) and [Wireles Regulatory Database](https://wireless.wiki.kernel.org/en/developers/regulatory/wireless-regdb) sources and patches the kernel. This unlocks the maximum WiFi TX power (on 2.4 Ghz) of the region BO according to the dBm value you specify in the script. 

As compared to original repository, only script relevant for my ARM platform (Rock64) was kept and modified for compatibility.
As opposed to original script, it aims at modifying existing values for defaut profile (should prevent the need to modify ```reg``` after each reboot).

## wifi_txpower_unlocker.sh
* Tested on Rock64 (linux 4.4.167-1169-rockchip-ayufan-g3cde5c624c9c)

## Usage
1. Run ```iwconfig``` or ```ifconfig``` to determine your interface and initial TX power
* ```iwconfig```
2. Check that your selected region is really `country 00` (modify gawk command in script otherwise)
* ```iw reg get```
#### Increase TX power
1. Login as root
2. Download wifi_txpower_unlocker.sh or arch-...sh script (or clone the repo)
3. Make the script executable
* ```chmod +x wifi_txpower_unlocker.sh```
5. Execute the script with the desired TX power (dBm) as a cli argument (I used 33 for 2W)
* ```./wifi_txpower_unlocker.sh 33```
6. When prompted to reboot type ```'y'``` and press ```[Enter]```
7. After rebooting, login as root and check if your TX power is set to 33
* ```iwconfig wlan1```
#### If not set to 33 after reboot, try to set it manually
2. Bring the interface down
* ```ifconfig wlan1 down```
4. Change the txpower of the interface (again, I chose 33). If you specified ```xx``` in the script before executing, ```xx``` will be the highest txpower you can set the interface to. 
* ```iwconfig wlan1 txpower 33```
5. Bring the interface up
* ```ifconfig wlan1 up```
6. Use ```iwconfig``` to make sure that the txpower is set to what you desired
* ```iwconfig wlan1```

## Contributing
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D


