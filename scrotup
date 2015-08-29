#! /bin/bash

## dkeg 2015
## join scrot and imgur to auto upload

## usage
# scrotup [name].jpg|png

## dependencies are 
  # bar for popups OR use dunst and change notify accordingly
  # imgur upload script (https://code.google.com/p/imgur-cli/)
  # figlet or toilet (in the repos)
  # hit 'q' to exit the scrot preview and continue

## globals
  check='sleep .5s' 
  scrotit='scrot -d .5' 
  geometry='-g 800x340+281+144'
  params="-R .01 --zoom 75 --auto-zoom"
  sendit="imgur upload $1 -t $1"
  notify="popbatt %{c}"
  fancy="figlet"
  #fancy="toilet --gay"

## clear the screen to look nice
  function clr() {
    echo clear
  }
  function saveit() {
        echo -e "Specify a location to save or Enter to skip."
        read location
          if [ -z  $location ] ;then
            echo "okay, we'll leave it be."
          else 
            if [ ! -d $location ]; then
              echo "$location does not exit. Bye!"
              exit 1
            else
              mv $1 $location
              $(clr) && echo ".... $1 was saved to $location"
            fi
          fi
  }
## scot it up!
  $check 
  if [ -z $1 ] ;then
    echo "Error! Missing parameter. Name your scrot!"
    exit 1
  else
    $scrotit $1
    #feh $geometry $params $1 
    $(clr) 
    echo -e "Upload to Imgur?
      a. Upload and Save
      b. Upload; don't Save 
      c. Save only
      d. Delete and Quit"
    read action
      if [ $action == "a" ] ;then
        saveit $1
        cd $location 
        $sendit && cd $HOME
        echo ".... $1 was uploaded." 
        $fancy "Success!"
        $notify "  $1 uploaded"
      elif [ $action == "b" ] ;then
        $sendit
        rm $1
        $(clr) && echo  ".... $1 was deleted."
        echo ".... $1 was uploaded."
        $(clr) && $fancy "Success!"
        $notify "  $1 uploaded"
      elif [ $action == "c" ] ;then
        saveit $1 
        $notify "  $1 was saved"
      elif [ $action == "d" ] ;then
        rm $1
        $(clr) && echo "... $1 deleted. Bye!
        Maybe next time."
        exit 0
      else 
        echo "Something went wrong. Try again."
        exit 1 
      fi
  fi
