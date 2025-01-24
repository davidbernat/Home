# Flowers: a dual GPU server in progress according to Starlight LLC
#### (and the original Stargates. Yes, OpenAI is lying. we are doing this for the money.)

### build dual GPU server for deep learning

These specifications complete a 2-GPU server built from hardware components totalling under $600 plus the cost of two
RTX 3050 8GB class GPUs, for a total of $1100 which allows concurrent training server inference for 100% uptime with
roughly state-of-the-art 2023 models (current year minus two). These computers use Ubuntu and on-prem open source
resources to minimize off-prem resource loading and will use the cloudnode system for development of services in Python.
These RTX 3050 8GB class GPUs are sufficient for real-time streaming video analysis and RAG generation models, thereby
satisfying the most arduous constraints on such a system, and are built with standardized hardware components that allow
all components to be flexibly sourced as stocks and performance changes into the future.

### going from components shopping to loading the operating system

#### building
Parts List: https://pcpartpicker.com/list/3XKCrM

PartPicker is an invaluable resource for making sure each component integrates without conflicts.

additional integration notes:
1. the 3050/3080 class of GPU fits the length of the standard motherboard size and has a width of 2 PCI slots, which is
   the limiting factor in how many GPUs fit physically on a board. the 4000 and 5000 series GPUs are larger and longer, and
   mark a major break in the industry, at only 3-5x increases in speed, which is why we stuck with the 3050/3080 series. It
   means that the total footprint of the computer can be roughly the size of a crowded motherboard unit, and with a power
   supply until 1000W, which means cooling requirements can be met with stock fans and cases can be as small as two large
   shoe boxes. in other words, this system meets nearly all your goals unless you specifically need a massive GPU for use
   cases with exceptionally large models, in which case you need high performance single-GPU compute builds, or you expect
   to be operating at a scale where industrial 8-GPU servers to operate a server center, which can be thought of as the
   upgrade from this 3050/3080 class server in volume.
2. the high quality power supply purchased is more than necessary in case I test out larger GPUs; and the case is much
   larger than necessary for personal aesthetic reasons; and the motherboard does not have Wi-Fi/Bluetooth integrated,
   which is not ideal. there are more than enough USB ports; but keep in mind that you want to purchase a USB Wi-Fi or PCIe
   that supports Ubuntu out of the box because you will not have Internet access to download drivers unless you tether your
   phone.

additional build notes:
1. motherboard attaches to case, then CPU to motherboard, then GPUs, memory, power supply, hard drive, then cables.
2. be careful with the parts, but most are robust to physical pushing and electrostatic shock; in other words, push hard
   but not too hard, don't slide metal contacts across your pristine new metal case, and you do not need to worry about
   grounding yourself: nearly every part is designed to be standardized and to fit in the clearly most obvious way. tighten
   the screws tight but not too tight, and not more than about 95%. the RAM modules are usually designed to go in the
   second and fourth slots; the CPU and fan should be oriented so the language reads correctly; all the parts are included.
3. USB 3.0 is nearly as fast as connecting directly to the motherboard nowadays which means USB Wi-Fi is easier than a
   PCIe board with nearly no loss of quality; and that very large storage requirements can be delivered by USB drives which
   you swap between machines; i.e., buy a large internal hard drive but when you imagine crunching thousands of hours of
   video files imaging yourself buying large USB drives for expansion or attaching directly to your home backup storage.

getting to the Ubuntu OS screen
1. when the components are integrated the machine should boot up naturally to the OS of the motherboard, called its BIOS
   screen, displaying the CPU and RAM characteristics, and menus to access all the fundamental sensor data of the hardware;
   this is the load screen which allows entering into a software OS or recovery mode or to configure fundamental settings.
   the monitor can be plugged into an HDMI in the GPU or directly in to the motherboard; and any mouse or keyboard plugged
   in should be working at this stage, even by USB: you have a machine.
2. to install Ubuntu on your machine search for "Ubuntu create a bootable USB stick on macOS" (or Windows, etc.) and find
   the ubuntu.com instructions. the task will be to download a roughly 5GB .iso file containing the software in a format
   that can be written to a DVD; then downloading what is called a flash kit to transfer the .iso file to your USB drive in
   a way that the BIOS will recognize as contents to boot up at its start. the steps are easy and should take you minutes.
3. insert the USB into your machine and reboot, select the Ubuntu option, and the USB will walk you through steps that
   will format your hard drive and transfer over the Ubuntu OS. you want the standard and minimal options which will copy
   nearly all the applications you are probably familiar with (browsers, drivers, settings, installations, documents,
   terminal, etc). you will need to select a root admin username and password, and a machine name which will nearly always
   be the primary way of referring to the machine instead of its IP address, even in a local area network. we have selected
   the name `jarvis` and will periodically refer to our machine as `jarvis` in documentation. transfer of the Ubuntu OS
   will complete, you will reboot, and now your machine defaults to landing on the Ubuntu OS: you did it.

### going from Ubuntu to a programmer station and internet server

So far what you have now is a computer with an operating system capable of being transformed into any other sort of
computer, including to play games, perform work, view movies, same as any other. What we are doing is customizing our
`jarvis` to be localized to data creation and processing, a process known as on-prem, and mostly disconnected from the
external Internet, a configuration known as off-grid.

We will install additional Ubuntu packages to enable different functionalities, then a set of programs to enable
familiar workflow patterns that uses software running on this machine instead of the broader cloud of the Internet.

- [ ] nginx - is a low-level system which handles all inbound traffic to the machine, from other computers in the local
  network or external Internet, and redirects those to locally running computer applications on machine known as services.
- [ ] Docker - is a container system for bottling applications and servers inside a sort-of replicated virtual computer,
  which allows programs to be bottled up as services, without needing to access the entire machine, designed to be
  scalable and shareable, and to crash in ways that would not impact other services and applications. It is very common
  for services and applications to be shared as what are called dockerized containers, which can then be downloaded just
  like applications and run, interacted with by creating Internet actions instead of clicks on an interactive application.
- [ ] gitLab - is a reasonable and nearly full-featured equivalent of GitHub for storing code repositories locally only
- [ ] ownCloud - is a reasonable and nearly full-featured Google Drive replacement to store and redundancy large storage
- [ ] Python - is the programming language most deep learning is coded in, and one of the most popular program languages

This system will be available to all local area network connected interfaces, i.e., all those which are connected to the
home router, but not yet accessible to the external Internet because that traffic is blocked by the router firewall. all
traffic that reaches programs running on the machine will enter through nginx to be redirected to any application needed.

We may later expand this set to additional core packages:
- [ ] keycloak - is a full-featured open source software package for storing personal identity information that various
  applications need once the user has verified their identity through a username password, bearer token, or API key; and
  the keycloak package generates these keys. we generally do not need to worry too stringently about API keys and security
  because we are running this system to and from within the home

what is docker? 

- [ ] docker is a magical and revolutionary tool which transformed the computer industry into the modern cloud-oriented
application-based ecosystem of connectivity we know today - docker at its fundamentals wraps a system of software in a
virtualized operating system environment at nearly no cost of memory overhead or latency that makes secure encapsulated
runtime environments that can be redeployed at scale and across machines differing in fundamentals. it is amazing. each
machine has thousands of particularities including excruciatingly fine details such as where essential program details
may be located on disk, and gigantic differences like fundamental substructure operation of monitors and processors on 
the different computer operating systems e.g. Windows, MacOS, Linux, and others. docker allows you to take any code or
other applications and bottle that up in what is called a container and further specify the maximum amount of RAM,
where on the disk the container may access or write files, which inbound Internet traffic is allowed into the container,
and what operating system and version is virtualized to be running inside the container; and when the container program
crashes only the container crashes. you can run multiple copies of the same container on the same machine to increase
your program scale; which is how Internet companies deploy duplicates of their servers across millions of machines by
simply changing configuration settings, allowing for the massive and effectively real-time operations of systems across
the Internet; the only caveat is that in order to deploy on different machines running different operating systems 
requires recompiling different containers which are for all intents and purposes the same inside with the wrapping built
to plug into the different hosting machines, a nuanced but remarkably effective role in system operations. for all
intents and purposes you can think of dockerized code containers as you probably think of applications on any graphical
operating system, with added benefits of customization and being able to run multiple copies. docker is so immersed in 
the Internet systems operation that most companies already provide their product as docker containers; when we install
ownCloud and gitLab, for instance, we will simply download and host their docker containers, and completely ignore all
the complicated command line compiling and configuration which can be so complicated to perform exactly correctly for 
even our machine, which we in principle are supposed to know inside and out. so our own code will usually be deployed
even on our own machine as docker containers, a functionality which cloudnode is also partially designed to do. here is
a quickly sourced evidence based description of the [overhead analytics measurement](https://stackoverflow.com/a/26149994/5573074)  of using docker everywhere.
- [ ] who owns docker - docker is private company which releases and maintains docker to open source in order to profit
from the easy hosting their machines can provide for users of open source docker containerization. yes, Microsoft and
Amazon partnered with docker in October 2014, and CIA invested through In-Q-Tel in early 2016. two months before 
Microsoft and Amazon partnered with docker, Alphabet released a system operations platform called kubernetes which uses
docker to orchestrate the difficulties of operating millions of docker containers across millions of machines, and is
still for all intents and purposes a re-map of the updated Google Borg system for us all to use in the open source; it 
is an imperfect instrumentation of the open source, and is for all intents and purposes all we have, unless you want to 
get so deep in the weeds your system operations expertise is so great that you would be qualified to manage teams of
system operators and never code a line of code for applications in your life. even in a quickly approaching future in 
which we can ask a generative coder AI to build you a function to do a specialized task, then pop that into a cloudnode
service wrapper, then deploy that as a docker container on your machine, nearly instantaneously with nearly no review, 
docker is the only standard we have available, and is Google, Microsoft, Amazon, and CIA: it is absolutely worth your
time to study the systems design concept of Promise Theory, which forms constructive assumptions servers across the
Internet and far disconnected may or may not make about critical components required to operate their piece in a larger
designed by application whole, which the individual servers may or may not know about; it is also worth reading in your
spare clock cycles, which is how programmers joke about unused processing time, about ant-assemblage and hive or swarm
intelligence, the structural logic not only of system designs of multiple component types, but how and when emergent
intelligence of the system as a whole arrives beyond the function of any one service component or not specified in its original design.

basic installations: 
- [ ] in progress

basics: 
- [ ] get your local area network IP address of your new machine. this [webpage](https://linuxconfig.org/how-to-find-my-ip-address-on-ubuntu-20-04-focal-fossa-linux)
shows the standard methods with `hostname -I` being the easiest terminal command. the local IP is usually `10.0.0.[NUM]`.
this number can occasionally change when machines are rebooted; and your router can establish a permanent one that does
not change; usually directly from within the app provided by your cable company or whoever provides your router. this 
local IP address makes no sense to every computer not connected to the same router (or that is accepted by the router
and forwarded by the router to a pre-approved local IP endpoint). this is also the reason [this meme](https://www.reddit.com/r/ProgrammerHumor/comments/pdhi77/localhost3000_breaks_friendships/) 
is humorous. the caveat is that every machine is aware of the local IPs of the other machines on the internet network
but also refers to itself by an additional IP address of `127.0.0.1` so that a machine may call itself without even
going to the router to access the local IP. in this documentation we may use `10.0.0.88` as the machine local IP.
- [ ] tell your other computers how to locate your machine. MacOS contains an `/etc/hosts` file that provides a simple
two column list from URLs hostnames to IP addresses with no magic. Everytime the MacOS machine makes an Internet action
the low-level system checks this file and substitutes the URL host with the IP address provided; this is precisely what
external Internet DNS servers do to reconcile how to deliver a URL request (e.g. cnn.com/page.html) to a specific
computer out elsewhere in the world with a specific similar public IP address. we simply need to add the line 
`10.0.0.88     jarvis.home` to the `/etc/hosts` on my secondary laptop etc. and any browser or Internet requests to 
`http://jarvis.home/page.html` we be transformed to a request for `page.html` on the machine with IP `10.0.0.88`. There
is no server running on the new machine yet so this request will fail until we implement the next steps. Windows also
has a similar host file you can find by no surprise by searching for "windows hosts file". 
- [ ] run nginx on `jarvis` to expect inbound traffic
    - first we need to understand what problem nginx solves. inbound Internet traffic lands at an IP address, and any
machine can be configured as a server to listen for inbound traffic, and inbound traffic to one machine is subdivided 
into what are called ports, ranging between 0 and 65535, e.g. `10.0.0.88:3000`. this allows a machine to relay different 
ports to different applications and services. mail servers usually run on port 25, http usually on port 80, https runs 
on port 8080, and so on, and each of your services will run on a different port. ports are entirely open to choose from,
though some clear expectations are baked into the history of the Internet, and running your server where other engineers
hard coded their expectations will create bugs. generally speaking 9000 to 9999 is wide open. we are already running
into a part of a server that needs managing (which is why we use cloudnode) but it is important to know the roots of the
Internet talking to itself among computers. nginx handles the low-level relaying for the machine, receiving IP and port
combinations and serving up specific files, redirecting to a waiting service on the machine, or redirecting elsewhere.
    - we will not be discussing the details of nginx configuration: but we do want to see what its configuration looks
like to configure nginx so that inbound traffic to `gitlab.jarvis.home` reaches the correct application on the machine.


addition server build notes: 






## Hire us to build.

![ferris.bueller.png](ferris.bueller.png)

<br /><br /><br />
Starlight LLC <br />
Copyright 2025 <br />
Not licensed for commercial use <br />
