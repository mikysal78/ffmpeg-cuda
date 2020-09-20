FFMPEG-CUDA
=========

Installazione di FFMPEG supporto di CUDA per usare la GPU NVIDIA.

La role non installa i driver ne cuda, è necessario prima installare driver e Cuda non dai repo ma dal sito nvidia.com


Requirements
----------------

- [NVIDIA x86_64 450.66](https://it.download.nvidia.com/XFree86/Linux-x86_64/450.66/NVIDIA-Linux-x86_64-450.66.run)
  vedere il link per l'[ultimo driver](https://www.nvidia.it/Download/driverResults.aspx/163405/it)
- [CUDA 440.33.01](http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run)
  vedere il link per l'[ultima release](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804)
- aggiungi nel tuo /etc/apt/sources.list:
```deb http://www.deb-multimedia.org buster main non-free```
Quando lanci il comando;
```apt-get update```
avrai un errore nella KEY non valida, usa il comando
```apt-key adv --keyserver keyring.debian.org --recv-keys CHIAVE```
- installa la role:
```ansible-galaxy install -f mikysal78.ffmpeg_cuda```


Installazione dei Drivers e Cuda
----------------
Disabilitare la gui con il comando
```
systemctl set-default multi-user.target
```
Riavviare

Editare il file /etc/default/grub modificando la variabile come sotto
```
GRUB_CMDLINE_LINUX_DEFAULT="nouveau.modeset=0 quiet"
```

Creare il file /etc/modprobe.d/blacklist.conf
```
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
Eseguire i comandi
```
update-initramfs -u
systemctl set-default graphical.target
```
Riavviare il sistema e installare prima il Driver e dopo Cuda.


Example Playbook
----------------

```Yaml
    - hosts: video-encoder
      roles:
         - { role: mikytux78.ffmpeg-cuda }
```

License
-------

BSD

Author Information
------------------

- [MikySal78](https://github.com/mikysal78)
