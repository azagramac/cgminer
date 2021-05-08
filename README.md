## cgminer v4.9.2
Cgminer v4.9.2, ready to compile to work with ASIC miner, Bitmain's Antminer U3 and USB Redfury. 

Compile and mine. 

### Prepare environment

    sudo apt update && sudo apt upgrade -y && sudo apt install -y build-essential git libusb-1.0-0-dev libusb-1.0-0 libcurl4-openssl-dev libncurses5-dev libudev-dev libtool automake pkg-config libjansson-dev ntp screen python-dev

### Build cgminer

    export CFLAGS="-O2 -Wall -march=native"
    export LIBCURL_CFLAGS=-I/usr/include/curl
    ./autogen.sh
    ./configure --enable-icarus --enable-bitfury
    make
    make install
    
### Copy files

    cp -rf 01-cgminer.rules /etc/udev/rules.d/
    mkdir /home/$USER/.cgminer
    cp -rf cgminer.conf /home/$USER/.cgminer/
    cp -rf cgminer.service /etc/systemd/system/

### Assign permissions

    chmod 0644 /etc/systemd/system/cgminer.service
    chmod a+x /etc/udev/rules.d/01-cgminer.rules
    usermod -G plugdev -a `whoami`

### Enable service on boot

    systemctl enable cgminer.service

### Monitor

Cgminer will start at every startup in the background, if you want to see its status you must run:

    screen -ls

It will show the process where it is running, to see the screen:

    screen -r PROCESS_NUMBER

If you want to exit, close the sale, DO NOT execute a Crlt-C or exit, because it will exit the program. 

### Single pool


    cgminer -o http://pool:port -u username -p password


### Solo mining to local bitcoind


    cgminer -o http://localhost:8332 -u username -p password --btc-address 1DCRu4pnnwtbUYRy1evVw7TzXGW8XMwMNc


### Donation

฿ 1DCRu4pnnwtbUYRy1evVw7TzXGW8XMwMNc
