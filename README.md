<span align="center">

# OpenCore EFI for AMD Ryzen and APU (iGPU) - Ryzentosh/Hackintosh

This EFI was covered with [this config](#Specs:), but it's possible that _FX and Athlon 2xxGE series_ also work. [Look at suported devices](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/).

Also, the EFI was tested with `13.6.3` MacOS version and OpenCore `0.9.7`.

</span>

## General information

![Screenshot](assets/system-info.png?raw=true)

### Specs:

| **Component** | **Model**                                                                       |
| ------------- | ------------------------------------------------------------------------------- |
| Motherboard   | [B450m Gamming](https://www.gigabyte.com/br/Motherboard/B450M-GAMING-rev-1x#kf) |
| CPU           | [Ryzen 7 5700g](https://www.amd.com/pt/products/apu/amd-ryzen-7-5700g)          |
| APU (iGPU)    | Vega 8                                                                          |
| GPU           | None                                                                            |
| Memory        | 2x 8GB 3200Mhz - Kingston                                                       |
| Ethernet      | Realtek RTL8111                                                                 |
| Audio         |                                                                                 |

# ⚠️ building ...

## Installing docker
Even if the virtualization on ryzentosh it's not fully suported you can try adapt using minukube.

First, you must:
- Enable SVM option into your bios config;
- Disble Kext Signing
- Intall the version `6.1.38r153438` of VirtualBox
  - To check the installed version use `VBoxManage --version`
  - To uninstall use `brew uninstall virtualbox` or uninstall manually using AppCleaner

### Pre-installation
1. Installing HomeBrew: https://docs.brew.sh/Installation
2. Installing VirtualBox `v6.1.38r153438` via brew:
  2.1 Updating cask versions list: `brew tap homebrew/cask-versions`
  2.2 Installing VirtualBox: `brew install --cask virtualbox6`

❕In the 2nd step, you will be asked to allow the "Oracle America Inc.", to accept go to `System Settings -> Privacity and Security` as shown in this screenshot:

![image](https://github.com/jpsaturnino/Ryzen-5700g-APU.Hackingtosh/assets/47997386/a8c62459-2691-4a51-93d2-926554b3f5b7)

❗**If there's no option to allow from Oracle, follow this:**
1. Check if the kext is enabled: `kextstat | grep VBox`, you are good to go if:
![image](https://github.com/jpsaturnino/Ryzen-5700g-APU.Hackingtosh/assets/47997386/428fb19b-d48c-49b4-8b86-d95713807fdf)
2. Othewise enter in recovery mode and use:
- ```kextcache --clear-staging``` 
- ```kextcache -i /```
- ```spctl kext-consent add VB5E2TV963```
- ```spctl kext-consent list```
3. After you restart, probably the option will show in your System Settings again, and you can chack if it's enabled using the command of the step 1

### Steps:
1. Installing minikube and docker:
```brew install minikube docker```
2. Creating the kubernets cluster using the virtualbox driver:
```minikube start --driver=virtualbox --keep-context```
3. Configures the Docker CLI in your current shell to use the minikube's docker:
```eval $(minikube docker-env)```
4. To use docker-compose just install it via homebrew:
```brew install docker-compose```
5. If you want to access a served application on a container (localhost:8080/route), you'll need the minikube IP to access it, using localhost won't work. And to retrieve the IP is just like that:
```minikube ip```
6. You can set this IP on /etc/hosts to access applications without typing the IP.
```sudo -- sh -c "echo $(minikube ip) minikube >> /etc/hosts"```

**ENJOY:**

![image](https://github.com/jpsaturnino/Ryzen-5700g-APU.Hackingtosh/assets/47997386/5642148b-4436-4e69-b7db-60b017bebb91)

### Benchmarks

**10/01/2024**

- CPU: https://browser.geekbench.com/v6/cpu/4341157
- GPU: https://browser.geekbench.com/v6/compute/1572448

### Used APPS

- [Karabiner Elements](https://karabiner-elements.pqrs.org): For keyboard remapping
- [Maccy](https://maccy.app): Clipboard manager
- [Alt-Tab](https://alt-tab-macos.netlify.app): windows switcher like Windows
- [Iina](https://iina.io) Modern mac media player
- [DevToys](https://devtoys.app) Tools for devs
- [MonitorControl](https://github.com/MonitorControl/MonitorControl) External monitor control options
- [Rectangle](https://rectangleapp.com) Window resizer
- [Orion](https://kagi.com/orion/) Mac browser
- [AppCleaner](https://freemacsoft.net/appcleaner/) Full app's uninstall
