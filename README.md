# bitsybox
a bitsy emulator

# build instructions

# linux

Install these dependencies if you don't have them:
 - Debian: sudo apt install build-essential nodejs sdl2-dev
 - Arch: sudo pacman -Syu base-devel nodejs sdl2
 
git clone --recursive (paste .git url from github)

cd bitsybox

make -j$(nproc)

copy the binary from the bin folder to the bitsybox_LIN one
