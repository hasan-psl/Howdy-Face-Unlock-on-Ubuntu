# How to Install Howdy (Face Unlock) on Ubuntu

Howdy is a Windows Hello–style facial authentication tool for Linux.  
Unfortunately, the official installation method is currently broken on recent Ubuntu-based systems, since it depends on direct system-wide `pip3` installs.  

This guide documents a **working method for Ubuntu 24.04+** using the patched PPA provided by [Panda Jim](https://launchpad.net/~ubuntuhandbook1), the maintainer of [UbuntuHandbook.org](https://ubuntuhandbook.org/).  

> ### ⚠️ Disclaimer:
> 
> This repository is *only documentation*. I am not the creator or maintainer of the Howdy software or the patched PPA.  
> Installing software from third-party PPAs is done at your own risk. Always review the source before trusting it with root privileges.  
>
> Full credit goes to **Panda Jim** for maintaining the patched PPA.  
> - Profile: [Panda Jim](https://launchpad.net/~ubuntuhandbook1)  
> - PPA: [ppa:ubuntuhandbook1/howdy](https://launchpad.net/~ubuntuhandbook1/+archive/ubuntu/howdy)  
> - Website: [UbuntuHandbook](https://ubuntuhandbook.org/)

---

## 📦 Installation Steps

### 1. Add the Patched Howdy PPA
```
sudo add-apt-repository ppa:ubuntuhandbook1/howdy
```


### 2. Install Howdy
```
sudo apt install howdy
```


### 3. Add Your Face
```
sudo howdy add
```



## 🛠️ Troubleshooting Section 

### 🔧 Fixing **"Camera Not Found"** error

> If you see "camera not found", you’ll need to configure the IR camera path.

  #### 1. Open the Howdy config:
  ```
sudo howdy config
```


  #### 2. Find this line: ``` device_path = ```

  

   ##### Now, change it to your IR camera device path, for example:
  ``` device_path = /dev/video2 ```


  
  #### 3. To discover your camera path, run:
  ```
v4l2-ctl --list-devices
```



   ##### If v4l2-ctl is missing, install it:
  ```
sudo apt install v4l-utils
```
  👉 Start testing from `/dev/video0`, `/dev/video1`, etc. until you find the working one.
  **Example:** on my laptop, the IR camera was at `/dev/video2`.





### 🔓 Optional: Enable Login-Screen Face Unlock

  #### 1. Edit the GDM password PAM file:
```
sudo nano /etc/pam.d/gdm-password
```


  #### 2. Add this line above `@include common-auth`:
  ``` auth    sufficient      pam_python.so /lib/security/howdy/Howdy.py ```
  > Move text input cursor with arrow keys.

  > To save the file, use ```Ctrl```+```O```. Press ```Enter``` to confirm the file name.

  > To exit the editor (from ```Nano```), use ```Ctrl```+```X```.


  #### 3. Save, exit, then reboot:
  ```
sudo reboot
```



## ✅ Credits

* Patched Howdy PPA by [Panda Jim](https://launchpad.net/~ubuntuhandbook1)
* Documentation inspired by a helpful [GitHub community comment](https://github.com/boltgolt/howdy/issues/1021#issuecomment-2996859175) (original source where I found the method).

This repo exists to provide a **clear, centralized guide** for Ubuntu users struggling with the broken official **Howdy** installation.

## 📜 License

This documentation is released under the [MIT License](https://opensource.org/licenses/MIT).

The Howdy software itself is under its own license (see the [official Howdy repo](https://github.com/boltgolt/howdy) for details).
