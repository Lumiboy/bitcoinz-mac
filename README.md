# Bitcoinz Builder for Apple Platform

![Screenshot](https://github.com/Lumiboy/bitcoinz-mac/raw/master/docs/bitcoinz-apple.png "Bitcoinz on Mac OS")

This repository builds standalone Bitcoinz binaries for macOS platform without installing brew.  
No additional dependency required except Xcode (https://developer.apple.com/xcode).  
All build tools (`autoconf, automake, libtool, pkgconfig, cmake, install and readlink`) and `Bitcoinz` are compiled from scratch (finally with `clang`).  

###  OSX - macOS.

Min. OSX version: 10.8.x  
Tested on 10.12.x :white_check_mark:  
Tested on 10.13.x :white_check_mark:  


### Build instructions
```shell
# run once to install Xcode CLI tools
$ xcode-select --install
# clone and build Bitcoinz on macOS
$ git clone https://github.com/Lumiboy/bitcoinz-mac.git
$ cd bitcoinz-mac
$ source environment
$ make
```

After successful build Bitcoinz binaries will be installed to `out` directory under project root  
You can then copy binary directory anywhere you like there are no dependencies to the build tree anymore  
```shell
bash-3.2$ ls -lrt out/usr/local/bin
total 31544
-rwxr-xr-x  1 lumi  staff       483 Dec 16 15:56 bitcoinz-init
-rwxr-xr-x  1 lumi  staff  13120252 Dec 20 01:06 bitcoinzd
-rwxr-xr-x  1 lumi  staff   1772400 Dec 20 01:06 bitcoinz-tx
-rwxr-xr-x  1 lumi  staff      4761 Dec 20 01:06 zcash-fetch-params
-rwxr-xr-x  1 lumi  staff   1237116 Dec 20 01:06 bitcoinz-cli
bash-3.2$ otool -L out/usr/local/bin/bitcoinzd
out/usr/local/bin/bitcoinzd:
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
bash-3.2$ otool -L out/usr/local/bin/bitcoinz-cli 
out/usr/local/bin/bitcoinz-cli:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
bash-3.2$ otool -L out/usr/local/bin/bitcoinz-tx
out/usr/local/bin/bitcoinz-tx:
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 307.5.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
```

### Run instructions

When launching `Bitcoinz` on MacOS for the first time, certain initalization steps should be completed.  
Please run the commands below once for the first time  

```shell
$ cd out/usr/local/bin
$ ./zcash-fetch-params
$ ./bitcoinz-init
$ ./bitcoinzd
```

You can just run `Bitcoinz` by launching the daemon afterwards  

`$ ./bitcoinzd`  

Console output from the first run is below:
```shell
bash-3.2$ ./zcash-fetch-params
Bitcoinz - fetch-params.sh

This script will fetch the Bitcoinz zkSNARK parameters and verify their
integrity with sha256sum.

If they already exist locally, it will exit now and do nothing else.
The parameters are currently just under 911MB in size, so plan accordingly
for your bandwidth constraints. If the files are already present and
have the correct sha256sum, no networking is used.

Creating params directory. For details about this directory, see:
/Users/lumi/Library/Application Support/ZcashParams/README

Retrieving: https://z.cash/downloads/sprout-proving.key
######################################################################## 100.0%
/Users/lumi/Library/Application Support/ZcashParams/sprout-proving.key.dl: OK
/Users/lumi/Library/Application Support/ZcashParams/sprout-proving.key.dl -> /Users/lumi/Library/Application Support/ZcashParams/sprout-proving.key
Retrieving: https://z.cash/downloads/sprout-verifying.key
######################################################################## 100.0%
/Users/lumi/Library/Application Support/ZcashParams/sprout-verifying.key.dl: OK
/Users/lumi/Library/Application Support/ZcashParams/sprout-verifying.key.dl -> /Users/lumi/Library/Application Support/ZcashParams/sprout-verifying.key
bash-3.2$ 
bash-3.2$ cat bitcoinz-init 
#!/bin/bash

# excerpted from zclassic/zutil/init-mac.sh

if [ ! -f "$HOME/Library/Application Support/bitcoinz/bitcoinz.conf" ]; then
    echo "Creating bitcoinz.conf"
    mkdir -p "$HOME/Library/Application Support/bitcoinz/"
    echo "rpcuser=bitcoinzrpc" > ~/Library/Application\ Support/bitcoinz/bitcoinz.conf
    PASSWORD=$(cat /dev/urandom | env LC_CTYPE=C tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    echo "rpcpassword=$PASSWORD" >> "$HOME/Library/Application Support/bitcoinz/bitcoinz.conf"
    echo "Complete!"
fi
bash-3.2$ 
bash-3.2$ ./bitcoinz-init 
Creating bitcoinz.conf
Complete!
```



## Thanks
Developers of `Bitcoinz`  
Developers of `Zcash`  
Developers of `ZClassic` for MacOS patches

## Donations
If you feel this project is useful to you. Feel free to donate.

    ZEL address: t1L6FizKPfikQatYTHydDbPnvgKhXFatiYm


### Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

