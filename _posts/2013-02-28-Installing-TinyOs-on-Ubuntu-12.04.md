---
title: "Installing TinyOs on Ubuntu 12.04"
description: "How to install TinyOs in Ubuntu"
layout: post
tags: jounal, tniyos
category: academic
comments: true

---


A great morning, I reached the College too early(I think 7:50). I had a strong desire to successfully install TinyOs on my Ubuntu12.04….ummm..i had been trying for over a day…


I followed some blog got huge error while running. But tried again and again and again :( :( :( …Finally @around 15:00 i installed and build successfully on my local :-) .


Here the steps to install…


TinyOS is an open source, BSD-licensed operating system designed for low-power wireless devices, such as those used in sensor networks, ubiquitous computing, personal area networks, smart buildings, and smart meters. Source www.tinyos.net

Suggestions:::

**1. Install Java**
TinyOS 2.1 requires the Java 6 JDK in order to make use of its PC to mote communication libraries. If you do not have Java 6 installed, run the following from a command line:

	$ sudo apt-get install sun-java6-jdk

You will need to make the java and javac commands point to the installed Java 6 if you have multiple Java versions installed. Otherwise, you will get errors when trying to compile or run the TinyOS Java libraries. To make java point to Java 6, run the following and select Java 6:

	$ sudo update-alternatives –config java

For the java compiler command,javac, run:

	$ sudo update-alternatives –config javac


**2.To EDIT Sources.list**

	$ sudo gedit /etc/apt/sources.list *Kindly take a copy of source file before editing it :)

In the file sources.list that would be opened add the following lines at the end of the file and save
and close the file afterwards :

**_tinyos Installation_**

	$ deb http://tinyos.stanford.edu/tinyos/dists/ubuntu <distribution> main
	*Set <distribution> = {edgy, feisty, gutsy, hardy, jaunty, karmic, lucid} depending 
	on your Ubuntu distribution. Next, we update the repository cache from a terminal window:
	Eg: For Ubuntu 12.04 deb http://tinyos.stanford.edu/tinyos/dists/ubuntu lucid main
 

 

**3.Update the apt-get repository using this command:**

	$ sudo apt-get update

**4.Install TinyOS through apt-get**
	
	$sudo apt-get install tinyos-2.1.1
 

**5.In-order to execute the compile the nesc codes you may need to change the ownership of TinyOS root directory to your user.**

	$ sudo chown bhartesh:bhartesh -R /opt/tinyos-2.1.1/
 

**6.Install python development package (headers) (*optional only for TOSSIM)**

	$ sudo apt-get install python-dev
 

**7.Now, we configure environment variables and install the TinyOS Java toolset. Add the following to your.bashrc file:**

	export TOSROOT=/opt/tinyos-2.1.1
	export TOSDIR=$TOSROOT/tos
	export CLASSPATH=$TOSROOT/support/sdk/java/tinyos.jar:.:$CLASSPATH
	export MAKERULES=$TOSROOT/support/make/Makerules
	export PATH=/opt/msp430/bin:$PATH

**8.Install the Java tools by:**

	$sudo tos-install-jni

Its show like this :Installing 64-bit Java JNI code in /usr/lib/jvm/java-6-openjdk-amd64/jre/lib/amd64 ....
done
 

**9.Installing Java docs**

Go to/opt/tinyos-2.1.1/support/sdk/java

	$make
	$make install $make javadoc 
 
**10.Compiling and installing my first TinyOS program**
Go to opt/tinyos-2.1.1/apps/Blink and compile the code using command make.

	$make micaz

**It Output as: **

>	mkdir -p build/micaz compiling BlinkAppC to a micaz binary ncc -o 
	build/micaz/main.exe-Os -fnesc-separator=__ -Wall -Wshadow -
	Wnesc-all -target=micaz -fnesc-cfile=build/micaz/app.c -board=micasb
	 -DDEFINED_TOS_AM_GROUP=0x22 --param max-inline-insns-single=1
	00000 -DIDENT_APPNAME="BlinkAppC" -DIDENT_USERNAME=
	"bhartesh" -DIDENT_HOSTNAME="ATI" -DIDENT_USERHASH=
	0x9ec8e428L -DIDENT_TIMESTAMP=0x50b486edL -DIDENT_UIDHASH
	=0xef33ececL -fnesc-dump=wiring -fnesc-dump='interfaces(!abstract())' -fnesc
	-dump='referenced(interfacedefs, components)' -fnesc-dumpfile=build/micaz
	/wiring-check.xml BlinkAppC.nc -lm compiled BlinkAppC to build/micaz/main.exe
	2048 bytes in ROM 
	51 bytes in RAM 
	avr-objcopy --output-target=srec build/micaz/main.exe build/micaz/main.
	srec avr-objcopy --output-target=ihex build/micaz/main.exe build/micaz/main.ihex
	 writing TOS image
