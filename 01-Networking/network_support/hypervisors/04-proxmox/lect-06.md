ntro
[Music]
thank you so much for checking out
learnlinuxtv your source for linux
related fun and learning
i just love making this content for you
guys
but making such content isn't cheap
if you enjoy my content please consider
supporting me by becoming a patron
as a patron you'll enjoy ad-free
versions of every video that i upload
and also at specific tiers you'll also
enjoy early access to select videos
before the rest of the world
but even if you're not able to support
me by becoming a patron no problem
there's other ways to help you can
simply click the like button on the
videos that you enjoy that would help
out
in addition to that word of mouth helps
as well so if you are enjoying my
content please help spread the learning
by telling your friends and co-workers
about the channel
if you're looking for something to read
well you're in luck i write books and
you can check out my latest books at
learnlinux.tv
books
are you looking for help for your linux
server related projects or are you a
business that has a linux related
project that you're working on and you
need another set of hands well you're in
luck go to learnlinux.tv
request hyphen assistance there you can
check out my schedule and consider
hiring me to help you out
with all of that out of the way let's go
ahead and get started with today's video
[Music]
hello again everyone and welcome back to
A few notes about the series
learnlinux tv
i am so happy that you guys have been
enjoying my proxmox series i had a lot
of fun filming that series and as i
record this video i'm still editing the
remaining episodes depending on when
you're watching this all the episodes
might already be available but i knew
when i started recording it that i'd
have to do some standalone videos about
things that i forgot to tell you guys
about along the way
and this video right here is one of
those
in an earlier video i showed you guys
how to create a virtual machine within
proxmox we set up a linux instance
when it comes to windows the process is
a little unique so i figured that i
would need to create a standalone video
to show you guys how to install windows
on a proxmox virtual machine and that's
exactly what i'm going to do in this
video and since this is a standalone
video that means you could watch this
video along with the others or by itself
but i will show you the entire process
of setting up a windows vm so let's go
ahead and get started
What you'll need to download
all right so let's get started with
setting up windows as a virtual machine
guest on proxmox
now there's going to be a few things
that you'll need to download first
so what i'll do is i'll just click over
here to my iso repository
and as you can see i have a bunch of iso
images here
and what you're seeing right here is my
production proxmox stack
so these are all of my vms and of course
i have all of these iso images
now as you can see i already have
windows 10 and windows server 2019
downloaded to the iso repository
i'll have links down below where you can
get the iso image for windows server as
well as windows 10
so what you'll need to do is download
the iso image and then upload it here to
proxmox
another thing that you're going to need
is the iso image that contains windows
drivers for proxmox
and without that iso image you probably
won't be able to install windows at all
so what i'm going to do is just click
download from url
i'll have a link down below that you can
use to download this for yourself
so paste in the url right here i already
have a copy to my clipboard
and as you can see the file name is
going to be virtiowin.iso
so i'm going to click download
and then i'll just give this a moment to
finish and i'll be right back
and as it shows right here
the process was successful
and we have the iso image for the
drivers right here so we're good to
continue
as far as which version of windows you
install it shouldn't matter windows 10
windows server whatever you need it
should be fine the process should be
exactly the same
so what i'm going to do right now is
actually create a virtual machine
Creating the Proxmox Windows VM
and to really make this vm stand out
i'll just give it a very high number
here 995 for example just to make sure
that it shows up at the end of the list
of virtual machines
i'm just going to call it windows
then next we'll select our iso
repository wherever it is that you store
your iso images
it doesn't matter if you have shared
storage like me or if you have it local
to proxmox either way is fine
we're going to drop this down
and then we'll choose the iso image for
windows whichever one you want
so i'll just set up windows server that
should be fine
then here what we're going to do is
select microsoft windows we want to make
sure that we select the proper type
and the version of windows that i'll be
installing again is 2019 which is
included here on the version so we
should be good on this tab i'll click
next
so what you want to do is check this box
right here for the qemu agent we'll be
setting that up later but we should
definitely check this box to make sure
that the agent will be enabled as soon
as we install the software
we'll make sure that the scuzzy
controller is on vert i o scuzzy which
it already is
then for the bus we're going to choose
scuzzy
and for the disc i'm going to bump that
up to 64 gigabytes windows can be a
little bit bloated it is what it is
i'll check the discard box here because
i am actually running proxmox on an ssd
and that'll make sure that i can take
advantage of trim support
under cache what we're going to do is
set it to write back
and these are all recommendations
straight from the proxmox documentation
which is why i chose that option
in this case right back should actually
increase performance
so let's go to the next screen and for
the cpu
i'm going to give it four cores
i mean you don't have to do that i just
want it to be fast
so i think four is going to be fine for
that
for the memory i'm just going to bump it
up to 4096.
now you don't have to go as high as four
gigs but i am in my case i have plenty
of memory free on this server
in fact i could probably double this and
still be fine
but i'll leave it up to you it just
depends on what your requirements are
and that'll determine how high you need
to set that
in my case what i'm going to do is
select vmbr1
and depending how far along you are in
the proxmox series you may or may not
have created other networks yet it
doesn't really matter just choose
whatever bridge you have and if you're
far enough along you can choose a
segregated network if you want to
but in my case i'm going to choose that
one right there
i'll click next
and i'm not going to choose this box
right here
i don't want the vm to start just yet
i'm going to click finish
so as you can see here the vm is created
Adding another CD-ROM drive, mounting driver disc
and before we go any further we want to
go to hardware
and what we'll want to do is add another
cd-rom drive
so next i'll select the storage
repository that contains all of my iso
images
pretty much the same as last time
and then for the iso image what i want
to do is select the vert i o win iso
this one right here that contains all
the drivers
the thing is if you don't include this
iso image right here and attach it to
your virtual machine it's possible that
windows might not be able to see the
hard drive on your virtual server
you might get an error that mentions
that the hard drive has not been
detected
and you'll actually see that later in
this video
so i'll select this one right here
and i'll click create
so now we have two cd-rom drives
one for windows server
or whatever version of windows you
happen to be installing
and the other one is the driver disk so
at this point we should be good to start
the vm so i'll go ahead and do that
and we'll switch over here to the
console
Installing Windows Server 2019
and as you can see it's loading
right so the windows installer has
started
so i'm just going to click next
i'll click install now
and in my case for windows server i'm
going to choose the option that has the
desktop experience installed
it'll probably just make it easier to
install the drivers later it might not
be required but anyway that's what i'm
going to choose so i'll click next
so i'm just going through all the
screens here
Providing the virtio storage driver during Windows installation
and then as you can see here it doesn't
detect a hard drive at all
and that's why we have the driver disk
so i'll click load driver
i'll click browse
and here's the vert i o disk right here
i'll click ok let's see if it finds it
so i guess it's not able to search the
disk properly i'll click browse again
so what we'll do is select this folder
right here vio scuzzy
then we'll select 2k19 because that's
the version of windows that i'm
installing
and then we'll click right here where it
says amd64
now click ok
and check this out it actually found the
driver that it needed
so i'll click next
and take a look at that now it's able to
see the hard drive this wasn't listed
here before
so the driver installation worked just
fine
we will need that iso image again later
but for now what i'm going to do is just
click next
and now windows is installing so i'm
going to let this run and then i'll be
right back as soon as it's finished
all right so it looks like the process
is finished it's going to restart the vm
Adding Administrator account
so right now i'll just set up the
password for the admin account
and again
so far so good so what i'm going to do
next is just pull this tray out right
here
click the keyboard icon
and then i'll send it the virtual
version of the three finger salute
so i'll type in the password
and as you can see we have windows
server installed as a virtual machine
that's pretty cool
Installing the remaining Proxmox Windows drivers
now we're not quite finished though if i
minimize this
and then right click the start button
and then i'll bring up the device
manager
you'll notice that we'll probably have
one or more devices that are missing a
driver
i open up the file manager
you'll see that i still have the driver
iso mounted right here
and that's what we're going to use to
install the drivers
so what i'm going to do is right click
this device right here
then i'll click update driver
and then i'll click browse
i'll click browse again
and basically what we have to do is find
out what driver it wants
so if i'm not mistaken i think this is
the balloon driver
let's see if i'm right 2k 19
amd64 let's see if it works
and it did
so now i have the vert i o balloon
driver installed
and that supports memory ballooning
which is pretty cool
i'll click close
we're down to one more device that needs
a driver so let's update that driver
i'll browse again and again
and what i did was i just selected the
entire cd
when i installed windows and i tried to
do pretty much the same thing it wasn't
able to search the disk properly and
find the driver but this time it did so
i guess when in doubt just select the
entire disk and if it finds a driver
then you're all set
so now we no longer have any unknown
devices that's pretty cool
Installing the QEMU agent
so next what we're going to do is
install the qemu agent
so we'll just open up the file manager
we'll go to the pc
double click on the cd-rom drive
and there should be a folder called
guest agent and here it is
and i'll double click on this one right
here the 64-bit version
that should be all i need to do
and that's it
we have successfully installed windows
server as a proxmox vm that's pretty
cool
now as a quick aside
Quick note about Windows licensing
if you go here to the file manager right
click on pc and go to properties
it's telling me that windows is
activated
but it's actually an evaluation version
i don't really have a license here
and you can see down here that it
mentions that it's actually an
evaluation version it's good for 180
days
if you want to continue using this then
you'll need to actually add a product
key to the installation and you can do
that right here where it shows change
product key
if you don't add a key it's possible
that after the evaluation period is over
the windows installation might be
disabled
windows licensing is beyond the scope of
this video and even this entire channel
so i'll leave it up to you to acquire a
product key for windows whatever version
you're installing and adding it here
where it shows change product key once
you do that your windows installation
should be all set
but anyway when it comes to this
particular video there you go we now
have a virtual machine running windows
right here on proxmox
so at this point if you followed along
with me you should have your very own
windows virtual machine running inside
proxmox
as you just saw the process is a bit
more involved when you compare to the
process of setting up a linux virtual
machine but we were able to get it going
sure we had to download a special driver
disk and that driver disc was required
for the storage media to even show up at
all but we were able to get it going and
hopefully you liked this video and it
was able to help you out
speaking of liking this video if you did
like this video please click that like
button that lets youtube know that you
want to see more content just like this
and make sure you subscribe if you
haven't already done so because i have
some very awesome videos coming very
soon and thank you so much for watching
i really appreciate it
[Music]
so
[Music]
you
