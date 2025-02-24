
Search in video
Intro
[Music]
you know as a tech youtuber
i find myself telling you guys to back
up your servers all the time
and other youtubers that are in the same
space as me they basically say the same
thing and there's a good reason for that
it's extremely important and i'll never
understand why so many people out there
just you know they don't do a good job
of backing up their servers
but i know that's not you because i know
you are great at backing up your servers
but i'm going to make it even better
because what i'm going to do in this
video is i'm going to teach you guys
about backups and snapshots in proxmox
so let's take a look
alright so let's take a look at backups
and snapshots as we've gone through the
series so far i've created a few
containers
and i've also created a few virtual
machines
now to be honest i don't have all that
much going on right now
these particular containers and vms all
they really include is apache and the
default apache configuration is what
they have so all they have is the
default start page
but what we're going to do instead is
pretend that these are extremely
important and we definitely want to back
these up
now proxmox supports both snapshots and
Backups vs Snapshots
backups we're going to look at both in
this video
so what i'm going to do is start with
virtual machines and i'm going to click
on this one right here
and you'll notice that we have a backup
section here as well as a snapshot
section so what's the difference between
a backup and a snapshot
so let me try to explain the difference
so the thing is a backup is completely
separate from the virtual machine
i mean it's not separate in terms of it
being a backup of the virtual machine it
includes everything on the disk because
it is actually a full clone of the disk
but you can move this back up to another
storage media and if you have shared
storage for example if you have a
trunast system on your network you can
actually mount that storage which we'll
be covering later in the series and send
your backups over to that
in addition to that there's a dedicated
proxmox backup server that's something
that i'm going to be going over in a
dedicated video but i just bring it up
because i want you guys to know that it
does exist
now a snapshot on the other hand is
actually a part of the virtual machine
itself you can't actually take the
snapshot and move it to another system
in fact snapshots are actually a part of
the virtual machine disk not a clone of
the virtual machine disk like a backup
is
so you might be wondering when you
should use the backup feature
and when you should consider using a
snapshot
now part of that is down to personal
preference in my opinion a snapshot
makes a lot of sense when you want to
test a piece of software you're not
really sure how that software is going
to behave
or maybe you want to evaluate the
software and find out if it's a good fit
for the purpose that you are installing
it for
in that case it makes sense to create a
snapshot
and then you could test that piece of
software
and then if you decide that you don't
like it or something like that you could
just revert the snapshot and it'll be
just like you've never installed that
particular application
of course you can just uninstall the
application you don't need a snapshot
for that but sometimes when you install
an application and then remove it
there's bits and pieces basically junk
files all over the disk and even when
you uninstall the application it's
possible that some of those files might
remain
so snapshots are a really good idea when
you're testing something
Example of taking a snapshot
so let's see a quick example of that
i'm going to take a snapshot of this
virtual machine right here i'll click
take snapshot
and let's just say i want to remove
apache
i'm going to give this snapshot a name
that's going to help me understand
exactly what its purpose is
so i'll just name it before removing
apache simple enough
Quick note regarding including RAM in the VM snapshot
now one thing that i want to call your
attention to is this box right here for
include ram
this is pretty cool
so you could think of this as snapshots
on steroids
i mean normally a snapshot is just a
snapshot of the disk
and actually if you choose to include
ram and that means you're going to get a
snapshot that'll include this state in
memory as well
which could actually be really cool it
could be very useful you could have a
snapshot that not only includes the disk
for the current state of the disk as
well as ram
now i'm going to uncheck this because i
don't really need that for this
demonstration i'll just click take
snapshot
and let's see the process
and as you can see it's fast that was
really quick and snapshots generally are
very quick that's one of the benefits
and we have the snapshot right here it
tells us when the snapshot was created
and i didn't change anything on the
virtual machine but i did create a
snapshot so what i can do now is
actually change something on the vm
and then see how to revert that change
but first of all i do need to know the
ip address so i can go ahead and connect
to it
i prefer to use ssh when i can
and there we have the ip address so what
i'll do is switch over to a terminal
and now i'm connected to the virtual
machine
so what i'm going to do is remove apache
to be on the safe side i'll add the
purge option
and i'm going to remove the apache 2
package
before i do that though
i'll just open up a new tab here
and i'll prove that apache is currently
working
and there's the default start page so
far so good
so back here in the terminal what i'm
going to do is complete this command
right here
and now apache is uninstalled you don't
believe me
what i'll do is refresh this page
and of course it doesn't work
now what i'm going to try to do here is
install nginx instead so i'll run sudo
apt install nginx just like that
you don't have to follow along with this
it's just an example
let's refresh the page
and now we have the engine extart page
so i've successfully switched this
particular server from apache over to
engine x
now the thing is i don't actually have a
preference between the two but i wanted
to give you guys something different and
enginex is something different compared
to what we had before
Restoring a snapshot
so we have nginx here what if i wanted
to revert the change that i just made i
did create a snapshot before i did
anything basically so i'll click right
here
i'll go over to snapshots
and what i want to do is roll this back
i'll confirm it
it tells me that it's done
so let's click over to the console
and since i didn't choose to include ram
the state of the machine was not saved
so i will need to start it up again
just wait for it to boot up
and now it started so if i go right here
and refresh the page
we're back to apache
so you can immediately see the value of
snapshots you could test something and
then revert it back and that's a very
powerful ability to have as an
administrator of virtual machines you
will definitely find yourself doing this
quite a bit
so snapshots for the most part are
fairly self-explanatory
Backups
let's go ahead and move on to backups
when we create a backup of a virtual
machine there's a few other options that
we can choose so it's not incredibly
complex but there's a few other options
here
so what i'm going to do is click backup
now
and as you can see we have additional
options
right here we could choose where we want
this particular backup to go i only have
local storage right here
now as an aside lvm thin which is the
storage that i've been using for virtual
machine disks that's not listed here but
for right now i only have this one
option i don't have all that much space
here so that's not great
that's why it's probably a good idea to
store the backup somewhere else
but actually it's always a good idea to
store the backup somewhere else i mean
if you are keeping all of your backups
here on proxmox itself and then proxmox
goes down maybe your disk goes bad or
something like that
well if that's the case you lose the
backups as well
so even though it's called a backup in
this case i don't really consider it a
backup if it's not somewhere else
but again we'll get to shared storage
later in the series so we're not going
to worry about that aspect so much right
now
now we have several options right here
as far as how the backup is going to be
captured we have snapshot mode suspend
mode
and stop mode
which of these should you actually
choose
Backup modes (snapshot, suspend & stop modes)
so each of these different modes
pertains to how much downtime you're
willing to have if you have a virtual
machine that absolutely cannot go down
for any reason
that's going to limit your options quite
a bit
now at the expense of less downtime
you're actually increasing the
possibility for disk corruption it's
incredibly uncommon but it could happen
think of it this way if you are creating
a backup of a disk and that disk has
open files and files are being written
to then if you take a backup in the
middle of a file being written to
it's possible that maybe data hasn't
finished writing when the backup is
created so there could be some integrity
problems there
however in the back end of proxmox
itself it has some magic and some kung
fu basically that it tries to do to
eliminate problems like that it's still
a possibility it's unlikely
but just keep in mind that these options
generally pertain to how much downtime
you're going to have and more downtime
in this case means better integrity it's
kind of like a trade-off so let's go
over stop mode first
if we set it to stop mode that's
actually going to stop the vm
and i literally mean shutdown it's going
to execute an orderly shutdown of the
virtual machine and then create a backup
that also means that your backup if you
choose this option will have the best
consistency and once the virtual machine
is shut down a back-end process within
proxmox will kick off and create the
backup
if the virtual machine was running when
you kicked off the backup process then
once it's done it's going to start the
vm for you
the vm was stopped when he created the
backup then it won't do that
so that's the stop option
we also have an option for suspend mode
as well
now the proxmox documentation actually
doesn't like or recommend this option
because it results in the greatest
amount of downtime
in my opinion whether or not this is
actually a good or bad option depends on
the use case and the importance level of
the virtual machine
if it's not really a big deal to suspend
it for a while then i don't really see
anything wrong with it
now you can think of suspend like
suspend on your laptop or your desktop
a lot of laptops and desktops will go
into suspend mode when you don't press
any keys for a certain amount of time
and then to resume the computer you just
press any key or press the power button
and it comes back to life in suspend
mode in that case your laptop or desktop
will resume exactly where you left off
you could think of suspend mode here as
pretty much exactly the same thing
it's going to put your vm into suspend
mode and once it is it's going to create
the backup then once the backup is done
it's going to resume the vm
now the virtual machine will not be
accessible at all while the backup is
happening in suspend mode just keep that
in mind
but being in suspend mode does actually
increase the consistency of the backup
so the trade-off might be worth it
another option that we have here
is snapshot mode
and that's a little confusing
i just went over snapshots
that's the option right here now i'm
going over backups so why is there a
snapshot option for a backup
now the snapshot mode isn't actually the
same thing as snapshots like i've gone
over in the past
this is a specific mode of the backup
feature
and this actually results in the least
amount of downtime when it comes to
backups
so if you're able to use this option
it's the one that i recommend
now in a nutshell the way a snapshot
mode backup actually works is that once
you kick it off proxmox is going to
create a backend process in the system
itself that's going to do a live backup
of that vm
and that's going to actually capture
data blocks while the vm is running if
you have the qemu agent installed then
it's actually going to increase the
consistency of the backup which is yet
another reason to make sure that all of
your vms actually have that installed
so on my end that's actually the option
i'm going to go with i'll click backup
and let's see the process play out
and now the process is finished but if
you take a look at the output something
that you'll see here that's fairly
interesting
you can see that the qemu agent executed
a file system freeze command
and that's helpful because again that's
going to improve consistency so it's in
snapshot mode
it's going to freeze the file system and
then it's going to resume the vm and
then create the backup like you can see
right here
so if this option works out for you i
highly recommend that you choose that
particular option when you create your
backup
and then right here we have the backup
Restoring a backup
so i could click restore if i wanted to
restore that snapshot
and even though i didn't actually change
anything i'll just go ahead and do it
just so you can see what it looks like
and i'm going to leave everything here i
mean you could choose a different
storage if you wanted to
but i'm going to leave it at the default
which is essentially just going to
restore the backup where the original
already is
so i'll just click restore
and i'll say yes
and right now it's actually complaining
that the vm is running so
what i'm going to need to do is actually
shut it down
and now that it's shut down let's try
that again i'll click restore
i'll leave the storage option here alone
but what i am going to do is check this
box right here because i do want this vm
to start as soon as it's done restoring
so i'll click restore
i'll confirm it
and now it's restoring
and as you can see the process is
finished
and the vm is starting up
so after the backup is restored it did
exactly as i asked it to do and started
the vm
so that part's pretty simple
now the thing is backups are great but
Creating backup jobs
if you don't actually have this
automated then well i mean you'll
probably forget we're all human i know i
would
so if you go here to data center view
before we were just clicking on vms and
running backups and snapshots within the
vm settings
but the data center view like i
mentioned earlier in the series pertains
to every server and every vm so if i go
to the backup options here underneath
data center
then what i could do is add a task
and this is going to allow me to create
a backup job this is how you automate
backups
and these settings here like i mentioned
allow you to create a backup job that
pertains to every server and every vm so
what you could do is back up each node
independently and by node it's talking
about the proxmox node so in my case
pve1 is the only one that i have
so i'm not actually able to choose
anything else but if i had other servers
here that i could have a separate backup
job for each
maybe i could have the backups for one
server kicking off at midnight and then
another server at 1am and then the third
server at 2 am however you want to do it
but i'm going to leave it on all because
i only have that one anyway
now for storage when this backup job
runs this is going to allow you to
determine where the backups end up which
again we'll get to later so for now i'm
just going to leave it on local
then we set the day of the week so
perhaps you might want this to run on
fridays and you can select individual
days here
as you can see but i'm just going to
make this run every friday
i think that's good enough
and then you can choose the start time
so maybe this particular server i wanted
to start backing up all the vms at one
in the morning
selection mode we can include the
selected vms so we can just choose which
ones we want to be a part of this backup
job
but i'm not necessarily a fan of that
what i'm going to do instead is choose
all and that's going to gray out this
section right here
now what all allows me to do is ensure
that every vm is backed up like it
mentions it says all and it means all
but another benefit of that is as i add
new virtual machines to the server it's
going to make sure that those are backed
up as well so i don't have to go in here
every time and add virtual machines
manually if i set it to all it's going
to take care of that for me
we could choose to have an email sent to
a particular person or mailing list when
the backup fires off that's a good idea
then for the emails
we can set it to always which means an
email will always be sent when a backup
job runs
or we can set it to failure only which
means we won't get an email unless there
is a problem i'll leave that up to you
now for compression i'm going to leave
that alone we have that option in the
normal backup settings as well
i think leaving it at the default is
more than adequate
and then we can choose a mode for the
backup job as well it's the same thing
as doing a manual backup
the same descriptions of what these
modes mean applies here as well so here
you just choose the mode that you like
the best and every vm that's a part of
this job will be backed up via that mode
so that's pretty self-explanatory
i'm going to leave it on snapshot mode
in my case
and then i'll click create
so now we have the backup job right here
now when we get to the point later in
the series where we set up shared
storage i recommend that you revisit
this and change the settings such that
it will create the backups in your
shared storage which is a lot safer than
creating the backups on the same server
that you're backing up and also make
sure you subscribe because at some point
in the future i'm going to be doing a
dedicated video on the proxmox backup
server which is going to allow you to
take this to a whole new level
so there you go now you guys know how to
create backups and snapshots within
proxmox that's pretty cool
now what's also pretty cool is the fact
that proxmox makes available a
standalone product called proxmox backup
server and that particular product will
help you take your proxmox backups to
the next level
now it's not actually part of this
series but if enough of you guys want me
to cover that what i'll do is i'll
actually cover it in a standalone video
so if you want me to do that please
click that like button if you like this
video that also helps youtube understand
that you guys want to see more tutorials
just like this
and i should have the next video in this
series uploaded very soon if i don't
already have that uploaded so i'll see
you there thanks for watching
[Music]
so
[Music]
you
