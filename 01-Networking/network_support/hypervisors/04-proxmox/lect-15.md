
Search in video
Intro
[Music]
hello again everyone and welcome back to
my proxmox course
believe it or not we are up to class
number 14 yes 14. it feels like the
series is just flying by almost like i
just started recording it yesterday or
something like that i just can't believe
how fast time is flying
okay well actually i'm recording the
majority of these episodes in one
sitting in one day so for me it feels
like today anyway in today's class we're
talking about shared storage and by
shared i'm not referring to nfs shares
or samba shares i mean proxmox is built
on linux you could create those things
on proxmox if you wanted to
but what i'm talking about instead is
mounting storage from other servers it's
called shared storage because
essentially if you have more than one
proxmox server which you know right now
we don't but if you did you could
actually share resources between servers
but shared storage is still useful even
with just one server as we're going to
find out here very shortly
and i mentioned earlier that we're not
creating nfs or samba shares in this
video but proxmox can connect to those
share types and specifically i'm going
to walk you guys through the process of
connecting to an nfs share to service
share storage so let's dive in
all right so at this point what i'm
going to do is show you guys how to add
network storage to your proxmox server
this is yet another video that not all
of you will be able to follow along with
if you do have a network attached
storage device on your network then you
should be able to follow along
on my end i actually use trunas but it
really doesn't matter you can use
synology
netapp qnap there's a number of others
out there the idea is that we're going
to create nfs storage and then mount
that storage here on our proxmox server
this also opens the door for potentially
setting up high availability which is
something that we'll be covering later
in the series
now again not all of you will be able to
follow along because not everyone has a
network attached storage device on their
network so even if you don't have that
you can just watch the video and take
notes and just understand how everything
works i think that's good enough if you
don't have access to the appropriate
hardware
now there's two volumes that i'm going
to be showing you guys how to mount in
this video
the first is going to be used for
backups
and the second is what's called shared
storage
shared storage is good for high
availability now if you have a gigabit
network as i'm sure a lot of you do then
backup storage is going to work good
enough sure gigabit is a lot slower than
10 gigabit but it's fast enough for
backups
however if you have a gigabit lan and
you try to implement shared storage for
clustering and high availability it'll
actually work well fine enough i guess
if you have more than one vm accessing
shared storage at a time then they're
going to slow down to a crawl
now as long as all of your vms aren't
doing anything intensive all at the same
time you'll probably still find gigabit
slow when it comes to shared storage but
it'll probably be fast enough
so the reason why i bring this up is
just so you keep in mind that it's
really important to understand that if
you have a gigabit network there's only
so much that you can do before it
becomes a bottleneck if nothing else
just have reasonable expectations
and you might be wondering what i mean
by shared storage
shared storage is storage that's well
shared
when we add more servers to our cluster
later on each of those servers will be
able to access that storage so
essentially i could have one nfs volume
one nfs share and every single host
basically every proxmox host will be
able to read from and write to that
share
and that's all well and good so long as
you don't have too much going on at once
but anyway just manage your expectations
and you should be fine
now what i'm going to do right now is
open a new tab
and i'm going to access my true nas
server
and here's the login screen for that
so i'll go ahead and log in and i'll
paste in my password
Creating data stores in TrueNAS
and here we have my trueness server
so if you haven't seen trueness yet
well this is what it looks like
trueness is not something that i
actually cover on my channel because my
friend tom lawrence he does a great job
already and honestly there's no reason
for me to cover it considering he does
such a great job definitely check out
his channel if you are curious about
trueness he has a number of videos on
trueness that'll teach you everything
you need to know
now in my case what i'm going to do is
actually create a new storage volume or
basically a pool for proxmox to use
so on this screen i have all my pools
and as you can see i already have one
for proxmox now what i'm going to do
instead of actually using my existing
proxmox pool this is for a production
system i'm going to create a brand new
pool
so let's go ahead and do that
and this is adding a new data set within
the pool
i'll call it pve tutorials
because that's what i'm using it for
and we need to set the permissions and i
do understand if you're not using
trueness then obviously none of this
applies to you
but you know what this is what i have so
this is what i'm going to use
i think these options are good enough
so what i'm going to do is just go ahead
and submit this
and then underneath this what i'm going
to do is add yet another data set
i'm going to call this one pve hyphen
backups
and i'll submit that
so we have pve backups right here
and what i'm going to do is create yet
another data set
and i'll call this one pve shared
i'll submit it
so i have these two data sets right here
pve backups and pve shared that i'm
going to be using for the remainder of
the series what i should do now is
actually set the permissions for those
data sets and ensure that the proxmox
user that i've already created in
truenas has access to these particular
datasets
so i'm going to create the permissions
up here
i'll edit permissions
i'm going to set the owner
i'll set that to proxmox
i'll do the same thing for the group
and i need to apply both so i check
those two boxes there
i'm going to give the group full access
i'll click apply permissions recursively
and they'll also have it traverse as
well i want to make sure that these
permissions are applied to everything
underneath this main data set
so pve tutorials is the upper level then
the pve backups and pve shared data
stores are underneath that so by
checking all of these options i'm
ensuring that the changes that i'm
making here are going to apply to those
as well so i don't have to go in and
manually make those changes to each of
those one at a time
so let's save it
and now
we should have everything set up here
for pve backups and pve shared
but that just gives us the data stores
Creating NFS shares in TrueNAS
it doesn't actually make proxmox able to
access these data stores so
what i need to do actually is create
some shares that proxmox can access i'm
going to use nfs
i'll add a brand new share here
then i'll select the path to the data
set that i created at least the first
one here
pve backups
and then under advanced options
i'm going to map all to the proxmox user
when it comes to group i'll map all to
proxmox as well
and that'll ensure that the permissions
work out
and for authorized networks i do want to
restrict this
my servers are on the following subnet
172.16.249.0
and i'm going to add another one here
10.10.10.0 both 24 subnets
if you recall we have the management
network
and then we have the vm network here as
well i always like to restrict my nfs
shares because i want to know what's
actually connecting to them
what i probably should do is add
individual host here instead of the
entire subnet but i didn't want to make
this tutorial too long so anyway
what i'm going to do is submit this
now what i'm going to do is add yet
another nfs share
and i'll be adding it for the other data
store that i've created
so i'll select that here
and i'm basically going to create it the
exact same way
and that should be all we need to do for
that
Adding NFS shares to Proxmox VE
so let's go back here to proxmox
and what i'm going to do is add the new
shares that i've created so i'm going to
go to the data center view i want to add
these particular shares to the entire
data center i want to make sure that
each of the servers that i end up adding
to the cluster also get access to those
data stores as well
so let's go to storage right here
and what i'm going to do is add storage
i want to add nfs storage
and for the id it's not asking for an id
number it's not like your vm id or
anything like that this is essentially
the name
so what i'm going to call this is pve
backups i'm just going to give it the
same name as the actual share that i'm
mounting and that makes it very easy to
do now here for server what we want to
do is add the ip address or the fully
qualified domain name if we have one to
the server that contains the nfs share
that we want to mount in my case it's
storage
dot home hyphen network dot io that's
actually the name of my truenas and for
the export i'm going to type the actual
path to that nfs share
in my case that's going to be mnt
volume 1
and it should be if i remember correctly
pve hyphen tutorials
and then the first one the one i'm
mounting right now
is pve hyphen backups
now here what we want to do is select
the types of objects that we plan on
storing inside this nfs mount
so what i'm going to do
is select container template
vz dump backup file
and snippets as well
so basically i've selected everything
except for iso image
and container
so that should actually be good enough
for me
let's go ahead and add it
so as we can see it's added right here
and it also appeared right here so as an
aside
i think i did show you guys this earlier
in the series you could click on any
storage volume
and you can see the types of things that
it allows you to store
now as you just saw i had to select the
things that i plan on storing so
that essentially allows me to enable or
disable certain things for this
particular storage
and here we have pve backups the one
that i just added
and we should be able to store the
things that i selected there in that
menu when i first created this storage
now i have nothing stored here actually
and i probably do need to clean my
trunas storage because oh my gosh i only
have 260 gigs free and considering the
4k content on my channel i could burn
through that pretty quickly anyway
let's go ahead and return back to data
center
and let's add the other storage volume
because i'm lazy i'm just going to edit
this one
and i'm going to just copy this right
here
i'll click add and i want to add another
nfs mount
and then for the export
i'll just change this to shared because
it's the same path
the id i'll call it pve shared
and the server again is storage dot home
hyphen network dot io
and it looks like it blanked out my
export here so i'll paste that back in
and i'll make sure i actually type the
correct share name and what i want to do
is configure this
i already have a storage volume for
backups here so
i'm not going to choose that i am going
to keep the disk image here
container template i should probably
choose that one
and container i'll choose that too
and as an aside i really like the fact
that you could just drop this down and
not type the entire path manually that's
going to save me a lot of time
i actually didn't know that you could do
that so i guess i just discovered
something new myself i've always been
manually typing the path to the share
that i want to mount but as you can see
right here proxmox is able to query the
server and get a list of all the shares
so what i should be able to do is scroll
down
and select the share and here it is
i'll go ahead and add it
and now we have that created right here
so now i have a place for shared storage
so i can actually add virtual machines
and have them store their disks right
here in the shared storage
and that makes high availability better
like i mentioned
because if a vm disk is in shared
storage then migrating that vm to
another host just becomes a lot faster
and i also have a place for backups
right here now earlier in the series i
went over backups
so since i do have a place for backups
now i'm going to go back here to backup
and this is the backup job that we
created earlier let's go ahead and edit
that
and the storage is currently set to
local
and that's not good we should probably
use the nfs mount that i designated for
the purposes of backups instead of the
local storage which will help ensure
that all the backups created from this
job will go to the external storage
rather than local storage
at the end of the day that's what we
want
now pve backups that is an option here
now when i added this particular storage
to proxmox if i didn't select the
correct items to enable the correct
features then i wouldn't actually see it
listed right here but it is listed so i
guess i must have done something right
so i'll click on it
now click ok
now from this point forward this
particular backup job is going to send
its backups over to my trunas server and
that's pretty cool
now how about we see it in action
i'll click on this server right here
Backing up a virtual machine to shared backup storage
and i'll just create a manual backup
i'll click the backup now button
and for the storage
i'm going to choose the pve backup
storage right here
and i'll leave it on snapshot i think
that's fine
and i'll click backup
let's see what happens
and there you go it looks like the job
has completed that's pretty cool
so if i go over here to pve backups
i'll go here to backups itself
and then here in backups we have this
particular backup file right here it's
currently using 1.6 gigabytes
this is the backup file
so we can see that it's working
now what i'll do is click over here to
true nas
i'll click on shell
and then let's change directory into
where that mount actually is pointing to
so i'm in that directory right now
so we have several different folders
here so i'm going to go into the dump
folder and these are folders that
proxmox itself created for
me and there we have the backup file
we have a log file in the actual backup
itself
so we can see that the log file is 1.8
kilobytes we have essentially 1.5
gigabytes when it comes to the backup
file itself
so as you can see i was able to easily
add additional storage to my proxmox
server i was able to create some shares
here on my trueness server mount those
in my proxmox server and now i could
benefit from both backups being on my
true nas server
as well as shared storage later in the
series
so as you can see shared storage is
pretty useful
but we're not really using it shared i
mean yeah it's shared storage but we're
not sharing it with any other server and
it's not accessible from any other
server because we only have one server
so how about we take care of that in the
next class and set up a cluster that's
exactly what we're going to do in that
video so i'll see you there
[Music]
foreign
[Music]
