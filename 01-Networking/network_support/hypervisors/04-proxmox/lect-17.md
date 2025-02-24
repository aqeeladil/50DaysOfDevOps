
Search in video
Intro
[Music]
so here we are the final episode of my
proxmox course
and i'm sad and happy at the same time
i'm sad to you know see it come to an
end i had a lot of fun filming these
episodes for you guys but like i
mentioned earlier in the series there
will be standalone episodes so it's not
actually the end it's kind of like a new
beginning
so in this video we're going to take
what we've built in the previous video
which was you know setting up a cluster
and we're going to take a look at high
availability
so let's dive in one last time to
proxmox
Discussing clustering and high availability
all right so let's go ahead and get
started with high availability
as you already know from the previous
video i now have three servers in my
cluster
and i have each one in their own tab
right here in my browser
now i didn't decide to set up three
servers randomly
three servers is required for high
availability
now i want to make sure you understand
that you don't actually have to have
three servers to have a cluster
but you do have to have three servers in
order to have high availability
what's the difference
if i have two servers in my cluster then
that's the minimum that's required in
order to live migrate a virtual machine
as you saw in the previous video i can
right click on a virtual machine
and i can migrate that virtual machine
to a different host
and it's pretty straightforward
but again only two servers are required
in order to benefit from live migration
now simply having a cluster doesn't
automatically give you high availability
what high availability means is that if
a node goes down then the virtual
machines are going to automatically
start on another node
with two servers like i mentioned you
automatically have the ability to
manually migrate a virtual machine from
one host to another
with high availability then you're
hoping that if something unfortunately
happens to one of your proxmox servers
that your virtual machines are going to
automatically start on another server
as you just saw i migrated this virtual
machine over to the other host it was on
pve one
now it's running here on pve two
but i did that manually
now when it comes to high availability
the reason why you need three servers is
technically because you need an odd
number of servers
so hypothetically if you have two
servers in your cluster and you enable
high availability
it might work just fine you might not
have any problems at all
until you do have a problem and when you
do have a problem it's going to be a big
problem
so let's pretend that i only have two
servers here
let's just forget that pve 3 even exist
at all so if i have high availability
set up with just two servers
then both servers are essentially going
to vote for themselves during the voting
process
so essentially what happens is when you
have a cluster and high availability is
enabled there's a heartbeat between all
the servers
if a server goes down the heartbeat is
lost
but never fear if you have three servers
you have two other servers that can well
take up the extra work
it's highly recommended that you have
three servers because you need what's
called quorum in order for the best
decision to be made about which host is
going to run the virtual machines that
are now not running on a host because it
went down those virtual machines need to
be running on some other node when
there's a problem with only two servers
your options are very limited there
and also with two servers your quorum
votes are well unreliable
so long story made short
when it comes to proxmox if you look at
their documentation
they recommend at least three servers in
order to enable high availability
you could have more servers than that i
mean it'd be awesome if i had a bunch of
servers i mean how cool would that be
but if you have access to three servers
feel free to set up high availability if
you want to
but even if you don't decide to set up
high availability you should still
cluster your servers because you still
have the option of migrating servers
manually and you just saw me migrate a
server manually
and i forgot to show it in the previous
video but of course you can migrate
containers as well i have these two
containers here
so i'm going to go ahead and migrate
this container over to pve 2.
and the thing is that all works just
fine as an aside you can't actually live
migrate a container
notice here it's shutting it down
so pings will be lost and the container
will not be accessible until the
migration is complete
it's actually going to copy this
container over to the other node and you
can see that transfer happening right
now
it actually copied that disk over to the
other server and now
that container is running on pve-2
and all of this works just fine even
without high availability yeah that's a
benefit but it's not the only benefit
one of the more common reasons why
people set up a cluster
is because you're able to update a host
and not have your virtual machines go
down sure your containers might go down
but we already know that containers
can't be live migrated
for example i don't have any updates
right now but if i did i could refresh
this right here
and of course i'll just go ahead and do
that it's not going to show any updates
i actually just checked before i hit the
record button so that's how i know that
there's no updates here
well let's say that there were updates
i could literally right click the host
itself
and i could do a bulk migrate and
manually migrate everything over to
another server
then once that's done and all these
containers and virtual machines have
moved over to another host i can install
all of the updates reboot it
and then i can migrate all the virtual
machines back onto this host or at least
the ones that were on this host
update the second one reboot that one
and then repeat that for however many
servers that i have and all of that is a
benefit of clustering and we haven't
even entered into the territory of high
availability just yet i just want to
make sure that all of you guys are fully
aware of why you would want to set up a
cluster and where high availability fits
in now i'm not recommending that you do
this but if i was to go ahead and just
you know yank the power cord out of the
back of one of these servers
if i had high availability set up then
the virtual machines will be running on
a different host and that's great that's
definitely a very cool thing to benefit
from
high availability takes clustering to
the next level now what i'm going to do
is actually migrate the storage of a
virtual machine actually i'll migrate
all of them to the shared storage
so right here i have a container
and if i click on resources
we can see that it's actually using
local lvm so what i'm going to do is
just shut down everything
i'm going to show you how to properly
convert everything over to high
availability it's not just enabling
settings we want to make sure that our
virtual machines their storage are on
the right storage medium specifically
shared storage
so i'm going to shut this one down
and this one
and this one
this one as well and i'll shut down this
one too
i basically want to make sure that
nothing is running
as a matter of fact to make this process
even better i'm going to delete all the
virtual machines that i don't plan on
using for this particular episode
so we have web server one right here i'm
going to keep that one
we already know that containers can't be
live migrated so at this point in the
series containers actually don't have
any other purpose whatsoever so what i'm
going to do is just go ahead and delete
this container
i'll remove it
make that one go away
and i'm going to leave the other ones
alone
and i'll do some more cleanup here
let's remove this container i'm just
going to make sure that everything is
purged
it's going to make this very simple
and this server right here is just from
one of my experiments off camera so
honestly i should have deleted that one
quite a while ago
let's go ahead and kill it
and i'll get rid of this one as well
Moving a disk to shared storage
so now we're down to just this vm right
here web server one
if i go to the hardware tab
we can see that the virtual hard disk
here
is actually stored in local lvm
now to get the full benefit of high
availability and clustering
and this is another thing that doesn't
require clustering as well it's just
definitely something you want to do you
want to migrate this particular disk to
a different storage medium specifically
shared storage
so right here we have an option for move
disk i'll click on that
where do we want to move it to
well what i want to do
is move it here to pve shared this is
the shared storage that i set up for
this tutorial series so that's where i'm
going to move it and i'll delete the
source i want it to only exist on this
medium right here
let's go ahead and move it
and it's happening very quickly i have
10 gig ethernet it's a beautiful thing
it's already done actually
so what i'm going to do is just wait for
this to refresh
there's probably a few other scans or
checks that it's doing in the background
i'll let that finish and i'll be right
back as soon as this finishes moving
and now it's done
you'll notice that the hard disk is now
on pve shared
so i'll start up the vm
you really shouldn't notice a whole lot
different here
now to be fair this particular vm might
be a little slower because shared
storage in my case is actually using
spinning rust hard drives
so yeah there might be a little bit of a
loss in performance but it's going to be
okay
now what i'm going to do is just log in
real quick
because i don't remember what the ip
address was of this host it's
10.10.10.205.
so what i'll do is switch over here to a
terminal and set up a ping
and now i have a continuous ping over to
that server
Live migrating a VM with shared storage
now what i'm going to do is live migrate
this server back to pve one
in the previous video i already showed
you how to do that but in that video i
didn't actually have this disk on shared
storage
so it took a minute or two which isn't
really bad
but it could be a lot faster let's see
how fast this is actually going to go
let's migrate it
we're going to migrate it again to pve
one
and it's done
so i made sure not to edit that part of
the video normally i do edit these
particular scenes to make them a little
bit faster
so i didn't actually edit this part of
the video up until task ok appeared on
the screen
so that was pretty quick
and it's still pinging
let's move it back to the other server
and i'm going to watch the pings more
closely let's see if one gets dropped
now it didn't actually lose a ping but
what i did notice is where it says right
here 4.7 milliseconds
it did actually pause on that for a
little bit longer than the others so it
there was a little bit of a delay but it
didn't actually miss anything so nothing
ever went down
and of course it's already on the other
server so
again everything that i just showed you
guys is par for the course when it comes
to clustering
Enabling high availability
now let's take a look at enabling high
availability and have even more fun
but the first thing that we want to do
is make sure that the virtual machine
that we're going to add to high
availability is shut down so
i'll gracefully shut down this one right
here
and now that vm is well shut down
so basically what i'm going to do is add
this virtual machine right here to high
availability if you have more than one
virtual machine that you want to have
enabled for high availability then
you'll set that up on each of those but
since i only have this one virtual
machine now i'm just going to focus on
that one i'm going to click on data
center
i'm going to scroll down right here to
ha
i'll click add
and then i'll add web server one i want
it to be started
and i'm going to leave max restart and
max relocate both at one those are the
default values
essentially if it needs to restart a
virtual machine it's only going to try
so many times it defaults to one that
should be good enough so i'm just going
to go ahead and leave it at one
and it'll try a maximum of one time to
relocate the server you can increase
this if you want to but honestly if you
need to increase these to higher numbers
then i would think that your environment
probably has bigger problems to worry
about than high availability anyway i'll
click add
and we can see that it's added right
here now if you recall this virtual
machine was shut down
but the desired state was to have it
started so it automatically started it
for us
Simulating a VM failure to another node
at this point if the node that this
virtual machine is running on has a
problem is going to restart the virtual
machine on another node
so what i'm going to do is actually
simulate this by logging into my switch
i'll do this off camera real quick
and i'm actually going to disable the
network port that this host is actually
using for the heartbeat
essentially i'm just going to pull the
plug on it
so i just disabled the port and any time
now this should actually show that it's
no longer available in fact i'll click
on it let's check the status right here
as you can see it's having a little bit
of trouble reaching this host and the x
already appeared right here so it's
definitely down
it's still powered on i just disabled
the network port for this particular
interface so proxmox has no way of
actually communicating with it
so i just went over to another tab and
i'm on the server right here
if you recall that server was running on
pve 2
and shortly it should actually go to
another machine
all right so i had to do a little bit of
behind the scenes work here but
as you can see the virtual machine did
in fact restart on pve one
the reason why i didn't do that right
away is because well actually i disabled
the wrong network port
i actually disabled the management
network on the server
not the network that the virtual machine
was actually using but as soon as i
disabled that other port the correct
port it went ahead and restarted the
virtual machine over here on pve one
because as you can see here pve two is
down it's not accessible
so we can see that high availability is
actually working now what i'm going to
do is re-enable the network right now
and we'll see this node right here come
back online
all right so i've re-enabled the ports
for pve-2 the switch that i'm using
takes a minute or so to reprovision when
i make a change like that and it should
be online here shortly actually i
already see some question marks here so
something is happening it looks like
it's coming back online right now
and there it is
we have the green emblem next to it so
it's actually back up and running
and this server here is happily running
on pve one what i'm going to do is just
migrate it back over to the other server
and it requested the migration
we can see that it's actually in the
process of moving
and it's already here
and it's done so as you can see high
availability is working it's definitely
something that you should take advantage
of if you can if you have the
appropriate hardware and if you do well
why not
but anyway we were able to set up high
availability in this video we could see
that it's clearly working and that's
awesome
[Music]
thank you guys so much for checking out
this series i really appreciate it and i
mean that i appreciate each and every
single one of you guys because you guys
helped make this happen for me
if it wasn't for you guys i wouldn't be
able to do what i'm doing and i'm having
so much fun creating these videos for
you guys
now if you want to help me out even
further please share this content with
other people
you can share it on your favorite social
networking group you can put an ad on a
billboard okay well don't do that that's
expensive but just feel free to share
this content with other people and
spread the learning that would be
awesome
now i'll have other proxmox videos on my
channel here very soon but for right now
that's the end of this particular series
i again appreciate you guys thank you so
much and i hope you enjoy your day
[Music]
you
