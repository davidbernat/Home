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
- [ ] ownCloud - is a reasonable and nearly full-featured Google Drive replacement to store and redundancy large storage
- [ ] gitLab - is a reasonable and nearly full-featured equivalent of GitHub for storing code repositories locally only
- [ ] openSSH - is a standard configuration to allow you to connect to your machine using the SSH process from terminals
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

basic installations and local internet configurations:
- [ ] docker - installation of docker on Ubuntu is a series of simple commands. the docker management system is
automatically configured to launch in the background at start. whether or not a container restarts 'on reboot' is
established by restart polices created for each container.
  1. install using the command `apt` which is the simplest of the application install and removal commands in Ubuntu.  
the extra steps about keyring is a way of telling `apt` how to install docker directly from the `apt` command itself.

        NOTE: https://docs.docker.com/engine/install/ubuntu/
  2. docker is now installed if the `hello-world` container operation successfully displayed its message, and reading
  closely you can see that a container named `hello-world` was downloaded (pulled) from a global public repository, and
  then run, which generated a tutorial description in the process of running, then stopped itself from running. 
  3. docker automatically creates a `docker` usergroup in the operating system which consists of all usernames with 
permission to interact with the docker management system; the username you created needs to be added to that usergroup.

        NOTE: `sudo usermod -aG docker $USER` adds `docker` usergroup permission to your username using its variable
  name `$USER` and then `newgrp docker` switches you into the newly permissioned group until you ever take yourself out.

        NOTE: https://stackoverflow.com/a/48957722
  4. we will install a tool named docker-compose that allows us to define how each docker container builds and runs by
creating a special configuration text file for each container; many applications user configuration approach. to install
simply use the `apt` package manager against: `sudo apt install docker-compose`
    
  5. we can get a feel for how docker is used and now show that docker is successfully installed by deploying our first
  web server as a test by using a preexisting containerized server that already exists in the global public docker 
  repository. for this example we will deploy a version of the container named nginx (which is a containerization of the
  same nginx we described previously). the command line to deploy a docker container uses the command `docker run` and
  uses a few additional flags to specify how we want the deployment to be characterized; in brief, `-d` (set as daemon)
  ensures that any operations or containers this container may launch on its own all stop when this deployment stops
  (that is what a daemon is, fundamentally, in computer terminology), and `-p 8080:80` sets traffic that reaches our
  machine on port 8080 (an unused port) will be allowed to enter the running container and redirected to and services
  inside waiting for traffic to arrive from port 80, the standard http port for which the default nginx server inside
  the container is waiting to hear from. this transfer of ports is a concept known as port mapping, and notice that no
  other port traffic ever reaches the inside of our container, and is blocked by the container with very little fanfare.
  The `--name web` flag provides a user chosen name to this deployed server instead of a randomly assigned name.
  Run `docker run -d -p 8080:80 --name web nginx` and you should see readout text to the terminal that shows the 
  container nginx:latest is not found locally and must be downloaded; and confirms the large file is downloaded 
  correctly by comparing the sha256 hash of the download data to the sha256 stored at the repository; the server nginx
  is now running: type `docker ps` to list each locally running container and you should see image nginx with name web.
  Finally, the familiar part: open the computer web browser (Firefox) to a private session and navigate to `http://localhost:8080` (not https).
  You should see a text web page that starts with "Welcome to nginx!". Congratulations; you have a web server, even if
  that web server is only visible from this same machine itself (as is evidenced by using `localhost` or `127.0.0.1`).
  Return to the terminal and type `docker rm -f web` and the docker management will force (`-f`) the container to stop
  running and then be deleted. If you close and restart your private browser to `http://localhost:8080` you will see the
  web server is not operating. A good rule of thumb is to test using private browsing because web browsers tend to cache
  results (in browser cookies) and then revert to the cached version of the web page when the server cannot be reached;
  you would not be surprised to know every engineer has lost countless hours sure they changed something on the backend
  only to toggle fruitlessly on a browser without seeing their change, until they delete recent cookies; but also now
  generally in the eras of infinity data we want to delete our browser cookies as infrequently as possible, or never.

  NOTE: https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/

  NOTE: https://docs.docker.com/config/containers/start-containers-automatically/

  NOTE: https://docs.docker.com/engine/security/#docker-daemon-attack-surface [very advanced; understand this and you are a hireable system operator]

  6. create `/home/$USER/_server/` to store files in one convenient location - as you build applications, and in some
cases deploy standard applications (e.g. ownCloud), it will be convenient to keep their configurations and input output
data files in one coordinated location on your new machine. every username has what is referred to as its home directory
at `/home/$USER/` and so we create the `/home/$USER/_server/` directory to store these aforementioned files; in computer
terminology `_`, the underscore, means "private", as in "only the machine or administrator should ever really need to be
in here", and `__`, the double underscore (not used here), means "internal" to imply that only the machine within that
directory itself should ever need to access that information. when we deploy ownCloud we will use its docker-compose
file instead of the `docker run` command, and we will hold that docker-compose file in `/home/$USER/_server/owncloud-docker-server/`
to store whatever we need and much of whatever that server application produces for itself.

- [ ] communicate between machines on your local area network - machines communicate through the local router, which 
assigns the local IP address of each machine; and each machine is usually by default configured to disallow all local 
inbound Internet traffic, and even then usually only previously specified (whitelisted) traffic is allowed, i.e., to a specific
IP address with URLs configured in specifically interpretable ways. The router is responsible for blocking all inbound
traffic from the global public Internet. A word of clarity: inbound refers to where the original request for information
was sent from; when your machine sends an outbound request for a global public website, by connecting to the router than
passing through to the public DNS Internet infrastructure, the return response data is, in a colloquial sense, inbound
through the router to the original requesting machine. this is not an inbound request to receive information from your 
computer; it is an inbound response carrying specifically defined data your machine and router already are expecting. an
inbound request to your machine would be like an app on your phone trying to connect to your machine while you are away
at the grocery store, external to the local area network of the machine; or, any number of inbound requests or attacks
once the global public IP address of your router is known or leaked. we will not be configuring our system (now) to 
operate outside the local network of the router; but, briefly, to do so is relatively simple for beginners and consists
of requesting a static global public Internet IP address of your router from your ISP, and then configuring your router
to forward inbound traffic to the static local area network IP of your machine. this setting is so common that you can
probably find this somewhere in the advanced settings tab of whatever app your ISP provides you to pay its bills and check
your Internet status and child use times. that global public IP address of your router is now enough to access your machine from anywhere, 
although most people take this one step further: buy a domain name; and configure its DNS settings to forward traffic 
from that domain name to the global public IP address of your router, a setting stored by the site that sold you your
domain name. that is all the global public Internet is: a set of global lookup tables and forwarding routers to a
computer somebody owns and maintains, probably running docker to serve your request its response data, performing a
system of calculations and file transfers on that machine locally. 

  1. get your local area network IP address of your new machine - this [webpage](https://linuxconfig.org/how-to-find-my-ip-address-on-ubuntu-20-04-focal-fossa-linux)
  shows the standard methods with `hostname -I` being the easiest terminal command. the local IP is usually `10.0.0.[NUM]`.
  this number can occasionally change when machines are rebooted; and your router can establish a permanent one that does
  not change; usually directly from within the app provided by your cable company or whoever provides your router. this 
  local IP address makes no sense to every computer not connected to the same router (or that is accepted by the router
  and forwarded by the router to the pre-approved local IP endpoint). this is also the reason [this meme](https://www.reddit.com/r/ProgrammerHumor/comments/pdhi77/localhost3000_breaks_friendships/) 
  is humorous. the caveat is that every machine can connect to the local IPs of the other machines on the router local area network
  but also refers to itself by an additional IP address of `127.0.0.1` so that a machine may call itself without even
  going to the router to access the other local IPs. in this documentation we may use `10.0.0.88` as the machine local IP, so
  prevent using placeholders in places where the characters `[` and `]` may have other syntactic meaning. 
  2. access your new machine from other computers using your local IP - your local IP address is enough for any computer
  connected to your router to send a request to your new machine and its servers. return to the docker nginx run command
  in the previous section and deploy a container containing the nginx server, precisely as above; you can keep that 
  container running whenever you want, and with very little system overhead, though in later sections the port 8080 will 
  be used for other applications and would cause a conflict, because low-level systems on the machine will prevent two
  servers from waiting for traffic from the same port. so deploy a container of nginx on your machine and then navigate
  any browser on your router network to its local IP at port 8080 (our `jarvis` here is `http://10.0.0.88:8080` at our local router) and you will see the
  same text webpage of "Welcome to nginx!"; you can also choose to launch your server on nearly any different port. 
  Congratulations; you engineered a network, or will after a short while of debugging. nothing to raise frustrations over.
  as a useful reference for exploration, the list of ports and what use cases have staked claims to them as their defaults
  over the years exists on Wikipedia, which makes an interesting kind of archeological ruins and yet also dark waters of the
  global public Internet.

  NOTE: https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers

   3. tell your other computers how to locate your new machine - this step provides a sort of tutorial in how computers
   use hostnames (e.g. cnn.com) to reference IP addresses. the function of the DNS layer of the global public Internet stack 
   is to hold the always-present lookup table, so that we can use words as shorthand (cnn.com) but also for longevity, so
   that cnn.com always points to some correct IP address somewhere containing CNN data even if those computers move their
   physical locations, or change their routers and Internet technology, or scale. each request to the global public
   hostname cnn.com first goes to the global public DNS layer to get an endpoint IP address instead. inside your local
   area network no such DNS service exists, and although your new machine has its own name (mine is `jarvis`) that name
   is unrelated to any Internet connectivity, just as my human name has no association to my telephone number until one
   is assigned to me, and you must call me by dialing my numbers until you add my human name to your telephone; but even
   then what you do to your phone has no bearing to my phone (machine) or the phone of anyone else. this is the `/etc/hosts`
   file of your computers, a low-level shorthand way for a computer itself to swap text hostnames for numeric IP addresses before
   executing any request outbound from the computer. the file (in MacOS and Linux, and search online for the Windows version) is
   a two column list of IP addresse hostname pairs with no magic. every outbound request from my computer checks whether
   the exact hostname (e.g. cnn.com or news.cnn.com) is in the file and makes a direct substitute to an IP address instead,
   in an analogy to DNS lookup tables, but localized only to this computer, not even the rest of the local network. it is 
   an often forgot step for tasks we will want to rely on later. we simply need to add the line `10.0.0.88     jarvis.home` 
   to the `/etc/hosts` file (on my secondary laptop etc.) and now `http://jarvis.home:8080` will be transformed to a request
   on the machine with IP `10.0.0.88`. You can edit the file using the command `sudo emacs /etc/hosts` from your computer
   terminal (and you should take a few minutes to fumble through using emacs for the first time because it will always be
   handy). Windows also has a similar host file you can find by no surprise by searching for "windows hosts file". this
   does not work for other computers with unedited `/etc/hosts` files, and we could even simply put `jarvis` or anything
   else: this computer file has no knowledge that our new machine also refers to itself as `jarvis`, a somewhat fragile,
   yet unburdensome reality. using `jarvis.home` helps us differentiate from `.com` and using the common two word hostname
   helps minimize inconveniences later when we run siloed applications such as `owncloud.jarvis.home` or `[myskillset].jarvis.home`. and
   you may notice that the first line in `/etc/hosts` is `127.0.0.1	localhost` which means that even our "special" use
   of `http://localhost:8080` was really a request to the special IP address `http://127.0.0.1:8080` which means to request
   to the computer itself without requesting information from the router.

   4. you may be asking whether your computer can be used to host servers too - after all, your laptop etc. is simply an
   operating system running on hardware; can you install docker and open terminal and launch a nginx server that can be
   reached by its own http://localhost:8080 or from your new machine itself to the appropriate local IP of your computer
   (mine is usually `10.0.0.193`). yes. the only caveat is that MacOS occasionally removes port 80 to default extra block
   any inbound http traffic from even getting to the layers of the computer that search for any active servers on that port,
   but except for that tiny caveat everything we are doing is operating system independent and computer hardware independent.

- [ ] install owncloud - ownCloud boasts the same functionality as real-time Google/DropBox with stated increased security, 
although that claim is not verified by us, and is used by CERN and several Swiss firms, including financial and crypto 
firms: about as best as our machine can get in the open source and free ecosystems. this allows us to store files from
any computer in our network as we would Google Drive and provides both a similar interactive browser interface as Google
Drive and an API in Python for our written programs to use its functionality. its shareable links are only accessible 
inside our local network (unless we open our router to accept global public Internet inbound); however, be mindful that
our machine is currently only a cloud of one machine: our files are not distributed over dozens or hundreds of redundancy
backups across multiple computers in various geographic locations; we have one hard drive, same as any external hard drive.
we will address these limitations in future updates, including selecting an inexpensive cloud provider to automatically
redundancy backup our local files here in an unreadable form to our cloud provider. it is a very good system considering
these limitations.
    1. create `/home/$USER/_server/owncloud-docker-server/docker-compose.yml` and download an ownCloud docker compose file - open a text
editor (plain text; with never rich text) to copy the docker compose text; we name our files `docker-compose.yml` which
is the tacit default choice for naming docker compose files. take a few minutes to fumble around reading the content to
familiarize yourself with the nuts and bolts of configuring a server. the "version" field refers to the version of docker
compose, not the version of the file itself; "volumes" tells docker to create three spaces on the hard drive with those
three names; "services" shows that this docker compose will actually create three individual docker servers, which is why
all this configuration is bundled in a docker compose instead of using the direct function of `docker run` to deploy one
service: here we have one service for the storage database on disk (mariadb), one for storage in memory for working with
files (redis), and one for the graphical browser interface and functions of the api to interact with its data. we see that
each service has its own various configuration: "image" is the name of the docker container (nginx in the previous example);
"container_name" is the name of the service once running; "restart" allows the service to redeploy unpon failure; "ports"
lists those ports mapping described previously; "depends_on" prevents the service from deploying if its dependencies are
not already successfully running; "environment" is a list of in-container operating system variables to set (exactly how
`$USER` is an environment variable containing your username in your machine operating system); "healthcheck" is a command
the container itself is requested every so often to make sure the container is still properly functioning internally; and
"volumes" is which volumes, which themselves correspond to file locations on the machine, the service may access, and where
inside the container a file may be written so that the file is automatically copied or stored on the persistent machine storage,
which will persist even after the container is stopped or deleted. the syntax `${OWNCLOUD_DOMAIN}` means that at deployment
the docker compose system will search the machine operating system for a environment variable named `$OWNCLOUD_DOMAIN` and 
replace its value directly before calculating its deployment: for instance, setting `$OWNCLOUD_DOMAIN=localhost:8080`
will mean that the ownCloud graphical ui can be accessed at the web hostname `localhost` and port `8080`, which we know what that means. 
  2. create `/home/$USER/_server/owncloud-docker-server/.env` and insert environmental variables - hundreds of environmental
variables are in use in the operating system, and additional variables can be created any time in a number of ways; a 
standard practice is to create a file named `.env` local to a directory where a command will be launched to contain its
specific application-specific environmental variable needs. the `.` means the "dot-file" is "hidden" and will not show up
in file directories and such unless the user specifically requests those be included. to create the `.env` file manually 
type the six lines of variables to the text file and save the file; instead is more illuminating than the `cat` command.
we want the configurations to be slightly different: `OWNCLOUD_VERSION=latest` always uses the latest version; `OWNCLOUD_DOMAIN=localhost:8000`
sets the URL to port 8000 instead of 8080 since 8080 is a common default and other applications are likely to conflict with this later; 
`HTTP_PORT=8000` does the same.
  3. launch `docker compose up -d` - read the output and you will see that three different images are downloaded and deployed
as three container services; type `docker ps` and you should see those three service deployed, and nginx if that is still running. 
notice that had you launched both owncloud at nginx on 8080 the deployment of owncloud would fail. now open your browser 
to `http://localhost:8000` (not `https://`) and you should be presented with the ownCloud login screen, using the username and 
password in the `.env` file which you should not change, and your browser is now communicating with the `owncloud` docker container
service as you click around. we will discuss the protections to secure using the default passwords later, but recognize that
once we open the service up to other computers on your local network, you computers will actually interact with nginx which 
will then forward your request to the service, then reply to nginx, which then replies to your computer. 
    4. set up owncloud to be accessible from local computers? - navigate your other computer browser to `http://10.0.0.88:8000`,
which is the local IP of your machine and the port the owncloud docker service is expecting to receive inbound requests from,
and you should be greeted by an owncloud webpage that says "You are accessing the server through an untrusted domain." but, on
the other hand, you are definitely using your computer to connect through your router to your machine and into the 
docker service you are running owncloud; congratulations! a "trusted domain" is the following: in addition to needing to
specify the exact local IP and port of the service running, a good standard is that applications already prevent all correctly
directed traffic unless specifically whitelisted to be received from that particular sender; the list of `OWNCLOUD_TRUSTED_DOMAINS` in 
`.env` only contained one entry, `localhost`, which means the service is rejecting all requests unless originating from `localhost`, 
and your most recent request was sent from a local IP address through a router, not from the machine to itself bypassing the router. 
even sending a request to `http://10.0.0.88:8000` from the machine browser itself lands at the same untrusted domains page, because
`localhost` and `10.0.0.88` are not the same Internet action, and only one has been whitelist. we will solve this in the next 
section, but note that we will not be solving this by creating a list of every trusted domain; instead we will install `nginx`
to act as a relay switch: pointing all traffic to a nginx server, which we configure to pass traffic to individual servers we
have running, and all of this traffic from nginx will be from the machine to the machine as so sent as `localhost`. this allows us
to bottle all the security configurations into one application, which also has the capacity to do all kinds of Internet relay mechanics
and scale later. but note that your local IP computers are communicating with your machine owncloud service, and we have entered
the dominion of network security from server deployment; congratulations.
  5. familiarize yourself with owncloud - login through the web UI using admin and read or delete documents included there. 
create new users and familiarize yourself with the functionalities you might as a system of Google Drive or Dropbox users.
remember that so far any shareable links are only accessible from the localhost itself; until we open up the service locally.

  NOTE: https://doc.owncloud.com/server/next/admin_manual/installation/docker/#docker-compose

- [ ] install nginx and redirect owncloud - in progress



## Hire us to build.

![ferris.bueller.png](ferris.bueller.png)

<br /><br /><br />
Starlight LLC <br />
Copyright 2025 <br />
Not licensed for commercial use <br />
