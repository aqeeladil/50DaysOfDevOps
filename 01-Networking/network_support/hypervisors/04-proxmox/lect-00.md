Intro
[MUSIC]
Hello again everyone and welcome back to Learn Linux TV.
In today's video, what I'm going to do is give you
an updated getting started guide on Proxmox,
and that's what I have right here, a Proxmox server.
You're probably wondering what the server was on my desk,
but given the title of this video,
you probably figured it out before I mentioned it.
Anyway, I have permission to
show you this build right here.
It was made for a client, and he was nice enough
to give me the go-ahead to show you guys this build,
which is exactly what I'm going to do.
But this entire video isn't dedicated just to this build.
Yes, I will give you a parts list,
and I'll give you my thoughts on my hardware selection,
in this case right here.
But it's more than just that,
because I'm going to tell you everything
that you need to know to get started with Proxmox,
even if you already have a server
that you plan on installing it on.
Also, I'd be remiss if I didn't at least mention the fact
that I have an entire Proxmox course here on this channel
that's available for free,
just like all the other videos on my YouTube page.
You can check out that entire series
and learn everything you need to know
when it comes to maintaining a Proxmox implementation.
This video is more of a getting started guide,
which is hit more towards beginners.
But if you like Proxmox,
especially after you check it out in this video,
and you want to learn even more about it,
then you should definitely check out that series.
That tutorial series went over an older version of Proxmox,
but Proxmox doesn't change a lot
for one version to another.
So you can still use that course here today in 2023
to get started with Proxmox or master Proxmox,
which is exactly what that series will help you do.
Now with all of that out of the way,
let's dive into Proxmox.
If you look below in the description,
you'll find time codes there.
So you can get started with Proxmox with the time code
that best matches where you are in the process.
If you want to build a server,
then you'll find a time code for that.
If you already have a server,
then you'll find a time code
that shows you how to install Proxmox.
Definitely check out the time code list down below
to get an idea of what I cover in today's video.
And with all of that said, let's dive into Proxmox.
My recent AsRock Rack Proxmox Build
All right, so let's get started.
And I figured a good place to start
is to talk about this build right here.
If you don't already have a server
that you can install Proxmox onto,
then well, if you have the budget,
this build right here is a good way to go.
Now, the cheapest way to go though,
is to use any hardware that you might have lying around.
And that's especially good
if you want to recycle those computers
rather than have them end up in a landfill.
Let's put them to use.
If you have something in your closet,
and this might not be the first thing
that everyone thinks of,
but if you have something in your closet
that is just collecting dust,
and it might be powerful enough to run Proxmox,
then that might be a great way to get started as well.
Again, that way, you know, things stay out of the landfill
and we make better use of our technology.
Anyway, let's check out this build right here
and I'll show you what I came up with.
In this section, we're going to check out the specifics
of the server that I've built.
The one that you just saw on my desk.
This was actually created for a client.
However, I have permission to show you
the build in this video.
For the motherboard, this build features ASRock Rack
and this was my first time
checking out their server line of products.
In case you're curious,
the model number is being shown on the screen right now.
The Server Management Utility Is Quite Useful!
One thing I really like about this motherboard
is the server management utility,
which is built in with nothing
for you to install whatsoever.
The best part is that you can use
the server management utility
to access an integrated KVM
and that will let you see an emulated display
that you can interact with,
just as if you had a monitor, keyboard, and mouse
attached to the actual server itself.
But this is the virtual version of that
and you'll see me use this later on in the video
when I install Proxmox.
Part Selections For This Proxmox VE Build
Other parts inside this build include
an AMD Ryzen 9 5950X CPU,
four sticks of 32 gigabyte ECC memory,
and two Samsung 970 EVO NVMe SSDs
for the OS and initial virtual machine storage.
In addition to those parts,
this build also includes a hard disk dock
that can hold up to six 2.5 inch hard disks.
With this build in particular,
there's six one terabyte SSDs
that are installed into this dock right now,
so it's not going to run out of space anytime soon.
Excluding the dock and SSDs,
the build comes to around 1800 US dollars.
The dock and SSDs add about $750 to the overall cost.
But keep in mind that these are all estimates
and part prices seem to go up and down nowadays,
so just look at the current prices
if you want to build something similar.
After putting together the build
My Overall Thoughts On This Build (And Some Issues I Ran Into)
and having a chance to check it out,
it really does seem like a very good stable build.
However, there were a few pain points that we ran into.
First off, no matter what I tried,
the HDMI port simply does not work on this motherboard.
I tried all the BIOS settings that I could find,
even as far as disabling dedicated GPU support,
even though I didn't even install a GPU at all.
And even with that, nothing I tried
would make the HDMI port function at all.
After doing some Googling, I saw some posts
from other people that are having this same problem.
Ultimately, the lack of an HDMI port
didn't really matter so much when it comes to this project.
Since you can't access the server
via the integrated server management utility,
then that means the HDMI port
probably wouldn't have been used anyway.
Still, if you have an HDMI port on a motherboard,
you would probably expect that to be more
than just a decoration, but it is what it is.
The second issue that we ran into was with the case,
specifically fitting a power supply into the case.
The chassis that we went with was from iStar USA,
and it's a fairly decent, if you know,
overly simplistic case, but the problem that we ran into
was sourcing a power supply that would fit inside the case.
Simply no power supply I could find would fit,
not a single one, and I tried various varieties
of power supplies, but I had no luck.
Thankfully, there are 3D
printer templates you could download
that'll enable you to print a bracket you could use
to make the power supply fit properly.
It's just really weird that the actual power supply
for server chassis made by this company
are sometimes really hard to source.
I went with an SFX power supply in this case,
and I used a alteration to ensure
that it is secured to the case,
but it's strange that this is something
I had to do in the first place.
All in all, though, other than the HDMI issue,
the ASRock Rack motherboard in this build is just awesome.
The CPU is quite fast too, and paired with NVMe storage
is just a really great server.
Anyway, enough about the build.
Let's talk about installing Proxmox itself,
which is what we'll take care of in the next section.
(scratching)
Installation walkthrough For Proxmox VE
So at this point, either you already have a server
that you've set aside for installing Proxmox onto,
or maybe you built one along with me
like I did in this video.
Either way, we need to install Proxmox,
otherwise, well, what's the point?
So let's check out the process
of setting up Proxmox on our server.
(scratching)
In order to get started,
the first thing we'll need to do is create bootable media.
I have videos on my channel already
that goes over the process of flashing USB media
with an ISO image to create bootable media,
so I won't go into too much detail about that here.
I'll leave a card for that video right about here
if you want to see a dedicated walkthrough
when it comes to using something like USB Imager.
But anyway, what you'll do is download the ISO image
for Proxmox VE from the official website,
and then you'll use a tool such as USB Imager
to create the media.
Once that's done, we'll boot the server
from our Proxmox installation media,
and you should see the start screen
that you see right here.
You can simply press Enter right here,
and then the installation media will boot the server
into the full Proxmox VE installer.
After that, we'll see the end user license agreement,
which you can accept by clicking I agree.
Aren't these license agreements just annoying?
Anyway, once you've accepted that,
the next screen will have us set up the hard disk
for Proxmox itself.
You should be able to see all of your disks
in the dropdown box right here,
and if you have only one disk,
then you can simply select that to keep it simple.
In my case, I wanted the two NVMe disks
to be used for the OS itself, specifically with ZFS.
So for this build, I chose ZFS RAID 1
for the disk arrangement.
After you make your selections,
you simply click Next to move on to the next screen.
Continuing, at this point,
we'll choose our location and time zone settings.
All you should have to do is change each selection
to match your desired preferences,
and once you've done that, you simply click Next.
After that, it's time to set up a password
for the root user, which you'll enter twice
on this screen right here.
You'll also enter your email address,
and you should use a real email address here
because, well, that's where notifications will be sent to.
So it is pretty important.
In my case, I just used a sample email address
since I was simply testing Proxmox
at the time I recorded this footage,
but in your case, I recommend
that you use a real email address.
The next screen is one that you'll want
to pay special attention to
because these network details need to be just right.
Otherwise, you won't be able to access the installation
once it's finished.
The first thing we'll do on this screen
is choose a host name for the server.
If you happen to have a
domain, you can append that as well,
but you have to add something here.
It doesn't matter so much what you name your server,
but I'd recommend coming up
with some sort of naming scheme.
For the IP address, you'll want to use an IP
that's not claimed by anything else in your network
and is also outside the DHCP range of your router.
So you'll fill in the IP address
and also the Gateway IP and DNS IP.
And once you've done all that, you should be good to go.
So click next.
Finally, a summary screen will appear
similar to the one that you see right here.
Just confirm that everything is set up properly
before continuing.
Also, keep in mind that this will erase everything
on the hard disk that you've chosen for Proxmox.
So definitely be aware of that before clicking install.
Once you do though,
it'll take some time for the process to finish.
And once it does, you'll see this final screen right here.
Now be sure to pay special attention to the URL
that you see right here, as well as the port number.
You'll need both of these
when it comes to accessing Proxmox later.
Anyway, we'll reboot the server and well, that's it.
After your server restarts, you should be good to go
to access Proxmox VE.
And then when it comes to logging in,
you'll use root for the username and the password
that you've entered in before during installation.
That's the password that you'll use right here.
Once you type that in, you'll be logged into the server.
Updating Proxmox Virtual Environment
Now, before we go any further,
it'll be a great idea to update Proxmox
and ensure that everything is up to the latest version.
To do that, we'll first click on the name of the node.
In my case, it's this one right here.
And after you click on your node,
you'll then click on updates.
On the update screen,
the next thing you'll do is click the refresh button.
Now keep in mind,
unless you've purchased a license for Proxmox,
you will see errors on the screen and that's okay.
The update process will still work.
You just won't have the updates
that are included in the enterprise repository.
However, we should be able to install
all the other updates just fine.
Once it's finished, you'll see a list of updates
on this screen, like you see right here.
However, there's one more recommendation
I would like to make.
Enabling the "No Subscription" Repository
If you don't personally have any plans
of buying a license for Proxmox,
then what I recommend is that you enable
the no subscription repository.
Now these updates won't be tested as much as the ones
in the enterprise repository,
but it's better to have this if nothing else.
To add this, what we'll do is click on repositories,
which is underneath updates.
Then we'll click add.
And when this box appears,
we'll simply click okay to get rid of that message.
And then we'll click add.
After that, we'll go back to updates.
We'll click the refresh button again
to make sure that the new repository is taken
into account when it comes to available updates.
And then once that's done,
we'll click upgrade the button right here.
This process will take some time,
depending on how many updates there are.
And when it's done, we'll reboot the server.
To do that, we'll make sure that our Proxmox node
is selected right here.
And then we'll simply click the reboot button.
After that, we'll wait some time
for the server to come back up.
And once it does, we should be good to go.
But now that we've installed Proxmox
and we've updated it, what should we do next?
Well, launching a virtual
machine would be a great next step.
So let's take care of that in the next section.
Launching a VM in Proxmox and Installing Debian
Congratulations.
At this point, we have our very own Proxmox server
that's set up and it's fully operational.
It's just waiting to do work for us,
but we haven't given it anything to do, have we?
In fact, we haven't even created a single VM yet.
So let's rectify that right now.
What I'm going to do at this time in the video
is show you the process of setting up
a Debian-based virtual machine on Proxmox.
So let's get started.
When it comes to spinning up a virtual machine,
the first thing that we'll need is to download an ISO image
for the operating system that we plan on installing
inside of the virtual machine.
Thankfully, Proxmox VE makes this very easy.
All we have to do is find the download link
for the ISO image that we want to download
and copy the link to that image.
Once you've copied it, you select your local storage
right here and then you click on ISO images.
And then we'll simply paste in the URL
into the top box right here.
After pasting in the URL, what we'll do is click Query URL.
That should automatically generate the file name
for the ISO image.
After that, we click Download,
and well, it's going to download the ISO image,
and after that, we'll be able to use it.
To create the actual virtual machine,
what we'll do is click the Create VM button
right here at the top.
Note that we can also create containers here,
but we won't be covering containers in this video.
If you want to learn how to create containers
within Proxmox, that's a good reason to check out
my Proxmox series that will go over that and a lot more.
Anyway, to create our VM, what we'll do is fill out
each of the required sections in the configuration panel
that appears.
Before we continue though, pay special attention
to the ID number that appears within this box right here.
We won't be configuring the ID number just yet,
but it's a good idea to know what it is,
at least in summary.
Basically, when you go to create a virtual machine,
the next unused ID number will be automatically placed
into this box.
You could use the ID number that's assigned as is,
or you could even set your own.
Regardless, every VM and container in Proxmox
needs a unique ID number, and if you try to reuse
an existing ID number, the process will refuse to continue.
Here, I kept the existing ID number
since I have no other VM anyway.
The next step is for us to select an ISO image,
which we've already downloaded.
So as long as the correct storage is selected,
all we should have to do is drop this down right here,
and we should see our Debian ISO image
listed in this section.
If you don't see it, just make sure that the dropdown above
is set to the same name of the storage volume
that you've added the ISO image to earlier.
And that should be all there is for this screen right here,
so we'll click next.
Our next step is to configure the primary virtual hard disk
for our VM.
In my case, since this build uses exclusively SSDs,
I made sure to check the discard box, this one right here,
and I left the size at 32 gigabytes for the volume,
but you could change that accordingly to suit your needs.
After that, we set the number of cores.
I set this to two in my case,
but you can add as many cores as you want,
but try to stay underneath the total number of cores
for the host if you can.
Anyway, continuing,
memory is the next thing that we'll configure.
I set it to two gigabytes in my case,
and one thing to note here is that some OS installers
are memory-hungry, so even if I don't plan on using
two gigabytes of RAM with the VM,
it's not uncommon to crank up the RAM and the cores
while installing an operating system
just to make the process faster,
and then you could always lower the number of cores
and amount of RAM afterwards if you'd like.
Some installers will literally crash
if you set this to be lower than two gigabytes,
but again, you could always adjust that
and lower the amount of RAM after some point in the future.
The next tab after memory gives us a chance
to set up our virtual network,
or more specifically, to choose the network
that the virtual machine will run on.
By default, you'll only have one.
Later on, it's a good idea to separate
the management network and the VM network,
but that's outside the scope of this video,
and that's also something you can learn
from my Proxmox course if you're interested.
For now, though, we'll leave this as is and click Next.
The final step is to review the settings overview
that's presented right here,
and if everything looks good, we can click Finish.
If we want the VM to start immediately,
we could check the box here.
That's labeled Start After Created.
If that's something that you want to happen,
check that box, but either way, we'll finish the process.
From that point forward, what we'll do
is install the operating system
just like we would on any other platform.
In the case of Debian, I kept everything at their defaults
for the most part, but if you want a dedicated video
that walks you through setting up Debian
and how to answer each of these prompts,
I'll leave a card for my video on that right here.
But for the most part, you could simply choose
the defaults for just about everything,
and you should be fine.
And, well, there's our video.
I hope you guys enjoyed this updated
Getting Started Guide for Proxmox.
I had a ton of fun producing this content,
and if you did enjoy it,
then please consider clicking the Like button
to let YouTube know how helpful this content was.
I'd really appreciate that.
Anyway, in the meantime, I have a ton of content coming,
so be sure to subscribe to Learn Linux TV
for the latest in Linux,
and I'll see you in the next video.
(upbeat music)
