
Search in video
Intro
today's video is proudly sponsored by
tuxcare the makers of qemu care
if you manage virtual machines then
you're no doubt aware of how tedious it
could be to upgrade qemu
typically the process involves
restarting each vm that is currently
running and with clusters you sometimes
have to play musical chairs with your
virtual machines and shuffle them from
server to server as you upgrade the host
qemu care by tuxcare can help you avoid
the tedious aspects of patch day by
allowing you to live patch qemu
with qemu care you can avoid unnecessary
downtime with your virtual machines and
hosts and still keep them patched and
secure
qemu care works by live patching the
qemu process itself which helps
immediately protect your systems from
malicious actors
and that means you could keep qemu
updated and secure without disruption to
the running virtual machines
tuxcare qemu live patching improves the
maintenance and operations for systems
that rely on qemu kvm virtualization for
the virtual it infrastructure
now you no longer need to orchestrate
complex virtual machine migrations to
perform the maintenance in situations
where qemu itself needs to be patched
and as most administrators will tell you
getting maintenance windows approved is
often the hardest part of the process
with qemu care such a window is no
longer necessary
it's time to stop restarting processes
and entire systems just to keep them
patched
live patching is the future and tux care
makes it easy
definitely check out the video on the
qemu care page that i have linked down
below and also subscribe for a free
trial so you can check it out for
yourself
thank you so much to tuxcare for
sponsoring today's video i really
appreciate it
now let's get started
[Music]
hello again everyone and welcome back to
my proxmox course
in today's class what we're going to be
doing is launching our very first
container i'm going to show you the
entire process
now before we get into that there's a
few things that you might be wondering
for example what kinds of containers
does proxmox allow you to create and the
answer to that is that proxmox uses
linux containers or lxc for short
lxc containers are actually pronounced
lexi in the industry and i know that's
weird don't hate me for that i'm just
the messenger here lexi is just how it's
pronounced we have all kinds of strange
things in the industry so it is what it
is now lexi containers are awesome
because they're more vm like than other
container types
now with other containers when you
actually stop a container it's deleted
and a state is gone
which means if you have a file saved
within that container that file is wiped
out everything is wiped out
now the reason why that's okay is
because people generally just create a
container image and that'll create the
container for them and they'll map some
kind of a network share or something
like that to the container so it's still
able to you know save its state but lexi
containers are more vm like you don't
even have to do anything it
automatically saves that state when you
think of a virtual machine when you shut
it down and then you start it up again
assuming your disc didn't fail or
something like that your data is still
going to be there and anything you have
saved on the virtual hard drive will
still be present
with linux containers it's kind of like
that the state is preserved
so that's why i say that they're more
vm-like than other container types now
another thing is that linux containers
are actually not specific to proxmox at
all i mean that probably goes without
saying the name is linux containers not
proxmox containers although i do often
refer to them as proxbox containers i
really shouldn't do that they're linux
containers or lexi containers you can
launch these containers on any other
type of linux distribution you might be
running so i don't care if you're
running debian ubuntu opensuse you can
run lexi containers but again what's
really cool about proxmox is that
they're fully integrated into the web
console
and we're going to explore that right
now
all right so in this particular class
we'll be walking through the process of
creating our very own container within
proxmox
Downloading a Template
but before we can do that we actually
need to download a template otherwise we
won't really have anything to base our
container on
so if i click right here where it shows
local
it's going to give me several options as
far as the different types of things
that this particular storage volume is
able to accept
and right here it's already selected on
container templates
you can also click right here to see how
much storage you actually have remaining
on that volume
so as you can see here i have more than
enough space available so i should have
no problem downloading a template
so back here on container templates what
i'm going to do is click on templates
and as you can see we have quite a few
different options here
and what i want to do is narrow the list
down to ubuntu
and as you can see we have more than a
few available
i'm going to choose the ubuntu 2004
template right here
and this particular release is an lts
release which is why i choose that one
instead of the latest and greatest
so i'm going to click download
and right now it's actually downloading
that template to my storage
it's already done in my case
and now you'll notice that i have the
template right here so it's ready for
use
Creating a container
now let's walk through the process of
creating an actual container
so i'll click this button right here
create ct ct obviously is short for a
container you probably already figured
that out i'll click on it and we have
some configuration items right here that
we will use to customize the container
that we're about to create
now first of all it's asking us which
host we want this container to run on
in my case i only have this one pve one
as you see here
we haven't actually gotten to the
episode yet where we set up our own
cluster so unless you're working ahead
you probably only have one server on
your end as well
and not only that depending on how much
hardware you have available you might
not actually go beyond one server but
anyway i have this server pve one and i
want to run a container on the server
easy enough
now here we have the container id
and even though it says container id
it's not actually different than vmid in
fact proxmox has only one set of id
numbers
there's no separate set of ids for
containers and virtual machines even
though the verbage here might imply that
container ids are separate they're not
really separate
and here it's automatically selected
container id 103
so just like with virtual machines it
selected the next available container id
because 102 is taken
so it just chose the next available
number which just happens to be one zero
three
now for the hostname we need to give
this container an actual name
what i'm going to do is call it web
server
hyphen ct
it's actually pretty easy to tell the
difference between virtual machines and
containers but i just went ahead and put
ct in the name to make it even easier
so next what we're going to do is create
a password for this particular instance
so i typed it in
and i typed it in again
if you do have an ssh public key feel
free to load it right here i'll leave
that up to you if that's something that
you want to use i'm going to go ahead
and skip that for now
i'll click next
and here we choose the template that we
want to use as the basis for creating
the container in my case i only have one
the one that we just downloaded so i'll
select that right here
easy enough
for the root disk for this particular
container it's defaulted to 8 gb so i'll
just set it to 16. i think that's a
little bit more reasonable and i'll
click next
just like with virtual machines we could
choose how many cpu cores we want to
allocate for this particular container
i'll leave it at one in my case but if
you are running an application that's a
little bit more intensive you might want
to consider increasing that
now for memory
it's defaulting to 512
i'm going to increase that
i'll just set it to 1024 out of habit
that's probably good enough
now of course you could choose to have
more ram allocated for your container if
you see fit but i think in my case
that's more than enough
now we're going to go over networking
later
but what i want to do is actually choose
dhcp right here for the ip address
i'll choose that for ipv6 as well even
though i'm not actually using ipv6 on my
local network
if you do have vlan setup you can add
your vlan tag here if you have one
i'm not going to actually fill that in
because well i'm not using that
the mac address we'll leave that at auto
we can add some rate limiting here if
we'd like but i'm going to leave that
alone anyway i'll click next
for dns i'm going to use the host
information here i don't really see any
reason to configure that at least not
yet and i'll click finish
and as you can see that was pretty quick
so i'll close this
and we have our container right here
Finished container shown in interface
now it's really hard to see you'll be
able to see it better in a moment when i
turn this on but there's a different
icon here for a container versus a
virtual machine
even though i added ct short for
container here in the name i didn't
actually have to do that
i mean considering that virtual machines
and containers both get different icons
it should be pretty much apparent which
is which
Setting up automatic start for the container
now before i actually start the
container though let's take a quick look
at the options
just like with virtual machines
i could choose right here whether or not
i want this particular container to
start automatically when the host itself
starts up
most of the time that's something that
you'll definitely want so i'll enable
that
we also have the start and shutdown
order just like we did with the virtual
machines that option is here as well now
i'm going to leave the rest of the
options here alone
Quick note about privileged vs unprevileged containers
but one thing i do want to mention is
this option right here on privilege
container that was actually a check box
on the very first screen when i went to
set up this container
and unprivileged containers are
generally safer than privileged
containers
an on privileged container actually has
a user mapping when it comes to the root
account inside the container such that
it doesn't map to the actual root
account on the host system and for
security that's a lot better
now without going too much into detail
about containers at this point if you
have an on privileged container there
might be some applications that will
have an issue running
so if you find that the application that
you're running inside your container
doesn't actually work as intended
sometimes this is the culprit
when in doubt just leave this set to on
privilege container that should be fine
Starting up a container
so what i'll do is right click right
here and start the container now click
on the host and let's watch it boot up
and it's already started
i didn't edit that out there wasn't a
bunch of scrolling text or anything like
that it just started
and it's not abnormal that containers
are faster than virtual machines they
often are
but anyway our container is up and
running
now you may or may not have noticed but
the process of setting up the container
it didn't actually ask me what i wanted
the username to be actually the default
username is going to be root
and it did ask us for a password so that
i do know i'll type that in right now it
asked us for that during the setup
process for this particular container
and now we're in
so what i'm going to do is run aft
install apache 2
i don't need to use sudo because i'm
logged in as root i'll press enter
enter again
and there we go there should be all
there is to it
now just like virtual machines
containers also receive ip addresses via
dhcp
during the setup process for this
container you actually saw me choose the
option for dhcp
so if i run ipspace a
it gives me the actual ip address
and the last octet there is 253.
so down here in my terminal what i'm
going to do is ssh username root
at
172.16.249.253 in my case
i'll say yes to this message
that's weird let me try this again
actually i already know what's going on
so let me go ahead and go back to
proxmox and let's fix it
Adding a user within the container
so what i'm going to do is add a new
user
and to do that i'll run add user
and then i'll add a user by the name of
j easy enough add user and then j
type the password for the new user
password that i want it to be
and again
and i'm going to skip all of these
prompts they're not required
there we go
now in order to execute commands with
root privileges i'm going to need to add
that user to the sudo group
and to do that i will run user mod
dash lowercase a uppercase g
the group i want to add a user to is the
sudo group
and the user that i want to add to that
group is mine so i'll type j right here
i'll press enter
that should be good enough
now let's try this again
and there you go i'm logged into the
container
the reason why that didn't work is
because by default ssh access for root
is disabled if you create a user for
yourself that's not a problem so i
created that user and i was able to log
in as that user as you see here
Testing out Apache within the container
now i did install apache so let's check
that out
in a new tab what i'm going to do is
type the ip address for the container
right here
so right here have the default web page
as you can see so that means that the
process is a complete success
so we were able to create a container
and inside that container we installed
apache
now apache is just an example you can
run whatever app you want
but you know it just shows that the
process is fairly straightforward
so there you go now you know how to
create containers within proxmox that's
pretty cool as you can see it's easy to
use and containers are awesome
at this point i challenge you guys to
create additional containers for
whatever you want i mean that's actually
part of learning right just creating
things deleting things
and just going through the process
that's how you learn at least that's how
i learn and i challenge you guys to
create some extra resources on your
proxmox server now if you'd like to help
me out if you like this series so far
please click that like button that lets
youtube know that you want to see more
tutorials just like this
in addition if you are enjoying this
series so far please spread the learning
just share it with your friends your
co-workers maybe post some links on some
social network sites things like that i
would really appreciate that
regardless i'll have the next episode
uploaded very soon
so definitely subscribe if you haven't
already done so and thanks for watching
[Music]
you
