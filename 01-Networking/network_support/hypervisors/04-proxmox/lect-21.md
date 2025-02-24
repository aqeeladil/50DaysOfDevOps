Consulting
are your Linux servers staging a
rebellion does every CIS log read like a
cryptic riddle and every config file
feel like it's written in ancient
penguin hieroglyphs I feel your pain
sometimes managing Linux servers can
feel like hurting penguins in a blizzard
and that's where I waddle in for the
past 20 years I've been the Linux
Whisperer teaching Millions how to tame
their Terminals and helping businesses
turn their Renegade servers into smooth
running machines and now I'm offering my
Consulting Services directly to you
whether your issue is a rogue process
wreaking havoc a server slower than a
turtle or the desire to automate tasks
so you finally take that vacation I've
got you covered whether you need help
with troubleshooting optimization
configuration automation or even
security hardening I'll help you solve
just about any Linux related conundrum
even the ones that make you feel like
you want to throw your laptop out the
window let's turn your Linux headaches
into high fives ready to team up if so
head on over to learnlinux.tv
and click on the Linux Consulting button
I look forward to working with
Intro
[Music]
[Music]
you hello and welcome back to learn
Linux TV in this video what I'm going to
do is provide you with more proxmox
content I love proxmox it's my
hypervisor of choice it's what I use and
and I also have all kinds of videos on
this channel that'll teach you
everything you need to know to learn how
to use it but in this video what I'm
going to do is combine proxmox with one
of my favorite provisioning tools
terraform if you haven't already heard
of terraform before it's an awesome
utility you can use to provision
resources on a variety of platforms you
could use it with various Cloud
providers and hypervisors and you could
fine-tune all kinds of things such as
RAM storage space networking you name it
it's a powerful tool and you're going to
see it in action today and by the end of
this video you'll be able to provision
proxmox virtual machines with terraform
it's going to be a ton of fun now let's
dive into terraform and
proxmox first let's talk about what
What you'll need for this tutorial
you're going to need in order to get
started first you're going to need a
proxmox server if you aren't already
using proxmox I have all kinds of
resources on my channel to get you
started I'll leave a card for a video
right about here that you could watch to
get started with proxmox in that video
it'll walk you through everything you
need to get it set up and it'll also go
over some of the basics continuing
another thing you'll need is a template
within your proxmox installation we'll
be using this template to serve as the
base for the virtual machine that we'll
be deploying if you haven't already
created a template within proxmox before
what I'll do is leave a card right about
here for the episode of my full course
that covers exactly how to do this so at
this point you'll need to jot down two
things you'll need the URL to your prox
Mo server and you'll also need the name
of your template
file so here what I'll do on my end is
Setting up Proxmox for Terraform
I'll sign into my proxmox server and yes
this is my actual proxmox server I'll
paste in the password and click
login type in my second Factor code
right here and as you can see I'm logged
in so right here we can see my actual
proxmox installation that I use at my
company see the servers that I have here
but what we actually need at this point
one we need the URL so I already have
that here but what we need to do is just
copy this so what you'll do is just
write that down and then the next thing
like I mentioned is you'll need the name
of the template that you plan on using
so right here I have a template that's
named Debian hyphen 12 and that's the
one that I'm going to use so again
you'll need a template already before
you could go through this
process now the next thing we're going
to is create some resources that we need
within proxmox now to be fair you can
use your normal user account with
terraform but I don't recommend that I
like to Silo things out in individual
accounts so that way we have more
control over how our server is set up so
what I'm going to do is click on data
center right
here and then once you do that you could
go down to users right here so what I'm
going to do is add a new user I'm just
going to call it terraform
and I'm not going to configure anything
else here I'm just going to set the name
for now and I'll simply click add and
now we have the terraform user right
here but that by itself isn't enough for
us to use it we're going to need to
configure the account as well now next
what we're going to do to configure
permissions we need to configure the
permissions that are necessary for
terraform to interact with proxmox so
what I'll do is go here to roles again I
went to Data Center then underneath
permissions if you expand that we have
roles we'll click on that and we're
going to create a new one so I'll create
one right
now I'll call it terraform
provision and now what I'm going to do
is add a few actually more than a few
permissions to this user there's
actually more than a handful here so
what I recommend you do is just refer to
the graphic that I'm going to be
overlaying on the screen and it's going
to have a list of all the permissions
that you need you'll need to make sure
that you add every single one of them if
you miss one then things aren't going to
work and what you could do is just
simply left click on one of them so the
first one that we need here is data
store. allocate space I'm going to
Simply left click on it one time you
don't have to hold shift you don't have
to hold control or anything like that
just simply click on it so that's the
first one we also need data store audit
so click on that next we need pool
allocate so I'll click on that
that next for software Define networking
we need sn.
use and then next we need cy.
console we need cy.
modify we also need vm.
allocate VM
audit we need VM clone we need to clone
the
template need VM config CD
ROM CPU and cloud in it so we need these
three so far here for VM
config we need VM config
disc VM config Hardware type VM config
memory so click on that one as well we
also need the network option here we
need config do
options we need VM
migrate VM monitor
and also power management again take
your time and make sure that you get all
of these just take a look at the graphic
on the screen and just make sure you
have everything here that I have
outlined in that graphic and you should
be fine so next you just click anywhere
here within this small window to make
the drop down go away and then we can
simply click create so at this point we
have a role called terraform provision
and it contains all of the settings
right here that we need so we should be
good to go for that that so next what
we're going to do is click on groups we
need to create a group that's going to
hold the permissions that we have in the
role so what we'll do is Click
create and what I'll do is call it
terraform clever I know just like
that and that's it we have a group we
just needed to create a group named
terraform and we've done that so the
next thing we'll do is Click permissions
because we need to add a group
permission so what we'll do is add
permissions to the group that we just
created so we'll click group permission
just like that we'll use the forward
slash right here we'll just leave that
there for the group we're going to
choose terraform the one that we just
created and then we're going to scroll
down and you should see the RO that we
created with all the permissions right
here so what this does is effectively
glue the permissions to the group and
then when we apply the group to the user
then effectively the user will have all
of the permissions here that's in the
role
so we'll click
add next we'll go back to users and
we'll select the terraform user that we
created earlier we're going to edit that
user and then under group we're going to
select the terraform group that we just
created and this is the final step that
links everything together so at this
point this user as soon as I click okay
is going to have all of the permissions
that we've created so I'll click okay
and now we have that so far so good next
Creatong an API key for Terraform
what we're going to do is create an API
token we want to create an API token
because we would rather not use
usernames and passwords if we can help
it API is better so click add and what
we're going to do is choose our
terraform
user for the token ID you could call
this anything you want really it's just
a
description I'm just going to type
terraform there I think that's good
enough and we're going to uncheck this
box for privilege separation we want
this user to be able to do all the
things that we've you know designated
for it to do so I'm going to uncheck
that box and I'm going to click add now
at this point we get two pieces of
information here and we need to jot this
down we need both of these things the
secret key we are not going to be able
to access after this so what I'll do
just open up a text editor here as
should you and what I'm going to do is
just paste the key right
here and then the ID is the first number
will need that as well so I'll grab
it and I'll paste it right here now
obviously you should never ever ever
show this key to anyone in clear text
the only reason I can get away with
showing you my key is because I'm going
to be deleting it by the time you see
this video actually before you see this
video so by the time you see the edited
version of this video this key won't
exist you won't be able to use it but I
think it's kind of cool to show people
how things actually look without
blurring anything if I can help it so
that's why I wanted you guys to see
that now what we're going to do is just
minimize this right here we'll need that
later but for right now we're almost
ready to get started with terraform now
what we're going to
do just open up a new
tab search for
terraform and right here it is it's
Installing Terraform
terraform doio so you just go to
terraform doio we're going to go to
download we're going to download it and
there's several different versions or
methods for installing
terraform now what I'm going to do is
scroll down and choose the
amd64 binary if you're using arm or
another CPU type then obviously you
would choose whichever one more closely
matches what you're running most of us
are going to be
amd64 so what we're going to do is right
click on this and click copy link
address so that's all we need right now
now what we're going to do is switch to
a
terminal and what I'm going to do is
type WG get and then I'm going to paste
in the URL that we just copied and what
this is going to do is download
terraform locally so I'll press
enter so in my output right here you can
see that terraform was downloaded now
what we'll need is to unzip it now you
may or may not have unzip available so
what we could do is just type command-v
and then unzip and when I press enter
you can see that I do have that
installed now if you don't you might
just have to install the unzip package
such as Pudu app install on zzip for
example but if you don't have it you
could go ahead and download that package
and we can unzip it to do that though
we'll type
unzip and then the name of the package
right
here and then if I list my storage I
have terraform right there it's the
third line from the bottom and the
output of Ls so what I'm going to do
just to be on the safe side I don't want
anyone to modify this file so what I'm
going to do is have root own this
file and as you can see it's now owned
by root so next what I'm going to do is
move this into SL user loal
bin just like
that and if I type command-v and then
terraform you can see that it is
recognized in/ user local bin terraform
now after moving it there if it's not
recognized you get type out the full
path to it and that'll probably work
just fine you really shouldn't have to
do that but anyway as of right now we
have the terraform command available and
what we're going to do is make a
terraform directory and this is going to
hold the files that we're going to be
working with so I'll just navigate into
that directory right there and what
we're going to do is create our very
first terraform file sorry to interrupt
Buy a shirt
my own video but I just wanted to let
you know that I appreciate each and
every single one of you and I I love
creating Linux related content for you
guys but unfortunately producing
highquality Linux content like this
isn't cheap but if you want to help me
make even more content for you guys then
consider supporting learn Linux TV and a
great way to do that is to check out the
official shop for learn Linux TV which
was just recently updated inside the
shop you'll find drro themed shirts bags
drink wear and more and there's some
other surprises there as well for
example I've just introduced a mouse pad
that doubles as a t-mo cheat sheet how
cool is that so check out the shop at
merch.net or you can check out the merch
shelf right here on YouTube you can get
yourself something really cool and
support Linux learning at the same time
so it's a win-win anyway thank you guys
so much for your support I really
appreciate it now let's get back to the
video and what I'll do is take you
Creating our Terraform "tf" File
through it so I'm going to use Vim it
doesn't really matter what text editor
you use you could use Nano Vim it
doesn't matter so you could do Nano
main.tf I'm going to use
Vim I have an entire series on Vim by
the way if you're interested in learning
that you can check out the full course
already on my channel but I'm going to
go ahead and create this
file now to save a little time what I'm
going to do is paste in the code right
here I will have this linked down below
so if you want to copy and paste this as
well you will be able to access this
code so I'll paste it
in and then I'll go up to the top and
I'm going to explain a little bit about
what we're doing now the the first thing
I'm going to do is go back to our text
file where I asked you to jot some
things down and here's mine so what I'm
going to do is copy this here this is
the ID and we're going to put it in
right here and after we set this up I'm
going to go back to the top and explain
exactly what we're doing but we
definitely want to make sure that we
have our secret key here and our ID we
need that to be
correct and then right here here under
pmore API
URL we have the URL to my server now the
URL stops here normally where you have
8006 that support number so you're
adding the SL API 2 SL Json to the end
of the URL so it should look similar to
mine obviously your key will be
different but it should look very
similar to that so that's what we're
setting up that's specific to our server
now another thing to pay attention to
before we go through all the code
here Target node and clone so Target
node is the name of your proxmox server
so if I was to go back to
proxmox you can see I have PVE hyphen 1
and PVE hyphen 2 so that's the name
you're looking for so I'm going to have
terraform launch a virtual machine
instance on PVE 1 so that's why I chose
to include that so let's minimize this
and that there's the PVE hyen one and
then the the template name so again if I
go back to the
browser right here I have Debbie and
hyphen 12 so we need to name the Clone
field here we're going to clone the
Debian hyphen 12 template so that's why
we need to make sure that that's correct
now that we have that set up let's go
back to the top and find out what
exactly we're doing here we have all
this code here what is going on so what
do is start from the top and I will
explain it so up at the top we have some
settings or mainly one setting that is
specific to terraform itself we need to
set some required providers now this
step isn't really always required I mean
in the past when I've done this I only
needed to start here where it has
provider proxmox and then everything
else kind of just worked but for some
reason or another lately I have to add
this what we're doing is we're creating
a provider called
proxmox and then we're telling it the
source that we want the provider to come
from now what this refers to is a
provisioner this is a system or a
utility or plug-in that terraform is
going to use to interact with the target
whether your target is AWS could be
VMware it could be virtual box or
whatever it is you need a provider for
that particular service so since we're
working with proxmox we're going to need
need the proxmox provider and what we're
doing here is we're effectively saying
that we are identifying a provider
called proxmox is equal to this so that
way down here we could just refer to it
as proxmox since that's what we typed
right here so we could refer to it as
that right here and in this section here
we have several things that we need and
we kind of already went over this I mean
you can use a username and password here
if you want to bypass the API don't
recommend that so using the API this is
what it looks like we have pmore API URL
and then we set it to the URL of the
server the target server again we're
adding SL API tojson to the end of that
the token ID came from the creation of
the API token earlier so this is the ID
field of that and then the API token
secret is right here and I want to
underscore the fact you should never
ever ever show a token anywhere do not
upload this file with a token to GitHub
do not post this anywhere if anyone gets
this key they can immediately start
provision provisioning virtual machines
on your instance and you want to be the
only one doing that you don't want
someone obviously breaking into your
server so keep this safe again since I'm
going to be deleting this API token
before this video is posted that's the
only reason why I can get away with this
we want to allow an insecure connection
on my end this isn't really necessary
because I do have TLS certificates on my
installation but I know many of you
won't a lot of you in my audience are
going to be using the IP address and
maybe you don't have a certificate set
up yet so I wanted to include that um
obviously you can customize that
accordingly but we're just going to
leave that alone for now now here on
line 16
continuing let's talk about what we're
doing right here we want to create a
resource or provision a
resource we want to provision a q mu
virtual machine with proxmox so that's
why we have this right
here and here we want to give the
instance a name to uh refer to it as so
here we're going to call it VM hyphen
instance and I have the name also right
here that's the name of the instance
Target node PVE
1 and we're going to clone the Debian 12
template like I mentioned we want to do
a full clone not a linked clone I mean
you could do a linked clone but I really
don't like that I like to just you know
instantiate everything immediately and
not have too many things be thin
provision but I want a full clone there
uh for Cores we have two I think that's
good enough for an example 248 megabytes
of RAM and then we have a subsection
right here notice that disk here is
aligned to memory that's important we're
going to set some parameters regarding
the disc now what I did on my end size
is required even though though we're
running you know with a template it's
already it already has a disc in my
opinion we shouldn't need to set a size
since it already has one but it's not
going to let us continue without it so
what I did here is I just set the size
to the same size of the dis in the
template so what I did was just match it
here type we're going to leave it as
scuzzy for storage I have mine set to
local hyphen lvm now this might be
different for you so before we go any
further let's talk about it so as you
can see right here my main storage is
local hyphen lvm that's the one that I'm
using yours might be different
especially if you're using ZFS then the
name will be different so for some of
you if you leave this as is it might not
work you want to match this to your
primary
storage and in my case it's going to be
local hyphen
lvm so that's good enough for me so
discard on it's an SSD my server uses
all SSD so that's why I have that um you
can that to be off if you have uh
spinning rust for example but I'm going
to leave that
on now continuing we have another
subsection here for Network we're going
to set this to vert iio it's beyond the
scope to change this around and show you
the differences but this one should work
just good enough now this is incorrect
let me fix this VM br1 now what you want
to do is kind of match the network here
so if I was to go to my node here then
down to network you can see that I have
four Bridges right here they're all for
a different purpose now what I want to
do is use my VM subnet so I have a VLAN
and subnet that's set up for virtual
machines specifically and I call it vmb
br1 that's something that I set up
offline um actually probably during the
filming of my original proxmox course
you should check that out if you haven't
already done that but from the output we
know that the bridge I want to use my VM
subnet bridge is VM br1 so we're going
to use that you can have a firewall if
you want you can also set it to not be
connected to the network when you first
get started but I'm going to leave that
alone for now uh what I'm going to do is
save the file and let's see what we need
Using Terraform to build our Proxmox instance
to do in order to use this so the first
thing we're going to do and this is only
necessary the first time you ever run
terraform inside a
folder we're going to type terraform and
it just like that and what that should
do is download the provider earlier we
designated that we want to use the
proxmox provider but terraform doesn't
actually have built-in providers well it
might but more often than not you need
to download a provider and when you type
terraform in it it's going to check your
main.tf file now
notice if I list my storage that's all
we have here okay so I'm Type terraform
in it but I'm not even giving it a file
name at all but the thing is terraform
knows that TF files are terraform files
and if any exist in the same directory
it's going to read those and since we
have the provider information right
there in the file and they should find
it so I'll press enter
here as you can see it's downloading the
proxmox provider right now and it says
that terraform has been successfully
initialized so you should only really
need to do this once unless you delete
all your files and you know have to
recreate something usually when you set
up terraform or go to use it for the
very first time you type terraform in it
and that usually is the last time you
have to do that now the next thing we're
going to do is type
terraform and then plan now this will
not make any changes to your server at
all but what it will do is at least try
to get a general idea if you have any
problems or syntax errors or something
so I'll press
enter and so far it looks okay we have
quite a bit of information here um again
this is plan it's not going to make any
changes but what this will do is tell
you about the changes that it wants to
make and you really should pay special
attention to this especially if it tells
you that it wants to delete something um
sometimes something can't be updated and
needs to be deleted it's just the way it
is we don't have anything created
through this yet though so all we're
going to do is see pluses here it wants
to create a VM instance well that's
great because that's what I wanted it to
do um automatic reboot we have all these
different options some of which we
haven't chosen but these are just
defaults but what you could do is look
through here and just make sure that all
the settings that are important to you
such as the network bridge you
definitely want to be on the right
Network make sure all of these are okay
and if everything looks good to you then
what we can do is go ahead and actually
run terraform and to do
that what we'll do is run terraform
apply we'll type yes and then press
enter and actually that should be it so
if we go back to our web browser right
here we can see that something is
happening here we have vmid 102 so
something is being
created and right here we see VM 922
which is going to be my Debian 12
template it's ID 922 it
matches it's being cloned right here so
VM
id12 so we should actually see this come
up we're just waiting for it to finish
so we'll just give this a moment and it
should be ready to go actually I think
it already is notice that the name is VM
instance that's what we called it inside
the file and what I should be able to do
is start this virtual machine let's see
what
happens and check it out the virtual
machine that we created through
terraform is now booting up so great job
you have successfully configured a
virtual machine through terraform
and there we go how fun was that in this
video we Ed terraform to provision a
virtual machine on proxmox and I really
hope that you found it helpful now I'd
love to cover more proxmox and I also
would love to cover more terraform as
well so if you'd like to see content on
either of those let me know in the
comments down below what in particular
you would like to learn in the meantime
though thank you so much for checking
out this video as usual subscribe if you
haven't already done so and I'll see you
in the next video
[Music]
[Music]
