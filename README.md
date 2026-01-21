# Running PC Version of Blue Archive JP on Linux

## Premeable

This repo documents the steps I took to have the Windows version of Blue Archive JP running on Linux. This is **not** a full guide. It is tailored to my specific distro and software setup. Feel free to reference this guide, but keep in mind that your mileage may vary.

## My setup

Here is a quick run-down of my environment.

### Hardware
- CPU: AMD Ryzen 7 7700X
- Memory: 64 GiB
- GPU: Radeon RX 9070 XT

### Software
- Distro: CachyOS Linux
- Desktop Environment: KDE Plasma 6.5.5

## Steps

### Preparation
Make sure that you grab the lastest version of your GPU driver. It is also advised to upgrade all your packages using your package manager.

Make sure you have Steam installed on your machine, and make sure that Proton compatibility layer is already working for Steam games. There are many guides out there. Find one that works for your specific environment. Test it out with some Steam games would help.

Head to <https://bluearchive.jp/> and download the Windows installer.

### Adding Installer to Steam

Add the installer to Steam as a "Non-Steam Game" by going to: **Library** - **Add a Game** (bottom Left) - **Add a Non-Steam Game...**.

In the pop-up window, click **Browse...**, then choose the installer executable, then click on **Add Selected Programs**.

Find the installer in your library. Then right click, go to **Properties...**. In the **Compatibility** tab, tick **Force the use of a specific Steam Play compatible tool**, and in the drop-down menu, choose **Proton Experimental**.

### Running Installer

Exit out of the Properties menu, then click **Play**. It may take a couple seconds to download some needed Proton runtime files. You should be expecting to see the installer window pop up. Follow the installer to install the *Launcher*. I left everything as Default.

### Checking Launcher Files

Pull out your terminal of choice, and run this command in order to find there the *Launcher* files are stored:

```
ls -lt ~/.steam/steam/steamapps/compatdata | head
```

The most recently modified directory is where that installer is stored. It will be a long number. Navigate into that directory, then under 

```
~/.steam/steam/steamapps/compatdata/<number_for_non_steam_game>/pfx/drive_c/
```

we will see 

```
/YostarGames/BlueArchive_JP_Gamelauncher
```

under which we can find `BlueArchive_JP_Gamelauncher.exe`. Of course, if you changed the installation directory earlier, this will be different.

### Editing Properties of Non-Steam Game

Now go back to your Steam Library. Go to the **Properties** of the installer we added just now. We are going to edit a few things.

- Under the **Shortcut** tab:
    - Change the name to `Blue Archive` (or anything you like).
    - Change **TARGET** to 
    ```
    "C:\YostarGames\BlueArchive_JP_Gamelauncher\BlueArchive_JP_Gamelauncher.exe" 
    ```
    - Change **START IN** to 
    ```
    "C:\YostarGames\BlueArchive_JP_Gamelauncher\"
    ```
    - Note: if you changed the directory during installation, make sure you change it here as well.

- Uder the **Compatibility** tab:
    - Change the Proton version to the latest Proton GE or whichever is native. For me it is
    ```
    proton-cachyos-10.0-20260101 (native)
    ```
### Running the Launcher.

Now, if you click on **Play** again, the Launcher should open. Proceed toinstall the game and play like you would on Windows.

## Caveats

The game won't properly close unless you use the **STOP** button from Steam. Not sure how to fix that yet.

The game would first start up in full screen. This can be adjusted in game. You can resize the window and it will stay at the same aspect ratio.
