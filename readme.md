# Readme for my fork

See code and readme in [users/manna-harbour_miryoku](./users/manna-harbour_miryoku/readme.org).  But basically:
- Clone qmk, then add (my) miryoku as another remote
- Check out `groxx-miryoku` branch
- Install the basics: https://docs.qmk.fm/#/newbs_getting_started
  - `pyenv install 3.12.1`
  - reload direnv
  - `pip install qmk`
  - `make git-submodules`
- Make sure it builds:
  - `qmk compile --clean --keyboard crkbd --keymap manna-harbour_miryoku `
- Update:
  - `git fetch --all`
  - `git merge miryoku_qmk/miryoku`

Do the real build:
```sh
qmk compile --clean \
  --keyboard crkbd \
  --keymap manna-harbour_miryoku

# maybe?  does this give me colemak on an optional layer?  but not colemak-tap?  sounds odd, not sure where it's documented...
  -e MIRYOKU_EXTRA=COLEMAKDH \
```

Flash it (seamicro is an aftmega that uses dfu, double click reset button to enter mode):
```sh
qmk flash \
  --bootloader dfu \
  --keyboard crkbd \
  --keymap manna-harbour_miryoku
```

I've added stuff to:
- [keyboards/crkbd](./keyboards/crkbd/) to enable rgb matrix lighting, works.
  - find the media layer combo, then RGB_MOD to rotate.  currently hold left-hand left-thumb (media layer) plus "u" key on right hand.
- [users/miryoku](./users/manna-harbour_miryoku/custom_rules.mk) to switch to qwerty and mac
- partly because it's easier than specifying the env vars every time on the cli.

OLEDs are off, some possible ideas:
- https://www.reddit.com/r/olkb/comments/kknwxc/layer_state_reader_oled/
- not sure what I had before.  look for the vendor's repo?  pretty sure beekeeb had something.

When happy, manually(?) transcribe the layers/etc to https://keymap-drawer.streamlit.app/?example_yaml=corneish_zen.yaml for a nice rendered map.
(qmk c2json doesn't seem to understand any file I can find, only like one looks even close to usable for this)

https://www.reddit.com/r/crkbd/comments/161bp8t/my_little_experiment_merging_miryoku_qwerty_for/ may also be interesting, looks close to what I want at a very brief glance.
