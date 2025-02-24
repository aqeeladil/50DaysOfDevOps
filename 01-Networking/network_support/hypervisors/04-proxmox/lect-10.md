
Search in video
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
hello again everyone and welcome back to
my proxmox course yet again in today's
episode we're going to talk about users
it's like the subject that all
administrators have to talk about you
know every now and then because users
are great and then you know sometimes
not so great we have to keep our eye on
them but we're not going to get into
that part of things but we are going to
talk about users in proxmox to help you
understand the two different types of
users that exist in proxmox when to
choose one versus the other
and how to manage them so let's get
started
all right so let's talk about users
if i click here on data center to go to
the data center view we have a user
section right here
we have one user currently named root
and this is actually the root user
that's on the underlying host system for
pve one
The two realms for users
now before we get into what that
actually means one thing to understand
is that there's actually two realms when
it comes to users
and you can see the realm listed right
here for the user root it's listed under
pam
and what pam actually refers to is the
user management on the underlying host
system itself
pam is just linux authentication
essentially now the difference between
pam users and proxmox users is going to
become more apparent as we go along with
the video so don't worry about it so
much right now
i'm going to walk you through the
process of creating a pam user and i'll
also walk you through the process of
creating a proxmox user now both pam and
proxmox users are able to use proxmox
the difference is mainly where the user
is actually created and where the
information for that user is stored
but anyway let's walk through the
process so we have the user root right
here
and let's just assume that we have
another person i'll use myself as an
example that wants to manage this
particular data center
Adding a PAM user
so what i'm going to do is add a user
and right here i'm going to add my
username
i'll just use my first name to keep it
simple
now we could select a group but i don't
have any groups just yet we'll get to
that
anyway i could create an expiration date
for the user i could enable or disable
the user and i could also add the first
name last name and email address if i
wanted to
and i could also add a comment if i
found that helpful to let me know why
that user exists on the system and what
they're there to do
i'll leave that up to you when it comes
to how to fill this out i'm just keeping
it simple by using my first name and for
the realm i'm selecting linux pam
standard authentication for this
particular user
so what i'll do is add the user
and now the user is added
now there's actually going to be some
confusion when it comes to this
particular user that i created right
here
so for example what i'm going to do is
click on pve 1
and then i'll click on shell to access
the shell console here
and i'm automatically logged in as root
as we see here
now if you aren't all familiar with
linux authentication then you know that
the etsy password file is where linux
systems store their user accounts
now as you can see my user is not listed
here
since i created a normal user account it
should have had the id of 1000 and by id
i'm talking about the user id this is
nothing to do with proxmox linux systems
have user ids or uids for all the users
that exist on the system
if i create a user on the linux system
itself it's assigned a uid the next
available uid
and as you can see here i don't have my
name anywhere
it would have been added to the end of
the file if it did add it so what we can
glean from this is that even though i
added the user to the gui here in
proxmox it didn't actually create the
user on the underlying system
now that might seem like a very annoying
thing
and i'll admit that it's not the most
convenient thing but it does make sense
and it will make sense more here in a
moment but basically what i'm going to
do is set a password for that user it
didn't even ask me to set a password for
that user
so i'll use passwd and then my name
this is just a standard linux command i
have an entire linux essentials series
that goes over this command as well as
others definitely check out that series
if you want to learn more about linux
anyway i'll press enter
and it tells me that the user j does not
exist
so if i was to log out
what i could do is type my username and
my password here but i can't type my
password because my user doesn't have a
password
so i'm not going to be able to do this
just type in my name
and then click login
because you need to have a password and
also the user does need to exist
so essentially when i added the user to
the gui all it really did was just add
it to the gui but you have to go through
another step and add it to the system
now what i'll do is just log in as root
Manually creating a Linux user
and now i'm logged back into the server
so what i'm going to do is fix this
right now and create the user here on
the proxmox server i'm on pve one and
i'm going to create the user right now
so what i'm going to do is type add user
and then the username that i want to
create in this case j i'll press enter
and i'll type in a password for that
user
and i'll type it in again
and i'm just going to skip these prompts
you can fill these out if you want to
but it doesn't really matter to me so
i'm just going to press enter through
all of these
and then is this information correct y
is capital which means it's the default
option i'll press enter
and now that user is created and to
prove
that you can see it there at the end
it's the second to last line
it shows my user right there with a uid
of 1000 and a group id of 1000 again i
have dedicated videos that explain that
in more detail
i have a video about adding users to a
linux system and also a video for adding
groups to a linux system
anyway
now that i did add that user let's go
ahead and log out
and i'll log in as the user that i just
created
let's see what happens
and now i'm in
now notice though that i do have the
server pve-1
i'm not able to see what's underneath it
and in addition to that i really don't
have access to all that much at all
so what we can see here is that my user
well it doesn't have permission to
anything so that's why i don't see
anything underneath this
so what i'm going to do is just log back
into the server again as root
and let's explore this a little bit
deeper to fully understand what's going
on with
users so i have this user highlighted
right here this is the user that i tried
to log in as well i did log in as this
user but i didn't have access to
anything i couldn't see vms or even the
stats of the server it was completely
useless
Adding a user into the pve realm
now notice that it's in the pam realm so
what i'm going to do is add the user
again
and i'll create it with the same name
but what i'm going to do instead is
actually add it to the proxmox
authentication server instead of pam so
i'll type in the password here for this
user
notice that it's actually asking me for
the password this time
and then here we can select a group but
i haven't created any groups so that's
okay we can do that later
but i'm adding the user to the proxmox
authentication server like i mentioned
i'm going to leave most of this blank
i'll just click add
and now we have the same user
twice
but one of them is in the pam realm and
the other is in the pve realm
now what i'm going to do is log out
i don't suspect that there's going to be
any difference as far as permissions are
concerned
but what i want to show you is that when
you go to log into the server
you can of course choose the realm that
you want to log into
so i was using pam before i want to make
sure that i'm choosing this option here
the proxmox ve authentication server
then i'll click log in
now for this user the access here is
virtually the same
meaning that this user in particular is
completely useless it can't do anything
but we have the user created in both
realms
and the reason why i did that
is because i wanted to show you that you
can have the same user twice
so i'll log back in as root i'll type in
the password i'll make sure that it says
pam right here which it does
and now i'm logged into the server
so we have these two users right here
that i created and they're both equally
useless
and the concept of user management seems
to be at least a little confusing when
it comes to new users of proxmox
but let's break down why we have two
different user accounts right here
so let's start with this one this is
actually the second user that i created
and i created it in the pve realm
what that means is that this user exists
in proxmox but it does not exist on a
system
so for example if i add yet another user
and i'll add spock to the system he's
pretty cool
and i'm going to create him in the
proxmox ve authentication server
i'll type a password for him
and then i'll add him
and here he is
now if i go here to my proxmox server
and then click on shell
if you recall earlier i mentioned that
the etsy password file is where the user
accounts are actually stored
let's check that out
and here's my user
that's the pam user that i created
earlier for myself
but notice that spock is not listed here
at all
so what you can glean from that is when
you add a proxmox user that user is not
actually a system user it's not a linux
system user it doesn't exist in the
linux system normally
and proxmox users are generally used to
manage the proxmox system itself
so if you wanted to invite a co-worker
for example to log into the server and
help create some vms for you maybe
manage the vms things like that
then you'll generally want to create
users like that in the proxmox
authentication server
and for the majority of your needs
that's more than sufficient
so if that's really all you need then
why would you even want to create a pam
user
the thing is pam users they can use ssh
to log into the server
so by me creating j in the pam realm
that means that that particular user is
able to log into the server via ssh and
manage it via the command line
a proxmox user is not able to do that
now sure a proxmox user can click on
shell like i've done numerous times so
far and manage it via the command line
that way but they wouldn't be able to
log into the actual system via ssh
unless they had a pam account
in fact you don't even have to add a pam
user here to proxmox at all you just add
it to the underlying linux server the
underlying proxmox server and that's
fine
so the main takeaway so far is that if
you want to create a user to access the
server via ssh then you want to do so
with pam
and it's a good idea to add that pam
user here to the proxmox gui now if you
want to allow someone to manage vms via
the gui the web console here then you
want to create that user in the pve
realm like this one
so this user here exists on the proxmox
server but it doesn't exist on the
underlying linux server itself
but now you know the difference
Creating a group
but the thing is though regardless of
which of these two users i logged into
the server with neither of them are able
to do anything so what we want to do
right now is actually try to fix that
now what i want to do first and foremost
is add a new group
and what i'm going to do is create that
group right here
and just keep it simple what i'm going
to do is call the group admins
now notice that there's no configuration
here whatsoever other than the fact that
i could type a comment
but what i'm doing is creating a group
and that's really all i can do here i
could create a group and that's it
there's no permissions options here at
all but i do need to make sure that this
group does exist before we continue so
i'll create it
so we have this admins group
and just like both of my user accounts
it's completely useless because it
serves no purpose whatsoever at least
not yet we need to give it a purpose and
Adding user permissions
to do that we'll click on permissions
and what i'll do is click add
i'll add a group permission
so what i'm going to do is just add
slash right here at the top
you can restrict the permissions down as
you can see here we have different paths
even vm vmids if you want to restrict a
permission to a specific virtual machine
that's pretty cool
you can restrict the permissions to
storage so for example if you want that
group to only be able to manage storage
you can limit it to just that
just to keep it simple i'm going to give
it everything in the real world you
wouldn't want to do this you want to
create a group for storage or virtual
machines
basically just give people the least
amount of permissions that they need to
do their job
but i'm just using slash right here
because i just want to show you what
that looks like
so i'll drop group down and we have the
admins group right here
and right now the role is no access
so what i'm going to do is assign the
role administrator to this group
and i'll click add
let me show you what that actually means
so if i click on roles
we have administrator right here
privileges tells us what this particular
role is allowed to do
so administrator is allowed to do
everything no access is the default
which gives you well nothing gives you
no access
we also have other permissions here that
are fairly self-explanatory
so for example
we can even create a group that is able
to manage users but not manage virtual
machines
so maybe you have a person at your
company if you do use proxmox in a
company and their job is to create users
when a new employee joins a company you
could give them access to do exactly
that
but the user if they were a member of a
group that had this role
they would not be able to delete virtual
machines or anything like that
and that's important
so this is what we're going with right
now
so under groups i created this group
and as you recall there's no permissions
here there's nothing i can do
but i went up here to permissions
i added a permission
this one right here it's applied to the
admins group
and the admins group in this case is
being given the role of administrator
Assigning a group to a user
now the thing is there's no user that's
a member of this particular group
so what i'm going to do is click on
users i'll click on the pve version of
my user
we'll edit it
and we'll assign my user to the admins
group
so now when i go to log out
i'm going to log in as that user
and i'll make sure i choose right here
but i want to log into the proxmox
authentication server i'll click login
and take a look at that
my user now has access to do pretty much
everything it didn't before but it
definitely does now
now i'm going to log back in as root
just wanted to make sure i showed you
guys that
so let's go ahead and take another look
at my pam user here because i mentioned
that you should only use this for ssh
and that's true generally speaking you
want to use the pve realm for anything
that's pve related
but what i'm going to do is delete the
pve user
and now we only have the pam user here
i'm going to edit that pam user and i'm
going to assign it to the group of
admins
so what i'm going to do is log out
and let's log in as my user but in this
case i want to log in as the pam version
of my user
and as you can see
my user is now able to do virtually
everything
that's pretty cool
so let's go through a quick summary of
how users works and just make sure that
we have a well-rounded understanding
so i went over the two different realms
we have pam and the proxmox realm as you
see here
as i discussed earlier pam users are
linux users
proxmox is a linux distribution so of
course it has linux users as an option
if i create a user here that's a pam
user it is not created on the underlying
linux server
that means if you create a pam user you
will not be able to log into the web
console for proxmox as that user at
least until you create that user on the
underlying linux system manually
yourself so once you create a pam user
on the linux system
you can use the shell to do that
but basically you create a pam user on
the linux system the same way you create
a linux user on any other system
then after you do that you add it to the
proxmox server as a pam user
so creating a pam user is done in two
steps
you create it on the linux system itself
and then you go into the web console for
proxmox and you create it there as well
a pve user is created in a single step
you create it here in proxmox itself and
you're done
pam users like i mentioned earlier are
mainly for people that are going to be
using ssh
if that user won't be using ssh then
it's probably a better idea to create it
as a pve user
so as an administrator it's pretty much
up to you how you create your users
you could create everybody as a pam user
which means you're going to have to
execute basically two steps for every
one user account that you want to create
or you could create everybody as a pve
user
now even though i have this pam user i'm
still able to add it to a group i added
it to admins
and i can add that same group here to
spock as well
so even though pam users and pve users
are two completely different types of
users they could both be used to manage
the system you just add them to the
group
but by default you don't actually have
any groups so what i did was i created
admins right here
there's no options this is just a place
to create a group and that's it
after you create a group you can go here
to permissions
and then you can add a permission for
that group so you can add a group
permission or a user permission so you
can give a permission directly to a user
if you want to
and it's pretty much the same thing
but i created a group permission which
resulted in this one right here
the path is slash which means this
particular group applies to everything
and the role defines what members of
that group are allowed to do
so the role applies to the path
that helps you define what each and
every group is allowed to do
so what i'm going to do is create
another group
i'll create user admin
so now we have that group
and then under permissions
i'm going to add a group permission for
that group
i'll give it access to the entire server
i'll apply it to the new group that i
created
and even though i'm giving it access to
the entire server i only want members of
that group to be able to manage users
so i'll scroll down here
i'll select user admin
and then i'll click add
so now i can add a user to this
particular group user admin
and we created it here
and that'll give that particular user
access to add and remove users to and
from the system
so as you can see you can define the
permissions that users are able to do
assign those permissions to a group and
then assign that group to a user
hopefully that makes better sense now
now i recommend playing around with this
just create some additional users
experiment with pve and pam users
and also experiment with permissions
definitely add some permissions for your
user maybe create another one and add
another group for that user as well
just have some fun with this and explore
it and if you don't already understand
it i'm sure you will shortly
alright so now you guys know how to
manage users within proxmox
and that's a very important skill for
any administrator because managing users
that's something that we find ourselves
doing quite a bit
but what's more important is the subject
of backups and snapshots which is going
to be the subject of the next class in
this series
and i should have that uploaded very
soon if i don't already have it uploaded
and i'll see you there
thanks for watching
[Music]
so
[Music]
you
