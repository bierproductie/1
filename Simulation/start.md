
# Make files ready
first we will need to change the port, to make sure we don't have to run
wine as root.  
all ports under 1000 can user space not use without root permission.

## editor's
every time you see vim, you can always use your preferred editor maybe nano or gedit.

#### The first file is 
`vim /Config1/X20CP1586/ADDONS/BIN/IATR/defaultConfig.mappviewcfg`
You will need to go to line 6 change the port to some thousand. 
Change it from 81 to 8100. It should look like this:
` <Property ID="WebServerPort" Value="8100" /> `
  
#### The second file is
`vim Config1/X20CP1586/ADDONS/DATA/IAT_Data/server/Config.mappviewcfg`
Do the same thing again.
You will need to go to line 6 change the port to some thousand. 
Change it from 81 to 8100. It should look like this:
` <Property ID="WebServerPort" Value="8100" /> `

# Launch file
You can make a launch file as well.
`vim start.sh`

```sh
#!/bin/bash
wine Config1/X20CP1586/ar000loader.exe &
sleep 5
notify-send "Remember to refresh the page" "If it is not loadet yet"
xdg-open http://localhost:8100/index.html?visuId=visu
```

chmod a+x start.sh
./start.sh


# Start it from anywhere
Link it so you can start it from any where.
Link's should always be absolute PATH.
ln -s /home/$USER/[where the start.sh file is] /home/$USER/.local/bin/beerSim
  
Edit your `vim ~/.profile`  
add `export PATH="$PATH:$(du "$HOME/.local/bin/" | cut -f2 | tr '\n' ':' | sed 's/:*$//')"`  
Then every sub folder in `$HOME/.local/bin` will be automatic add to your $PATH variable, on every user login.
