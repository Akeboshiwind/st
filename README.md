# st

A fork of the `st` AUR package.

## Install

Run the following, or add it to your system install script.

```bash
git clone git@github.com:Akeboshiwind/st.git
cd st
makepkg -si
cd ..
rm -rf st
```

## Adding patches

Add the patch in the correct place in the `_patches` list in `PKGBUILD`.

Check to see if the patches override eachother or if they modify config.def.h, see [here](https://brianbuccola.com/how-to-build-and-install-st-suckless-simple-terminal-from-source-on-arch-linux/) for instructions.

Remember to run the following to update the `PKGBUILD`, build and install `st`.

```bash
updpkgsums && makepkg -sif
```

## Changelog

See `CHANGELOG.md.`
