
Search in video
Intro
[Music]
now i don't know about you guys but
networking is one of my favorite topics
when it comes to computing
and i'm not even sure why it's just fun
to me i just love making things talk to
other things connecting hardware
together
setting up rules and routes and all the
other aspects that are associated with
networking it's a ton of fun
and in proxmox networking is definitely
an important thing
and what i'm going to do in this video
is show you guys a little bit about
networking in proxmox specifically what
we're going to be doing is separating
the vm network and the management
network which is absolutely an important
thing to do so let's get started
now at this point in the series we're
Quick comment about hardware requirements
getting into territory where not all of
you guys will be able to follow along
the reason for that is because not
everyone is going to have the hardware
that's required for the topics that are
coming up in the series
so if you don't have the required
hardware in order to follow along that's
okay you can simply take notes and watch
that's absolutely reasonable
and like i mentioned in the intro we're
going over networking in this video
so it's very helpful if you guys have a
network already that you can use the
goal essentially is to separate the
management network from the vm network
that's a very good practice
but again the ability to do that depends
on whether or not you have another
network to use
we're getting into the territory of
vlans and subnetting at this point and
teaching you guys how to create vlans
and subnets is beyond the scope of this
video
i already have other vlans and subnets
set up i've already been using vlans and
subnets in my network and another thing
that complicates this is that even if i
did show you guys how to set those
things up each of you will have a
different router or firewall in your
network
so it's impossible for me to go over the
process in the probably thousands of
devices that are out there so it's
probably easier to just follow along
now what we're going to do is focus on
the individual host right here
i'm going to add an additional network
if you do add additional proxmox nodes
to your cluster and essentially create a
cluster then any networks that you
create on your first host you'll also
want to create those on the secondary
host as well
but we haven't actually set up a cluster
yet so we're not going to worry about
that right now so to set up an
Looking at the available network interfaces
additional network you first click on
the host where you want to set up that
network onto i'm on this one right here
and then you click on network
in my case i have vmbr0
that's vm bridge 0
and right here we can see what port is
assigned to that particular bridge
and this particular card has an ip
address of 172.16.249.4
it's a 24 subnet
and that's essentially the same thing as
a class c network but in the industry we
don't really use classful networking
anymore
anyway that's the ip address in the
subnet
and here's the gateway
all of this right here was set up when
we first installed proxmox so we didn't
have to configure any of this
if you recall when we went through the
installation process it asked us for all
of this information here
so you should have this part right here
all set
in my case this particular port right
here
is on the same network card as this port
right here so these two
are actually the same network card this
is a 10 gig ethernet card
which is probably overkill but it's
great i love it
and these are the two individual
ethernet ports that are on that card
so right here we have this port
enp5s0f0
and of course the name will most likely
be different for you
but we could see that that port is
assigned to this bridge but i have this
port here
and what i want to do is assign that to
a different network now i can use any of
these devices if i wanted to it doesn't
really matter which one but i'm going to
choose this one right here because it's
another 10 gig port and i'm going to
prefer to use 10 gig whenever i can
so it makes sense to use that one
so what i want to do is create another
network here and have my vms use that
network and then dedicate this network
right here for the management layer when
i say management layer i'm talking about
this entire web console
generally speaking you don't want the
web console on the same network as the
virtual machines you want to have some
separation there and that helps make
sure that if someone breaks into one
network that they hopefully won't be
able to access the other network
whether or not they can access other
networks of course depends on how good
your firewall rules are
but i'm not going to get into that i'll
just assume that your firewall rules are
on point
so even though i have this interface
Adding a network (Linux bridge)
right here i'm not actually going to
adjust the settings right here on the
interface itself i mean i could click
edit and add the network that way but
what i want to do instead is create a
bridge
that's standard practice
so i'll click right here where it shows
create and i want to create a linux
bridge so i'll click that
and it automatically gave it the name of
vmbr1 i could customize that but i won't
i think that's good enough
and then next what i'm going to do is
type in the network subnet that i want
to use for this particular interface
in my case it's going to be 10.10.10.0
24.
as far as what you should type on your
end that all depends on your network
hopefully you've already created this
subnet and vlan on your end and whatever
your network classification is for your
vm network that you hopefully have
already created you type that in right
here
but if you haven't done that don't worry
about it you can just watch this video
and take notes you don't actually need
multiple networks yes it's a good
practice but it's not required
now what we need to do right here is
type the port of the ethernet adapter
that we want to use for this bridge
i'm going to move this over here because
it's in the way
i want to add this right here
so what i'm going to do is type it in
right there so it's emp and then 5
and s
0 f 1.
right here i'll add a comment of vmnet
i'll click create
and that should be all we need to do
now notice that there's no actual
gateway here
we already have a gateway right here so
with proxmox you only want one gateway
and that might seem weird for some of
you but it really doesn't matter
just keep in mind that you traditionally
leave the gateway field blank unless you
do run into a situation where you
actually need a gateway
but we already have one so we don't
really need to add another one
if i scroll over
you can see the comment here to the
right
it's kind of hard to see because of the
font size of my browser here but this is
where the comment would be right here
we're going to ignore that though
now at this point we have some pending
changes as it shows here we could apply
the configuration now
or we could just reboot the server
and it's going to go ahead and apply it
at that time
i'm going to apply it right now i'll
click apply configuration
i'll say yes
and now we have two bridges here
and this one right here is active and
ready to go
Creating a virtual machine on a separate network
so when you are going to create a
virtual machine what you're going to do
from now on
i'm not actually going to go through
with the creation but i'll show you the
section that pertains to networking
just going to keep clicking through here
until we get to network
so by default it's using vmbr0
and what i'm going to do is drop that
down to vmvr1 so going forward every
time i create a vm i want it to be on
the virtual machine network not on the
management network
i'm going to cancel this i don't
actually need to create a vm to show
that point
but i do have virtual machines already
that do exist so what i need to do is go
over here to the vm and then to hardware
and right here we have network device
let's go ahead and edit that
and we can just change the bridge right
here
click ok
i'll do the same thing for this one
right here
let's edit that
change it to vmbr1
click ok
let's start up this vm
and this vm has already started so what
i'm going to do is log in
let's see if it got a new ip address
and right here we have an ip address we
have an ip address of 10.10.10.206.
i know the font is really small so what
i'll do is i'll just go down here
and there we go i'm logged into web
server 2
and if i check out the ip addresses here
here's the ip address it's on the proper
network
so i was able to separate the management
network from the vm network
from this point on when i create virtual
machines i'll make sure that i create
them in the proper network
not the same network that i use for
management
and that's actually a best practice
since we've taken a look at networking
in today's class
that actually opens the door for other
exciting features of proxmox for example
shared storage clustering and there's
actually more
in the next video we're actually going
to set up shared storage which is going
to be especially fun so join me in that
episode as soon as i have it uploaded if
i don't already have it uploaded and
i'll see you there
thanks for watching
[Music]
foreign
