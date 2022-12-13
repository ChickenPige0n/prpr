# prpr - <ins>P</ins>hig<ins>R</ins>os <ins>P</ins>layer, written in <ins>R</ins>ust

## Usage

To begin with, clone the repo:

```shell
git clone https://github.com/Mivik/prpr.git && cd prpr
```

For compactness's sake, `font.ttf` used to render the text is not included in this repo. As the fallback, `prpr` will use the default pixel font. You could fetch `font.ttf` from [https://mivik.moe/prpr/font.ttf].

```shell
wget https://mivik.moe/prpr/font.ttf -O assets/font.ttf
```

If your chart contains textures, place them in the `assets/texture` folder. Now the folder structure should be like this:

```
prpr
├── assets
|   ├── texture
|   │   └── ...
|   ├── (font.ttf)
|   └── ...
└── ...
```

Before building, a small patch should be applied to the crate `macroquad`. Navigate to `$HOME/.cargo/registry/src/github.com-..../macroquad-VERSION/src/text.rs`, and comment out the line that panics on vertical fonts, namely:

```rust
if metrics.advance_height != 0.0 {
    panic!("Vertical fonts are not supported"); // comment out this line
}
```

Finally, run `prpr` with your chart's path.

```shell
# .pez file can be recognized
cargo run --release --bin prpr-player mychart.pez

# ... or unzipped folder
cargo run --release --bin prpr-player ./mychart/

# Run with configuration file
cargo run --release --bin prpr-player ./mychart/ conf.yml
```

## Chart information

`info.txt` and `info.csv` are supported. But if `info.yml` is provided, the other two will be ignored. 

The specifications of `info.yml` are as below.

```yml
name: (string) (default: 'UK')
level: (string) (default: 'UK Lv.?')
charter: (string) (default: 'UK')
composer: (string) (default: 'UK')
illustrator: (string) (default: 'UK')

chart: (string, the path of the chart file) (default: 'chart.json')
format: (string, the format of the chart) (default: 'rpe', available: 'rpe', 'pgr', 'pec')
music: (string, the path of the music file) (default: 'music.mp3')
illustration: (string, the path of the illustration) (default: 'background.png')

aspect-ratio: (float, the aspect ratio of the screen (w / h)) (default: 16 / 9)
```

## Global configuration

The optional second parameter of `prpr-player` is the path to the configuration file. The specifications are as below.

```yml
adjust-time: (bool, whether automatical time alignment adjustment should be enabled) (default: false)
aggresive: (bool, enables aggresive optimization, may cause inconsistent render result) (default: true)
aspect-ratio: (float, overrides the aspect ratio of chart) (default: none)
autoplay: (bool, enables the auto play mode) (default: true)
line-length: (float, half the length of the judge line) (default: 6)
offset: (float, global chart offset) (default: 0)
particle: (bool, should particle be enabled or not) (default: false)
speed: (float, the speed of the chart) (default: 1)
volume-music: (float, the volume of the music) (default: 1)
volume-sfx: (float, the volume of sound effects) (default: 1)
```

## Acknowledgement

Some assets come from [@lchzh3473](https://github.com/lchzh3473).

Thanks [@inokana](https://github.com/GBTP) for hints on implementation!

## License

This project is licensed under [GNU General Public License v3.0](LICENSE).
