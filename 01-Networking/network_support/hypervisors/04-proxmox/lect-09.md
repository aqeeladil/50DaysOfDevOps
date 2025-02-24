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
hello again everyone and welcome to
class number eight yes eight in the
proxmox course i'm really excited to
have you guys here thanks for checking
out these videos in this series i really
appreciate that
in today's episode what we're going to
do is look into the concept of creating
templates for our containers i mean we
already did that with virtual machines
but you could do that with containers as
well
and you know what it's also pretty
convenient now to be fair there's not
nearly as many steps when it comes to
creating a container but i think setting
up a template could still save you some
time
so let's go ahead and dive right in
General info on converting a container to a template
all right so in the previous video i
walked you guys through the process of
creating a container and we have our
container right here
this number 103 in my case
so just like i did with the virtual
machine section of this course
i'm going to show you in this video how
to convert this container into a
template as a spoiler all you really
have to do is right click on it
and then convert it to a template so
video over let's go on to the next one
but actually not so fast there's more to
it than that there's a few things that
we should do to make this process even
better before i actually convert it into
a template what i want to do instead is
configure it a bit further to make the
process even easier going forward
Installing updates inside the container
so here i am right here logged into that
container
just like i did with the process of
creating a virtual machine
what i want to do here is make sure that
the container is fully updated
so to do that i'm going to run sudo apt
update
ampersand ampersand
sudo apt dist hyphen upgrade
i'll press enter
and as you can see here there's quite a
few packages that need to be updated so
i'm going to press enter and let it
update everything
alright so all the updates have been
installed so we'll clear the screen
and we'll move on to the next step
Running a few commands to clean the container before converting
so just like before there's a few
commands that i like to run
and this will help alleviate some of the
issues that you might run into in the
future
so an easy command to start with is sudo
app clean
and just like i did with the virtual
machine section this will essentially
clean out the app package database and
things like that and it's not going to
make a huge difference but you may as
well save a little bit of space if you
can
and that's all there is to it there's no
output it's just that simple to be on
the safe side we can run sudo apt and
then auto remove
and in my case that did absolutely
nothing but if you have any orphan
packages basically packages that were
installed as a dependency of another
package
and that particular dependency is no
longer needed this command will actually
help you wipe that out
in my case that doesn't actually benefit
me at all
and that's because there's no offering
packages in my container that's a good
thing
now next what we're going to want to do
is go into the etsy ssh directory just
like we did with the virtual machine
creation process
we have ssh host keys here and we
definitely want them to be different
if we don't delete the host keys here
then every container that we create from
the template will have the same host
keys that's not a good thing
that's going to cause a lot of confusion
for your ssh client
so what i'm going to do is run sudo rm
and what i'm going to delete is ssh
underscore host underscore star so i
want to delete every file that begins
with the name ssh underscore host
underscore
and what that's going to do is actually
purge out all the ssh host keys i'll
press enter
and we're done
now at this point we absolutely don't
want to disconnect our ssh session if we
were to do that we wouldn't be able to
get back into our server the ssh host
keys are required in order to make an
ssh connection
so i'll clear the screen
and another thing that i want to check
is the etsy machine id
and right here we have our machine id
Purging /etc/machine-id
now just like with the virtual machine
that we created earlier what we're going
to want to do right here is wipe out
this file the machine id is not
something that we want to be the same on
each container it should be different on
each container and also different in
every virtual machine
so what i'm going to do is run sudo and
then truncate
we'll do a size dash s of zero
and what we're going to do is run that
again slash etsy slash machine id
just like that i'll press enter
so i think that's enough configuration
i'm going to run sudo and then power off
and that's going to shut down this
container
and back here in proxmox we can see that
it's not running the icon actually
turned gray
and there's nothing here on the console
so what i'm going to do is just convert
Converting the container to a template
it to a template right now
and here's the option i just right
clicked on it
pretty much the same idea when we walk
through the process with a virtual
machine so i'll click convert to
template
i'll say yes i do want to convert this
to a template
and we can actually see that the icon
changed right here
it's similar to the icon here for the vm
template
kind of looks like a piece of paper
beside a monitor right here
and now it looks like a piece of paper
next to a box a box a container i think
you get the idea
Cloning the template into a VM
so now i have a template that i can use
to create containers with so what i'm
going to do is right click on it
and then click clone
i'll leave it on 104 i think that's fine
i'll change it to a full clone
for the hostname i'll call it web server
dash ct-1
for target storage i'll choose local lvm
and that should be good enough
and now that that's created i'll
right-click on it yet again
i'll clone
it and i'm going to give it a very
similar hostname
and there we go
all right so now what i'm going to do is
start each of these containers
and we'll give them both a moment to
start
actually they should be started let me
check the first one here
we have a login prompt so let's log in
all right so we created a container
template and then we created two
containers from that template but there
is one more thing that we should do on
the containers to make sure that
everything is okay
now what i'm going to do is ssh into one
of those containers
and here's one of the containers
now when it comes to cloud init it's not
actually supported when it comes to
containers when we set up the virtual
machine we installed cloud init and then
after we did that we enabled cloud init
in the gui for proxmox
but when it comes to containers there's
no such option so in that case we're
going to need to improvise
after you create a container what you'll
need to do is reset the ssh host keys
manually
Resetting the OpenSSH host keys within the container
so here we have the ssh host keys on
this particular container
so what i'm going to do is run sudo and
then rm be very careful with the rm
command
and what i'm going to do is remove ssh
underscore host underscore and then star
that's going to remove everything that
has ssh and then host in the name i'll
press enter
type in the super secret password and we
should be good
now at this point don't log out of the
server we're going to want to regenerate
the host keys before we go any further
and at least in the case of ubuntu
that's pretty easy like run sudo
then dpkg hyphen reconfigure
and the package name for the ssh server
is open ssh hyphen server
so what we're doing is we're essentially
telling the package manager to
regenerate the configuration for this
particular package
and now the ssh host keys will be
different between the two containers
that i created
to be on the safe side though
what i'm going to do is log into the
other container
so what i'm going to do is fetch the ip
address
and here it is
it's actually the same ip address except
one number is different
so i'll change it to 201 at the end
and we're in
so what i'm going to do is just repeat
the exact same process that we just went
through with the other container
so i'll go into the sc ssh directory
i'm going to remove the host keys
and then regenerate the host keys
and there we are
so as you can see we were able to set up
two containers from the template that we
created in this video and even though we
had one manual task it wasn't so bad
sure we can automate that task because
we can automate virtually anything in
linux but in this case that's beyond the
scope because there's all kinds of extra
things that we could do but i think if
we have it down to a couple commands
where we manually regenerate the host
keys that's not the worst thing
if you do decide to automate the process
of resetting the host keys on your end
go ahead and let me know in the comments
below how you decided to go about doing
that i think that would be an
interesting piece of homework for you
guys
an extra credit assignment if you will
just think of it like a challenge
so as you can see creating templates for
your containers is yet another really
awesome feature of proxmox
i'm really enjoying this series so far i
hope you guys are as well and if you are
please click that like button and i'll
have the next episode in this series
uploaded very soon so keep your eye on
the playlist and i'll see you in the
next video thanks for watching
[Music]
so
[Music]
you
