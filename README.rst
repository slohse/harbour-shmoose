===============================================================================
Shmoose - XMPP Client for Sailfish OS
===============================================================================

Shmoose builds on and includes code from the following projects:

* XMPP library `Swiften <https://swift.im/swiften.html>`_ from Isode
* Image picker is from `hangish <https://github.com/rogora/hangish>`_ written by Daniele Rogora

-------------------------------------------------------------------------------
Feature Stack until version 1.0
-------------------------------------------------------------------------------

* Login to Jabber server [done]
* Get roster [done]
* Send and receive messages [done]
* Notification on new messages [done]
* XEP-0184: Message Delivery Receipts [done]
* XEP-0199: XMPP Ping [done]
* XEP-0363: HTTP File Upload [partial]
* XEP-0198: Stream Management  [partial]
* XEP-0045: Multi-User Chat [ ]
* OMEMO Multi-End Message and Object Encryption [ ]
* Add, edit and delete roster items [partial]
* Make database persistent [WIP]

-------------------------------------------------------------------------------
Ready to use binaries can be found on openrepos
-------------------------------------------------------------------------------
`Shmoose on openrepos <https://openrepos.net/content/schorsch/shmoose>`_

-------------------------------------------------------------------------------
Installation
-------------------------------------------------------------------------------

On Linux do the following:

Create a working directory::

 * mkdir src
 * cd src

Fetch swift source::

 * wget https://swift.im/downloads/releases/swift-3.0/swift-3.0.tar.gz
 * tar -xzvf swift-3.0.tar.gz
 * cd swift-3.0/

Install all dependencies to build swiften::

 * ./BuildTools/InstallSwiftDependencies.sh
 * ./scons Swiften -j<Number of threads>

If you happen to have the ``libidn`` headers installed on your system (``libidn11-dev`` on Debian), SCons will not link the LibIDN under 3rdParty into libswiften.a, which in turn will cause the shmoose build to fail. To prevent that, add ``try_libidn=false libidn_bundled_enable=true`` to the build command.
   
Install dependencies to build Shmoose (example for Debian)::

 * sudo apt-get install zlib1g-dev libssl-dev libxml2-dev libstdc++-5-dev libqt5quick5 libqt5quickparticles5 libqt5quickwidgets5 libqt5qml5 libqt5network5 libqt5gui5 libqt5core5a qt5-default libglib2.0-dev libpthread-stubs0-dev

Get Shmoose source code::

 * cd ..
 * git clone https://github.com/geobra/harbour-shmoose

Either::

 * open pro file within qtreator

or use command line::

 * cd harbour-shmoose
 * qmake
 * make -j<Number of threads>

-------------------------------------------------------------------------------
To cross compile for Sailfish OS, do the following
-------------------------------------------------------------------------------

 * Get and install Sailfish OS mersdk (tested with version 1608)
 * Ssh into mersdk and do the following in a newly created directory

Fetch swift source::

 * wget https://swift.im/downloads/releases/swift-3.0/swift-3.0.tar.gz
 * tar -xzvf swift-3.0.tar.gz
 * cd swift-3.0/

Install all dependencies to build swiften::

 * sb2 -t SailfishOS-armv7hl -m sdk-install -R zypper in openssl-devel libiphb-devel libxml2-devel

Patch the BuildTools/SCons/SConstruct file to do a PIC build of the library archive

Add::

 * env.Append(CCFLAGS='-fPIC')

under the line 'env.SConscript = SConscript' on line 14

Build Swiften Library::

 * sb2 -t SailfishOS-armv7hl /bin/bash ./scons Swiften

Note that the MerSDK VM's default RAM setting of 512MB is not sufficient to build Swiften. Increasing it to 4 GB should do the trick.

Get Shmoose source code::

 * cd ..
 * git clone https://github.com/geobra/harbour-shmoose
 * cd harbour-shmoose
 * mb2 -t SailfishOS-armv7hl build


