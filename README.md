# vnote-mpr

This is where I keep a few words on packaging the source package
[`vnote`](https://aur.archlinux.org/packages/vnote) from the AUR for the
[MPR](https://mpr.makedeb.org).

## About

I spent about one day on a weekend to see if I can basically copy an entire
`PKGBUILD` from the AUR and paste it into `$ makedeb`, with minor rewrites of
Debian-related.

Basically, this process worked with a lot of trial and error to determine what
dependencies were needed in Debian, as opposed to the more simple and direct
package naming conventions in Arch Linux.

### AUR to MPR changes

The only changes I noticed were:

* different naming conventions from Debian in depencencies
    * `qtbase5-dev` needed to be added
    * packages with the suffix `*-dev` are important for "development" packages
      -- i.e., building [Qt](https://en.wikipedia.org/wiki/Qt_(software))
      applications from source, which is what we are doing here in this AUR/MPR
      package
    * `qt-make` is most likely a dependency for the make process, but not at
      runtime
* adding `git submodule update --remote` at the end of each `git submodule init`
  "stanza"
    * this prevents a git commit mismatch -- I am not sure if this behavior is
      due to Debian "modifying" Git from upstream

## Credit

Credit goes to:

* Fabio 'Lolix' Loli ([@FabioLolix](https://github.com/FabioLolix)) as the
  current AUR maintainer
* erk `<v at erk dot io>` as an AUR contributor

Consideration goes to:

* Pop!\_OS, for fighting the good fight against Canonical's monotonically
  regressive changes to Ubuntu (except for -- this is an upstream change from
  Ubuntu)
* The [`makedeb`](https://www.makedeb.org/) project, for giving a pragmatic path
  for `npm`, Node&period;js, and/or Electron application binaries to be used on
  Debian- or Ubuntu-based Linux distros when maintainers do not have any plans
  to make a custom APT repository
    * Some examples from the MPR include:
        * [`electronmail-bin`](https://mpr.makedeb.org/packages/electronmail-bin)
        * [`freetube-bin`](https://mpr.makedeb.org/packages/freetube-bin)
        * [`tutanota-desktop-bin`](https://mpr.makedeb.org/packages/tutanota-desktop-bin)
    * A counter example would be [Signal Desktop](https://signal.org/download/linux/)

## License

The PKGBUILD is licensed under the GPLv3 license.

(This is not to be confused with [VNote](https://github.com/vnotex/vnote) being
licensed under the [LGPLv3](https://github.com/vnotex/vnote/blob/master/COPYING.LESSER)
license.)

### Aside

I do not know if declaring a FOSS license for a `PKGBUILD` actually matters --
however, if this is not correct convention, then I will change the license or
remove it in the future.
