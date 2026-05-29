# windows11-wsl2-docker-etc
Hints and tips for working with WSL2 etc

I'm a longtime UNIX/BSD/Linux/Ubuntu user, but like a lot of folks I use a Windows laptop for work, or sometimes a Mac.  The current incarnation of WSL2, especially as it now include X-Windows is pretty good for folks like me who know the usual Unix tools, but haven't got useful skills with Powershell, Registry, and other Windows voodoo.

## WSL2
Network access from wsl, particularly mDNS, didn't work well for me with the defaults.  Here's what I have in my C:\Users\mike\.wslconfig

```
[wsl2]
dnsTunneling=false
memory=24GB
networkingMode=mirrored
```


## Docker desktop

Docker desktop is really handy for working with containers that can be accessed easily from both Windows, e.g. from a browser, and Linux (wsl), e.g. bash command line.
Under the hood it's also using wsl2, but has its own virtual disk. Watch out for this filling up if you aren't regularly cleaning up old containers and volumes, as it will grow but never shrink on its own.  To shrink it back down to a sensible size, delete any containers, etc. you don't need, quit docker desktop, and then in Powershell run -

(replace the path with your path, found with WizTree or whatever method you like)
```
Optimize-VHD -Path C:\Users\mike\AppData\Local\Docker\wsl\disk\docker_data.vhdx -Mode Full
```
