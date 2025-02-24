today's video is proudly sponsored by
lenode
the note has been doing cloud computing
since 2003 which is actually before
amazon web services was even a thing
on the notes platform you can get your
server up and running in minutes
and they include all the popular
distributions such as debian fedora
ubuntu and get this even arch linux
and let's be honest what could be better
than a linux focus cloud server provider
that lets you tell all of your friends i
run arch the note has multiple server
plans available to make any app scalable
and flexible you could use it to host a
blog a vpn server a minecraft server and
much more
in fact lenode is the platform of choice
to host the entire web presence of
learnlinux tv
in addition the note offers 24x7 365
support regardless of plan size so you
can get help from a live person when you
need it
new users can get started right now with
one hundred dollars towards your new
account and i highly recommend you check
them out because lenode is awesome
and now let's get started with today's
video
[Music]
hello and welcome back to my proxmox
course here in class number five we'll
be creating our first virtual machine
and i'm really excited for this because
starting now everything that we go over
is going to build on the last thing that
we went over so it's going to be a lot
more fun going forward so let's dive
into the process of creating our first
virtual machine
so like i mentioned in the intro in this
particular class what we're going to be
doing is walking through the process of
creating a virtual machine
and before we do that we really should
take a look at our resources and just
make sure that we have enough memory
available in order to create a virtual
machine
so as you can see i have quite a bit of
memory free i don't think i'm going to
run out anytime soon on your end unless
you are working ahead you probably don't
have any virtual machines either so
unless you have a host that has very
little in the way of ram
you actually should have no problem
creating a virtual machine
then again some of my audience you guys
are using things like intel nux and some
of those well they don't have as much
ram as others
so you might be a little starved for
memory and in that case if you are a
container like i mentioned in the
previous episode probably makes more
sense
but anyway on my end i'm good i have
plenty of memory free plenty of cpu free
i can go ahead and continue
if yours is actually trending to be very
high in ram and or cpu
well you might want to find out why
before you continue anyway
what i'm going to do is click create vm
like you see right here
and now let's walk through the process
so the first thing we're going to do is
select a node it's automatically
selected node 1 for me that makes sense
considering i haven't even added a
second node yet i don't have a cluster
so i only have this one node
as you would expect when i drop it down
we only see that one node
now right here we have the id and that's
very very important
each resource needs its own id and by
resource i mean containers and virtual
machines
and the thing to keep in mind here is
that the id always needs to be unique so
if i assign this virtual machine an id
of 100 then that means that i'm not able
to use 100 for the id anywhere else i
can't have another virtual machine in
that case with an id of 100 if i've
already used it that also means that i
can't have a container with an id of 100
either again it has to be unique
100 is okay i'll leave it up to you but
i'm always a fan of setting up some kind
of a scheme here so for example i might
have 100 to 200 being reserved for
containers
maybe 300 to 400 is for virtual machines
i might even have a different grouping
for templates and things like that as
well
of course i'm getting ahead of myself
i'm just letting you know that it's
something that you might want to
consider
but if you don't have a preference what
it's going to do is select the next
available id number starting at 100 like
you see here
when i create another virtual machine
it's going to create it with an id of
101.
of course i could actually just go here
and change that to whatever i want it to
be
i'm going to leave it at 100 though to
keep it simple
just keep in mind that you do have full
control over what number you want
assigned as far as id to each virtual
machine and container
i recommend that you give it a name if
you already have a hostname picked out i
recommend that you use that so you could
have something like web server for
example
in fact i'm going to leave it on that
i just recommend that you give it a name
that helps you identify what it actually
is so you can name it after its purpose
or its host name if you have one domain
name if you have one i'll leave it up to
you
so we give it a descriptive name
and then we drop down where it shows
resource pool we don't actually have one
yet we'll go over that later but if you
did have resource pools set up then you
select the one that matches the use case
for that particular virtual machine
again we'll cover that later
next what we're going to do is go to os
we can also click next or back down here
as well if we want to
what we need to do is actually give it
an iso image and that's important
because we need to have installation
media for the virtual machine
so even if you're setting up windows or
linux whatever it is you have to have an
iso image for that operating system
now i don't have any iso images
currently under storage it defaults to
local
but i don't actually have anything other
than local here
so in that case we can't actually
continue because we have no iso image
so what i'm going to do is add an iso
image and then i'll come back to this so
i'm going to x out right here
so i'm going to drop this down i'm going
to click on local right here
and as you can see we have a section for
iso images
now what's really cool is we can click
this button here to download from a url
you can also upload an iso image as well
if we already have it downloaded
so what i'm going to do is just download
ubuntu server
so i'll go to ubuntu.com
then up here i'll select download
i'll choose ubuntu server
and then manual
and what i'm going to do is download
ubuntu server 2004.2 lts
of course debian works as well
but ubuntu server is pretty cool so i'm
going to go with that
it's probably a good idea to have a mix
of distributions on your proxmox host
that just gives you more exposure to
other operating systems and platforms
but to keep it simple i'm just going to
stick to this
and what i'm going to do is actually
cancel it
and right here it's telling me if your
download doesn't start automatically you
can click on this button to kick off the
download
but what i'm going to do instead is
right click on it
i'm going to copy the link
and then i'm going to go over here to
proxmox
and click download from url
as you can probably guess i'm going to
paste the url right here
and if all goes well this should
actually download the ubuntu server iso
image
so i'll click query url
and that's going to automatically
determine the file name
it's basically just the end of the path
anyway
and i'll just click download i'll keep
it simple
and now it's downloading the iso image
straight to proxmox that's pretty cool
in the past before version 7.0 we used
to have to download it and then upload
it
so there was like two steps for one task
now we just paste the url in here and it
does the rest for us
and here it says task ok
and as you can see we have the iso image
listed right here so i can go back to
create vm
and again we were going to call this web
server
and now we have the iso image listed
here previously we didn't even have an
iso image at all
and that makes it really easy so i'm
going to click on that
and then here we have the type of guest
os that we will be running now you want
to make sure that you select the correct
thing here it's really important because
proxmox might be adjusting things behind
the scenes to you know to facilitate the
operating system that you intend to be
running so if you choose the wrong thing
here it's not going to really know how
to deal with that so we want to make
sure that we're honest i drop this down
we have other options
so we have linux of course
we have windows and we have other
under version
we could choose the version
i click on other
then we can choose whatever we want but
we don't really have any selections for
that i'm just going to leave it on linux
because ubuntu server is a linux
distribution so that's appropriate
i'll click next
and then here we have some additional
options for the system that we want to
take a look at for example the scuzzy
controller if i drop that down
we have a number of different options
now i'm going to leave it on its default
that should be good enough for
now and then for the graphics card i'm
going to leave that on the default as
well but we have other options here
it's not very common that any use case
will require you to change this so it's
beyond the scope
just know that it is a possibility to
configure that if you do find yourself
in a situation where that makes sense
so let's go next
now here we have some options that are
specific to the virtual hard disk
one thing that i definitely want to
point out first is that proxmox has
support for discard
that's really important for ssds
if your server storage is actually using
an ssd then you're probably going to
want to enable this
and since mine is using ssd then i will
enable that
it's just a good idea to implement trim
support which is what this does on your
guest operating systems because that
definitely helps optimize the storage
which is something you'll definitely
want to do if you can
if you're using a spinning rust hard
drive you won't want to check this box
right here and even if you do have an
ssd if the operating system you are
running in your vm if that doesn't
support discard then you won't want to
enable this
recent versions of linux and windows
should have no problem you'll definitely
want to turn this on if the host server
has ssd itself
so we have several options here we're
going to leave this alone
but if you did have any particular
reason to change the order of hard
drives on the bus for the vm you can do
that here
and here it's defaulting to local lvm
for the storage which is actually
correct
we don't have any other option anyway
but in the future
if you do implement something like
shared storage or another hard disk then
you'll be able to choose the storage
pool that you want to use right here i'm
going to leave that alone
and for the size i'm going to change
that to 16.
i think 32 is a bit overkill i'll leave
that up to you
basically you want to size the gibby
bytes to however many you think you
might need
the more data that you plan on storing
on your server determines how much
storage you actually want to allocate
for it i'll leave that up to you
let's continue
cpu
now depending on how many cores your
physical host server has
that's going to determine how many cores
you want to provide your vm right here
the more cores you have the better
but the way i would look at it is if
your server isn't really going to be
doing all that much
maybe it's just not going to be seeing
that much usage
then there's probably no reason to give
it two cores
now if you're running something like
nexcloud or something that's going to
get some serious usage you might want to
crank that up
but for right now i'm going to leave
that on one
my general rule of thumb for this is
that you should probably always use one
and only increase it if the application
that you're running is showing signs of
being starved for cpu attention
so the cpu on the vm is running at 100
all the time then there might be grounds
for increasing the number of cores i'll
leave that up to you
when in doubt start at one if things are
running slow or the system requirements
for the application you want to run
imply that you'll need more go ahead and
adjust it accordingly
when it comes to memory
i'm going to leave it at 2 gigabytes
generally i don't recommend less than
one
which would be exactly half of this
but i have plenty of memory on my server
as you just saw
so two gigabytes that's not really going
to hurt me any i think one is probably a
safe minimum for most people
512 megabytes is probably even better
because it'll stretch it a little bit
further
but unfortunately i don't really know
what kind of hardware you have or
whether or not that's possible
and some operating systems actually
require more than that just for the
installation alone so your results might
vary
if you do set this to a lower number and
the operating system installation
process crashes
more often than not it's because you set
this too low
anyway i'll continue
now here i want you to pay special
attention to this even though we're not
actually going to be straying from the
defaults this time
in the future it's a good idea to
separate the management interface in the
vm network
now we can't do that because we only
have this interface right here
vmbr0
or vm bridge zero
and that's okay that's all we need right
now in the future i do recommend that
you set up an additional network we'll
get to that later but for right now i'll
leave that alone so that's what i want
you to keep in mind that it's a good
idea to separate the management network
and the vm network which we'll do later
so i'll click next
and then it's given us a summary
so i could actually start the vm right
here if i'd like to which i'm not going
to do
i'll just click finish for now
now we can see 100 right here which is
the id
and then the name was just added here
so the vm is created it's not running
though
but before we run it let's just have a
look at the options so if i click on it
and then i go down here to options
i'm not going to go over all of these
options right here but there's a few
that you definitely want to keep in mind
start at boot is especially important if
you reboot your server and this is set
to no then this virtual machine will not
automatically start in that case you'll
need to log into your proxmox interface
and then start it manually
most of the time especially for
production vms you will want them to
automatically start
and since this is highlighted i can
click on edit
i can check this box right here and
click ok
we also have a start and shutdown order
and that's helpful if you need to make
sure a particular vm is started before
another one you can configure that here
a good example of that is if you have a
database server and you have other vms
that rely on that database server
then you certainly won't want those vms
to start before the database server does
you're going to want to make sure that
the database server starts first
so if i edit this
we can essentially give it a number of
priority
i'm not going to do that right now
because well we only have this one vm
anyway
but just keep in mind that you can
determine the order that the vms start
in and you might want to do that
now the guest agent right here that's
disabled that's okay
but we will want to turn that on later
but right now let's go ahead and start
up the server
so we have the server right here i'm
going to click on console
and it's telling me that it failed to
connect to the server
and something that i really don't like
about proxmox is when you do get this
message
it logs it right here
honestly i kind of think that's a waste
i mean i know that the console here is
going to fail if the machine is not
started i just clicked on it because i
want to see it as soon as it does start
so personally i don't really consider
that an error and sometimes a section
down here can be full of errors like
that
i'm going to ignore it
and we have the console here so let's
start it up we have a power button right
here i'll click on it
and then i'll click on start
do you really want to start the vm yes
in fact i do
now it's booting up we see the bio
screen here
and this icon should change here shortly
and there it is sometimes there's a
little bit of a delay in the icon
updating right here
you can see that the icon is now lit up
it's not dark and gray like it was
it's black it's obvious and we have the
green play button next to it
so what you see right here is the vm is
actually starting
it's the same thing that you would see
if you are starting up a physical server
with ubuntu server because it pretends
to be a physical server
so we're going to give this a moment to
start up and i'll go through the
installation process of ubuntu
should be ready to go here shortly
and here we are
so
the installation process for ubuntu
server is pretty straightforward right
now it's asking me what my primary
language is i'll press enter and now
it's giving us a chance to select a
different keyboard layout if our
keyboard layout is something other than
english us i'll leave that up to you you
can just hit the up and down arrows here
to select something and press enter on
something to change it
but that's correct in my case so i'll
just press enter on done
if you have more than one ethernet
adapter on your virtual machine you can
select the ethernet adapter here i only
have one anyway so i'll just press enter
there's no proxy in my case if your
connection does have a proxy you can
enter that here
probably unlikely but maybe some of you
will have one
for the mirror the default is usually a
good choice here it's where ubuntu will
download updates and new packages from
this default mirror is adequate i'll
press enter
and right here it's asking us if we want
to use the entire hard disk
i have an entire book on ubuntu server
if you want to know more about the
specifics here
but as far as this video is concerned we
don't really need to go any deeper than
just choosing the default so i'll just
press enter on done
enter again to confirm the changes that
we want to make
are you sure that you want to continue i
do that's going to wipe out the virtual
disk which is okay because it's a brand
new virtual disk anyway i'll press enter
and now i'm going to fill in my user
info i'll keep it simple
and enter again
i do recommend that you install openssh
that helps you remotely manage your
server which is always good
so i press the space bar to check that
box
and then i'll go down to done i'll press
enter
there's additional packages that we can
install into ubuntu server if we'd like
i'm going to skip all of these i just
press tab to immediately go down here to
done i'll press enter
and now it's installing
so i'm going to give this a few minutes
to finish installing and then i'll be
right back
all right so the installation at this
point is all done
so i'll press tab
and then down go down here to reboot now
i'll press enter
and this error message right here has
nothing to do with proxmox itself
it's just trying to unmount the virtual
cd-rom drive it's okay i'll just press
enter
and there you go
so as you can see the web server right
here as i chose to call it is booting up
and the first boot of an ubuntu server
instance is going to take longer than
subsequent boots going forward
and as you just saw the login screen was
visible
but it didn't really give me a chance to
log in as of yet
because there's some additional
configuration that ubuntu server does
before it's fully ready what we're
seeing in particular right now is cloud
init is doing its thing and i'll talk
about cloud in it later on in the series
but anyway the process should be
complete because the last thing it does
if i remember correctly is the ssh host
key fingerprints which has been done
so what i can do is just press enter
you can see the login prompt down there
i know the text is fairly small but all
i'm doing is just typing in my username
and then the password
the same username and password that we
set up during the installation process
of ubuntu server i'll press enter
preferably i should type the password
correctly
and there we go
so now we have the web server instance
so to make things easier to see what i'm
going to do is switch over to a terminal
which i just so happen to have open
already
down here on this workspace
so i'm going to ssh into that particular
node
so it's just ssh and then the user name
that we chose during installation
at and then the ip address
and that's the ip address that it was
given by dhcp on my network
i'll press enter
i'll type yes
type in the password
and we are now connected to the web
server instance via ssh
and it is running in proxmox
and we could tell that because we should
have a kvm cpu like we see here
so this is definitely running inside our
proxmox server that's pretty cool
the next thing that i recommend you do
with every instance of ubuntu server is
update it
and i have entire videos about this
subject right here so i'll spare you the
details but essentially all we're doing
is just refreshing the index and then
installing updates
so i'm running sudo apt update
and the double amper sand allows me to
chain two commands together one after
another
and then the next command is sudo
apt-dist upgrade
we have quite a few updates as you can
see that can be installed
it's just a good idea to start from a
freshly updated state so i'll press
enter
i'll let these install and then i'll be
right back
all right so that's done
and next what i suggest you do is
install the qemu guest agent for your
distribution
i'm going to show you the process right
here in ubuntu
if you're using a different distribution
then you'll have to look at the
instructions for that distribution to
load the agent but for us here on ubuntu
it's really easy so what i'm going to do
is run sudo apt install
and the package name is qemu
hyphen guest
hyphen agent just like that
so i'll press enter this should go by
pretty quickly
and it's already done
and now let's check the status of that
particular service and see if it's
running
and it's not actually running that's a
problem
so what we actually need to do is start
it up
i will need sudo for that
i change the status keyword to start so
we're going to start the service
as you can see here it's taking a little
bit of time to start up that's okay
because actually
here in the options we have the guest
agent disabled you can see that right
here
so we need to enable that
i'm going to check this box here
and click
ok
now anytime a setting turns red when you
change it what that means is that change
will not take effect until the vm is
restarted and that's okay let's go back
here to the terminal
we can see that the start of the agent
did fail that's all right
again we just enabled that option in
proxmox so that's to be expected
what i'm going to do is run sudo and
then power off
that should power off the vm i'll press
enter
then as you can see it's shut down
i go back here to options
you can see that the enabled is still a
different color it looks red to me but
the colors could be off on my display
anyway
what i'm going to do is right click and
start the vm
we can see that it's starting up
and there's no red or orange text here
it's actually enabled
the server server's ready to go
so what i'm going to do is connect back
to the server
and now i'm connected to the server
let's check the status of the qemu guest
agent service
we can see that it's running
if for some reason it wasn't running
then you could change the status keyword
to start
add sudo to the front of the command
that should start that process i don't
need to do that obviously because it is
running
so let's have a bit of fun what i'm
going to do is run sudo apt and then
install
and the package that i'm going to
install is the apache 2 package
and apache is a web server if you didn't
already know this is a web server
instance or at least that's what the
name says so that makes sense i'll just
press enter
it's a good example of nothing else
and i'm just installing the package it's
going to go by really quick
and it's already done
so back up here
we have the vm running and i have the ip
address committed to memory i don't know
why
i'm just going to type the ip address
right here of the vm it was
172.16.249.249 at least in my case
right here we see the default sample web
page for apache so not only is the vm
working
we're also able to access an application
running inside the vm as well
and that means we're in really good
shape
so now you have your own virtual machine
that's pretty cool
i'm sure you're itching to create a
bunch of virtual machines your own fleet
of vms if you will but not so fast in
the next video i'll be showing you how
to create a template of that virtual
machine
which is going to save you a lot of time
when it comes to provisioning and
launching additional virtual machines in
the future so i'll meet you over there
as soon as that video is uploaded if it
hasn't been already thanks for watching
and make sure you click that like button
if you're enjoying this series so far
and also subscribe if you haven't
already because you'll be the first to
know as soon as i have a new episode in
this series uploaded on my channel and i
have some awesome things coming so stay
tuned
[Music]
you
