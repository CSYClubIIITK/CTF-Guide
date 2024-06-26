# Forensic Platforms

&#x20;Above we have explored techniques for image and audio files. Now we shall see how to investigate artifacts from a disk image. We shall briefly cover the uses of Autopsy toll to perform analysis on disc images.  We will be using the Windows OS for this section.

### AUTOPSY&#x20;

Autopsy is an open source forensics platform which analyzes all mobile devices and digital media.&#x20;

We start by opening a case. We may be given an .aut file for analysis. There is an option to add data sources if required.&#x20;

In this guide we will focus on Disk image or VM File options.  The supported formats are :&#x20;

* Raw Single: (For example: \*.img, \*.dd, \*.raw, \*.bin)
* Raw Split: (For example: \*.001, \*.002, \*.aa, \*.ab, etc)
* EnCase: (For example: \*.e01, \*.e02, etc)
* Virtual Machines:  (For example: \*.vmdk, \*.vhd)

Remember, Autopsy adds metadata about files to the local database, not the actual file contents.

#### Walkthrough - Autopsy

We will be looking at an example on how Autopsy is used in CTFs. We will be using windows for this example.&#x20;

Sleuthkit Intro(PicoCTF): [https://play.picoctf.org/practice/challenge/301?category=4\&page=2](https://play.picoctf.org/practice/challenge/301?category=4\&page=2)

Download the disk image. Open Autopsy and select a new case and follow instructions. Once it has loaded, open up the disk image. You should be seeing this.

\


![](https://lh7-us.googleusercontent.com/docsz/AD\_4nXc\_bXV3KAbUdAX-8y1nib3xzdjmQEkuBdzQ56\_ZA5lJFMPzPxtUphUiDMTyMHpCF-LNSb7THiqLk0dY6Uetp\_P1ScQi-zMbFtt0LuAmp-dLxyW9GG1lh4xAFL5roPMnEwQbJSePFVukrADmPjTgMIDH8MC6?key=3tC4LW6BC-ghAujvhgrQ3Q)

\


If you are on Kali you can use mmls to get to the same.

![](https://lh7-us.googleusercontent.com/docsz/AD\_4nXc3N3wgmzcVpEZy2M0AJ1sxZZfIJdxWBdItPuR7Ho7\_FpC1rEJUi0fxox44XJIgAyxVXYJLoU7ikHh5oiW6V4XdSnqFouF8IhK29B3ouYCA9\_wqV8nL5mTDoajA-9UNJouOMLRJzzQZq34ibA9\_0Yp6TDo?key=3tC4LW6BC-ghAujvhgrQ3Q)

After this you can connect to their portal given and enter the number of the partition. The right one opens up to the key as you see above

Refer : https://otuva.medium.com/tryhackme-autopsy-walkthrough-a97468393a8a



### WIRESHARK

Wireshark is a platform that we use to analyze networks real-time. In CTF Challenges it is used to analyze pre recorded  network traffic. To record files wireshark uses PCAP files.&#x20;



To familiarize yourself with wireshark ref: [https://ctf101.org/forensics/what-is-wireshark/](https://ctf101.org/forensics/what-is-wireshark/)

Downloading Wireshark is easy. Visit their website and download the installer as per your OS.

We will be using wireshark in the below example.

Its highly recommended that you pay a visit to [https://www.wireshark.org/learn](https://www.wireshark.org/learn)

#### WALKTHROUGH - WIRESHARK

Wireshark doo dooo do (picoCTF): [https://play.picoctf.org/practice/challenge/115?category=4\&page=1](https://play.picoctf.org/practice/challenge/115?category=4\&page=1)

Open up your file in wireshark. You will see a couple TCP, HTTP protocols listed down.

Right click on one of the listed protocols(preferably the first one) and follow it. You should see a window pop up and on the bottom right you can view your selected stream. Analyze each stream for any suspicious strings.&#x20;

On the 5th one you should see something like this!&#x20;

![](https://lh7-us.googleusercontent.com/docsz/AD\_4nXdVsMV01oC18xzsmIhI8tXTGmGI\_zSEU8JPdkIdAY3UiOpIIdDPoTtizeh5189R\_CmJxeOy-XPe8UjnyxuWfYZYKT4IXViR279hkLbYTWvLedaOfGx5wnl9fRM9ITQdLR9Lxm-vEPGLMsx9A0GoFi\_U9pgj?key=3tC4LW6BC-ghAujvhgrQ3Q)

We can see what looks like a flag with { }, just that its not in are usual flag picoCTF format. The string that we see is encrypted! On close observation, we see that PGS should have been CTF, this means the cipher is ROT13!&#x20;

Simply copy paste this text to an online ROT13 decoder to get your flag, picoCTF{p33kab00\_1\_s33\_u\_deadbeef}
