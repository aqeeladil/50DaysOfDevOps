Transcript


Search in video
thank you so much for tuning in to
learnlinux tv your source for linux
related fun and learning
i love producing linux related content
for you but i can't do it alone if the
content on this channel has been helpful
to you then please consider supporting
learn linux tv and one of the ways that
you could do that is by becoming a
patron which will give you access to
exclusive perks
also be sure to check out my latest book
mastering ubu server 4th edition
and while you're here be sure to
subscribe new content is uploaded each
and every week
thank you so much for your support i
really appreciate it now let's get
started with today's video
[Music]
hello again everyone and welcome back to
learn linux tv in today's video we're
going to take a look at the process of
creating an ubuntu 2204 template within
proxmox
and creating a template is a great way
to simplify the creation of a virtual
machine
once you have your template set up you
can simply right click on it you can
clone it and you can create any number
of vms from that template it saves a lot
of time now if you're a longtime
subscriber of learnlinuxtv you might be
thinking well jay's already done videos
about creating templates in proxmox so
why is he covering this again well
actually the method that i use to create
templates has changed a little bit so i
figured i would make an updated video to
show you guys how i'm creating templates
nowadays or specifically i'm actually
using an official cloud image of ubuntu
rather than the iso image so i'm going
to show you that and also i'm using
cloud init as well so that's another
thing that you'll get to see in this
video anyway i'm excited to show you
guys my new and updated approach when it
comes to creating templates within
proxmox so let's go ahead and dive in
so what i'm going to do first is create
a new virtual machine
and this vm in particular will become
the template but we need to have a
reference vm to start with
for the vmid i'm going to give it id 900
as you might know if you've seen my
proxmox series that i have on this
channel you can set the vmid to any
number you'd like as long as it's not
actually in use already
but i like to give it a high number for
the id
that'll make it show up lower on the
list but again you could give it
whatever number you'd like
for the node i'll set that to the second
node
you can create it on whatever node you'd
like though doesn't matter
and then for the name
what i'm going to do is call it ubuntu
2204
template
just like the vmid you can name it
whatever you'd like you can't use some
characters like you know periods or
underscores but for the most part you
could just set this to whatever you'd
like the name to be but so far so good
let's click next
for the os this is where we would
otherwise select the iso image that we
want to boot from
but what i'm going to do
is choose not to use any media like i
mentioned in the intro i'm going to be
using a cloud image not an iso image so
i really don't have any use to attach an
iso image here so that's why i'm
choosing to attach nothing
on the next tab
i'm going to choose qemu agent
i always like to make sure that this is
checked now keep in mind the qemu agent
only works if you actually have it
installed but you may as well check this
box reason being if you install the qemu
agent in the future then it's already
enabled in the virtual machine so that's
one less thing that you have to change
later
let's go to the next tab
and then here we can actually configure
the disk for the vm
but actually i'm going to diverge from
my normal process right here and i'm
going to delete the disk
so now we have no disk at all
but without a disk how are we actually
going to use this
well i will be adding a disk i'm just
going to go about it a bit differently
so for now i'll just choose to not have
a disk and we'll create that later
so we'll go on to the next screen
and for the number of disks i'm just
going to leave that at 1. i think that's
fine this is just a template anyway we
can always increase that later
and for the memory
i'm going to lower that down to 1024
again it's just a template so i want
that to be the lowest number that i can
comfortably set it to anything lower
than 1024 might be a bit uncomfortable
so i think this is a good minimum right
here
moving on
on the network screen what we're going
to do is choose the network that we want
the vm to be on by default we'll be able
to change this later so it really
doesn't matter but i do like to be
consistent and i do have a dedicated
virtual machine network here
in my case it's vmbr1
on your end if you only have vmbr0 and
no other network you can go ahead and
choose that there's no problem but if
you do have another network that's
dedicated for virtual machines like i do
you may as well select it
let's go to the next screen here
and we can review the information here
make sure that everything is correct and
i think it looks good enough for me
so i will click finish
you can see that the virtual machine is
being created
and now the name that we've selected for
the virtual machine has appeared right
here so actually we're done with this
particular step
now next what we're going to do
is go to the hardware tab for the
virtual machine so i will click on the
vm right here
and then hardware
and what i'll do is add the cloud init
drive
we don't actually have to do that right
now but since we're in the gui we may as
well so i'll click on that
and for the storage i will use local lvm
that's my local storage
and i'll click add
now that we have the cloud init drive
what we can do
is go to the cloud init tab
and we can have a little bit of fun with
this
so what we'll do is set some default
values for the vm
for example the username
normally when you install ubuntu server
it actually asks you for your username
during the process but with a cloud
image it's not going to ask you anything
at all because there's nothing to
install it's already installed ubuntu is
already installed in the image and ready
to go but the image has cloud init built
into it and cloud init will read these
values and actually make them the case
within the vm so i'll set my username
right here
and i'll click ok
dns domain and dns servers i'll leave
that alone
for the ssh key if you have one then i
recommend that you paste it right here
in this window and you know what that's
what i'm going to do
and by doing this your public key will
be present in the virtual machine that
you create from the template which saves
you a step so why not
so we have the ssh key set
next we'll click on the network section
here
and what i'm going to do is set the vm
to dhcp
i actually prefer dhcp for all of my
servers most people use static ips but i
like static leases better they're also
known as dhcp reservations so if you
haven't heard the term static lease then
now you know what i mean and by using
dhcp i can control which vm gets which
ip right for my firewall and like i said
that's how i prefer it so i'm going to
set mine to dhcp
but also you should set this to dcp even
if you do plan on using a static ip
because if you don't set it to dhcp then
your vm will have no network
connectivity whatsoever when you create
it so we don't want that so i'll set it
to dhcp and if we want to set a static
ip for it we can always do that later
so click ok
and i can't believe that i almost forgot
to set the password
without that then our user account would
be useless we wouldn't even be able to
log in
i'll set the password
and i'll click ok
so here we should have everything that
we need for cloud init in order to
finalize the process i'll click
regenerate image
and now we should be good to go on cloud
init
and that's it for the web gui at least
for now let's switch over to a terminal
because there's some commands that we'll
need to run so make sure that you
already have access via ssh to your
proxmox server you could always do this
by clicking on the console if you don't
have access to ssh right now but
considering that there's some commands
that i want to paste it'll be a lot
easier if i use a terminal so i'll
switch to a terminal
so here in the terminal i'll type ssh
then root
and what i'll be doing is connecting to
the same proxmox node that i created the
vm on
which in my case was pve 2.
i'll say yes
and i'm logged in instantly and i wasn't
asked for a password or anything like
that because i already have an ssh key
that's associated with my proxmox
servers
but anyway i'm logged in to pve2 via ssh
and i'm ready to move on to the next
step
now the first thing that we're going to
do is download the cloud image
and to do that i'll type wget and then
after wget i'll type in the url
but i highly doubt that you have the url
for the cloud image memorized so we're
going to need to find out what that url
is
back on the web browser what i can do is
open a new tab and i'll paste in the
address right here to the download page
i'll have this url as well as all of the
commands that i'm using in the blog post
for this video the blog post will be
linked down in the description below so
if you want to copy and paste the
commands into a terminal you'll be able
to do that anyway i'll press enter
and here we have a download page for
cloud images specifically the minimal
version for ubuntu 2204.
i scroll down
we have a dot img file right here and
that's what we want to download
so i'll right click on it
then i'll click copy link
and then here in the terminal i'll paste
in that url
and since i'm using wget that will
enable me to go ahead and download this
particular image now i don't remember if
you have to install wget so if the wget
command comes back as command not found
you just simply run sudo apt install
wget
but anyway i'll press enter
and now the image is downloading
and it's done
so if i list the storage here
you can see that i have the cloud image
here on my local file system
now before we go any further there's a
command that i need to run on this
virtual machine
and it's one of those standalone
commands that we really should run but
doesn't really fit into its own section
so i'm just going to get it out of the
way right now and i'll paste it in
and here what we're doing is we're
creating a vga console and without this
we wouldn't actually see anything on the
screen when the vm boots up you know
when you click on the console within
proxmox well without this option being
set you're not going to see anything at
all i'll leave a link in the blog post
for the other blog posts that i found
online when i was actually experiencing
that same problem that blog post helped
me figure it out it led me to this
command right here so i'm going to give
that blog post credit and i'll put that
right in the article
now before you press enter though
pay special attention to the vmid
i set my vm to id 900 which is what i
have here so in my case it's correct if
you set your vmid to anything else make
sure you change that in the command
before we go any further
and now that's set with that out of the
way let's get back to the disk it's not
actually completely ready to use just
yet there's a few things that we'll need
to do first
so again we have our cloud image right
there and the first thing that i'm going
to do is rename this particular image
i'm not sure why this is required it
makes no sense to me at all but it is
what it is
we're going to move
that file name to a new name
and i'll actually use this opportunity
to shorten the name
and i'll give it the extension of dot
qcow2
now shortening the name was not required
i could have left the name as is the
file extension is what's important in
this step for some reason
if i don't rename the file extension to
dot qcow2 it doesn't work again i don't
know why it is what it is
so i'm going to rename the file to
include the dot qcow2 extension
but the disk still isn't ready just yet
there's one more command that we'll need
to run to condition the disk properly
before we actually import it into
proxmox and because i'm lazy i'll paste
in the command right here
and what i'm doing is i'm going to
resize the image
as you can see i'm setting it to 32 gb
bytes we can see that at the end of this
command right here
you can set it to whatever you'd like
you can set it to 16 8 or whatever you
think is appropriate all of my virtual
machines have a minimum of 32 gigs so
i'll set it to 32g in this example
and of course make sure you actually
update the file name in this command
right here if you are copying and
pasting to whatever you named the file
but anyway we're all set on that
and now we're actually ready to import
this disk into proxmox
and the command that i've just pasted
into the terminal this one right here
that's the command that's going to do
exactly that
but before you press enter there's a few
things that you should actually check
here before you actually continue
first of all we have the vmid set to 900
again in this case
which is correct for me
on your end just change that to whatever
it's supposed to be
and the same for the file name change
that as well and then finally i have
local hyphen lvm that's the local
storage on my proxmox server now on your
end yours might not be named local lvm
especially if you're using zfs so what
you can do
is actually go back to proxmox if you
don't already know what the name of your
local storage happens to be
we have a list of storage volumes right
here
and i know this is mine it has the
majority of the extra space here
and by default you'll probably have
local lvm as well if you went along with
lvm for your installation
but i know that's the correct one in my
case
so the final command looks like this
and the qm command is a proxmox command
you can actually operate proxmox from
the command line you don't even need the
web gui we want to import that disk into
vm 900
the image that we want to import is the
one that i gave it right here the one
that i have local
and then i have the name of the storage
volume that i want to import it into so
i'll press enter
and as you can see it was able to import
the disk
now let's switch back to the proxmox
console here
and let's go back to our vm
and then if we go to the hardware tab
we have right here an unused disk
this is the disk that we imported right
here but even though we imported it into
the virtual machine the virtual machine
will not use it unless we tell it to
so for this i'll click edit
and we'll click add to finalize the
process of attaching this disk to the
virtual machine but before we do that if
your underlying disk is an ssd then what
i recommend is you click discard right
here
also click advanced
and then enable ssd emulation
you should only do this if you have an
ssd if that's the storage type that you
have for your proxmox server that's what
i have so that's what i'll set
so i'll click add
and here we have the vm disk
and this is the very same cloud image
that we've imported earlier
we went ahead and resized it we attached
it to the vm so the disk is all set and
ready to go
well almost
let's click on options
and take a look at the boot order right
here we definitely need to edit that
because we created this virtual machine
initially without a disk then of course
our disk is not even going to be a boot
option at all so if we were to create a
template without actually setting the
boot order then we would actually need
to configure our vm after we create it
to set the boot order every time so we
may as well just do that right in the vm
so what i'll do is i will enable it
and i will drag it to the second
position
i like to keep the cd drive as number
one
i mean i might want to at some point
boot from an iso image for some purpose
or another so it's good to have that
option here even if i really don't think
there's a good chance that i'll use it
what's going to happen is it's going to
check the virtual cd drive for an os or
a disk if you will
and if it doesn't find one then it's
going to move on to the second option
here
and the second option is of course our
cloud image that we've converted into a
vm disk
so click ok
and we should be good to go on that
another thing that we might want to
actually consider is changing the start
at boot option
by default it's set to no
so what that means is that any vm you
create from this template will not
automatically start up
now this is completely up to you
you might have virtual machines that you
don't want running all the time
if that's the case then you should
probably leave this alone and keep it at
no
in my case i actually do like all of my
vms to start automatically
so i will check this box
now with all of that done that should be
it
now we can finally create our template
so what i'll do is i will right click
right here
and then i'll click convert to template
now before you click this be double sure
that you've set everything exactly the
way you want it
there's just no way to reverse this
process so just take your time
verify all of your settings and if
you're sure that you have everything
exactly how you want it then you can
finalize the process and convert it to a
template
i'm ready to go on my end so let's
convert it to a template
i'll say yes
and the icon right here should change
anytime to show that the process is done
and it just changed
so now we have a vm template
and now that we have the template let's
take a look at the process of creating a
new virtual machine with this template
and to do so i will right click on it
and then i'll click clone
that's going to bring up this window
right here
you can give the vm an id
so i'll give it 799 as an example that
should show it right above the actual
template itself
and instead of a linked clone i like to
do a full clone it takes a little bit
longer to do that but it is my preferred
way to go
you can actually save some space by
setting it up as a linked clone but i
literally never do that i like to
allocate everything all at once just to
be done with it
so i'm going to set it to full clone
and of course i need to give it a name
so what i'll do
is call it ubuntu test
i'll click clone
and we can see that the process is
starting
down here in the task window we can see
that it's spinning
and it's already done
that didn't take any time at all
so now we have the virtual machine
and what i should be able to do is right
click on it and start it up
and if i go to the console we should see
it boot up
which is exactly what i'm seeing right
now
now we see a login prompt but we
shouldn't try to log in yet
we want to make sure that cloudinit has
actually provisioned our user account
first
so you might run into a race condition
if you try to log in as your user
account the one that you set up in
cloudinit before it's ready so we want
to make sure that we give it enough time
to finish
and right now we actually see some
information about the ssh host keys
which for me only shows up when the
process is done so it should be done
so what i'll do is press enter
and that brings me back to the login
prompt
i'll type in my username
the one that we set up in the cloud init
drive
and then the password
and now i'm logged in
another thing that we should check is we
could run ipa to see if we have an ip
address which i do it ends in 205 in my
case
if i didn't set the dhcp option i might
not have actually seen an ip address
here so that's a good sign
and then next what we're going to do
is we're actually going to install the
qemu agent
and we could do that by typing sudo apt
install
qemu hyphen guest hyphen agent
and that should do it
i just press enter to accept the
defaults here
and now we have the qemu agent
and at first it's not actually going to
run
and i'll show you what i mean so if i
run systemctl
status qemu guest agent
it's going to show inactive and dead
but all we should have to do is reboot
it
i'll type sudo reboot
and now the machine is already coming
back up
so i will go ahead and log in yet again
i'll recall the previous command where i
checked the status
as you can see right here the qemu agent
is actually working
and because we have the qemu agent we
could do things like this i could right
click the vm
and i can actually shut it down
i could have done that in the console
window but with the qemu guest agent
that enables things like this you know
restarting the instance from the web
console
and as you can see i was able to shut it
down
so i think it's safe to say that our new
template is working
so there you go in today's video we set
up a brand new template for ubuntu 2204
within proxmox i showed you the process
of downloading the cloud image for
ubuntu 2204 importing that into proxmox
building the template setting up cloud
init and then launching a vm from that
template if this video has helped you
out then please consider clicking that
like button to let youtube know that it
helped you out which in turn helps me
because it spreads learning to other
people that might also benefit from this
knowledge anyway thank you guys so much
for checking out this video and
subscribing to learn linux tv i really
appreciate it and i'll see you again
very soon
[Music]
[Music]
you
