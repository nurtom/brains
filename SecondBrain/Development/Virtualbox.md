### [VBox 7.1.6 on Windows Error In supR3HardenedWinSpawn](https://forums.virtualbox.org/viewtopic.php?p=553256#p553256)

[Post](https://forums.virtualbox.org/viewtopic.php?p=553256#p553256 "Post") by **[ILP](https://forums.virtualbox.org/memberlist.php?mode=viewprofile&u=140134)** » 28. Jan 2025, 13:58

I've had the same problem since upgrading to version 7.1.6.  
It seems that you have to start the VirtualBox service manually with the command:

```powershell
net start vboxsup
```