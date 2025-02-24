Intro
[Music]
hello again everyone and welcome back now that i'm doing a full tutorial series on proxmox virtual environment i
figured that it's time to also check out the proxmox backup server as well which is exactly what i'll be doing in this
video as we go through today's video i'm going to give you a full overview of the proxmox backup server which will include
sections for installing it i'm also going to show you how to integrate it with proxmox virtual environment the
command line interface for the backup client and more so i can't wait to get started let's go ahead and get started
right now and i'll show you everything that you need to know to get started with the proxmox backup server let's get
right into it [Music]
Section 1 - General information
alright so before we get started i'm going to give you some general information about proxmox backup server
specifically what it is what's the goal it tries to solve for us as well as some
other details about this piece of software if you already have a general idea of what the proxmox backup server actually
is then feel free to skip over to the next section and we'll get it installed
okay so what exactly is the proxmox backup server at its core it's an enterprise backup
solution basically what you do is you install it from an iso image that you can write to
a flash drive and it's a targeted installation of linux that is built to be an entire backup server that you can
send your backups to it integrates with proxmox virtual environment but you don't have to use
proxmox virtual environment but if you do have a proxmox ve server or cluster it's fully optimized for virtual
environment so it's definitely a great way to go if you are already using virtual environment in your network
also proxmox backup server features an easy to use web console that you can use from your web browser
and it makes it very easy to configure the server to view your backups to view the health of your server and there's
many more things that you could do on the dashboard there's also a backup client that you can use with proxmox backup server as
well and this is true even if you're not using virtual environment the backup client can help you send backups to the
proxmox backup server even if the source isn't proxmox virtual environment for
example you can have a debian or ubuntu virtual machine or physical server and
you could actually create a file level backup from that server and send that back up to the proxmox backup server
in addition to that there's many other features that proxmox backup server supports such as encryption
deduplication data integrity and more
What do you need to get started?
but what do you need in order to get started well first of all you need a server to
install pbs onto the minimum requirements for that server include having a 64-bit cpu
two or more cores two gibby bytes of memory eight gigabytes of storage
and a network interface card those are the minimum requirements now your experience overall will be a
lot better if you have four or more cores four gibby bytes or more of memory and 32 gigabytes or more of storage
but as long as you meet the minimum requirements you could definitely evaluate the proxmox backup server and
if you can meet the recommended requirements or even go beyond the recommended requirements even better
now continuing solid state storage is highly recommended it's not required but it's highly recommended if you have a
lot of servers that are sending backups to your proxmox backup server having solid state storage is going to enable
your server to be able to better keep up with all of the i o that's coming at it especially if you have a bunch of
servers that are backing up to it when it comes to the web console all the usual suspects are supported when it
comes to browsers so it's recommended that you have the latest version of at least one of the browsers as shown here firefox chrome
edge and safari those are all supported so as long as you have a recent version of one of those you should be in good
shape so with the general information out of the way what's next well this particular video is broken
down into several sections in the next section i'm going to show you how to install the proxmox backup
server once that's done i'll give you an overview of the user interface
after that i'll walk you through the process of creating backups which will include a section that'll show you how
to integrate proxmox backup server with proxmox virtual environment so in the next section we'll go ahead
and get it installed so what you'll need to do is grab a usb key download the proxmox backup server iso image there's
going to be a link down in the description you'll use that image to create a bootable flash drive once you boot your
server from that flash drive you'll be able to install proxmox backup server and that's exactly what we'll take care
of in the next section so i'll meet you there [Music]
Section 2 - Installation Process
all right let's go ahead and install proxmox backup server what i'm going to do in this section of the video is walk
you through the entire installation process so off camera i went ahead and created a
bootable flash drive with the proxmox backup server iso image and i've inserted it into my server
powered it on and here we are now what you're seeing on the screen is my tinypilot kvm the server that i'm using
doesn't have an html5 console of its own so i'm using a tiny pilot which is actually my favorite kvm solution it's a
raspberry pi kvm solution and that's how i'm able to see what's on the screen of my server right here in my
web browser anyway what i'm going to do is select this option right here because this actually corresponds to my
flash drive so i'll press enter and the screen size might fluctuate a little bit here that's normal different
resolutions so here we have the very first screen of the proxmox backup server installation
process so we're going to get this started all right so i'll press enter on the first option to install the proxmox
backup server so here we are we have the license agreement on our screen i'll just click
i agree so right here it's giving us some
information about the installer and down here it's asking us which hard
drive we want to use for the installation you can see i have a number of hard
drives on this particular server i'm actually going to use my sata dom for proxmox backup server
and i have a bunch of other hard drives here that i could use for my backups but we'll get into that
we click on options we could choose how we want that to be formatted i'm going to leave it on ext4
that should be good enough for our use case today i'll click next and then on this screen right here we
set our country and our time zone which i'll set mine right now i should be able to find detroit in the list and here it is
so on your end you just choose whatever your location happens to be and your keyboard layout in your country and
things like that just make sure everything here is correct so i'll click next
so here on this screen it's going to be asking for some more information for the installation administration password and
email address specifically so i'll scroll down here so here what i'll do is type in what i
want the root password to be
then down here what we should do is type in our email address i'm just going to change the n2.com on a
real production installation you should put your actual email address here especially if you're going to be paying
for support later but since this is just a demo installation that's why i'm just going to use this invalid email just to get us
through the process so click next and it's already filled in some
information here for my network and actually this is correct we have a fully qualified domain name of
pbs.homehyphen.network.io which is actually correct it must have pulled that information from my router which is
pretty cool and it's also selected the proper management interface as well
and the ip information is also correct so on your end what you'll do is type your desired host name your ip address
your gateway and your dns server whatever that happens to be for your network and once you're done you click
next on this screen right here it's giving us a summary of everything we've selected
so far so just make sure that everything looks correct and if it does
we'll click the install button and that'll get the installation started so i'm going to wait for this to
complete and i'll be right back
all right so it's booting up so far so good and here we have a login screen
and what's really handy here is it gives us the ip address and the port number so i know what exactly to type in my
address bar so i'm going to type this right here into another tab
and the port number is 8007 let's see what happens and it doesn't have a proper tls
certificate so this error message is actually expected so what i'm going to do is just accept
the risk even though there isn't a risk here and now we have a login screen so the username is going to be root
and then the password is going to be whatever password you typed in during the installation process
and here we are we are now logged into the proxmox backup server and it's ready to go
in the next section i'll show you guys around the user interface and then once that's done we'll go ahead and get some
backup started [Music]
Section 3 - User interface Overview
all right so in this section what we're going to do is take a look at the user interface for the proxmox backup server
but the first thing we're going to need to do is log in and if you aren't already logged in you just type in root as a username unless
you've already created other users and then for the password you type whatever the password is that you typed in during the installation process
and that should do it for me i'll press enter and here we are
now this message right here is expected it's letting me know that i don't have a valid subscription for the server and
that's fine i highly recommend that you support the proxmox project because they're doing some awesome things
and even though we could download this for free it's a really good idea to pay for support if you can because that
helps projects like proxmox thrive but for right now i'm just going to click ok to bypass that message and then let's go
ahead and get started and take a look at the user interface now right after we log in we are presented with a dashboard that you see
right here that gives us all kinds of useful metrics about the overall health of our server so here we see things such
as cpu usage memory usage how much hard drive space we have and things like that
we also see i o delay which is very important to keep your eye on as this particular meter starts to get full that
means there's some sort of resource contention with io something you definitely don't want just keep your eye
on that and you should be fine you also have swap usage right here in my case it's using zero percent which i
think is great we like to see that using zero percent if we can it's perfectly fine if some swap is
being used but if swap is being completely used then there's some sort of problem we also see some information about the
server that we're running proxmox backup server on so as you can see we have a xeon cpu
here we actually have two of them we're currently running linux kernel 5.11
and it's giving us some information about the repository so we have a green check box right here for the production
ready enterprise repository but we need a valid subscription in order to use the repository but it is what it is
if you subscribe then you get some additional features enterprise ready packages and also support from the team
themselves so again it's a good idea now what we're going to do is just go down this list right here
so the next one is going to be configuration and here on this screen we have a few
very useful tweaks that we can make during the installation process for example we set the time zone but if for
some reason that wasn't correct you can go ahead and correct it here and while you're here also take a look at the time
we want to make sure that the time is correct so just compare this with your local time and if it matches you're good to go
during the installation process we also set the dns server as well and this is the dns server that i chose
during installation but if for some reason you need to change that you can click the edit button you can make your changes so
that's how you change your dns server if you ever need to do that in the future in addition i have several network
interfaces on this server right now i'm using this one right here we have an ip address for this
particular interface we have a gateway now if you are actually using proxmox virtual environment with different
networks then you'll probably want to make sure that you set up those networks right here so for example you just click on an
interface that's not being used you can click edit and then fill in the information now this is beyond the scope of today's
video though just know that if you do need to set up additional networks here in proxmox backup server
especially if you do have other networks set up maybe something like a segregated network inside of proxmox virtual
environment then you can fill in the information here and make sure that it has a matching network configuration
now one more down on the list we have access control and here we can actually set up multiple
users when we install proxmox backup server we get a user named root which is
very common when it comes to a linux distribution but it's a good idea to create additional users especially if
you have multiple people that are going to be helping you out with backups so i'm here on the user management tab
right now we also have an api tab a permissions tab and a realms tab so if i wanted to add a
user i can click add right here so for example i could type in my name and then i'll type in a password
i'll confirm it we can set it to expire if we need to do that
we could create it as enabled or not so you can put in your name and last name here which i'll put in right now
so you basically fill in your user information if you want to create a user so i'll click add
and interesting enough it doesn't like the fact that my name only has three characters so what i'll do is just type my first
initial and then my last name and that should satisfy that requirement i'll click add
and now i have a user account right here for myself now by default i'm not actually able to
do anything as you can see i have no permissions at all i'll be able to log in but i won't
be able to do anything and it's very important that you only give users permission to do the things that you actually want them to be able
to do that's called the principle of least privilege so what you can do is you can go over
here to the permissions tab i'll click add and i'll add a user
permission and then right here we can choose a path so the permissions that i'm about to add
what path do those permissions pertain to if i choose slash that's going to give
the user access to everything now i am the owner of this server so in my case that's okay
so what i'm going to do is just add my user account right here and the scope is going to be slash for everything
but pay attention to this though the role is no access so if i was to add this right now
then i have no access to everything because slash means everything
and what i want instead is to be the admin of everything now if you have another user and maybe
they have a very specific job to do let's say for example you want them to be able to audit your backups to make
sure that they've completed that you could give them access to the appropriate scope here under path
so we have all kinds of different things here so i'll leave it up to you to configure permissions accordingly but
again since i'm the owner of this server it's okay for me to have everything and i'll go ahead and click add
now you can also set up two-factor authentication as well and that's probably something that you should set
up it's always a good idea to do this if you can so for example i can click totp
and then for the user i could drop that down choose my user account
and then what i could do is go ahead and scan this barcode right here with my google authenticator or whatever
authenticator app i might have and then i type in the resulting code down here and then i click add
again not required but having two factor authentication is a good idea especially considering that a backup
server houses very important information so you definitely want to control who was able to access it
now it's beyond the scope of this video but we also have the ability to create an api token as well and this is useful
if you want to automate backups maybe you have a backup script or anything that needs to interact with a server
like some sort of automated process you could create an api token right here so you click add and then you fill in
the information now i'm not going to do this because it's beyond the scope of this video but just keep in mind that it is possible to
set up access via api if that's something that you need
going further down the list we have a section for remotes and this might be confusing to some of
you out there that are just starting out with proxmox backup server a remote is not a backup destination we'll get to
that later but what a remote is is actually another proxmox backup server
so for example suppose you have this backup server right here but you have another backup server and you want them
to be able to sync so you back up to this server and then you want everything from here to sync to
another proxmox backup server that's a good idea now this isn't something i'll be showing
you today because i only have this one server anyway so just keep in mind that setting up another proxmox backup server
here under remotes is a possibility underneath certificates what you could
do here is actually solve that message that came up asking if you are sure you want to connect to the server because it
didn't have a valid tls certificate if you do have a certificate such as a wildcard cert or maybe you purchased a
specific cert for your backup server then you can add that information right here you can also use acme for let's
encrypt which is a good idea as well let's encrypt as a very good default if you have no other way to get a
certificate and let's encrypt certificates are perfectly valid there's nothing wrong with them so if you have
the ability to do this you may as well now on my end my proxmox backup server is not routable to the public internet
so there's no way for let's encrypt to verify ownership of a domain because there isn't one
but if you do have a domain you can add it you can add a certificate and that way you actually have a tls certificate
for your proxmox backup server and like i mentioned my server isn't publicly available at all and i never
recommend that you make it publicly available unless you absolutely need to so whether or not you need a certificate
here actually depends on your use case if you're just using this on your local network there's no problem but if
there's any exposure to the public internet then you'll definitely want to add a certificate here to make the connection secure
here underneath subscription if you were to buy a subscription for proxmox backup server you could upload your
subscription key right here to verify ownership of that license and that'll give you access to those premium
features for example the enterprise repository for now i'm not going to do that though
just know that if you do actually have a license for proxmox backup server you could add that information right here to
get it associated with your account moving on we have the administration section next
and right here we have even more metrics about our server's health and i like this because we have graphs
which are always fun so we can see the cpu usage the load average memory usage swap usage
some of the same information that we have on the dashboard but we have everything here in graphs which is pretty cool but we also have network
traffic so if things are slowing down or there's i o contention you can kind of see what kind of network traffic you're
dealing with we have a section for root disk usage
transfer input output i o delay and so on so definitely check this out and keep an
eye on this because this way you can actually make sure that there's no resource contention
and if anything is running slow of course you can check this section and you'll probably get your answer right here
on this tab we have a list of services so this is showing us which services are currently running
so you can start stop and restart services right here but another thing that's pretty cool is you could click on a service so i'll
click on sshd for example and then you can click on syslog
and it's going to show syslog entries for that particular service and that's really helpful because that way you see
log entries for that particular service it makes it really easy to narrow down the log entries for that service because
that's all it's going to show you anyway so if you're troubleshooting any one of these services you can check out the log entries for that service get some
information about it and that should help you troubleshoot if you ever need to do that
Installing updates
and here we have a tab for updates so we can click the refresh button right here to check for updates i'll do that
right now and it's going to warn us that we don't have a valid subscription which is fine
we'll just click ok and now it's going to go ahead and check for updates
and it is giving us an error right here that we can safely ignore but the process is complete
we'll let it load and as you can see we have a ton of updates here
and that makes sense because well i just installed it so of course there's updates because i haven't installed any
updates before so what i'm going to do is click upgrade we're going to definitely want to make
sure we have all of these installed and then this update window appears we can simply press enter to start the process
and we won't want to close this window at all we're going to leave it open and let this finish
and every now and then when you update you might see a screen like this that's asking you for some sort of information
in my case it's just confirming my keyboard layout which is fine i'll press enter and now the updates are installing
so i'll let it finish and then i'll be right back
all right so at this point all the updates have been installed so i'm going to close this window
and to confirm that all the updates have been installed i'll just refresh it one more time and when this is finished the window
should be empty and it is because well we just installed
all the updates there's no more updates available so we should be good to go now going down further we have shell
right here this is actually going to give us a terminal window that's open to the server logged in as root and since
proxmox backup server is based on debian we have access to all the usual linux commands that we would have access to on
such a distribution so if you need to use the command line for any reason at all you could do that right here
you could also enable ssh and things like that if you wish but you have a terminal right here in your browser so
that's very helpful if that's something that you need going down further we have storage slash disks right here and it's
going to scan the server for any additional hard disk that i might have installed inside the chassis
so as you can see i have quite a few here so the whole point of this section is to actually be able to initialize
your disk so that way proxmox backup server can use them so what you could do is just click on a
disk that you want to wipe out and set up for proxmox backup server and then you can click on initialize disk with
gpt just keep in mind of course that if the information hasn't already been wiped from the drive this will definitely do
so but actually what i'm going to do instead is click on directory what i want to do is create a mount with
one of these disks so that way there's a target for the backups so what i'm going to do is click create directory and
right here it's giving me a list of all the hard disks that are unused so i'll click on the first one slash dev
sda for the file system i'm going to keep it simple i'll use ext4
and for the name i'll just call it backup one we're going to make sure to add it as a
data store we want somewhere to send our backups to it's not a good idea to use the root file system for backups you should have
a different storage media for that and that's what we have now or at least that's what we will have as soon as i click create
and now it's going to go ahead and set that up for us
and now it's done and it gives us the path for the data store right here which is pretty cool
so now we actually have a place where we can send backups now going further there's also a tape
backup section as well but i don't actually have any hardware for backing up to tape
so i'm not going to be able to show you guys how this works however if you have tape backup hardware
you could go ahead and add that here so if that's something that you want to use you definitely can
and then right here we have a section for our data stores and it's giving me an overview right now
i'm using approximately zero percent of my storage that makes sense we haven't even set up any backup jobs yet and here
we have backup one that's the data store that we've just created with one of the disks that were available
we don't have any backups on there right now but we will shortly and of course you can go here to content
to see all the backups that you might have on that data store on the prune section you can set up some
pruning scheduling here so for example we have a garbage collection schedule we have a prune schedule
so what i'm going to do is keep the last certain number of backups let's just keep the last five this will help us
make sure that our disk doesn't get overwhelmed because we certainly don't want the disk to get full
so for example we can set the prune options to keep the last certain number of backups a certain number of monthly
backups you can set this up however you wish i think this is probably good enough for me for right now
you can also set up sync jobs that's beyond the scope of this video but that's definitely something that you can do
with a sync job you could back up this proxmox backup server to another proxmox backup server
i mentioned earlier that you can add additional backup servers to remotes so once you do that you can send your data
over to that remote by creating a sync job there's also the ability to verify jobs
as well which is always useful we also have some options here for who is going to be notified when backups are
completed if that's something that interests you we also have a permission section as well my user is given access
to admin which is everything so i should be good to go there but that's the interface in a nutshell
that was very high level but i just wanted to give you guys a rundown of what each of these options are
and in the next section what i'm going to do is show you how to backup proxmox virtual environment vms to proxmox
backup server it's going to be a lot of fun so i'll see you there
[Music]
Section 4 - Proxmox VE VM and Container Backups
all right so it's time to get some backups created what i'm going to do in this particular section
is show you how to add the proxmox backup server to proxmox virtual environment
and then what we'll do is send some backups from virtual environment over to the backup server
now if you don't actually have proxmox virtual environment installed that's okay in the section after this one i'm going
to show you how to create file level backups of non-virtual machines or actually file level backups that don't
depend on whether or not it is a virtual machine we'll cover that in the next section but specifically in this section
i'm going to link proxmox virtual environment to proxmox backup server and create some backups
so let's get started so on my other tab right here i actually pulled up my proxmox virtual environment
cluster as you can see i have two proxmox servers here and various vms running on
each of those servers i even have a container right here as well so what i'm going to do is show you how
to backup containers in addition that's one of the things that we'll be working on but before we do anything else we need
to add the proxmox backup server as a remote here on virtual environment and
to do that we'll click on data center next we'll click on storage
we're going to add another storage repository here and notice that proxmox backup server is
an option here at the end so that's exactly what i'm going to choose
so for the id i'm going to call it pbs short for proxmox backup server of course
and the server what i'm going to do is actually just copy the ip address
if you have a fully qualified domain name you could type that in right here but i'm just going to paste in the ip address
the username is going to be root at pam or whatever other user account you might
want to add for this purpose i'll type in the password
which i've done then here on the proxmox backup server
we have a button here on the dashboard section that shows show fingerprint i'll click on that
and we're going to copy the fingerprint then here in proxmox we're going to
paste that fingerprint in this box right here and then we're going to choose a
datastore so here we've named the datastore backup1
so that's what i'm going to call it here as well
and then i'll click add
now as you can see we now have pbs added to this server and if i scroll down we have it added to
this server as well since we configured the proxmox backup server in the data center it went ahead
and made sure that each of my servers in my cluster have access to that particular backup store
which is great because if you have a cluster then you only need to add it one time and you're good to go
so to illustrate the process what i'm going to do is create a brand new virtual machine
and right here i have a template so i'm going to clone that template
i'll give it a high number just to make sure that it stands out maybe something like 8.75 that isn't being used already
and for the name i'm going to call it backup hyphen test i'm going to make it a full clone
i'm going to start it on proxmox 2. i'll click clone
and then it should show up right here and here it is it shows locked right now because it's being cloned i'll wait for it to finish
and then i'll be right back so now we have a vm right here that i'm
going to use as a guinea pig so we'll use this server right here for our first backup job
now even though i've just created this let's assume that this is a very important virtual machine that's running something that is urgent to our business
we want to make sure that we back it up so how do we actually go about doing that now that we've added the proxmox
backup server to proxmox virtual environment let's take a look so what i'm going to do right now is
click on backup i'm still on the virtual machine i clicked on backup
i want to click backup now and now it's asking me where do i want
to store the backup well i certainly don't want to store it on the local storage because if we store our backups
on the local storage that's not really a backup is it so we don't want that so what i'm going to do is drop this
down and i'm going to choose pbs our proxmox backup server
and we have several different modes here that we could choose i'm going to choose stop that's going to give us the greatest consistency that we could
possibly get in the proxmox virtual environment series i actually went over each of these options and what they mean so i'm
not going to worry about going over that again in this video but for right now i'll click stop it's stopped anyway so
it doesn't really matter now if we wanted to we can send an email to someone right here by typing in their
email address if that's something that we want to happen but i don't need that right now i'll
just click on backup and we'll let this finish
and as we can see the task is okay the backup is finished
but where's the backup i just created a backup but it's not actually visible here
well that's just because by default storage is set to local so if we drop this down and choose pbs
then it's going to show us backups for the server on that backup storage and here it is here's our backup that's
pretty cool we could do a restore we could do a file restore we could remove the backup if we no
longer need it and to confirm if i go here to the proxmox backup server
and then i go to the data store that we've just created this is where we're actually sending backups to
and then i click on content you can see that we have vm 875.
now it's important to understand this naming convention right here this is actually known as a backup group
a backup group consists of a type and then the id number so the type of backup here is vm
and then the id number of the virtual machine that was backed up with this job right here is number 875.
so if i go over here this is the server that we set up for this purpose
the vmid is 875. so what type of resource is it it's a vm
what's the id number it's 875. that's how proxmox backup server actually keeps track of backups
this way everything is sorted by the type and the id it makes it really easy to match a backup to the server that it
came from now going even further what i'm going to do right now
is back up this container to the proxmox backup server so i'll click backup
up now pretty much the same thing as before for the storage i want to send it over to the proxmox backup server
snapshot mode is fine i'll click backup and this should happen pretty quickly
because containers are a lot smaller than virtual machines so they should be done in no time at all
and as you can see the backup job is done so i'll click reload
and now we can see the container is located here the naming convention is going to be similar
again this is the backup group and it consists of a type and id and ct of course is short for container
and the container id is one zero one so now we have two different backups here
now going even further if we want to automate this and you probably should
we can go to data center and then back and i already have a backup job right
here that backs up to my trunas server so i could change this to point it to the proxmox backup server or i could
just add another job so for example maybe i want that one to run on sunday
so i'll just take off saturday add sunday for the storage i want to send it over
to the proxmox backup server i want it to email me we could choose the mode
and we could choose the vms that we want backed up via this method or we could just select all so that way we can make
sure that any container or vm on this cluster is backed up or is a part of the backup job and then from this point
forward it's going to back up automatically at the time we choose to the storage where we want to send it
proxmox backup server of course we have the time we have the mode and that's great now i'm not going to
create this backup job on my end because i'm going to reinstall the proxmox backup server after i'm done with this tutorial but if you wanted to create a
backup job then this is how you would do that now one of the things that's really cool about proxmox backup server is that we
could do a file level restore as well even though we did a container backup and a virtual machine backup
we actually have access to the file system of the container
so let's take a look at our backups real quick just to see what else we can do here so here we have the container i'm going
to click on file restore because that's a very cool feature of the proxmox backup server
and check this out we have the entire root file system right here and we can individually restore files which is
great of course we could restore the entire container if we wanted to but if all you wanted to do was actually
restore a specific file you could do that right here from this menu and we'll be going over that in more
detail later in the video but i wanted to show you that as possible
if i wanted to restore the container outright i could just click restore i'm not going to do that though that's a
production container but i will restore this one right here so i'll click on restore this is the virtual machine that we created just for this purpose
so we can choose the storage if it's going to be something different and in this case i want it to be
something different because i don't want to run it from the backup server i want the vm to run from local lvm
so right here i just go ahead and choose a vm id for this particular instance i'll set that to 876 to make it
different and you can choose to start the vm after you restore if you wanted to but i'll
just click restore and it's in process of restoring right
now we can see that the vm is being created and the process is moving along
so i'm going to let this run and i'll be back as soon as it's finished
so the process is done and now i have a clone of the original
server right here as vmid 876 that was restored from the backup so if you want
to restore a virtual machine you can absolutely do that but you just saw examples of how to
backup virtual machines it's literally that easy containers as well so in the next section what i'm going to
do is show you how to create a file level backup and it doesn't matter if the server is a virtual machine in this
case you could back up any debian or ubuntu or debian and ubutu-based distributions
via the backup client that you could download from proxmox and we're going to take a look at that right in the next
section so i'll meet you over there and we'll continue [Music]
Section 5 - Installing and using the backup client
all right so in this section i'm going to walk you through the process of installing the proxmox backup client
and then i'll show you how to create and restore backups and this is going to be a file level backup and it doesn't
matter if you are running proxmox virtual environment the backup client for proxmox backup server supports
debian and ubuntu virtual machines and physical servers so you can simply just install the client and you'll be good to
go now even if you're not running debian or ubuntu you could use the api to backup
anyway we're not going to get into that in this video but i'm going to assume for now if you're following along with
me that you are running on either debian or ubuntu so in the last section i created this
backup test server and then i cloned it by restoring a backup so what i'm going to do is just go ahead and start it
i'm going to create a file level backup from this server right here
and it's already started so i'll log in
and we have an ip address of 10.10.10.203
so let's open up a terminal and using ssh i'll connect to that server
again this is the virtual machine that is running in proxmox virtual environment but again it doesn't matter what the source vm is running on
as long as this debian or ubuntu or based on those distributions it should be fine
and now i'm in now right now i have a hostname of ubuntu on configured that's just a
naming scheme that i use with the template so whenever i look at my firewall and i see ubuntu on configured then that helps
me narrow down what the new vm is when it goes to get an ip address and then i change the hostname later to whatever i
want it to be i'm not going to worry about that so much right now let's go ahead and get the backup client installed and we'll set up a backup
now the first thing that we're going to need to do is add the repository for the backup client
and to do that we'll need to use a text editor with sudo privileges i use nano bim is actually my favorite
nano is easier to explain in videos so that's what i'll go with on your end you could use whatever text editor you want
it really doesn't matter and the file that we want to create is going to be slash etsy slash apt
sources.list.d [Music] and we're going to call it pbshyphenclient.list
just like that and now we have an empty file up on the
screen now for debian and ubuntu what we're going to do is add a special line right
here to add the repository we'll start it off by typing deb
and then we'll type arch equals amd64 and adding this will help silence any
warnings that we might see if it's going to complain about the lack of 32-bit packages
ubuntu for example is 64-bit only now so this may or may not be required on your end but i'm going to add it just in
case the url is going to be http colon slash then we'll type download.proxmox.com
debian slash pbs hyphen client bullseye
and then finally main now if you are running on an older version of debian
then what you could do is change bullseye to buster bullseye is actually the proper selection for me so i'm going to leave
it on that but if you are running on an older debian system then you'll have to change the keyword here accordingly
anyway i'll hold ctrl and press o to bring up the save dialog enter to save it
and then ctrl x to exit out next what we're going to do is add the key for the repository
this is going to be a longer command so bear with me we're going to use wget
and then we'll type in a url for what we want to pull down
and as long as i didn't type anything in correctly this should add the repository key for the repository that we're adding
so i'll press enter and it looks good to me
so next what we'll do is run sudo apt update
and then next we can install the proxmox backup client by running sudo apt install and the name of the package is
going to be proxmox hyphen backup hyphen client just like
that so i'll press enter enter again it's going to install some dependencies which is fine
so at this point we actually have the proxmox backup client here on this particular server
so the idea is that you can add this proxmox backup client to any server that you want to be able to do any kind of
file level backup to your proxmox backup server and of course i'll show you how that works
but we have the proxmox backup client installed now so we should be good to continue so let's go ahead and create a backup
Using the client to send a backup to the server
and as a fun test what i'm going to do is just type echo
echo hello world and we'll put that in a file just so we have you know something to
reference here and what i want to do now is back up the entire server's file system over to the
proxmox backup server how do you do that well i'm about to show you so what i'm going to do is switch to
root that's not always required but i'm going to be doing a backup of the entire file
system so i want to make sure that i actually have access to everything so now we'll run proxmox hyphen backup
hyphen client and i want to do a backup i'll type root.pxar
colon and then what do i want to back up i want to back up everything the root file system or forward slash
and then next what we need to do is give it a repository where do we want to send the backup
so i'll type dash dash and then the word and we're going to set that equal to
172.16.249.218.
colon and then the name of the data store that we want to send it to which i called backup one
and that should be it so i'll press enter and now it wants us to type the password for the proxmox backup server
which i've done are you sure you want to connect i'll say yes yes again
and it looks like i typed the password in wrong so let's try that again
and there we go it's actually backing up that's pretty cool so what i'm going to do is just wait for this to finish and then i'll be right
back and you know what it looks like the backup is complete
it gives us a summary of how long it took how big was the backup the compressed size of that backup
so that's really cool let's go back to our server
so go back to the proxmox backup server let's reload and we see another backup right here and
the backup group is quite different isn't it the type for the backup group is host because we actually created a file level
backup from a server and then we have the name of the backup so it's in a bit of a different format
when you compare it to the other backup group names but it's pretty straightforward we know what type of backup it is
and we know the name of the server here that was backed up we have the size of the backup
and that's awesome we can see the individual components of
the backup right here we also have a file folder icon right here where we can browse the contents of that so i'll
click on it and here we can see the root file system of that server that we just backed up so
if i click on home and then my username we can see the hello.txt file that i've
created on the file system as an example it's right here so what i could do is actually download
it and what i'll do is open it
i'll open it in a text editor and would you look at that it opened up
the file it has the contents right here that i typed during the ssh connection earlier
so i am able to restore this file right here that's pretty cool now let's take a look at some additional examples of using the backup client
Creating an encrypted backup
and let's take a look at creating an encrypted backup there's various options for creating encrypted backups in the
proxmox backup server i'm going to show you one method right now what we need to do is actually create a backup key
so to do that i'll type proxmox hyphen backup hyphen client just like before
and i want to work with keys i want to create a key
and i'm going to name it my hyphen backup dot key just like
now that wants me to type an encryption password which i'll do right now and again
and now we have a backup key we can see it right there in the file system when i list the storage we've
created a backup key and we can use that to encrypt the backup so let's create an encrypted backup so
i'll type proxmox hyphen backup hyphen client yet again i want to create a backup
and what i want to do is back up the root of the file system
and then we'll add a repository again this just tells the proxmox backup client where to send the backup to
and i'll type in the ip address of 172.16
and the data store we called that backup one now we're going to give it a key file
and that's the key file that we've just created so i'll press enter type in the password for the root user
on that server now it wants the encryption password
which i'll type in right now and now it's running
and the backup's done we were able to create an encrypted backup which is really cool
and keep in mind there's other options for how to create encrypted backups i can't go over every single method in
this video but check out the documentation if you want to take this concept even further and change how
exactly you go about the encryption but i just showed you one of the methods right here it works just fine we have an
encrypted backup and that's awesome now another thing that i want to show you guys is actually how to simplify the
Setting up an environment variable to shorten backup commands
command because adding the repository can sometimes be annoying to add that every single time so what we can do is
create an environment variable that's actually going to help us out quite a bit so what i'll do is type the word export
and then we'll type the name of the variable that we want to create we need to give it a specific name and that name is going to be pbs in all
caps underscore repository also in all caps
we're going to set that equal to something and what we want to set that equal to is the ip address of our
proxmox backup server
then we'll type a colon and then the name of the data store which again was backup one
now keep in mind that as soon as i close this terminal window i'm going to lose this variable right here and i'll need
to create it again but you could add it to your dot bashrc file and that way
it's always going to be there every time you open up a terminal that might be something that you'll have to do if you
don't want to add this variable manually every single time and i do recommend you do that it just makes everything a lot easier but we do
have the variable so if i run echo and then dollar sign because we create variables in bash
without the dollar sign but we use the dollar sign when we refer to variables
and we called it pbs underscore repository and as you can see this is what that
variable equals which is correct so we should be good to go so next let's take a look at how to list
Listing Proxmox backup groups
the backup groups that we have on the server
so we'll type proxmox backup client and then list and if we didn't have the environment
variable we would have had to type the repository right here just like we did before
i'm not going to complete the command you get the idea but we don't need to do that because we set up the environment variable so we're
able to simplify our commands by not adding the repository every time we still need to enter the password
though and there we go
we have a list of the groups right here and also the most recent snapshot for each
that's pretty cool and it's going off to the side because of the font size of my terminal but you get the idea this is
how you list the backup groups that you have on the server so that way you can see what types of backups are included
there so another thing we could do is list the individual backups for a group
so like always we start off the command with proxmox backup client and instead of list we're going to do snapshot list
and then we're going to type the group that we want to list the backups from so for example i'll type vm
875. let's see what happens
and now i have a list of backups for that particular virtual machine i only have one backup for that virtual machine
but we can of course change the group anytime we want to inspect a different resource
so i could certainly do that here for the container as well
so now we see the snapshots listed here for that particular container so now what i'm going to do is show you
Mounting a backup to the local filesystem
guys how to mount a backup with the command line this is going to be really cool
but first what do we actually mount and how do we know what to type to start it off what we'll do as normal
is type in proxmox hyphen backup hyphen client and then we'll do a list
we want to see what type of backup groups we have here on the server as a reminder so i'll type in my magic password
and we have these three so now that we have our list here we can set up the command to mount a backup to
the local file system but first we actually need to have a directory for where to mount it to so
i'll create a directory right now and i'll create it inside slash mnt
i'll call the folder mybackup i think that's good enough so again we could type proxmox hyphen
backup hyphen client and what we want to do this time is mount a backup
now here says last snapshot so we could simply just use that if you want to use something else you
can always do a snapshot list but i'll copy this string right here and then i'll paste it
and the root file system snapshot is saved as root.pxar and then next we type where we want to
mount this to which is of course the directory that i've just created which was at slash mnt slash my backup
and that should do it as long as i don't have any typos that should mount that back up right here to the local file system in that directory let's see what
happens i'll press enter i'll type in my password yet again
and it looks like we have an error so i think that's because i encrypted the backup of course i need to include the
key otherwise i can't unencrypt it my mistake so what i'll do is just add another
option to the end of this command dash dash key file and then i save the key in slash root
slash my hyphen backup dot key let's give this another shot
so now i'll type in the password for the encryption and it looks like it actually worked
let's see so check this out we actually see the
contents of the backup that we've saved right here and i can access it as if it was here on
the local file system because it is mounted here to the local file system so for example if i wanted to restore an
individual file i just navigate through the directory where it might be saved i pull it down and then put it in the
location where it needs to go that's pretty cool so mission accomplished of course there's other variations of
the backup commands that you can get from the documentation and i might do a follow-up video to go
deeper into proxmox backup server in the future but for right now i think these commands are enough to get you started
hopefully this content was helpful in getting you started with proxmox backup server i think it's an awesome piece of
software and as usual i had a lot of fun creating this content for you guys and
if you found it helpful please click that like button that lets youtube know that you want to see more
tutorials just like this one and also subscribe if you haven't already done so i have some awesome content coming if i
do say so myself so definitely stay tuned for that and thanks so much for watching
[Music]
you
