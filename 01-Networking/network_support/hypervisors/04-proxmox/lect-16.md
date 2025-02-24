
Search in video
Intro
[Music]
thank you so much for checking out learn
linux tv your source for linux related
fun and learning
i just love making this content for you
guys
but making such content isn't cheap
if you enjoy my content please consider
supporting me by becoming a patron
as a patron you'll enjoy ad-free
versions of every video that i upload
and also as specific tiers you'll also
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
hello and welcome back to my proxmox
course
this is actually class number 15
and i've been looking forward to this
one because we're actually going to set
up our very own cluster of more than one
proxmox server now i do understand that
some of you guys out there you might not
have the spare hardware to follow along
maybe you only have one server and
that's okay you can still watch this
video and i'll show you how to create a
cluster so that way if you do actually
bring in a new server at some point in
the future you'll be able to cluster it
if nothing else clustering is awesome
and that's what we're going to be taking
a look at so let's go ahead and dive
right in
Some general info before getting started
all right guys so let's get started with
the process of setting up a cluster
now to be clear i want to mention that
in this video we are talking about
clustering only not high availability
yes high availability is part of
clustering but we're going to tackle
that specifically in the next video
in this video i'm going to be adding
these three servers that you see on the
screen right now i have each one in a
different tab in my browser so off
camera i set up two other servers
so i'll be adding those other two
servers to the cluster and then i'll
show you how to actually migrate a
virtual machine from one host to another
in the next video it's more of the same
but just a little bit more advanced
now i do understand that many of you
guys out there you probably don't have
access to three different servers
especially for those of you that are
using proxmox in a home lab maybe you
only have one server
so it's okay if you can't follow along
and set up a cluster on your own but by
watching this video if nothing else
you'll at least see what the process
looks like
so like i mentioned off camera i went
ahead and installed proxmox on this node
right here and this node right here
so we have the servers let's go ahead
and cluster them
so i like to start on the first server
here now what we could do is jump
Setting up the same networks on subsequent Proxmox VE nodes
straight into creating a cluster right
now but there's something that i like to
do first before i do that just to make
sure the process is smoother
and what that is is that i want to make
sure that the same networks that i set
up on the first server are available on
the second so if you recall
here's my first server
so here in the network section
we have this interface right here this
is the original interface the one that
we set up when we set up proxmox
originally so it came with it so to
speak
and then in a later video
we created this bridge right here vmbr1
the idea being that virtual machines
will use this network
and then the management layer will use
this network
now obviously whether or not these two
networks are truly separated depends on
your firewall which i'm not going to get
into
but at least that's the purpose for why
i created this other network
but the issue though
is if i was to go to pve 2 for example
i don't actually have another network
set up here
i only have
vmbr0
and that's the same here
and server number three is very
different than the other two the first
two servers are my actual proxmox
production servers that i just wanted to
wipe and redo anyway which you know
really helped out with the creation of
this series but anyway
i actually have just one network here as
well
now you can cluster these hosts right
now without doing anything at all
it's just a best practice that i like to
do to set up the same network on each
so what i'm going to do is go here
and because i'm lazy whoops wrong one
[Music]
it's this one right here because i'm
lazy i am going to copy the subnet
i'm not actually going to make any
changes
but i'll go over here to the second
server
i'll create another bridge
and i'm going to type in the name of the
other interface here so first i want to
paste in the subnet citer
and the ports that i'm going to bridge
right here i'm going to add enp
5s0
i'm not going to fill in any of the
other fields here
that's actually enough i'll click create
so now we have that other bridge
and it's going to require a reboot
but i want to do the same thing over
here on this other node
this node in particular doesn't actually
have 10 gig ethernet and i want to
mention that because we are going to be
doing live migration so obviously any
migrations to server number 3 are going
to be slower than migrations to and from
server one and server two
but that's just an aside what i want to
do for sure is add that other network so
eth0 is already used so i'm going to use
eth1 again i'll create a bridge
i'll paste in the cider
and i'll type eth1 right here
for that interface
alright so now that i've added this
network to the other host i can go ahead
and reboot them
and as a quick aside you might be
wondering why did i go through all that
trouble well the reason why is because
over here on this server even though i
do plan on deleting these virtual
machines and recreating them anyway
they're actually using the vm network
that i set up right here so if i cluster
these and then i try to move a vm from
this server
over to another server that doesn't have
that network set up that's not going to
work so just to make it easier on myself
i'm essentially setting up that other
network ahead of time on the other two
servers before i actually cluster them
and you know what i'm not going to
reboot them what i'm going to do instead
is just apply the configuration that
should be good enough
so i'm going to do that on both
and i did get an error message right
there
this test server is a new server to me
just to be on the safe side i'm going to
reboot it
and then i'll go ahead and reboot this
one as well
just want to be on the safe side i don't
think that was necessary but you know
what i think that's going to work out
just fine so i'll be right back i'll
give these servers a few minutes to
start back up and then once they do i'll
go ahead and show you guys how to set up
a cluster
alright so enough time has passed the
Creating our Proxmox VE cluster
servers have rebooted they're back in
action
let's get right into it so what i'm
going to do is go over here to pve one
and i'm going to click on data center
now first of all notice that each of
these tabs right here
they have their own server as the only
server listed
so for pve 3 we have a data center view
we have pv3 and of course we have pve 2
right here
so even though i have a data center
option on each
these are three separate data centers
these servers are not linked in any way
the only thing that they have in common
is that one server can ping another one
but aside from that there's no relation
but anyway
on server number one in data center view
what we could do is click on cluster
and we don't have a cluster yet so we
can simply create one
so for the name i'll just call it pve
and then hyphen cluster
and i'm going to leave this ip address
right here alone that's the correct ip
address i'll just click create
and it says ok
Adding additional Proxmox nodes to our cluster
so now we have a cluster
the cluster exists here on this server
pve1
this is still the only node in this
cluster
so by creating a cluster we're basically
saying that we intend on adding other
hosts to the cluster but we have to
actually add those hosts to make it a
cluster
so what you'll do is you'll click join
information right here
and you absolutely should not show this
right here in the open in the clear
because this is private information
right here so you don't want this
fingerprint to leak out into the public
so i'll click copy information
that should be enough
so i'll go over here to the second
server
then i'll go here to data center view on
this server right here i'll click on
cluster
and this time i'm going to click on join
cluster
and i'll paste the cluster info right
here the same info that i actually
copied to the clipboard earlier
so i just pasted that in
it autofilled the ip address for me
which is pretty cool
and right here what i need to do is type
the root password for the first server
which i've done so i will join the
cluster
now sometimes you might not see output
right here but if you go to the first
server
and then you open up the task view here
at the bottom
you should see a message here that the
join cluster
has a status of okay
so i don't know why this happens here
why we don't see anything
it is what it is
so we can safely ignore that
now i'll refresh the page
let's log back in
now notice that i have both of the
servers listed right here
if i go back to pve one
i also have both servers listed here
let's go ahead and go to pve 3
and let's add that server to the cluster
so i'm just going to do the exact same
thing i'll paste in the information
right here i'll type in the magic
password
let's join the cluster
and i don't know why this happens
as you can see i'm seeing output on this
server
but the second server there's no output
at all when i added that one to the
cluster
it is what it is sometimes you see
output and sometimes you don't i'm
actually glad that the other server
didn't show any output so you can see
what i'm talking about
but anyway i'll close this
and then i'll refresh the page
and now we have all three servers
and regardless of which ip address for
the host we type in for the management
console
we should see each of the servers on the
list and i do
so we have pve one
two
and three
so we have a few containers running here
Live-migrating a virtual machine from one node to another
and we also have a few virtual machines
as well
so what i want to do is actually show
you guys a migration
migrating a vm from one server to
another
so i need to get the ip address for this
server right here
i actually don't need the ip address but
it just makes it cooler you'll see what
i mean in a minute
so we have
10.10.10.205. so what i'm going to do is
switch over to a terminal
and what i'm going to do is actually
ping that server
and now i have a continuous ping going
to that server
so what i'm going to do is live migrate
this server right here over to pve 2.
if i expand pve 2
you'll see that it doesn't actually have
any vms at all
one thing that's pretty cool though is
that it has both of the nfs shares
mounted that we set up in an earlier
video
i didn't have to go to the other servers
and manually set those up since i joined
them to the cluster it synchronized that
over to the other servers
as far as what this is right here true
nas backups don't worry about that i was
just restoring some backups earlier to
test it out
that's why i have this home assistant
server right here i was just restoring
one of my own vms just to test out the
backup testing out backups is a great
thing to do it has nothing to do with
this series so we could safely ignore
that
anyway let's go ahead and migrate the
server
but wait a minute
this server right here is not using
shared storage
i do have shared storage right here
but if i go to the hardware tab
and then i go to the hard disk
you can see that the hard disk is stored
in local lvm
so this server is not using shared
storage at all
and you know what i don't have any
intention at least right now of setting
that up i'll probably do that in the
next video i mean yeah we have pve
shared right here
but i'm not actually using that quite
yet
now what's really cool is that proxmox
supports migration even without shared
storage
so what that means is that you don't
actually have to implement shared
storage you can actually go direct from
one server to another it's going to copy
the blocks from the local storage on
server one
to the local storage on server 2.
now a migration is going to take a lot
longer this way
if you do have shared storage then it's
super fast but you might have some
dropped packets here it is what it is
but it's pretty cool that proxmox still
allows you to migrate a server even when
you haven't set up shared storage just
yet anyway
we can see if i go down here that it's
still responding to pings
i'm curious to see how many pings are
dropped during this process let's find
out
so i'll right click on the server
and i'll click migrate
and here i get to choose which of the
hosts i want to migrate the server to
i'm going to migrate it to pve-2
and the reason why i'm choosing that
particular server is because it uses an
ssd so it has fast storage
and it also has 10 gig ethernet as well
so it should be fairly fast at least
considering that i don't have shared
storage so i'll choose that one
for target storage
i'll just make sure that it's also going
to the same storage or at least the same
named storage local lvm that same
storage exists on the others that's
local to pve two so i'm going from pve
one to pve two so this server here
should drop down
and be available here on the second host
now one problem that we have is that it
has a cloud init disk attached and it's
not going to actually migrate while
that's the case so let me go ahead and
cancel out of here
and what i'm going to do is just remove
this right here let's get rid of that
and unfortunately i do need to shut it
down to finish the process of removing
that piece of hardware so i'll shut it
down
and i'm going to do the same thing here
may as well
you know what i don't actually need a
cd-rom drive at all
so i'll remove that one
just to clean this up a little bit i
like to remove unneeded hardware it's a
good practice
so let's start these servers back up
and of course the pings have stopped
because well the machine is down so that
should resume shortly
and we see it starting up
and now the server is responding to
pings
so let's try this again
i'll right click on it let's click
migrate
again pve to i could probably keep it on
current layout but i like to be explicit
so i'll just go ahead and choose that
storage right there
and it's telling me here that migration
with local disk might take long well
that's true i mean i'm going from disk
to disk over a network that's going to
be orders of magnitude slower than a
true live migration or live migration
with shared storage which you'll see in
the next video i do understand that i am
going to accept my fate and click
migrate
let's see what happens
so it looks like it's starting it
it's still pinging that's good
so it's actually going pretty quickly
look at this
i would expect it to go a little bit
slower than that but i think that's
reasonable
and is still responding to pings
still going strong
and there we go
now it's possible that it did actually
lose a few pings i don't know it doesn't
look like it did
but the process was successful that's
pretty cool
now what i'm going to do is migrate this
over to the other server as well
i'm doing the exact same thing
and actually i can close this right here
you don't actually have to keep that
open while the process is going on
we have this cool little icon next to
the main icon or an emblem if you will
that looks like a paper airplane and
that basically means that it's migrating
that over to another server
all right so you saw me go through the
process of migrating a virtual machine
over to the other server
and of course in this video we set up
our cluster so we got a lot done today
i have one more video in this series
coming up for you guys
in the next episode we're going to take
it a step further and set up high
availability so definitely make sure you
subscribe and i'll see you there
so there we are we now have our very own
proxmox cluster or at least i do you may
or may not have extra hardware in order
to set up your own cluster but like i
mentioned in the intro
it's okay at this point in the series
you may or may not have the required
hardware to follow along anymore
but either way we're all learning we're
learning proxmox and is still fun
in the next episode which is actually
the final class unfortunately
we're going to take this to a whole new
level and take a look at high
availability
so be sure to subscribe to my channel if
you haven't already done so so that way
as soon as that episode is up you'll be
notified of that and it could already be
up actually because it depends on when
you're watching this maybe the entire
series is already available and you're
just going right through the episodes
either way i really appreciate you
watching this video and all the other
episodes in this series and i'll see you
in the next episode thanks again for
watching
[Music]
foreign
[Music]
