# sxhkd_plasma

I have been playing with ![sxhkd](https://github.com/baskerville/sxhkd) for a while and I decided to just change **ALL** my keyboard shortcuts to it.

My config can be found ![here](https://github.com/RaitaroH/Random-Code/blob/master/dot/sxhkdrc). Take a look.

## Prerequisits

1. Install the actual program itself. Example: `sudo apt install sxhkd`  
2. You will also need to understand how to edit the config file. Please see the manual.
3. You will have to understand how to use qdbus.

Putting aside the usual shortcuts you can make, this tutorial will focus on the KDE side of things.

## qdbusviewer

As the name implies this program allows to browse different commands. Alternatively using *TAB* for autocompletion also works. For example if yakuake is investigated then:
```
qdbus org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState
```

### Krunner

Krunner can be binded to some shortcut. Alternatively it can be binded to super alone using the functionality in kde itself.
```
super + @space 
	qdbus org.kde.kglobalaccel /component/krunner org.kde.kglobalaccel.Component.invokeShortcut 'run command'
```
To bind it to super alone:
```
kwriteconfig5 --file ~/.config/kwinrc --group ModifierOnlyShortcuts --key Meta "org.kde.krunner,/App,,display"
qdbus org.kde.KWin /KWin reconfigure
```

### Kwin

Kwin has many shortcuts available but is difficult to find out what is the right command for them. In this case it does not matter as long as there is a shortcut for them.
Alternatively it is possible for entire scripts to be written and used instead.
```
# Zoom
super + {equal, minus}
	{qdbus org.kde.kglobalaccel /component/kwin org.kde.kglobalaccel.Component.invokeShortcut 'view_zoom_in',\
	 qdbus org.kde.kglobalaccel /component/kwin org.kde.kglobalaccel.Component.invokeShortcut 'view_zoom_out'}

# Virtual desktops
alt + {s, w, shift+s, shift+w}
	{qdbus org.kde.KWin /KWin org.kde.KWin.nextDesktop,\
	 qdbus org.kde.KWin /KWin org.kde.KWin.previousDesktop,\
	 qdbus org.kde.kglobalaccel /component/kwin org.kde.kglobalaccel.Component.invokeShortcut 'Window to Next Desktop',\
	 qdbus org.kde.kglobalaccel /component/kwin org.kde.kglobalaccel.Component.invokeShortcut 'Window to Previous Desktop'}
```
