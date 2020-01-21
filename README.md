FFMPEG-CUDA
=========

Installazione di FFMPEG con CUDA ed uso della GPU NVIDIA.

Installare prima i driver e Cuda non dai repo ma dal sito nvidia.com


Requirements
------------

- [NVIDIA x86_64 440.36](http://it.download.nvidia.com/XFree86/Linux-x86_64/440.36/NVIDIA-Linux-x86_64-440.36.run)
- [CUDA 440.33.01](http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run)
- add in your /etc/apt/sources.list: deb http://www.deb-multimedia.org buster main non-free
- install role: ansible-galaxy install -f mikysal78.ffmpeg_cuda


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
