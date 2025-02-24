Intro
[Music]
hello again everyone and welcome back to
learn linux tv
i am really enjoying creating proxmox
videos for you guys it's such a fun
technology and now that you have your
very own proxmox server it's time to
dive into the web console so i could
show you how to use it let's go ahead
and take care of that right now
Interface Overview
all right just like i mentioned in the
intro to this video
we're taking a look at the user
interface for proxmox in more detail
as you can see here i'm currently using
a web browser which means that the
interface is a web console
you should be able to access this from
any browser on your lan so there's
nothing special here you just enter the
ip address and the port number of 8006
which is the default port number for the
interface you type that into the url bar
in your browser and you should be able
to log in
and you should see the user interface
like you see here
i'll be giving you more and more
information about the interface as we go
along throughout the series
so right now i'm going to focus on an
overview of the interface without going
into too much detail
as we go along the complexity in each
class will increase
so if you are curious about higher level
details here we'll get to that later on
so the interface is broken down into a
tree menu like you see right here
at the very top level we have the data
center
that's your entire data center
if you have more than one proxmox server
you'll actually see each individual
server listed down here directly
underneath it
in this course on my end at least i'm
going to be walking through the process
of setting up multiple servers as we go
along on your end you only really need
one if you have multiple servers then
you're welcome to follow along as i
create additional servers but for right
now just keep in mind you only need one
server
and if you do have more than one server
and you decide to create a cluster
you'll see each of your hosts right here
in this menu
we also have additional views up here if
i drop this down
we have a folder view a storage view and
a pool view
Server Overview
i'm not going to show you these just yet
because we don't really have anything to
show yet i haven't even created my first
virtual machine
so there's not really a huge benefit
with these additional views just yet
so here we have the actual server that
we set up
if we click on summary
then you can see some details about the
specs for this particular server
so as you can see we have various meters
here such as ram hard drive and cpu
that shows us how the resources are
doing in general on this particular
server
as you can see there's really not a lot
going on here and that makes sense
because like i mentioned i haven't even
created my first virtual machine just
yet so there's not really a whole lot of
work for proxmox to do
proxmox tries to stay out of the way as
much as it can
so i think this memory usage and cpu
usage is pretty good it's leaving the
majority of the resources available for
the work that i'm going to have it do
later
in addition we get some specs regarding
our server right here so you can see in
my case that i'm using an amd epic cpu
it gives us the kernel version
right here for this particular release
of proxmox
and also our repository status is here
so you can see that we have the
enterprise repository listed here but is
currently disabled
and that subscription does require a
cost but proxmox is free so you don't
have to worry about losing features if
you don't pay for proxmox but you will
get additional features such as
enterprise quality packages and updates
which are pretty cool
and there are several different tiers
that are available that each have
different benefits so the higher level
tiers are going to get you support
the higher cost options for support are
going to get you well more support
so if you're going to be running proxmox
in the enterprise then it's highly
recommended that you consider that
if nothing else giving a little money to
proxmox actually helps a project i do
recommend that
and in exchange for that you'll at least
get access to the enterprise repository
which is definitely very good to have
Interface
now going through the interface here
we have a section for notes
and that's pretty handy actually
you might find it helpful to keep some
notes about your server that's pretty
cool
especially if you have more than one
individual that are going to be
assisting you with configuring and
maintaining your proxmox server such as
those of you that are working in a team
for example
so this might be something that you'll
find useful
you also have the shell section
which is pretty cool because this gives
you access to a terminal window that is
running on that actual node
as you see right here it says pve1 so if
you need to use the command line
interface you could do that right here
we'll be exploring the command line
interface later on in the series so
we're not going to worry about that too
much right now
under the system section we have a
networking section
we're going to be exploring this later
on in the series so i'm not going to
worry about it so much right now but if
you want to create additional bridges
maybe activate other adapters you can do
that here
but again we'll get to that later
in this section we see the individual
certificates that are enabled for this
server in most cases the self-signed
cert is fine
now to be fair i don't really like
seeing this exclamation mark right here
for the padlock
but again it's okay i don't recommend
that you make your proxmox server
publicly available unless you have to
if nothing else don't make the
management interface publicly available
the vms can be publicly available just
not the interface so i don't really see
much value in setting up a cert
and anyway in order to do that you have
to set up an account with a registrar
and also purchase a domain
and that's just beyond the scope of this
video
but anyway the reason why i want to show
you guys this is because if you do have
access to create a domain
and then purchase a certificate or maybe
use let's encrypt that's definitely
something you should consider if you can
it definitely doesn't hurt
you also have a section for dns right
here
so if you have a custom dns server in
your network you should make sure that
the ip address for that matches right
here
and this is pretty cool we have access
to the host file for the server
so if there's any static host entries
that you want to add here you can
definitely do that
now i actually recommend you avoid this
if you can because it's better to use
dns for hostname lookups anyway
so if you have access to a dns server i
recommend you add any entries there
because that makes those particular
entries available anywhere on your
network
but if you do have a reason to update
the etsy host file you can do that here
under time we can set the time zone this
is something that we did during the
installation process
but i do recommend that you take a look
at this date and time and make sure that
it's correct
just like with every distribution of
linux if the time isn't correct really
strange things will happen
so you'll definitely want to make sure
that the date and time is correct right
here if it is we can continue
and right here we have a section for the
syslog
if you're having any trouble at all with
your proxmox server it might be a good
idea to take a look right here and just
see if there's any error messages if
nothing else if you do see an error
message you can google that error
message and see if there's a solution
just keep in mind that the syslog is
available right here if for some reason
you do need to take a look at the logs
Updates
so that's it for the system section
we have an update section as well if i
click on that
we'll get a list of updates right here
if any updates are available
now i just literally installed this
server so perhaps it hasn't had time to
check to see whether or not there's
updates or maybe there's actually no
updates available
we can click refresh to find out
and it's giving us this error again that
we don't have a valid subscription for
the server which seems egregious and
horrible but again it's really not bad
it doesn't matter i'll click ok
and even though we saw that error you
can see that the process is continuing
it's going to give us an error message
as we see right here which again is
normal because i don't have
authorization to use that particular
repository because i didn't pay for it
it's still enabled but it's going to
error out and it's going to give us an
error right here
so it considers the overall process a
failure even though technically it isn't
it just wasn't able to hit that one
repository it's okay like i said several
times we could definitely ignore that
and continue on
now notice right here that a bunch of
packages actually showed up as being
available
and this is very common when you first
install proxmox
you'll definitely want to make sure that
you install every single update here
i'm going to click upgrade right now
that opens another window
as you can see right here
and it's going to give us another
confirmation of the packages that are
going to be upgraded if i was to
continue
and you could type y or n depending on
if you want to continue or not if you do
want to continue you could just press
enter
y is default it's capital that's what
that means i'll press enter
we're going to leave this window open
and actually let these updates install
and every now and then you might
actually get a prompt like you see here
it's asking us what encoding to use it's
utf-8 in my case so i'll press enter
generally speaking if you do see prompts
like this you can just accept the
defaults that should be fine
all right so the process of updating the
server is complete you can safely close
this window now
i'm going to click refresh again just to
confirm that everything has indeed been
installed
i'll close this out
and the window here is now empty which
means we did indeed install all the
updates that were available and that's
great
at this point i do recommend that you
reboot the server we'll talk about high
availability later on in the series but
for now we did install a bunch of
updates and some of those are going to
be security updates so we definitely
want to reboot the server so i'll click
on reboot right here
then i'll click on yes
so i'll give it a few minutes to reboot
and then i'll be right back
Repository
so i just updated the server and that
all went well we can see that there's no
more updates available so next we have
this section right here which is simply
called repositories
now here is telling me that the
enterprise repository is enabled
but there's no active subscription at
this time
anyway this particular section of the
interface right here just shows you
which repositories are enabled on your
server
if i did want to add another repository
i can click on the add button like i
just did
and again of course it's going to show
me that nag screen one more time
but we have other repositories here that
we can add including test repositories
we also have this no subscription
repository here as well because it
includes some testing and less stable
updates in this repository which i don't
want on this server at this time
but if you do want to test features that
are up and coming you can enable that
repository along with these test
repositories if you'd like but i don't
recommend that we do that because that
could lead to breakages and things like
that that's only for those of you that
really have a good reason to test these
things such as early adopters or those
of you that would like to help proxmox
test new features before they come out
which is of course always helpful but
again that's beyond the scope just keep
in mind that in this section we can
enable or disable additional
repositories
now you might be thinking why don't you
uncheck that enterprise repository so
you can stop seeing that nag screen
the thing is it's grayed out you can't
actually disable it
and the reason why is because it's a
file as you see here it tells you where
that particular file actually is
but i'm going to leave that alone i
don't really think it's that big of a
deal to click on a nag screen every time
it comes up
so i'm not going to make any actual
changes here
also these repositories right here are
also file level repositories like it
shows here
so we're not able to comment those out
either i'm going to leave it alone but
again
just keep in mind if you want to make
changes to repositories you can do that
right here
Storage
now i'm not going to actually talk about
the firewall in too much detail in this
class
because we're going to be spending some
time with this later on in the course so
for now just be aware that there is a
firewall inside proxmox
and you can use that to allow or
disallow traffic as you see fit
but later on we'll get to that so i'm
going to skip this section for now
here we have a section for storage
and what's cool about this is that you
can get a listing of all the storage
volumes that you have on your server
right here
so if for example you add a new physical
disk to your server you can see it right
here
you can also wipe storage volumes in
this section as well
just exercise caution if you're going to
be doing that
but anyway i think that this particular
section is mainly useful if you want to
just get an overview of the storage
volumes that you have and here we can
see some information about the ssd that
serves as the root file system for my
server
it's a samsung ssd 980 it's one terabyte
and then we see the individual
partitions underneath we have a
partition here for lvm
and actually that corresponds to this
right here
now it might be alarming that i am using
98 of my storage and i haven't even
created my first virtual machine yet
here is telling me that i only have 17
gigabytes free that's not really true
you don't want to go by that
what this is telling us is that lvm is
using up all of the hard disk
so we need to consult lvm itself to find
out how much space we have free
and we can do that right here
we have a storage volume called lvm thin
and we're literally using zero bytes of
this storage zero percent
so there you go
an lvm thin is actually what we'll be
using when we create a virtual machine
and we tell it to create a virtual disk
it's going to store the virtual disks in
this section right here lvm thin so if
you want to know how much storage you
have available you can find out right
here
moving on
we have a path for directory storage
that's beyond the scope of this video
we also have a section for zfs and
that's also beyond the scope here
like i mentioned in the previous episode
if you have very capable hardware
especially hardware with a lot of memory
zfs is a really good choice especially
if you are using proxmox in production
if you don't have really awesome
hardware
or if you're not using it in production
then you should probably leave it on the
default of ext4
in my opinion
moving on we have soft storage
that's also beyond the scope of this
video
replication we need two nodes to go
through that
and we will go through clustering later
on so we're not going to worry about
that right now
we have a task history section
pretty much the same stuff you see here
so actually you could leave the bottom
section here fully collapsed and just
look at this section if you want to look
at the task history it's up to you
then we also have a section here for
subscription
we have the server id for our specific
server
we probably shouldn't allow that to be
seen in the public the only reason why
i'm allowing you guys to see this is
because this is a test server
and actually it's going to become a
production server for me after i'm done
recording the footage
so this server id right here it doesn't
really matter if you guys see it
if you do decide that you want to
support proxmox and benefit from that
enterprise repository and possibly their
additional support options
then this is where you would actually
insert that key so if you click upload
subscription key
you can paste your subscription key
right here
so now you know
now here on the left i mentioned that we
have the data center view
and the data center view just to be
clear this contains settings that are
specific to the entire cluster we don't
actually have a cluster yet which is why
i'm not going through this in too much
detail
but if you do see an option that's
available here in data center view
and it's also available here on the
server view
then just know that the data center
version is going to override the one
that's here on the server
because the options here are
cluster-wide
like i mentioned we're going to be going
over clustering later on in the course
so right now i'm going to ignore most of
these options
Additional Features
now here next to the server
we can actually expand it to show more
options underneath
we don't really have much here though
we have the local storage for the server
and what's pretty cool about this is
that you can see the individual vm disks
that you might have
and that gives you more information than
the previous screen that we saw earlier
that showed you how much space is
available here not only do you get to
see how much space is available
zero percent is being used as you can
see
but also like i mentioned you can view
individual disks
and also individual container volumes as
well
now
there's really not much here honestly
but there will be when you create vms or
containers then this section here is
going to fill up all the vms that are
running on this particular host will
show here underneath that host if you
have more than one host you can expand
those servers and see what's underneath
those
and in a cluster environment that's
great because you can see which servers
are running on which host
i think the usefulness of this
particular structure will become more
apparent as we go through the course now
up here we have two blue buttons that
are very important
we have a button to create a new virtual
machine
and we have a button to create a new
container
now the reason why i haven't mentioned
this until now is because the next video
is going to talk about this in more
detail
specifically in the next video what
we're going to talk about is whether you
should be creating virtual machines or
containers
when is it appropriate to use a
container for your goal and when is it
appropriate to use a virtual machine
that's exactly what we'll be talking
about
and again that's the next video
in the video after that we're going to
create a new virtual machine
then later on in the course we'll create
containers as well but for right now i
think that's enough when it comes to the
web console yes there's a lot more than
what i just showed you in the console
there's definitely a few things that
i've completely glossed over
but like i mentioned we'll get to those
things i think at this point though the
information that i did provide you with
in this video should be more than enough
to help you navigate the ui
as you can see it's pretty
self-explanatory when you know the
general overview and now you should
so you now have your very own proxmox
server that's awesome you can create
virtual machines and you can create
containers
but which one should you create well
that's the question that we're going to
be answering in the next video which
should already be uploaded on my channel
so i'll meet you over there
[Music]
so
[Music]
you
