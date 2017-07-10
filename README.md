# Screengif

Turn a .mov file to a .gif file using docker fully transparently.

![screencast](https://i.imgur.com/nKeb83U.gif)

### Run directly

```bash
docker run -it -v `pwd`:/srv/screengif/input --rm ambroselli/screencast-gif /bin/bash \
    -c 'umask 002; bin/screengif -i input/file.mov -o input/file.gif'
```

### Run using script

Create a file with the following content (I named it `screencast` and moved it to `/usr/local/bin/screencast` (and made it executable):

```bash
#!/bin/bash

if [ -z "$1" ] || [ ! -f "$1" ]; then
  echo "Usage: $0 file.mov"
  exit
fi

docker run -it \
    -v `pwd`:/srv/screengif/input \
    --rm \
    ambroselli/screencast-gif \
    /bin/bash -c "umask 002 && bin/screengif -i 'input/$1' -o 'input/$1.gif'"
```

Then I run it using `screencast file.mov`.

### Upload to imgur
You can use [this script](https://github.com/tremby/imgur.sh) to upload the resuling gif to imgur and get a linkable url with one one command.

#### Thanks
Heavily based on [screengif](https://github.com/dergachev/screengif).