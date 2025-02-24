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
Course Overview
hello and welcome to my proxmox series
you guys have been asking for this for
quite a while now
i mean i did do a proxmox series in the
past but that was a short series you
guys were asking for something a little
bit more in depth and i'm happy to
announce that's exactly what you're
getting in this course
and in this course i'm going to teach
you guys everything you need to know to
get your very own proxmox server up and
running but not to be outdone i'm also
going to teach you how to maintain it
update it and even create your very own
cluster it's going to be a lot of fun
in this episode it's all about getting
started what you need to get started
what you can expect out of this course
and so on
so who is this course for exactly
well this course is for those of you
that have never used proxmox before or
perhaps you have and you want to explore
the finer details such as clustering
which is one of the topics we'll be
getting into later on in this course
if nothing else if you're like me and
you love proxmox i think you're going to
love this series because again i'm going
to teach you everything you need to know
to maintain your very own proxmox server
and possibly even a cluster
now what i'm going to do at this point
is give you guys some additional
information as far as what you can
expect out of this course
Proxmox Overview
so like i mentioned in the intro
this is an introduction to my course on
proxmox
we're going to be getting started with
proxmox in this series
and for this presentation i'm going to
make it as short as possible because i
know presentations are boring but
there's definitely some information that
i want to make sure you guys have at
your disposal before you get started
now first of all it's important to
understand what proxmox actually is
i'm sure most of you guys probably
already know what it is because well i
mean if you're looking for a tutorial
series on it then chances are you've
already at least googled it and you know
what the goal is that proxmox is trying
to achieve
but at its core it's a virtualization
platform
its competitors include things like
xcpng
vmware a number of others and there's
nothing wrong with those other solutions
those other solutions are pretty cool in
and of themselves proxmox is also cool
but you know that's what it is it's a
virtualization platform it allows you to
run virtual machines
but not just virtual machines i mean
yeah that is the main point here you use
proxmox because you want to run virtual
machines
but one of the things that i really like
about proxmox is that it also lets you
run containers as well
and when you create a new resource with
proxmox you as the administrator you get
to choose whether or not that resource
is a virtual machine
or if it's a container
it leaves it completely up to you to
decide what the best route is for the
applications that you want to run
it also has an integrated web ui or a
web console
now that might seem like a no-brainer
but you'd be surprised
there's actually virtualization
platforms out there that don't integrate
the web ui you have to integrate that
yourself and that might sound like a
downside but honestly if you weigh the
pros and cons you might prefer to have
that separate or if you're like me you
prefer to have it integrated with the
current solution so you install one
thing and everything you need comes
along for the ride that's one of the
things i like about proxmox you install
it and you have everything you need
right then and there
in addition to that the proxmox ui
allows you to manage storage so you can
mount storage volumes you could install
updates and there's plenty more that's
built right in to the web ui
Course Structure
now let's talk a little bit about this
particular course how i decided to
structure it
and where we go from here
in this course there's going to be 16
classes in total
and right now
this is the first class you are here
so i don't need to explain what we're
doing in class 1 because we're already
doing it
in the second class what i'm going to do
is walk you through the installation
process
what i'll do is show you how to install
proxmox so by the end of the second
class if you're following along with me
you will have your very own proxmox
server set up and ready to go
in the third class what i'll do is show
you the web console
it's going to be more of a general
overview in that video
because we'll be exploring the
individual concepts in more detail as we
go along so i don't go into too much
detail in class 3 about any one thing
but i do give you a high level overview
of the web console so that way you know
how to navigate it
now class number four is more lecture
based
we're not going to be working on
anything in particular in that class
we're just going to have a discussion
the number one question that comes up
with proxmox is should you use
containers or virtual machines
we're going to talk about that
by the end of that video you'll have a
better understanding about what the pros
and cons are of virtual machines when
you compare them against containers
for class number five we're going to
dive right into virtual machines
specifically i'm going to show you the
process of launching virtual machines
within proxmox
class number six is all about creating
virtual machine templates
i mean you could actually just set up
virtual machines manually every time
which means you have to install the
operating system every time
but honestly i don't really think
there's any value in doing all of that
work over and over and over again
when you could just set up a template to
essentially automate a lot of that
if nothing else templates make the
process easier
continuing
class number seven
we're going to take a break from virtual
machines and we're going to dive into
containers
so i'll show you the process of
launching containers in that class
class number eight
is all about creating container
templates
just like we can with virtual machines
we can set up templates for containers
as well
class number nine is all about managing
users
by default you get the root user with
proxmox
but if you are using proxmox in an
organization
then you'll probably not want to use the
root account anymore than you have to
it's a better idea to create additional
users and you can set up each user to be
able to do different things
and that's because proxmox leaves you in
complete control of how you set up
everything including users so by the end
of class 9 you'll understand how to
manage users
in class number 10 we're going to
explore backups and snapshots
i think that's fairly self-explanatory
but in that class you'll learn what a
backup is compared to a snapshot
and when you should use one versus the
other
in class number 11 we're going to
explore the integrated firewall
firewalls are great now you don't have
to use the firewall in proxmox
if you have your own firewall in your
network for example pfsense you can just
use that
but if you don't have something like
that or if you want to benefit from an
additional firewall then the firewall
within proxmox is pretty good so in that
video i'll show you how to enable that
firewall
and i'll show you how to create your
very own rules
in class number 12 we're going to
explore the command line interface
i mean yeah proxmox has a pretty cool
web console
but what if that isn't working or maybe
you're like me and you just like the
command line
proxmox allows you to manage your
containers and your virtual machines via
the command line and that's exactly what
we're going to go over in class number
12.
in class number 13
we're going to explore networking
generally speaking it's a good idea to
have a separate network for your virtual
machines when compared to your
management network by default when you
set up proxmox you only have one network
so in that video what we're going to do
is explore separating that which is a
best practice again you don't have to do
that
and honestly you don't have to follow
along with anything in this series if
you don't want to or if you don't have
the hardware to enable you to follow
along
but it's definitely something that
you'll want to understand and you will
understand that by the end of that class
in class number 14 we're going to
explore shared storage
i'll show you how to mount additional
storage basically nfs shares into
proxmox which increases its
functionality
class number 15 is all about clustering
before class 15 we're basically using
one server every single time but in
class 15
that's where things get especially
interesting and we work with multiple
servers it's going to be a lot of fun
and i know that because i've already
recorded it
the final class class number 16 is all
about high availability
you could probably argue that i could
have included high availability within
class 15
but i figured it would be more fun to
put it in its own video which is exactly
what i did
in that video what i'll do is show you
how to enable high availability after of
course i tell you what's required in
order to enable that and then i'll just
disconnect the network to a host and you
can see the virtual machine actually
start on another server
What You Need
okay well all of that's exciting and all
but
what do you actually need in order to
get started i mean do you need to go out
and just buy a really expensive server
with a ton of ram and cpus
well i mean that would be awesome if you
have the money to do that if you have
the extra money to do that why not have
fun
but you don't have to
and that leads me to the first bullet
point here as far as what you need you
need a server you need something to
install proxmox onto
it's not a good idea to install proxmox
inside of a virtual machine you probably
could do that and it might work but i
don't recommend that
you'll definitely want to install
proxmox on a piece of actual hardware
but again you don't have to buy
expensive hardware in order to run
proxmox you can buy a cheap server from
ebay for example if you want to
perhaps you have an extra desktop that's
in the closet
and you're not using it for anything if
that's the case why not turn it into a
server another thing you could do is run
proxmox on laptops i know that sounds
weird right
but i did actually do a couple of videos
on that subject where i set up proxmox
on laptops
that was really fun
the thing is as weird as that might
sound a laptop includes a battery a
keyboard a mouse and a display
so it's almost like having a server with
a built-in kvm all in one
so for those of you that are running
proxmox in a home lab
that might be something that you want to
consider doing
some people within my audience they've
set up prox knox on intel nux that's
totally fine
i mean some of these computers might be
a bit resource starved but as long as
you could run at least one virtual
machine then that's probably enough to
get started with this course
another thing that you'll need for sure
is virtualization support in your cpu
now this is something that pretty much
most computers have nowadays
definitely check the spec sheet for your
computer to find out if it does support
virtualization because that is required
now what i've found is that quite often
most cpus will in fact support
virtualization but in the bios it'll be
disabled by default there's a very good
chance that when you go to install
proxmox that it's going to complain that
you don't actually have support for
virtualization even when you do
if you see that message just go into the
bios settings for your device and make
sure that virtualization is enabled if
you don't actually have an option for
virtualization then unfortunately you
won't be able to run proxmox on that
particular device but that's rare i
think most of you will have no problem
installing proxmox because it doesn't
really require all that much to get off
the ground
now in addition you do need a 64-bit cpu
so if you have an older machine that's
32-bit only then you'll probably not be
able to run this
i don't know why this is but
there's a lot of people out there in the
linux community that are under the false
impression that their cpu does not
support 64-bit
keep in mind we actually had 64-bit
support in cpus since around 2004 or so
so chances are you probably do have
64-bit support
you also need one gigabyte of ram
minimum
and i do mean minimum
if your device has one gig of ram
that's pretty much enough to run proxmox
and that's it
i mean it's pretty much useless so when
the documentation for proxmox suggests a
minimum of one gig
they are literally referring to the
absolute minimum
now i would say it's better to set the
minimum to two gigs of ram and i would
be even more comfortable if it was four
because when you hit four gigs of ram
you have a gig of ram for the operating
system itself for proxmox itself you
also have a couple gigs available for a
vm or two maybe you can squeeze two vms
out of that but containers use fewer
resources so with four gigs of ram i
think you could do pretty well
if you have more than that even better
next you need the fastest storage that
you have access to
so if you are building a brand new
system for proxmox or if you just have a
bunch of junk parts in your drawer and
you want to assemble them and create a
server out of them just make sure that
you choose the fastest hard drive that
you have access to because the faster
the hard disk the faster proxmox is
going to respond
so if you have an extra ssd lying around
you might want to consider using that
and finally this probably goes without
saying
but you need a network card you access
proxmox over the network so you
absolutely need a network card i mean
sure you can run proxmox on a machine
with no network connection but you won't
be able to do anything with it so you
may as well consider a network card as
being a hard requirement
What Does It Cost
okay what does proxmox actually cost
well nothing
you can download it right now no problem
you will not be billed for the download
and there's no license that you'll need
to purchase in order to use it
now you can purchase support if you'd
like to but you don't have to
there is an error message that will
appear a number of times while you use
proxmox complaining that you don't have
a license
and you can safely ignore that message
you're not going to actually lose
functionality by not paying for it
just keep in mind that proxmox is a
project that requires a lot of time and
attention to develop so if you are able
to purchase support then that actually
helps the project so if you have the
extra money i highly recommend that you
give that a consideration
and supporting proxmox gives you access
to the enterprise repository at least
and the reason why i say at least is
because at the minimum tier the lowest
tier the cheapest tier that's what you
get you get access to the enterprise
repository which includes more
enterprise quality packages
that increases stability so it's
definitely a good thing to benefit from
as you go up in the tiers you actually
benefit from support from proxmox so if
you are planning on using this in
production for example at a company
you probably do want support that way
you'll have a means to reach out and ask
for help if something goes wrong but
How To Get Help
what if you need help and you don't
actually have a support agreement
one way you can get help is by visiting
the forums for this youtube channel at
community.learnlinux.tv
if you do decide to post there just make
sure you give us as much information
about your problem as you can
the more information that you give us
the more empowered we will be to assist
you every now and then somebody might
show up and say it doesn't work
if that's all you say then there's
really not a whole lot we can do there
if nothing else just give us as much
detail as you have
let us know what the desired effect
actually is what you want to achieve
what's going wrong maybe an error
message tell us what's failing
then also let us know what you've tried
to do in order to fix the problem
we'll do our best to help
another thing you could do is visit the
proxmox wiki
there you'll find documentation from
proxmox themselves
and they actually have quite a bit of
documentation so you'll definitely want
to check them out
proxmox also has its own community at
forum.proxmox.com
it's very possible that you might go to
my forums and maybe we unfortunately
don't know the answer to your question
if you go to the official community for
proxmox it's possible that you might
find your answers there
but this course is going to be a ton of
fun you're going to love it
in fact as a snake preview
Outro
this is the actual cluster right here
that we'll be building in this course
and the reason why i'm able to show you
guys this is because i actually come
from the future i come from the future
where every episode in the series has
already been uploaded and this is the
final product right here
okay to be honest i don't actually film
all the videos in the same order that
you see them in
so this introduction video is actually
the final video that i'm recording all
the other episodes have already been
recorded and are being edited right now
but yeah this is actually the cluster
that we'll be building
as it will be by the end of video number
16.
i have three nodes right
here pve one pve two and pve three
and throughout the video we'll be
building this cluster right here what
you see on your screen right now
now the thing is you don't really need
three hosts if you have three servers
lying around that's great you could
definitely use them
but you only really need one it's not
until somewhere around class 14 or 15
that you'll start to need additional
hardware and by then you can just watch
the videos and learn you don't have to
follow along but if you're able to
follow along i definitely welcome you to
do so
so at this point i hope you guys have a
better understanding as far as what you
can expect out of this particular course
and i hope you'll join me for the next
episode because in that episode i'll be
walking you through the process of
setting up your very own proxmox server
that'll serve as the basis for the
remainder of the series i'll see you
there
[Music]
you
