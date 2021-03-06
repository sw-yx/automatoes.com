# Convert a .mov file to .gif

Solution: Create a shell alias that uses [[ffmpeg]] to convert a .mov screen recording to an optimized gif

Filename: ~/.zshrc, ~/.bashrc or similar

```bash
gif() {
  ffmpeg -i "$1" -vf "fps=25,scale=iw/2:ih/2:flags=lanczos,palettegen" -y "/tmp/palette.png"
  ffmpeg -i "$1" -i "/tmp/palette.png" -lavfi "fps=25,scale=iw/2:ih/2:flags=lanczos [x]; [x][1:v] paletteuse" -f image2pipe -vcodec ppm - | convert -delay 4 -layers Optimize -loop 0 - "${1%.*}.gif"
}
```

Usage:

```
gif ~/Desktop/Screen\ Recording\ 2020-07-29\ at\ 2.00.00\ PM.mov
```

Tags:

- [[ffmpeg]]

Contributor: [[Trevor Brindle]]

[//begin]: # "Autogenerated link references for markdown compatibility"
[ffmpeg]: ffmpeg "Ffmpeg"
[Trevor Brindle]: trevor-brindle "Trevor Brindle"
[//end]: # "Autogenerated link references"