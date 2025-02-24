
Search in video
Introduction
[Music]
hello again everyone and welcome back to
my proxmox course
here in class number six what we'll be
doing is creating our very own template
for our virtual machines
i don't know about you but installing
operating systems is fun i love checking
out different operating systems and
linux distributions but when i want to
launch something into production i
really don't want to go through like 10
000 steps every single time it's time to
launch a virtual machine i want to
simplify that process and that's what
we're going to do right now
alright so in the previous class we went
ahead and created our first virtual
machine and we see that virtual machine
right here
now what i'm going to do like i
mentioned in the intro is show you guys
the process of creating your very own
virtual machine template this will
definitely save you a lot of work in the
future
now here in the terminal i'm connected
to the vm via ssh and what i want to do
is add some additional value to the
template before we create it
if we're not careful there's some things
that will remain the same in every vm
that we create from the template things
that we actually don't want to remain
the same
one example of that is the ssh host keys
we can see the ssh host keys right here
and this is not an ubuntu specific thing
in general when you have ssh there's
host keys the host keys themselves are
created when you first install ssh and
if these ssh host keys are the same on
every vm
then your ssh client is going to be very
confused every time you connect your
servers
so what can we do about that
first what we're going to do is search
for the cloud init package which is most
likely already installed
so i'm just going to run apt search
cloud init
i'll scroll up a bit here
we can see the cloud init package right
here
and it's currently installed
so we already have it
if we didn't have it already
then we could simply run sudo apt
install and then cloud hyphen init
just like that
but obviously i don't need to do that
it's already
installed now i have an entire video
What is CloudInit
that is dedicated to cloud init so i'm
not going to go into too much detail
about it here but what does cloud init
actually do
the short answer is quite a bit actually
cloud init features a number of modules
that you can use to essentially master
an image or in our case a template
in a nutshell it allows you to automate
a series of tasks that you normally
would do every time you set up a new
linux server
and when it comes to resetting the ssh
host keys that's a given that's one of
the many things that cloud init does for
us
Resetting SSH Host Keys
having cloud init installed and ready to
go
isn't actually enough to fully reset the
ssh host keys so what we're going to do
is change directory into the sc ssh
directory
and there we have the host keys you
could tell which keys are the host keys
because they have host in the name
so what i'm going to do is sudo rm
ssh underscore host underscore and then
star
upper center
and as you can see all the host keys
have been deleted
and with the host keys being absent
that's going to help trigger cloud init
to regenerate those for us
Emptying the Machine ID
now the ssh host keys aren't the only
files that we want to make sure are
reset when we go to master this template
there's an additional file that we want
to empty out as well
and it's this one right here
the machine id is something that needs
to be unique per vm
and not every linux distribution is
going to have this particular file right
here but ubuntu has it and we need to
make sure that this is emptied out
now you might be under the impression
that you could probably just delete this
file but in my experience that doesn't
actually work
but what we could do instead is empty
the file
completely and one easy way to do that
is to run sudo and then truncate
and then we type dash s for size we set
the size to exactly zero
and the file that we want to empty out
is slash etsy slash machine id
so i'll press enter
and that was easy
Checking for Symbolic Links
now there's actually a symbolic link to
the machine id file
and we want to make sure that it is in
fact a symbolic link
and this is a different machine id file
actually it's located in slash bar
lib
slash dbus and then the name is machine
id
and we can see here that this particular
file is in fact a sim link and we know
that we have this little arrow right
here we also have the l right here
and it's pointing to the same file
that we emptied out
now if for some reason that's not a
symbolic link you can simply create a
symbolic link
Creating a Symbolic Link
but if you did run the ls command
against that file and it shows that it's
a symbolic link then you're fine and you
don't have to do what i'm about to do
so what we're going to do is run sudo
and then ln s we're going to create that
symbolic link that's what the lm-s
command allows us to do
and the file that we want to link to is
of course slash jetsea slash machine id
and we want to store this link at slash
var
live slash dbus
slash machine hyphen id
i'll press enter and now let's just make
sure that everything is correct
ls dash l slash var slash live dbus
machine id
and we can see that it is indeed
pointing to the correct place
the machine id file
and here we can see that the etsy
machine id file is empty
and if all that checks out we should be
good to go
now don't worry too much about what the
etsy machine id file actually is
just keep in mind that it's an
identifier that differentiates this
server from other servers if every vm
had the same machine id that would be a
problem
it just helps servers identify each
other by id if every server had the same
id that would be well confusing
and again not every linux distribution
uses this so just keep in mind that the
machine id has to be unique if your
distro doesn't use etsy machine id then
you don't need to do any of this
Cleaning the Template
now there's a few other commands that i
recommend you consider running
just to clean the template basically we
want to make sure that it's as clean as
we could possibly get it and i'm not
going to go into too much detail on this
there's all kinds of things that you
could do to clean up an image
but what i'm going to do is give you
some easy ones right now that'll
certainly help
first of all let's run sudo apt clean
that's a quick command it's just going
to essentially clean the apt database in
downloaded packages and things like that
there's probably no reason to have that
template include a cache of packages
especially considering that those
packages could very well be out of date
by the time you get around to creating a
new vm from this template
another command to consider is sudo apt
auto remove
now it didn't do anything for me
but every now and then there could be
orphan packages that are just installed
for no apparent reason or no longer have
a use
and what sudo apt auto remove does is
that allows you to remove those orphan
packages
after all packages that are not required
are just wasting space
Creating a Template
now those are the only things that i'm
going to walk you guys through when it
comes to preparing this vm to become a
template
obviously there's all kinds of things
that you can do here
for example if there's any packages or
configuration files that you want to
make sure that every vm has
it's a good idea to add it
we already installed the qemu agent in
the previous video but if you haven't
already done so it's a good thing to
include
anyway i'm all set on my end so what i'm
going to do is just power down this
particular vm so
i will run sudo and then power off
i'll press enter
and that's it
so now we have our vm right here and
like i mentioned we want to create a
template from this particular vm
just keep in mind that the process we're
about to go through is destructive
meaning we can't undo this
so just be sure that you actually do
want to create a template from your vm
before you continue
anyway i'll right click on it
and then i'll click convert to template
i'll click yes
and that's all there is to it
it might take a few seconds or maybe a
minute
but we should see the icon right here
change as soon as it's converted
and now we can see that the icon did in
fact change
so instead of a vm
this web server instance right here is
actually now a template so we actually
have a template
and we can even start using it right now
but i'm not going to have you guys do
that just yet
the next step is arguably optional but
it's a good practice to get into
so what we're going to do is click on
hardware
and what we're going to do here is
actually remove the attachment to the
iso for the virtual disk
so i'll click edit
then i'll click do not use any media
i'll click ok
so now that's done and then next i'll
click add
and then what i'll do is add a cloud
init drive
for the storage i'll drop this down and
i'll choose local lvm
let's go ahead and create it
and as you can see here we have a cloud
init drive listed in the list of
hardware here
that's pretty cool
and now that we have that we can go here
to cloud init
and we can go ahead and edit some of
these items right here so
i'm going to edit the default username
my user is actually included in the
image anyway
but it's a good habit to get into and
this is something that will give you
further customization as you get further
ahead in proxmox i'll click ok
and here i can set the password i'll
click edit
and that allows us to set the password
for the default user
and in our case that's redundant because
we already did that during the
installation of ubuntu
but this is part of the normal workflow
when it comes to the process of setting
up cloud init
so it's a good idea to get in the habit
in addition to that we have other
options here
i'm not going to go over these but one
thing that you might want to consider
doing is adding your ssh public key
right here if you decide to
if you have one that could be very
useful
but other than that that's about it i'll
click regenerate image
and now we're actually done with the
template
so to create a brand new vm from the
template we simply right click on the
template
and then we click clone
and cloning is the verbiage when we
create a vm from a template we are
cloning the template into a vm
so naturally it's going to select the
next available id by default you can of
course change that if you wish
and for this i'm going to change it to
full clone
full clone is better it's an entire copy
of that particular template it's not a
differential or anything like that it's
a full-blown copy
the target storage
even though same as source is probably
okay i like to be explicit i'll set it
to the storage that i want it to be
which is the local lvm
for the name i'm going to call it web
server hyphen 1
and that should be good enough
so i'll click clone
[Music]
it's going to begin the process
but you know what i'm going to go ahead
and create another vm from this template
and i'm going to go through the same
process here as i did last time
and i'll call this one web server 2.
and now we can see that it's creating
and of course we could check the status
down here
it looks like it's already done so
what i'm going to do is right click on
this vm i'll start it up
i'll do the same thing for this one here
and we can watch the progress here on
the console it's already starting
the other one should start shortly
and that one's starting to
and there we go we have a vm
so what i'm going to do is just log in
real quick right here and grab the ip
address
and see what it was assigned
text is kind of small but it's 249.250
the last two octets here
so i'll go down here to my terminal
and there we go we're connected
now the name here says web server so we
should fix that i'll do that in a moment
let's go ahead and connect to the other
one
so back up here in proxmox i'm going to
do the same thing i'll grab the ip
address
so i'll log in
ipspace a that's the command i can use
again to grab the ip address
and in this case it was given an ip
address that ends in 251
so let's go ahead and do it
there we go we're logged into both vms
Updating the Host Name
now the last thing that i recommend that
we do is update the host name
and the reason for that is because
they're both called web server
and that's a bit confusing so let's go
ahead and update that we'll run sudo and
then nano
and the first file that we want to edit
on this vm right here is slash etsy
slash host name i'll press enter
type in my super secret password
so i'll append dash 1 to the end of the
name here
ctrl o and then enter to save the file
ctrl x to exit out
the next file i'm going to edit is slash
etsy hosts
and i'll do the exact same thing here
change it to web server hyphen 1
save the file
let's reboot it
then here do the same thing
we'll change that to web server hyphen
2.
and again in etsy hosts
web server hyphen two
and then i save the file
again ctrl o and then enter and then
ctrl x to exit out
now the server should be rebooting
and that's exactly what they're doing
this one should already be done actually
we can see the host name right here is
web server hyphen one
and here we have web server hyphen two
so we were able to create two vms from
the template that's pretty cool
i think that's going to help you guys
out in eliminating some of the work that
goes into setting up a new linux server
with a template you can automate all
kinds of different things
so i'll let your imagination take over
from here
but as far as this video in particular
is concerned i think that'll do the
trick
Outro
so at this point you guys now know how
to create your very own virtual machine
templates and that's pretty cool it'll
no doubt save you a ton of time going
forward you won't have to go through the
10 000 or however many steps there are
in the os install process because let's
face it that can get a little old after
a while
now what we're going to do at this point
in the course is actually take a break
from virtual machines for the next two
episodes because it's time to get into
the topic of containers
so make sure you keep your eye on the
playlist on the series because i'll add
all the new episodes to this series to
that playlist as soon as they're out and
make sure you subscribe if you haven't
already done so and i'll see you in the
next video thanks for watching
[Music]
you
