.set GIT=https://github.com/zeromq/curvezmq
.sub 0MQ=ØMQ

# CurveZMQ - authentication and encryption library

CurveZMQ implements the http://rfc.zeromq.org/spec:26 elliptic curve security mechanism and makes it easy to use in ZeroMQ applications. This library is primarily a reference implementation for the specification but may also be used for end-to-end security.

The ZeroMQ core library has its own implementation of CurveZMQ over TCP, since July 2013. This library is intended:

* To facilitate CurveZMQ implementations in other languages by providing a reference implementation.
* To provide security for older versions of ZeroMQ.
* To provide end-to-end security over untrusted intermediaries, for instance between two chat clients connected over a public ZeroMQ-based chat server.
* To provide security over other transports that fit the one-to-one model (it will not work over multicast).

CurveZMQ creates encrypted sessions ("connections") between two peers using short term keys that it securely exchanges using long term keys. When the session is over, both sides discard their short term keys, rendering the encrypted data unreadable, even if the long term keys are captured. It is not designed for long term encryption of data. 

The design of CurveZMQ stays as close as possible to the security handshake of [CurveCP](http://curvecp.org), a protocol designed to run over UDP.

## Ownership and License

CurveZMQ's contributors are listed in the AUTHORS file. It is held by the ZeroMQ organization at github.com. The authors of CurveZMQ grant you use of this software under the terms of the GNU Lesser General Public License (LGPL). For details see the files `COPYING` and `COPYING.LESSER` in this directory.

## Contributing

This project uses the [C4.1 (Collective Code Construction Contract)](http://rfc.zeromq.org/spec:22) process for contributions.

This project uses the [CLASS (C Language Style for Scalabilty)](http://rfc.zeromq.org/spec:21) guide for code style.

To report an issue, use the [CurveZMQ issue tracker]($(GIT)/issues) at github.com.

## Dependencies

This project needs these projects:

* libsodium - git://github.com/jedisct1/libsodium.git
* libzmq - git://github.com/zeromq/libzmq.git
* libczmq - git://github.com/zeromq/czmq.git

## Building and Installing

This project uses autotools for packaging. To build from git (all example commands are for Linux):

    #   libsodium
    git clone git://github.com/jedisct1/libsodium.git
    cd libsodium
    ./autogen.sh
    ./configure && make check
    sudo make install
    sudo ldconfig
    cd ..

    #   libzmq
    git clone git://github.com/zeromq/libzmq.git
    cd libzmq
    ./autogen.sh
    ./configure && make check
    sudo make install
    sudo ldconfig
    cd ..

    #   CZMQ
    git clone git://github.com/zeromq/czmq.git
    cd czmq
    ./autogen.sh
    ./configure && make check
    sudo make install
    sudo ldconfig
    cd ..

    git clone git://github.com/zeromq/curvezmq.git
    cd curvezmq
    sh autogen.sh
    ./autogen.sh
    ./configure && make check
    sudo make install
    sudo ldconfig
    cd ..

You will need the libtool and autotools packages. On FreeBSD, you may need to specify the default directories for configure:

    ./configure --with-libzmq=/usr/local

## Linking with an Application

Include `curvezmq.h` in your application and link with libcurvezmq. Here is a typical gcc link command:

    gcc -lcurvezmq -lzmq -lczmq myapp.c -o myapp

## Documentation

All documentation is provided in the doc/ subdirectory.
