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

We may later expand this set to additional core packages
- [ ] keycloak - is a full-featured open source software package for storing personal identity information that various
applications need once the user has verified their identity through a username password, bearer token, or API key; and
the keycloak package generates these keys. we generally do not need to worry too stringently about API keys and security
because we are running this system to and from within the home






## Hire us to build.

![ferris.bueller.png](ferris.bueller.png)

<br /><br /><br />
Starlight LLC <br />
Copyright 2025 <br />
Not licensed for commercial use <br />
