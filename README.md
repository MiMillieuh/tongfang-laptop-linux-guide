# tongfang-laptop-linux-guide
A guide for tongfang laptops and other constructor that uses tongfang motherbords

# Steps to follow :

## 1 : Install acpi-call

We need to use acpi-call to comunicate with the motherboard : 

Install acpi-call from your repo (if you have the luck of having it in your repo) or compile it by yourself with this repo : [nix-community/acpi_call](https://github.com/nix-community/acpi_call)

if you're using ublue or fedora I've made a package with dkms or a way to install it pretty much easily in this repo : [MiMillieuh/acpi_call-fedora](https://github.com/MiMillieuh/acpi_call-fedora)

## 2 : Allow acpi-call without sudo password :

We don't want to enter our password each time we launch a game, so just edit sudoers with `visudo` and go to the end of the file and add : 

```
yourusername ALL=(ALL) NOPASSWD: /usr/bin/tee /proc/acpi/call
yourusername ALL=(ALL) NOPASSWD: /usr/bin/cat /proc/acpi/call
```

## 3 : Install tongfang-control

Download it from that repo : [GitLab extrenal : siphomateke/tongfang-control](https://gitlab.com/siphomateke/tongfang-control)

and install it by following the readme.md


## 4 : Configure tongfang-control for games

We're going to use gamemode to trigger some settings :

in `/etc/gamemode.ini` in the **[custom]** section add :

```
start=powerprofilesctl set performance
start=tongfang-control -fl loud; tongfang-control -fm boost

end=powerprofilesctl set balanced
end=tongfang-control -fl quiet; tongfang-control -fm intelligent
```

## 5 : For nvidia users

We want to enable nvidia-powerd if not already done : 

```
sudo systemctl enable --now nvidia-powerd
```

You can trick the crappy nvidia driver to allow the gpu to use more power with a custom service. you can install it with this command : 

```
sudo wget https://raw.githubusercontent.com/MiMillieuh/tongfang-laptop-linux-guide/main/tongfang-nvidia.service -O /etc/systemd/system/tongfang-nvidia.service ; sudo systemctl enable --now tongfang-nvidia.service
```

## And you should be good to go !
