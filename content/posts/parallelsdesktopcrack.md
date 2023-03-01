---
title: Parallels Desktop Crack
date: 2023-02-26
author: 夏明
---

Crack for Parallels Desktop 18.1.1 53328

You can contact me if you need.

- [x] Support Intel
- [x] Support Apple Silicon (M1 & M2)
- [x] Network
- [x] USB

## Usage

1. Install Parallels Desktop.

    https://download.parallels.com/desktop/v18/18.1.1-53328/ParallelsDesktop-18.1.1-53328.dmg

2. Exit parallels account.

3. Download this repo files.

4. Extract and run Terminal in this directory.

5. `chmod +x ./install.sh && sudo ./install.sh`

If you got "Operation not permitted" error, enable "Full Disk Access" permission for your Terminal app.

`System Preferences ▸ Security & Privacy ▸ Privacy ▸ Full Disk Access`

If you got `codesign` error, ensure xcode command line tools installed. Install with command `xcode-select --install`.

Check installed with `xcode-select -p` will output `/Library/Developer/CommandLineTools` or `/Applications/Xcode.app/Contents/Developer`.


## Manual

1. Open `Parallels Desktop` and exit your account.

2. Exit `Parallels Desktop`.

3. Ensure prl_disp_service not running.

```bash
pkill -9 prl_disp_service
```

4. Copy cracked `prl_disp_service` file.

```bash
sudo cp -f prl_disp_service "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
sudo chown root:wheel "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
sudo chmod 755 "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
```

5. Copy fake licenses.json.

```bash
sudo cp -f licenses.json "/Library/Preferences/Parallels/licenses.json"
sudo chown root:wheel "/Library/Preferences/Parallels/licenses.json"
sudo chmod 444 "/Library/Preferences/Parallels/licenses.json"
sudo chflags uchg "/Library/Preferences/Parallels/licenses.json"
sudo chflags schg "/Library/Preferences/Parallels/licenses.json"
```

6. Sign `prl_disp_service` file.

```bash
sudo codesign -f -s - --timestamp=none --all-architectures --entitlements ParallelsService.entitlements "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
```


## Notice

Parallels Desktop may upload client info or logs to server.

You can use a firewall, hosts or custom DNS block there domains.

This prevents the built-in downloader from working, but you can download prebuilt Virtual Machines via
* Apple Silicon
    * https://update.parallels.com/desktop/v18/appliances_arm.xml
    * https://update.parallels.com/desktop/v18/appliances_arm_Monterey.xml
* Intel
    * https://update.parallels.com/desktop/v18/appliances.xml

### Hosts

```
127.0.0.1 download.parallels.com
127.0.0.1 update.parallels.com
127.0.0.1 desktop.parallels.com
127.0.0.1 download.parallels.com.cdn.cloudflare.net
127.0.0.1 update.parallels.com.cdn.cloudflare.net
127.0.0.1 desktop.parallels.com.cdn.cloudflare.net
127.0.0.1 www.parallels.cn
127.0.0.1 www.parallels.com
127.0.0.1 www.parallels.de
127.0.0.1 www.parallels.es
127.0.0.1 www.parallels.fr
127.0.0.1 www.parallels.nl
127.0.0.1 www.parallels.pt
127.0.0.1 www.parallels.ru
127.0.0.1 www.parallelskorea.com
127.0.0.1 reportus.parallels.com
127.0.0.1 parallels.cn
127.0.0.1 parallels.com
127.0.0.1 parallels.de
127.0.0.1 parallels.es
127.0.0.1 parallels.fr
127.0.0.1 parallels.nl
127.0.0.1 parallels.pt
127.0.0.1 parallels.ru
127.0.0.1 parallelskorea.com
127.0.0.1 pax-manager.myparallels.com
127.0.0.1 myparallels.com
127.0.0.1 my.parallels.com
```

Parallels Desktop will uncomment hosts file, can use this command lock your hosts file:

```bash
sudo chflags uchg /etc/hosts
sudo chflags schg /etc/hosts
```

### AdGuardHome

Add the following rules to your `Custom filtering rules`:

```
||myparallels.com^$important
||parallels.cn^$important
||parallels.com^$important
||parallels.de^$important
||parallels.es^$important
||parallels.fr^$important
||parallels.nl^$important
||parallels.pt^$important
||parallels.ru^$important
||parallelskorea.com^$important
||parallels.com.cdn.cloudflare.net^$important
```
