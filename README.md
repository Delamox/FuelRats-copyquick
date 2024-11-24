# FuelRats-copyquick
Automatically copies system name for a less annoying experience

# Installation (AdiIRC only)
1. go to `Tools > Edit Scripts` or press `ALT+R`
2. create a new file `File > New` or press `CTRL+N`
3. paste the script provided below into the editor
4. uncomment your version by removing the semicolon before the line
5. press `Save`, name the file `quickcopy` and press the `Save` button
6. profit

# Script
```
on *:TEXT:*RATSIGNAL*:#: {
   
  ;uncomment your version by removing the semicolon
  
  ;var %trigger = /ODY_SIGNAL/
  ;var %trigger = /HOR_SIGNAL/
  ;var %trigger = /LEG_SIGNAL/
  
  if ( $regex($1-, %trigger) == 1 ) {
    $regex($1-, "(.*?)")
    var %system = $regml(1)
    clipboard %system
    echo -ag quickcopy system %system copied to clipboard
  }
}

```
