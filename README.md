# qtum-snapshot
A snapshot of the Qtum source code

This is a snapshot of the prototype source code for evaluation purposes only. You can setup a functioning mainnet or testnet network, but this version has several known bugs, and we do not recommend making it public, and only using it for evaluation. 

Details:

* Based on Bitcoin 0.13.2
* Implements PoS v3.0
* Includes a port of the EVM
* Includes an early version of the Qtum Account Abstraction Layer

No support is provided for this release, and it is released “AS-IS” without indemnification, support or warranty of any kind, expressed or implied.

[Download Link](https://github.com/qtumproject/qtum-snapshot/releases/download/prototype-snapshot/qtum.zip)


# Build instructions

For Ubuntu 16.04 LTS (though we know it works on OSX and Arch Linux as well, these instructions don't cover those)

    #bitcoin deps
    sudo apt-get install git build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
    sudo apt-get install libboost-all-dev
    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:bitcoin/bitcoin
    sudo apt-get update
    sudo apt-get install libdb4.8-dev libdb4.8++-dev
    #qt (optional)
    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler


    #install crypto++
    git clone https://github.com/weidai11/cryptopp
    cd cryptopp
    git checkout CRYPTOPP_5_6_4
    export CXXFLAGS="-DNDEBUG -O2" # add -g2 for debug
    make -j2 shared static
    make install #on production systems, you might want to use an install prefix instead to keep your system dirs clean

    #build qtum (use chmod +x where needed, sorry about not preserving permissions)
    chmod +x share/genbuild.sh
    chmod +x autogen.sh
    ./autogen.sh
    ./configure
    make -j3

You may have to mess with LD_LIBRARY_PATH if you get an error about a missing shared libary.

Afterwards you can run it. There is some kind of weird bug with the RPC, so you may need to manually specify -rpcport, -rpcuser, and -rpcpassword to both quantumd and quantum-cli

Use the `generate` command to create blocks, including PoS blocks. 
