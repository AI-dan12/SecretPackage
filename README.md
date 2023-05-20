# SecretPackage
In simple words: A small program that will create a secret .deb package with a hidden malicious payload

## How does this program work (in detail)
When developing malware, there are multiple ways in which you can hide a malicious payload in plain sight. One of the well known methods is considered
in the form of a 'trojan horse', in which the initial program looks to be completely innocent however in fact has malicious 
intentions behind it. 

What my program will essentially do is that it will pretend to be a well known debian/ubuntu package known as 'cowsay'. Usually, this can
be considered completely normal to the ordinary person, and this package is in fact a normal program that returns text-based ASCII
art animal prompts. However, this program rather takes advantage of this, by embedding a malicious payload before allowing the package
to be sent to someone.

#### Typical cowsay program
![image](https://github.com/AI-dan12/SecretPackage/assets/127414645/132ac8da-f4cd-40c1-8aca-0f10947058a7)

What exactly will happen if the target installs and runs this program? Well, this will spawn something known as a reverse shell prompt. A reverse
shell is a well known term in network security that involves exploiting the target system and connecting back to the attacker. In a typical connection, it would usually
involve someone sending a request to their target, and then the target will be listening for any connections. If a request is found and it's valid, then it's accepted by
the listener at which point the two ends are connected and can send data reliably. However, a reverse shell completely turns this idea on its head, and instead the attacker
who would usually be the one sending out a request, instead takes on the role of the listener. Therefore, the target would be the one sending out the request. As long as the
reverse shell program can be executed on the target system, then this would allow the attacker to gain remote access to their target.

The reason why this is preferred over a non-reverse connection is due to the fact that the target's firewall can block/deny any suspicious incoming requests. This would defeat the
point of remote access. However, firewalls will generally allow outgoing requests from the user, unless specifically stated otherwise with security methods such as whitelisting etc.
So, what this allows for is the ability to create a seemingly normal and stable connection between the attacker and target, without causing any problems.

#### Principles of a reverse shell
![image](https://github.com/AI-dan12/SecretPackage/assets/127414645/a62a020e-8bb3-41b5-830c-f5aacf9b5477)

SecretPackage uses a popular exploitation framework known as Metasploit. This will provide the program needed to create a reverse shell connection. The original purpose of this program is for automation and it was intended for another project **that has now been abandoned**, which I will explain more about later on. This program focuses solely on
creating an efficient program that can be run to create, deploy and instantiate a session that allows a reverse shell connection. 

#### Okay now here's the step by step process of the program below
Note that this program must be run as root. If msfconsole (the program that runs metasploit) is not
installed, then I have written a shell script called 'install.sh' that will install all the necessary dependencies - this must also be run as root. I then allow the user to choose the payload that they wish to run. The way that this program works is that the payload has to already be written, as it essentially creates the package and the reverse shell, however not the actual payload that desires to be sent. 
A few checks will be performed to ensure that the payload is valid, and then the host address is given and stored into a constant. If no host address is given, then it will be automatically found by capturing a portion of the output from the hostname command using awk in the terminal. After all these checks have been fulfilled, and a hostname has been provided, then the program will display its banner
and then run the cowsay installation. The package will then be constructed by making a new directory and writing all the necessary files commonly found inside a normal deb package. At some point, your desired payload will be embedded into the postinst file that determines what gets run after the package has been extracted from a zip file. After this has been complete, the reverse shell payload will be run using the metasploit console, and the deb package will be built before allowing to be sent to the target. The final thing that will be run is a listener for the reverse shell connection. This listener must be kept running in a terminal if the attacker wishes to receive a potential connection. Also, the deb package must be sent to the target system to be run, although how this is done is outside the scope of the program. 

## What was the purpose of this program?
This program was a small sidepiece to a much larger spyware program that I wrote called 'Sly Eye'. I eventually abandoned Sly Eye because it became too complex for the skillset that I had at the time, although it was a great learning experience. This is also the reason why this program requires you to provide a payload that already exists - due to me having written my own scripts for a server/client connection on Sly Eye. Although this is a slight inconvenience, it won't be too hard for people to find such a payload or make one themselves.

## Contact 
I'm probably not going to be updating this package anymore, and I just decided to include it on my repository to focus on what I have achieved in the past. 

Nonetheless, if you need to contact me about something relating to the program then my email is below:

acatchpool@protonmail.com
