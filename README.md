# FuelRats-quickcopy
Autocopy and one-click-copy functionality for system names for a less annoying experience.

# Installation (AdiIRC only)
1. Go to `Tools > Edit Scripts` or press `ALT+R`.
2. Create a new file `File > New` or press `CTRL+N`.
3. Paste the script provided below into the editor.
4. Uncomment your version by removing the semicolon before the line.
5. Press `Save`, name the file `quickcopy` and press the `Save` button.
6. Profit.

# Usage
### Manual
Click the 'RATSIGNAL' text field to copy the system name.
### Automatic
`/qctog` 
 - Toggles all autocopy functionality.

`/qcver [ody/hor/leg]`
 - Toggles autocopying for specific versions (multiple can be enabled, but not at the same time).
 - Running without argument lists status for all versions.

# Script
```
on *:TEXT:*RATSIGNAL*:#: {
  if ( $regex($1-, %qcreg) == 1 && %qcenabled == $true) {
    $regex($1-, "(.*?)")
    var %system = $regml(1)
    clipboard %system
    echo -ag quickcopy system %system copied to clipboard
  }
}

on *:HOTLINK:*RATSIGNAL*:#: {
  if ( $hotlink(event) == sclick ) {
      $regex($hotline, "(.*?)")
      var %system = $regml(1)
      clipboard %system
      echo -ag quickcopy system %system copied to clipboard
    }
  }
}

alias qctog {
  if (%qcenabled == $true) {
    set -g %qcenabled $false
    echo -ag quickcopy disabled autocopy globally
  }
  else if (%qcenabled == $false) {
    set -g %qcenabled $true
    echo -ag quickcopy enabled autocopy globally
  }
  else {
    set -g %qcenabled $false
    echo -ag quickcopy disabled autocopy globally
  }
}

alias qcver {
  if ($1 == ody) {
    if (%qcody == $true) {
      set -g %qcody $false
      echo -ag quickcopy disabled autocopy for odyssey
    }
    else if (%qcody == $false) {
      set -g %qcody $true
      echo -ag quickcopy enabled autocopy for odyssey
    }
    else {
      set -g %qcody $false
      echo -ag quickcopy disabled autocopy for odyssey
    }
  } else if ($1 == hor) {
    if (%qchor == $true) {
      set -g %qchor $false
      echo -ag quickcopy disabled autocopy for horizons
    }
    else if (%qchor == $false) {
      set -g %qchor $true
      echo -ag quickcopy enabled autocopy for horizons
    }
    else {
      set -g %qchor $false
      echo -ag quickcopy disabled autocopy for horizons
    } 
  } else if ($1 == leg) {
      if (%qcleg == $true) {
        set -g %qcleg $false
        echo -ag quickcopy disabled autocopy for legacy
      }
      else if (%qcleg == $false) {
        set -g %qcleg $true
        echo -ag quickcopy enabled autocopy for legacy
      }
      else {
        set -g %qcleg $false
        echo -ag quickcopy disabled autocopy for legacy
      }
  }
  if (%qcody) { var %odyval = enabled } else { var %odyval = disabled }
  if (%qchor) { var %horval = enabled } else { var %horval = disabled }
  if (%qcleg) { var %legval = enabled } else { var %legval = disabled }
  if (%qcenabled) { var %qcval = ON } else { var %qcval = OFF }
  if (%qcody) { var %odysig = ODY_SIGNAL| }
  if (%qchor) { var %horsig = HOR_SIGNAL| }
  if (%qcleg) { var %legsig = LEG_SIGNAL| }
  echo -ag quickcopy autocopy is %qcval  with [ODY: %odyval ] [HOR: %horval ] [LEG: %legval ]
  set -g %qcreg $eval($+(%odysig,%horsig,%legsig,q^))
}
```
