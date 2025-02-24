Intro
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
Introduction
hello again everybody and welcome back
to my proxmox course
in today's class it's all about the
command line
i've been really looking forward to this
because well i love the command line
now there's actually a ton of different
commands within proxmox and there's no
way that i could show you guys all of
them but what i'm going to do in this
episode right here is i'm going to teach
you guys my favorites as well as the
most common commands that you're going
to need to manage your proxmox servers
via the command line so let's dive right
in
Connecting to the Proxmox server via OpenSSH
okay so here i am on my laptop i have
the proxmox console right in front of me
it's time to get started with the
command line
so what i'm going to do is go over to my
terminal
because i prefer to use ssh for these
commands
if nothing else it's easier to see in
the recording because the font size is
larger in my terminal than it is in my
browser
so what i'm going to do is use ssh and
then i'll ssh as root
the ip address of my proxmox server is
172.16.249.4
and now we're in so there's two sets of
commands that i'm going to give you guys
the first set is going to pertain to
virtual machines and then the next set
is going to pertain to containers
so in terms of virtual machines we have
The qm command
the qm command
and the queue in the qm command stands
for qemu
and the m stands for manager so this
command is the qemu manager this is the
command that we will use to manage
virtual machines
and the command syntax is fairly easy
now you can also view the man page for
qm
and what that's going to do is give you
a full list of all the options that you
have available
but again i'm going over the most common
in this video so i'm not going to make
you read all of this
just keep in mind that if you want to
extend your knowledge even further you
can check the man page
Listing virtual machines
so the first command that i'm going to
start you guys off with is qm and then
list
and as you can see here it's a fairly
simple command it's listing all the
virtual machines
and of course you'll notice that none of
my containers are showing up right here
that's to be expected because qm is for
virtual machines we'll get to containers
shortly
Starting virtual machines
now with the qm command there's all
kinds of things that we can do
and one of the things that i want to
show you guys is how to start stop and
restart a virtual machine
so up here what i'm going to do is
actually shut everything down
all right so everything is shut down
and now what i'm going to do is show you
how to start a virtual machine with the
qm command
so the first thing you give the qm
command is a keyword we've already given
it the list keyword before
and that's how we ended up with the vm
list so what i want to do is start a
virtual machine
and let's start virtual machine number
100
now this is actually going to fail i'll
press enter anyway
and right here it tells us why it fails
because that particular virtual machine
is a template
and the reason why i brought that up is
because we actually see the templates
here in the list
the name doesn't really tell us whether
or not it's a template but if we try to
start a virtual machine that's actually
a template it's not going to let us
now i should probably refresh that list
because it shows virtual machines 101
and 102 are running and that's no longer
true
as you can see they're both stopped
so what i'm going to do is go up to the
console i'll click on web server 1
just to get it ready
and now what i'm going to do is type qm
and then the keyword start
and the one i'll start is
vmid101 i'll press enter
we'll go up here really quick
and we should see it start up and there
it is it's starting up
so i'm going to do the same thing with
the other virtual machine
and we can see that it's already started
i know that because this little green
triangle appeared right here even before
i clicked on the console
and that one's booting up
and now it's ready
so as you can see already the command
line syntax is fairly easy and it's very
useful
i can ssh into a server and manage
virtual machines but so far you've only
seen me start virtual machines
let's look at some additional examples
Stopping virtual machines
so what i'm going to do is shut down one
of them i'll do qm and then shut down
and i'll shut down virtual machine 101
which is this one right here
and it's already down that was pretty
quick
let's see if i can catch the other one a
little quicker though
nope that one's already down as well
but anyway you saw me shut down the
virtual machines that was pretty easy
all i had to do was type qm and then
shut down and then the id number of the
virtual machine
just go ahead and get these both started
up
let's go up here and we can see the vms
are starting
Rebooting virtual machines
so as you could probably guess you can
reboot a vm as well
and i think that's fairly
self-explanatory so i'll enter that
command right there
and already we see that virtual machine
101 is rebooting
just like we would expect
Handling misbehaving virtual machines
so as a quick recap i showed you how to
start stop and reboot virtual machines
another thing that i want to show you
guys is how to handle misbehaving
virtual machines
and this actually happens every now and
then where you might have a virtual
machine that runs into a problem and
it's not able to shut down gracefully
now the next two commands i'm going to
give you are potentially destructive
so you would never want to use these
commands unless you had no other option
again sometimes every now and then it's
rare but if a virtual machine runs into
a problem then through the web console
you'll most likely not be able to shut
it down or reboot it so the vm will be
kind of like stuck
so the next command is qm and then reset
and then you give it the virtual machine
id
unlike reboot reset is abrupt
it's pretty much the equivalent of
holding down the power button and then
immediately pressing the power button
because it's definitely not a graceful
reset
if you want graceful go with reboot
anyway i'll press enter
and you can see that it immediately
reset the vm and it's coming back up
and similar to that
we actually have qm and then stop
which will do the exact same thing
except it's not going to start the vm
after it stops it
if this was a real server it's
essentially the same thing as just
yanking the power cable so that's why
you definitely don't want to use this
unless you absolutely have to
but you know perhaps you'll run into a
situation someday where you might need
to do this i certainly hope not but
technology is what it is
sometimes it misbehaves and we have to
do something that we would really rather
not do
Configuring VM options via CLI
so with this vm off let's go ahead and
look at the options tab right here
you can see that start at boot is set to
yes now what i could do if i wanted to
disable this is i could click edit
and uncheck the box but i'm not going to
do that what i'm going to show you how
to do right now is configure options
with the qm command
notice right now it still says yes for
start at boot
so what i'm going to do is run qm
and i'm going to type set that's the key
word for setting an option we type set
and then we type dash dash
along with the name of the option that
we want to change and the option i'm
going to change is called on boot
i'm going to set that equal to zero
and the virtual machine that i want to
execute this against is vmid101
it looks like it did indeed update that
virtual machine
and start at boot is now set to no
and to reverse that
as you could probably guess we just
simply changed the zero back to a one
and what i've noticed is that this
doesn't always refresh right away you
can see that it just changed to yes so
sometimes there's a few second delay
here but i guess it doesn't really
matter
if nothing else you know how to set the
on boot status for a virtual machine and
you can do that with or without the web
console because now you know the command
to do that
in addition to that there's other
configuration options that we can set
when it comes to the qm set command but
before we do that
i probably should have shown you this
earlier in the video
but an important command to remember is
qm and then config
and then the id
i'll use 101 as an example yet again
and that's going to spit out a bunch of
information about that virtual machine
so right here you actually see the
options that you can set
right here we have the on boot option
that's what we were playing around with
earlier
it's currently set to one
so if you want to get a list of all the
settings you can easily get that from qm
config
and if you are looking for a specific
thing then you can grep for that
specific thing
so for example
i can grip for cores
if i want to limit the output to just
how many cores there are with the
virtual cpu
it'll give you the answer
same with memory
and so on
in fact let's go ahead and change the
memory
so again to change a setting is qm and
then set we want to set something
and specifically i want to set the
memory is currently set to one zero two
four or essentially one gigabyte
i want to set it to two zero four eight
i'm just going to double it
and what i want to do is run that
against virtual machine number one zero
one
and if i go ahead and grep again for
memory
previously it was set to one zero two
four
and now it's set to two zero four eight
now of course there's a lot of other
options that we can set with a qm set
command but i think that's enough for
now those are some of the most important
ones anyway but again if you want to
grow your knowledge even further you can
check the man page as well as the
proxmox documentation
i would love to go over every single
variation of the qm command but that
would be a very long video and i
definitely want to show you guys
container commands
so let's go ahead and do that right now
Managing containers via CLI
now when it comes to containers we have
the pct command
and that stands for proxmox container
kit
just like with qm list i could do pct
list
you're going to see quite a few
similarities with the syntax anyway i'll
press enter
we have these three containers right
here
one of which is actually a template so
we can't actually use it but it's still
in the list and that's similar to the qm
list command that command also showed
the template in the list as well just
keep in mind when you run this command
you will see containers as well as
templates
similar to the qm config command we
could type pct config
and give it an id number i'll just go
with 104
i'll press enter
and it of course gives you the
configuration options for that
particular container you see the memory
we see an on boot option
so it's fairly similar when it comes to
looking at the options for virtual
machines but there's going to be some
variations because we're dealing with
containers now rather than virtual
machines
Stopping and starting containers
so next what i'm going to do is show you
how to start stop and restart containers
again we have these containers right
here
and they're all stopped
so you can run pct start and then an id
number and of course this is not going
to work
and that's because 103 is a template i
just wanted to show you that it's the
same thing here with containers just
like it is with virtual machines
but anyway let's go ahead and start up
container number 104
and also
five
so you can see this one has started up
and now this one has started up so we
were able to start both of these
containers via the command line
we also have similar options for
shutdown and restart so for example we
could do pct and then shutdown
and i'll run that against container 104.
we also have pct reboot
i'll run that against container number
105
so container 104 is not running
and container 105 was rebooted and it
happened so quickly that i wasn't able
to catch it but i think you get the
point you can shut down a container as
well as reboot a container with a
command line
let's go ahead and start up container
104
and there it is now it's available
that's pretty cool
Accessing a shell within a container
now let me show you one of my favorite
pct commands actually
which is pct enter
so if we execute pct enter against a
container id
in this case i'll use id number 104 what
do you think is going to happen
i'll press enter
and check that out
i actually get access to a shell running
on the container when i run the pct
enter command which is exactly what it
does it opens a shell on that container
and then you can run all of your
commands right then and there of course
you can access the container via ssh or
however you want to access it i think
pct enter is simple it gets the job done
and i like it
i'll hold ctrl and press d to disconnect
now i'm back to my proxmox server
let's take a look at how to change the
configuration of a container
Changing container options
but first of all before we change
configuration we should see what the
current configuration actually is so
that's pct and then config which i
showed you guys earlier
than the container number
on boot is currently set to zero
so that container will not start up
automatically let's go ahead and fix
that
so it's pct and then set
we give it the container number in my
case 104
and the option is on boot
and what's different about this is that
the option has one hyphen in this case
but with the qm commands that we ran
earlier this would have two hyphens
but it doesn't matter it's simple enough
let's change that to a one
and now we can see that on boot
is now set to one
so there you go we were able to do it
so let's check out the config yet again
for 104
and there it is
Updating the memory limit for a container
so right here for the memory this is in
megabytes by the way you have 2048. so
to change that i personally think is a
little high
you can run pct
and then set
then the container id
in this case i'm going to change memory
i'm going to set that to 1024.
i'll notice that it's 2048 right here
and now it's 1024.
again it's out of scope to go over every
single variation of these commands
but there's other commands out there if
you do need to use them just check the
documentation i think as far as this
particular video is concerned i've gone
over all the basics
so that should be good enough for now
so there you go
now you guys know how to use the command
line in proxmox which is pretty cool i
hope you found that useful
and if you did find that useful please
click that like button because that'll
let youtube know that you want to see
more tutorials like this one in the next
episode we're going to get started into
the world of networking that's another
one of my favorite topics actually so i
can't wait to get that video uploaded
and out to you guys if i haven't already
done so depending on when you're
watching this
so please click that like button again
and also make sure to subscribe and i'll
see you in the next episode thanks for
watching
[Music]
you
