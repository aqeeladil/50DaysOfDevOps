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
The Question
to create a vm or not to create a vm
that is the question
whether it results in more memory usage
and a pinned cpu causes you troubles oh
i'm sorry this isn't proxmox shakespeare
but i am actually here to answer a very
important question which is whether or
not you should create your resource as a
virtual machine or a container there's
pros and cons when it comes to each and
that's exactly what we're going to
tackle in this particular video
now it's going to be a lecture in this
video right here but don't worry we'll
get back into the action of proxmox
shortly but we do need to answer this
question so let's go ahead and dive in
Demo
so here on your screen right now you are
seeing an actual proxmox cluster
in fact this is the actual proxmox
cluster that we will be creating later
on in the course
and i'm able to show you this because i
don't actually record the videos in the
same order that you see them in
but this works out for me because i have
a container right here
and i also have a virtual machine if you
take a look at the icons they're
different for each so for this one right
here this icon it kind of resembles like
a cube so to speak so essentially it's
an icon of a container
down here we have an icon that looks
kind of like an imac or some kind of
integrated computer interesting choice
for an icon for a virtual machine that's
supposed to represent a server but i
digress this is a virtual machine right
here
now this in case you're curious is a
container template this is something
that we'll be creating later in the
course
and this right here is a virtual machine
template and what's cool about a
template is that i can right click it
click clone and spin off a virtual
machine or a container from the
respective template
now we'll get to those things later in
the course
but for right now what we're trying to
do is understand what to choose when it
comes to creating a container or a
virtual machine i mean right up here
we have a create virtual machine button
and we have a button for creating a
container so you could do one or the
other
you can have multiple containers
multiple virtual machines a mix of both
it's up to you
so what should you pick now the short
answer is that you should pick whatever
makes the most sense for your use case
what i like to do is base this decision
on how much ram i have on the host
so if i click right here on this host
right here
you can see that i have quite a bit of
memory free
i'm actually only using 1.6 gibby bytes
out of about 125. technically it's 128
gigs of ram but anyway i have a lot of
memory
so if this was a resource star server
let's just say for example i had four
gigs of ram that's not very much
you can still use four gigs of ram
but you're kind of limited there because
if you think about it each virtual
machine will use at least 512 megabytes
of ram
but honestly nowadays i wouldn't create
a virtual machine with less than one
gigabyte of ram so if you have a system
with four gigs of ram then you could
already consider one gig sacrificed for
proxmox itself
so that leaves you about three
and if you estimate one gigabyte per
each vm and that's on the low end
then you can basically run just three
virtual machines on that host
and even less so if you are running a
resource intensive virtual machine maybe
an application that is just memory
hungry perhaps you can only get away
with one virtual machine
now containers are a little bit
different in this regard because they
use fewer resources so if you are
running a home lab and you just don't
have the funds for a server like this
i get it this is expensive this hardware
is not cheap
and it's very common to have a system
with about four gigs of ram in the home
lab because well when it comes to home
lab you use what you can get
so in the case of a resource starved
server then in my opinion it makes sense
to use containers as much as you can
there's an additional downside when it
comes to containers that i'll get to
here very shortly but the first thing to
think about is how much resources you
actually have available on the server on
the host server itself
and in some cases that'll actually
decide for you so again if you have like
four gigs of ram in my opinion your
decision is already made go with
containers
now when you create a virtual machine
and i'll use this one right here as an
example
and i'll go to the hardware tab
i have two gigs of ram more or less
that's allocated for this virtual
machine in particular
i have one cpu core
so i guess that's not all that bad
but all i'm doing right here in this
virtual machine is running apache and
all that's doing is just serving the
default apache start page
so honestly two gigs of ram is probably
a waste for a use case like that
this particular server is most likely
better served as a container instead of
an actual virtual machine
now if i take a look at this container
right here
i have one gig of ram allocated for this
but this one gig of ram you can actually
think of this as a limit
it's not actually using one gig of ram
but it can use up to one gig of ram
if this container only needed like 768
megabytes or something then that's all
it's going to use
but it can't use more than one gig so
it's a limit
that's one of the differences between
virtual machines and a container
and of course it gets way more involved
than that i mean we're dealing with c
groups and all kinds of linux kernel
things here that i'm not going to get
into in this series
but to make it simple
containers use fewer resources than
virtual machines
so in my opinion anytime you can get
away with using a container you probably
should
but there's one downside though when it
comes to containers versus virtual
machines that you need to be aware of
so here we have a virtual machine
and as you can see i have three hosts
this particular virtual machine is
running on pve-2 that's the name of this
proxmox server that is running on right
now
i have pve-1 and pve-3 as well
and since i have a cluster here which is
something we'll create later on i can
right-click on this vm and i can migrate
it over to another host so i'm going to
migrate it over to pve one let's see how
long it takes and here's the thing
normally what i do is i edit loading
times because i just can't stand loading
times it's just a waste of your time if
something takes a bunch of minutes to
finish
then that translates to several minutes
of video time so i'll fast forward
through it i'll speed it up that's what
i do but this time i'm not going to do
that i'm just going to click migrate and
i'm not going to edit this part of the
video at all
let's see how long this actually takes
so
wait a minute
that's it
i could barely finish my sentence it
says task ok well actually all it's
doing is requesting a high availability
migration
so it takes a little bit more time than
that
so we see an icon right here that looks
like a paper airplane so that means that
this server here is migrating to another
host and it's already done
Containers
okay so you saw that it didn't really
take too long to migrate a virtual
machine but what does that have to do
with containers versus virtual machines
now one thing you didn't see in the
output is you didn't see any notation
that is going to shut down the virtual
machine it was a live migration and that
means exactly what it sounds like it
just simply migrated it over to another
host and it did that live now
now let's see what that looks like then
if i try to live migrate a container
over to that other host so i have this
container here running on pve one
i want to move it down here to pve to
let's do it
so i'll click on migrate
and let's take a look at the output
this is going to take a little bit
longer
and that's one downside right there is
that migrations with containers they do
take longer
and one thing to note is that
if you look at this
it's telling me that it's shutting down
that container
so actually live migration is not
possible with containers at all so if
you are running an application that
cannot go down
then already that rules out containers
because if you migrate a container it
does stop the app it shuts down the
container it's not available your users
cannot access it and it's going to
literally copy that container over to
the other host so it's not a live
migration it's copying it from host a
over to host b
now the process is already done and if
you look at the output here there's a
lot more going on
first it shut it down
it started the migration
it created a logical volume
that makes sense so far
and then as you can see here it's
actually copying data
and then it's doing a final cleanup
and then it's going to start the
container on the target so now
the container is right here
so again you can't live migrate a
container if that's something that you
need to be able to do that rules out
containers
your app will be down while it migrates
now another thing that i want to bring
to your attention
is that not all applications will
actually run properly in a container
now there's no master list of
applications you can download somewhere
like a spreadsheet or something that
lists which apps work in containers and
which apps don't
it's more or less trial and error i've
run into applications every now and then
that for whatever reason just won't run
in a container
another downside about containers is
that if you are running an application
that is supported by a vendor
and they discover that you are running
their app in a container
sometimes their stigma against
containers and i don't really understand
why that is but if that's the case they
might actually deny you support
there's no actual reason why they can't
help you but you know software vendors
are what they are
if it's an unsupported configuration
something that they don't have any
information about then it's possible
they may not support you
so if you are running an application
that has some sort of support contract
you might want to check that first to
see if there's a clause in there that
they don't want you running that in a
container yes i know they should get
with the times it's silly
but it is what it is no judgment
sometimes that's the case
but even if support is not the case or
not a concern
usually what it comes down to is
resources containers use fewer resources
so they allow you to stretch your
hardware even further
now again here i'm not really resource
starved i mean
i have a lot of ram
so in my case i could create vms or
containers all day long it doesn't
really matter
but some of you guys you are not running
a production proxmox server like i am
maybe you just have an old server that
you're learning on
or maybe you work in an enterprise
that's very cheap and you can't get them
to buy that awesome server that you want
and they end up buying something cheap
that doesn't really have all that much
in the way of resources it is what it is
so as long as you choose according to
your hardware i think you should be fine
Outro
all right so now that we have answered
the question as far as whether you
should be creating resources as virtual
machines or containers why don't we
actually create a virtual machine in the
next video i'll be showing you the
process of launching a virtual machine
the video after that i'll show you how
to create a template of that virtual
machine and then after that we're going
to start getting into containers
specifically and you know what that next
video should already be uploaded so i'll
meet you over there and we'll launch our
first virtual machine
[Music]
foreign
