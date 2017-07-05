# BeeeOn Gateway feed for LEDE

Gateway package and related packages.

## Setup (including LEDE itself)

```
git clone https://git.lede-project.org/source.git lede
cd lede
# edit feeds.conf.default
vim feeds.conf.default
# add our feed, i.e. that line:
src-git beeeon https://github.com/BeeeOn/lede-packages-frc.git
# download feeds and install all packages
./scripts/feeds update -a
./scripts/feeds install -a
# Ensure that our updated packages are used (reinstall them)
./scripts/feeds uninstall poco openzwave
./scripts/feeds install -p beeeon poco openzwave
# Start the build and wait. When the menuconfig is invoked, don't forget to select
# beeeon-gateway package.
make
```
