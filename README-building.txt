HOW TO BUILD WIRING ON YOUR FAVORITE PLATFORM

These instructions apply to the Wiring distribution available on
GitHub:

    https://github.com/WiringProject/Wiring


////////////////////////////////////////////////////////////////////

//// Steps for First Time Setup


1. INSTALL DEVELOPMENT TOOLS

At a minimum, you will need the following things to build Wiring:

+ A Java Development Kit (JDK). Any Oracle JDK compatible with Java
  1.5+ should work. (We make use of some com.sun.* APIs that may
  render other JDKs inoperable).

  - Windows: after installing the JDK, you'll need to:

    1. Set the environment variable JAVA_HOME to point to the JDK
    directory (by default, this goes into C:\Program
    Files\Java\jdk-VERSION\).

    2. Add the JDK's bin\ directory to your PATH (check this by
    running javac at the command prompt).

  - OS X: use Apple's. (We haven't tested with Oracle's; feedback is
    welcome).

  - Linux: you're on your own. Your distribution's package manager
    likely provides many choices.
    
    For clean minimal CentOS installation, install git, then install java. Tested with Oracle Java 
    wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-x64.rpm"

    sudo yum localinstall jre-8u60-linux-x64.rpm
    
    add JAVA_HOME environment variable to startup scripts
    
    following
    https://www.digitalocean.com/community/tutorials/how-to-install-java-on-centos-and-fedora
    https://www.unixmen.com/install-oracle-java-jdk-8-centos-76-56-4/
    
    You will need to get GMP, MPFR and MPC to compile recent versions of the GCC compiler suite.
    You will also want libusb and libelf to complie AVRDUDE
    (repository versions in Cent OS 7 installed using yum seem to work)
    
    Add builds of GCC for AVR target following instructions at:
    www.nongnu.org/avr-libc/user-manual/intsall_tools.html
    Add a build of AVRDUDE following instructions at:
    www.nongnu.org/avr-libc/user-manual/intsall_tools.html
    After compling and installing avrdude, copy a file that is
    needed by the wiring IDE from the avrdude directory:
    >cp obj-avr/avrdude.conf $PREFIX/bin
    
    
+ Apache Ant.

  - Windows: download and install Ant from its Apache page:

      http://ant.apache.org/

    Pay attention to the Windows install instructions (setting
    JAVA_HOME, ANT_HOME, and updating your PATH) here:

      http://ant.apache.org/manual/install.html

    However, the recommendations that page makes about *how* to set
    environment variables are bogus; to make the settings permanent,
    you'll need to go through the usual environment variables dialog
    dance in the System control panel.

  - OS X: last we checked, Ant is included by default with the JDK.

  - Linux: you'll likely find Ant in your distribution's package
    manager (e.g. on Debian or Ubuntu: sudo apt-get install ant).
    
    For source build on Cent OS
    git clone https://git-wip-us.apache.org/repos/asf/ant
    cd ant
    sh build.sh -Ddist.dir=/usr/ant
    following
    https://www.unixmen.com/install-apache-ant-maven-tomcat-centos-76-5/

Depending on your platform, you will also need some other stuff:

1a. Windows:

    - Launch4j: You need this to build wiring.exe. After you download
      and install it, make sure that launch4jc.exe (which is in the
      top-level Launch4j folder under Program Files) is on your PATH.

      http://launch4j.sourceforge.net/

1b. Mac OS X

    - Apple's developer tools (XCode). You may be able to get by with
      just the free command line tools.

1c. Linux:

    - tar: We test with GNU tar. This is almost certainly already
      installed on your system.
    - current ant build installs an old version of avr binaries,
      once the build finishes, copy your version of avr, assuming
      PREFIX in the avr installation process is set to $HOME/local/avr
      and $WIRING_DIR is the location where Wiring was cloned to then
      >cp -r $HOME/local/avr $WIRING_DIR/Wiring/out/dist/wirint-v1.0.1-dev/tools
      
    - when building from source, be sure to add user to dialout group
      to ensure can upload code to wiring board for example using
      >sudo gpasswd --add $USER dialout

2. GRAB THE CODE FROM GITHUB

That means you'll also need Git. If you're reading this, you've
probably already got that ;). If you don't, the following GitHub guide
should help you install Git:

    http://help.github.com/set-up-git-redirect

Once that's installed, get the code with:

    $ git clone git://github.com/WiringProject/Wiring.git

3. BUILD IT

From the top-level Wiring directory, run

    $ ant

To build the Wiring IDE for your system. (This is the same thing as
running $ ant make).

NOTE: the first time you run ant, some external dependencies will be
automatically downloaded and extracted, so it may take a while. After
the first time, though, builds will go much faster.

Once it's built, use

    $ ant run

to run the Wiring IDE.

////////////////////////////////////////////////////////////////////

//// Updating to the Latest Version


4a. Each time you want to update to latest version, run

    $ git pull

    From within the Wiring directory (you may also use a Git GUI to do
    this, but that depends on your platform).

4b. If you're getting strange errors when you try to build, especially
    if significant changes have been made to the Wiring repository,
    you can clean up with:

    $ ant clean

    If you want to nuke _everything_ (compiled IDE, downloaded
    dependencies, etc.), then use:

    $ ant clean.all

    IMPORTANT: Using clean.all means your next build will require an
    internet connection, as the external dependencies will have to be
    re-downloaded. You have been warned.


////////////////////////////////////////////////////////////////////

//// The Frequently Asked Question

- What about Eclipse? Command line sucks.

  The command line stuff isn't as scary as it might initially
  seem. Hopefully it's just a matter of following the instructions
  above (and being patient).

  However, there are plenty of GUIs out there for Git etc., and
  Eclipse has good Ant integration. Wiring should build using Ant
  within Eclipse, and we're moving development over to it. However,
  we're not documenting it until the dust has settled, so for now,
  you're on your own.


////////////////////////////////////////////////////////////////////


Original author: Hernando Barragan
Current build system maintainer: Marti Bolivar <mbolivar@leaflabs.com>
