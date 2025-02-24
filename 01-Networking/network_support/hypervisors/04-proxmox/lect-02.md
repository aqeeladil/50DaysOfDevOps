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
hello and welcome to class number two in
my proxmox series i'm very excited to
have you here and i'm also very excited
to get started because in this video
we're going to be setting up our very
own proxmox server
i'm going to walk you through the
installation process on my actual
hardware this is not going to be a test
server
or maybe one of my laptops or something
like that this is a real production
server that i have already wiped and
what we'll be doing is installing
proxmox on that server
the thing is i wanted to redo and
rebuild my proxmox cluster anyway so i
figured it would be a lot of fun to do
this series on real hardware and i
figured you guys would get a kick out of
that
so let's go ahead and get our proxmox
installation started i'm going to walk
you through the process of creating your
very own bootable media for proxmox and
then we're going to use that media to
get our installation started and i'll
walk you through it every step of the
way so let's dive in
all right so the first thing that we're
going to do is download proxmox
you can get it from the proxmox.com
website specifically the download
section like you see here
and this is the url
but don't worry if you can't read the
url in the address bar
i will have a direct link to everything
you'll need in the show notes down below
so you can simply click on the link and
it'll take you to this page
so what we're going to do is click on
proxmox virtual environment right here
and then we'll click on iso images
and right here we have proxmox ve 7.0
which is as of the time i'm recording
this video the latest version but if a
newer version is available when you're
watching this don't worry about it even
though proxmox is constantly releasing
new versions with new features generally
speaking the content in this video
series should still work even if you do
see a newer version on the download page
when you get around to watching this
if proxmox does change to the point
where this tutorial series is no longer
valid i'll go ahead and update it for
the newer version when that time comes
for now i'm going to click on download
and then i'll save the file
and we can see that it's downloading
right here
so what i'm going to do is give it a few
minutes to finish and then i'll be right
back
all right so as you can see here
download for proxmox 7.0 the iso image
that we're going to need is all set and
ready to go
and what we're going to need is one more
thing so what i'm going to do is search
for usb imager
and this is it right here don't worry
about the url i'll have a link in the
show notes down below along with
everything else
and if you are on the correct page it
should be a git lab page
as we can see here
and what i'm going to do is scroll down
and we have quite a few different
versions available for usb imager that's
why i always recommend it
because it doesn't matter what operating
system you are running on your end it's
still the same tool
and that works out pretty well for me
i mean as a content creator if i have a
tool that works on various operating
systems then i only need to film the
process in one single tool
also usb imager is a very small download
size
so it's going to download very quickly
now in my case what i'm going to do is
download this version right here for
windows
windows is not my daily driver but i
figured i would show the process in
windows because i know quite a few of
you are using windows and that makes
this video look more familiar to most of
you
but if you are running something else
just go ahead and download the version
that corresponds to the operating system
that you are running on your end
i'll save it
and it's already done
i didn't even have to edit this part of
the video it was literally that fast
that's pretty cool
all right so at this point if i go to
downloads
we can see both of the files that we've
downloaded right here
so if you weren't already aware an iso
image is actually an image that's
intended to be written to a cd or dvd
but i don't actually recommend that you
write this to a dvd or a cd
and the reason for that is because
optical media is very slow
what we're going to do is actually write
this to a usb flash drive
so even though it's intended for a cd or
dvd we still use the same format today
when it comes to flash drives
and flash drives are as you probably
know orders of magnitude faster than
optical media which is why it's
recommended first of all i will extract
this right here
and that should already be done
and inside here we have the actual
utility
and this is a save file so i'll click on
more information and then i'll click run
anyway
all right so usb imager is open and
ready to go
so i'll get this out of the way
and we can continue
so next you'll just insert your flash
drive into your computer just keep in
mind that this process will actually
erase everything on that flash drive so
be sure that you've already backed up
everything you need off of that flash
drive before we continue
in addition it's probably helpful to let
you guys know that you should probably
have a two gigabyte flash drive or
larger i mean the iso image was
somewhere around a gigabyte or so so it
might be just above the one gigabyte
barrier
but then again most flash drives sold
today are more than two gigabytes anyway
so you should be fine
so what i'll do is i will click right
here
and then i will select the iso image
that we've downloaded
and we can see the path to the iso image
right here
next what i'll do is actually insert the
flash drive
and if you see this particular message
when you insert your flash drive
i don't think very many of you will you
could just go ahead and ignore it
as an aside if you have ever used your
flash drive the flash drive that you're
using right now with another linux
distribution
it's usually a good idea to delete the
entire partition table from that drive
before you continue for whatever reason
windows itself doesn't really do a good
job with this
so this is something that only you
windows users out there will need to do
mac and linux users won't have to deal
with this but anyway
you can right click here on the start
button and go to disk management
and then you find your flash drive and
this is mine right here
now mine says on allocated on your end
you'll probably have at least one
partition here
what i recommend that you do is right
click each partition and delete it
just make sure that you are actually
deleting the partitions from your actual
flash drive the one that you want to use
with proxmox because obviously if you
delete the wrong thing then you are
going to suffer data loss
now i don't need to delete anything on
my end because i don't even have a
partition table so i'm good
this is something that i generally
recommend that all windows users do
after they use a flash drive for a linux
install when they want to write a
different image to that flash drive
so many of you you probably won't need
to do that
anyway what i'm going to do is select
the flash drive
it's this one right here it's the only
option anyway
and then i'll click right
and at this point it's actually writing
the proxmox iso image to the flash drive
i'm going to let it continue and then
i'll be right back
so at this point the flash drive has
been successfully converted into a
proxmox installer
so i can go ahead and close this
and i'll safely remove the flash drive
just to make sure
and what i'm going to do at this point
is insert the flash drive into my server
i'm actually going to be using a real
hardware server for the series so i'll
plug in the flash drive and then i'll be
right back
all right so what i've done is i
inserted the flash drive into my server
and then i switched the recording scene
over to my laptop which is what i'm on
right now
and what you see in my browser is
actually the ipmi interface for my
server
this particular interface actually
allows me to show you a remote console
as i go through the installation process
on your end you might have a keyboard
mouse and display attached to your
server and that's totally fine
it doesn't really matter
i just figured that i'd mention this
just in case you're curious why i'm
showing you a web browser when we're
about to install proxmox
anyway what i'm going to do right now is
log into my ipmi interface
and yes the username is velociraptor
and that might seem weird but just keep
in mind they can open doors so that
username made sense to me
anyway i'll type in my password
and here we are
so what i'm going to do right now is
click on remote control
and the server is actually powered down
right now so i'm going to click on the
power button right here to turn it on
that should allow it to boot up
so in the console here i can actually
see what's on the screen if i actually
did have a screen attached
and if i remember correctly it's f11 to
access the boot menu
just make sure i catch it
hopefully i did that fast enough
a couple more times just to make sure
and here we have the actual boot menu
so in my case i'm going to select this
option right here
because i want to boot into uefi mode
which is preferred if you have access to
that i'll press enter
what this should do is boot it right
from the flash drive and as you can see
that's exactly what it did
i think the screen is a little bit too
large so i'm going to try to shrink it
down just a little bit
and hopefully that'll allow you to see
it better so
right here what we have is the actual
installation menu for proxmox ve
the first option is install proxmox ve i
can press up and down to select a
different option
but the first option is actually what i
want so i'll press enter
i'll give it a moment to start up
so the first screen here we have the end
user license agreement
so i'm just going to agree
hopefully nothing too egregious in there
and then down here we select the actual
hard disk we want to install proxmox
onto
so you simply click right here and
select the hard disk i only have one
anyway so i have no other option
i have a one terabyte ssd as you can see
here so that's going to be fairly fast
because again you want to use the
fastest storage that you have access to
now before we click on next there's a
few things that i want to mention so if
i click on options
you can see that the default file system
choice is ext4
so if i was to click next then that's
what i would get
zfs is a really good choice if you have
some higher end hardware or a lot of
memory
generally speaking you probably won't
want to enable zfs if you have a small
amount of memory
but if you have good enough hardware it
is actually something that's worth
considering there's features here that
would be a great value add if you were
to use zfs
such as increased reliability
better file system integrity
more snapshot features and so on
we also have butter fs options as well
but we're not going to cover those
options in this series
in fact we're not going to cover zfs
much either because that really depends
on your hardware
for the most part 50 of your ram is
going to be set aside for the arc
and you can think of the arc as a cache
which is going to certainly help your
performance but at the expense of using
more memory
for the most part you'll probably want
around one gigabyte of memory for zfs
for every one terabyte of storage but
honestly i don't think i can recommend
zfs for anyone that has less than 32
gigs of ram
that's just a personal recommendation
not something that you find in the
proxmox documentation
but considering that having that much
memory available as a potential
requirement would really limit my
audience i'm going to stick to ext4
and what i'll say about zfs at this
point is that again if you have the
hardware i do recommend that you use it
you will benefit
so for now i'll click on ext4
actually i can cancel out because ext4
is the default
i'll click next
and here we're going to select the time
zone
and it's very important that we set this
correctly proxmox is heavily reliant on
the time to synchronize everything so
you'll want to make sure that you select
the right time zone here just to make
sure that everything is correct
so what i'm going to do is just scroll
down a bit here to detroit
which is right here and that's close
enough
and then of course you can select a
different keyboard layout if you have a
different keyboard layout i'll leave
that up to you
anyway i'll click next
and next what we're going to do is set a
password we definitely want to remember
this password because this is how we're
going to log in here very shortly
so what i'm going to do is type it in
and then down here we type in our email
address
i recommend that you actually type a
valid email address especially if you
want to consider support options later
on
but since this is just a tutorial for me
i'm just going to change the last few
characters here to com
what that'll do is trick proxbox into
thinking that i typed a correct email
address there
anyway i'll click next
on this screen right here this is where
we set up the default networking
if i drop this down right here you'll
see that i have a number of different
network cards that i could use
it defaulted to this one right here if
you have more than one you'll definitely
want to make sure that it's defaulting
to the correct one
in my case it's not
what i want to choose instead is this
option right here which is actually 10
gigabit ethernet
now obviously i know a lot of you guys
aren't going to have 10 gigabit ethernet
but if you can get access to 10 gigabit
ethernet it's definitely worth it
i do have a video on my channel where my
friend tom and i we actually discussed
10 gigabit ethernet
he was here in the studio and he helped
me upgrade to 10 gigabit ethernet
and then he also has a video on his
channel as well that goes more into the
specifics of what's required to
implement 10 gigabit
and this is completely out of scope for
this series but it's just an aside
if you can get access to 10 gigabit you
may as well
so what i'll do is select this card
right here
and then here we need to choose a host
name for this particular server
i'm going to call mine pve one
later on in the series we will be
setting up clustering and i want to make
sure that i'm able to differentiate this
host from the others when we get to that
point so pve one that should work for me
next what we're going to do is choose an
ip address for the management interface
for proxmox
and in my case it defaulted to this ip
address right here which is actually
incorrect
what i'm going to do on my end is change
the last octet here to a 4
and the default gateway that's correct
but the dns server that's not correct
so what i'm going to do is change that
it's actually the same as the gateway in
my case
and now i've typed in all the values
that i'm going to use with my
installation for networking
on your end the key here is to use an ip
address that is not already taken on
your network
the problem on my end is that there's
thousands of different devices out there
when it comes to firewalls and routers
so i can't really show you the process
of determining which ip address is open
and available for use
the general idea when it comes to how
you determine which ip address to use is
you log into your firewall or router
interface and inside there you'll have
some dhcp options
inside the dhcp options you'll have a
range you'll have a starting ip address
and an ending ip address
so what you want to do is choose an ip
address that is not within that range
that way you don't have to worry about
the ip address that we're setting here
being assigned to another device which
would create a conflict
and that's actually what we're doing
here we are setting a static ip address
that's going to be used for this
particular proxmox server
in my case it's this one right here
172.16.249.4
and in case you're curious that belongs
to my server subnet
subnetting is obviously beyond the scope
of this particular video
but i just figured that'd be fun to
mention anyway i'll click on next
and here what it's doing is it's giving
us a summary of all the options that
we've chosen throughout the installation
process
if anything looks out of place here make
sure you go back and adjust it
and if everything looks correct
we can continue so click on install
and now proxmox is installing on my
server
so what i'm going to do is give it some
time to finish and then i'll be right
back
all right so the process is actually
finished
proxmox is installed and ready to go and
it's rebooting right now
so i'll just give it a few moments to
start up
all right so far so good this is the
very first screen that you should see
when proxmox is starting up for the
first time we're actually starting up in
general
and the screen is refreshing quite a bit
here which is okay
and here we are proxmox has booted and
it's ready to go
in fact it even gives us the ip address
right here i mean we should already know
what that is because we typed it in
earlier but it's basically telling us
that we can navigate in a browser to
this url right here with this particular
port
and if all goes well we should actually
be able to access the proxmox interface
so let's see
so what i'm going to do is type in that
exact url right here in my browser
moment of truth let's see if it works
so by default proxmox uses a self-signed
certificate which my browser right here
doesn't actually understand
so this is normal behavior
it's recommended to get a certificate
for your server if you can
but that's beyond the scope of this
particular tutorial series because i
don't really recommend that you make
proxmox publicly available if you can
help it so what i'm going to do instead
is just actually ignore this error
we'll accept the risk even though there
really isn't a risk the self-signed
certificate was expected
and here we have the actual login screen
for proxmox
i'll type in root for the username
then i'll type in the password the same
password that we chose during the
installation process
and then i'll log in
now this particular message right here
is normal
proxmox is an open source solution
but you know what they have bills to pay
as well so they have a value add service
that you can subscribe to if you wish
and in particular that's the enterprise
repository
it gives you packages that are more
catered for enterprise deployments
so we can safely ignore this particular
message right here
but anyway we have the user interface
right here so we know that our
installation was successful
and in the next class what i'm going to
do is show you guys the proxmox user
interface in more detail
so now that you have proxmox installed
all set and ready to go it's time to
dive into the user interface the web
console if you will because in the next
episode that's exactly what i'm going to
walk you through
i'm going to give you an overview of the
web console itself so that way you'll
know where everything is where it's
located and some other things as well so
i'll see you over in that video which
should actually be already uploaded
right now so i'll meet you there
[Music]
you
