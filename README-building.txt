HOW TO BUILD WIRING ON YOUR FAVORITE PLATFORM

These instructions apply to the Wiring distribution available on
GitHub:

    https://github.com/WiringProject/Wiring


////////////////////////////////////////////////////////////////////

//// Steps for First Time Setup

GNOME Desktop Install
Add-Ons:

Developement Tools (Arendusvahendid) 
Security Tools

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
    
    In home directory /home/ttaveter
    
    For clean minimal CentOS installation, install git, then install java. Tested with Oracle Java 
    # sudo yum install git-all
    
    https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
    # sudo yum update
    
    Removed the java openjdk version
    # sudo yum remove java-1.8.0-openjdk
    
    # cd ~
    # wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-x64.rpm"

    # sudo yum localinstall jdk-8u60-linux-x64.rpm
    
    add JAVA_HOME environment variable to startup scripts
    
    For example, if you installed Java to /usr/java/jdk1.8.0_60/jre/bin (i.e. java executable is located at /usr/java/jdk1.8.0_60/jre/bin/java), you could set your JAVA_HOME environment variable in a bash shell or script like so:

    # export JAVA_HOME=/usr/java/jdk1.8.0_60/jre
    
    If you want JAVA_HOME to be set for every user on the system by default, add the previous line to the /etc/environment file. An easy way to append it to the file is to run this command:

    # sudo sh -c "echo export JAVA_HOME=/usr/java/jdk1.8.0_60/jre >> /etc/environment"
    
    # rm ~/jdk-8u60-linux-x64.rpm
    
    following
    https://www.digitalocean.com/community/tutorials/how-to-install-java-on-centos-and-fedora
    or
    https://www.unixmen.com/install-oracle-java-jdk-8-centos-76-56-4/
    
    ---------------------
    
    Installing GNU Binutils for the AVR target
    
    ------------
    sudo yum install binutils.x86_64
    -------
    or
    
    Follow instructions on 
    http://www.nongnu.org/avr-libc/user-manual/install_tools.html#install_avr_binutils
    
    Before installing make sure you are in the directory where you want to install something.
    
    Use $PREFIX to refer to whatever directory you wish to install in
    Insatalling destination can be chose with command ./configure ... with flag --prefix=install_destination folder
    
    I put downloads in home/Programmid
    and installed GMP, MPFR, MPC in /home/Install
    
    /
    First
    # PREFIX=$HOME/ttaveter/Programmid/Install
    # export PREFIX
    
    # PATH=$PATH:$PREFIX/bin
    # export PATH
    
    http://www.nongnu.org/avr-libc/user-manual/install_tools.html
    
    Find the latest version of Binutils on 
    http://ftp.gnu.org/gnu/binutils/
    open the .tar.bz2 (or .tar.gz) link in a new tab. Then copy the address, for example
    http://ftp.gnu.org/gnu/binutils/binutils-2.27.tar.gz
    
    In directory /home/ttaveter/Programmid/Source
    # wget http://ftp.gnu.org/gnu/binutils/binutils-2.27.tar.gz
    
    (If you choose .tar.bz2 file, then you need to first unzip it with
    # bunzip2 binutils-2.27.tar.bz2
    )
    
    Next unzip the .tar.gz file 
    # tar -xvf binutils-2.27.tar.gz
    
    Continue with 
    # cd binutils-2.27
    
    and next instructions from
    http://www.nongnu.org/avr-libc/user-manual/install_tools.html#install_avr_binutils
    
    # mkdir obj-avr
    # cd obj-avr
    
    Note. Before
    # ../configure --prefix=$PREFIX --target=avr --disable-nls
    It was necessary to install a compiler
    # yum install gcc.x86_64
    
    Then
    # ../configure --prefix=$PREFIX --target=avr --disable-nls
    
    # sudo make
    # sudo make check
    # sudo make install
    
    ----------------
    
    You will need to get GMP, MPFR and MPC to compile recent versions of the GCC compiler suite. Following
    
    http://stackoverflow.com/questions/9450394/how-to-install-gcc-piece-by-piece-with-gmp-mpfr-mpc-elf-without-shared-libra
    
    Quite similar as Binutils install
    
    NOTE! 
    Make sure you read the previous page carefully from the beginning. 
    Pay attention in which directory you put the downloads and in which directory you build the infrastructure.
    
    Get the GCC infrastructure:
    # wget ftp://gcc.gnu.org/pub/gcc/infrastructure/
    
    Put downloads in a temp directory (you can use whatever directory you want).
    /home/ttaveter/Programmid/Source
    
    Build the infrastructure in a temp directory that is different than the downloads directory or its subdirectories:
    /home/ttaveter/ttaveter/Programmid/Install
    
    Configure the infrastructure using static libaries like this:
    ./configure --disable-shared --enable-static --prefix=$PREFIX
    
    GMP
    
    Find the latest version of .tar.bz2 file from 
    ftp://gcc.gnu.org/pub/gcc/infrastructure/

    In directory /home/ttaveter/Programmid/Source
    # wget ftp://gcc.gnu.org/pub/gcc/infrastructure/gmp-6.1.0.tar.bz2
    
    Unzip the .tar.bz2 file
    # bunzip2 gmp-6.1.0.tar.bz2
    
    # tar -xvf gmp-6.1.0.tar
    # cd gmp-6.1.0
    
    Before
    # ./configure --disable-shared --enable-static --prefix=$PREFIX
    I needed to install another compiler
    
    # yum install m4.x86_64
    Maybe not necessary in your case.
    
    Pay attention to change the prefix according to which directory you want the GMP to be installed
    # ./configure --disable-shared --enable-static --prefix=$PREFIX
    # make && make check && make install
    
    ----------------
    
    MPFR
    
    In directory home/ttaveter/Programmid/Source
    # wget ftp://gcc.gnu.org/pub/gcc/infrastructure/mpfr-3.1.4.tar.bz2

    # bunzip2 mpfr-3.1.4.tar.bz2
    # tar -xvf mpfr-3.1.4.tar
    # cd mpfr-3.1.4           ///////  cd mpfr/3.1.4
    
    # ./configure --disable-shared --enable-static --prefix=$PREFIX --with-gmp=$PREFIX
    # make && make check && make install
    
    -----------
    
    MPC
    
    # wget ftp://gcc.gnu.org/pub/gcc/infrastructure/mpc-1.0.3.tar.gz
    # tar -xvf mpc-1.0.3.tar.gz
    # cd mpc-1.0.3
    # ./configure --disable-shared --enable-static --prefix=$PREFIX --with-gmp=$PREFIX --with-mpfr=$PREFIX
    # make && make check && make install

    -----------
    
    You will also want libusb and libelf to compile AVRDUDE
    (repository versions in Cent OS 7 installed using yum seem to work)
    
    LIBUSB
    
    # yum install libusb
    
    ----------------
    
    LIBELF
    
    # yum install elfutils-libelf-devel.x86_64
    
    --------------------
    
    Add builds of GCC for AVR target following instructions at:
    www.nongnu.org/avr-libc/user-manual/install_tools.html
    
    GCC
    
    # wget ftp://gd.tuwien.ac.at/gnu/gcc/releases/gcc-6.2.0/gcc-6.2.0.tar.bz2
    # bunzip2 gcc-6.2.0.tar.bz2
    # tar -xvf gcc-6.2.0.tar
    
    https://gcc.gnu.org/wiki/FAQ#configure
    Make a peer gcc-build directory next to the GCC source code directory
    
    # cd $HOME/Programmid
    # mkdir gcc-build
    # cd gcc-build
    
    Read important info about where to run configure from the following link.
    https://gcc.gnu.org/wiki/FAQ#configure
    
    First, I needed to install the following thing
    # yum install gcc-c++.86_64
    
    If prefix declared and exported earlier, then you can use --with-gmp=$PREFIX -with-mpfr=$PREFIX --with-mpc=$PREFIX
    
    #  /home/ttaveter/Programmid/Source/gcc-6.2.0/configure --prefix=/home/ttaveter/ttaveter/Programmid/GCC --target=avr --enable-languages=c,c++ --disable-nls --disable-libssp --disable-shared --with-gmp=$PREFIX --with-mpfr=$PREFIX --with-mpc=$PREFIX
    
    For each of the files you are using, GMP, MPFR, MPC, Libelf, you need to add the directory where these files are installed.
    
    # make
    # make check
    # make install
    
    http://stackoverflow.com/questions/9450394/how-to-install-gcc-piece-by-piece-with-gmp-mpfr-mpc-elf-without-shared-libra
    http://www.nongnu.org/avr-libc/user-manual/install_tools.html
    
    Might be helpful
    
    https://gcc.gnu.org/install/download.html
    https://gcc.gnu.org/wiki/InstallingGCC
    https://gcc.gnu.org/install/index.html
    https://gcc.gnu.org/wiki/FAQ#configure
    
    ---------
    
    Add a build of AVRDUDE following instructions at:
    www.nongnu.org/avr-libc/user-manual/install_tools.html
    
    http://download.savannah.gnu.org/releases/avrdude/
    http://download.savannah.gnu.org/releases/avrdude/avrdude-doc-6.3.tar.gz
    
    # wget download.savannah.gnu.org/releases/avrdude/avrdude-6.3.tar.gz

    # tar -xvf avrdude-6.3.tar.gz
    # cd avrdude-6.3
    # mkdir obj-avr
    # cd obj-avr
    # ../configure --prefix=$PREFIX
    # make
    # make install
    
    After compling and installing avrdude, copy a file that is
    needed by the wiring IDE from the avrdude directory:
    # cp avrdude.conf $PREFIX/bin
    
    ...............
    
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
    
    # sudo yum install ant
    
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
      
    #  sudo yum install tar.x86_64
    already installed
    
    ---------------------------- done so far
    
    need to clone Wiring code from github first
        $ git clone git://github.com/WiringProject/Wiring.git
      
    - current ant build installs an old version of avr binaries,
      once the build finishes, copy your version of avr, assuming
      PREFIX in the avr installation process is set to $HOME/local/avr
      and $WIRING_DIR is the location where Wiring was cloned to then
      >cp -r $HOME/local/avr $WIRING_DIR/Wiring/out/dist/wiring-v1.0.1-dev/tools
      
      I used the following command
      # cp -r $HOME/ttaveter/Programmid/Install/avr $HOME/Programmid/Source/Wiring/out/dist/wiring-v1.0.1-dev/tools
      
      # cp -r $HOME/ttaveter/Programmid/Install/avr $HOME/Programmid/Source/Wiring/out/dist/wiring-v1.0.1-dev/lib
      
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
