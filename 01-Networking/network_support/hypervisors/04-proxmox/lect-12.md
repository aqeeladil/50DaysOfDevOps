
Search in video
Intro
today's video is sponsored by crowdsec
crowdsec is an open source and
collaborative intrusion protection
system that brings a whole new meaning
to the phrase knowledge is power
this solution protects your servers by
blocking unwanted behaviors including
but not limited to port scans cross-site
scripting brute forcing and more
and it does this in a very exciting way
by making security a community effort
rather than a personal one
you've no doubt seen the impact that
collaborative processes have had on
businesses and end users but have you
ever seen a collaborative security
solution
well neither have i until now
and that's what crowdsec is it's an
intrusion prevention solution that takes
real security events into account and
leverages that information to enhance
the protection of your servers
whenever krautsec prevents an intrusion
attempt on your server
it actually allows all the other servers
out there in the wild to benefit from
that as well because any time a server
with crowdsec installed sees an
intrusion attempt it helps other servers
also prevent attacks from that same ip
and one of the best things about
crowdsec is that they follow a
scientific community-based approach to
help make the industry better and safer
for everyone
by just installing a few packages you
can start protecting your servers
immediately
and the best part about this is that
crowdsec is free
and by free i mean actually free
not free for a certain number of servers
there's no trial period you can
literally install it right now without
so much as signing up anywhere
to get started all you have to do is
simply add the repository to your server
install the required packages start and
enable the service and you're literally
done
that's it
for further information and
documentation check out the url that you
see on your screen right now
and in addition to that you could also
check out the installation video that i
did on this very channel that goes over
the entire process
thank you so much to crowdsec for
sponsoring today's video i really
appreciate it now let's go ahead and get
started
[Music]
hello again everyone
in the previous class we went over
backups and snapshots
and that's really important
but security is also really important
and thankfully proxmox actually includes
an integrated firewall feature by
default you don't have to use it
especially if you have another firewall
that you prefer that's ahead of proxmox
but it doesn't hurt to have a firewall
feature within proxmox itself and it's
worth checking out setting up a firewall
is very important so if you don't
already have a solution the proxmox
firewall is pretty effective and
configuring firewall rules is almost
like an art form especially when it
comes to administrators that you know
are into that kind of thing but even if
it's not your cup of tea it's still a
very important thing and we're going to
explore in this video we're going to
take a look at the integrated firewall
feature of proxmox in more detail so
let's do that
all right so let's start exploring
firewalls
Location of firewall settings
now the first thing that's probably the
most confusing to newcomers is that
there's firewall settings well all over
the place
right now i have the host highlighted
pve one
and you can see that we have a firewall
section here
if i click on a container
we have a firewall section
if i click on a vm
you guessed it we have a firewall
section if i click on data center
we also have
a firewall section
so if you want to add some firewall
rules where should you put those
firewall rules
that's what i'm hoping to break down in
this video i'm going to show you exactly
where you need to create those rules
now first and foremost it's easy to
think about this as a top down kind of
view so if you add a firewall rule here
to data center it's going to apply to
the data center
if you add your firewall rules here
underneath the host
then those firewall rules are going to
apply to the host same for containers
and vms
so where you create those rules kind of
depends on where you want that
abstracted
now the thing is though none of what i
just said will actually matter if
firewalls are disabled altogether
Warning about enabling the firewall prematurely
so here i am on data center view
and underneath firewall and then options
firewall is set to no
now you shouldn't actually enable the
firewall just yet
just understand so far that when the
firewall is turned off it doesn't work
but if you turn it on without actually
creating firewall rules then the issue
is going to be that you'll lose access
to the proxmox web console and we don't
want that
Locking myself out (on purpose)
now you don't actually have to follow
along with what i'm about to do
but what i am going to do is lock myself
out on purpose which is why i don't want
you to follow along
i think seeing this will help you
understand how the firewall actually
works
so what i'm going to do is edit this
i'm not going to save it just yet i'm
going to drop down to a terminal
and i'm going to start a ping to the
proxmox host itself
and now we can see that the ping is
happening
and back up here in the web console
again don't follow along with what i'm
doing i'm going to enable the firewall
i'll click ok
and then if i go back down to the
terminal
nothing is happening
the ping has stopped
and now i have a connection error i've
actually lost access to the web console
i can't click on anything
nothing is actually going to work it's
just going to load and i can't actually
disable the firewall here
so again i'm locked out now thankfully
Disabling the firewall via CLI (to restore access)
on my end i have an easy solution for
that i can actually just access the ipmi
console which i'll do right now
then i'll go to remote control
and now i have a terminal right here i
can use to re-enable my access to the
web console
and thankfully that's actually easy to
do i can run nano or whatever text
editor i want it doesn't really matter
and the file that i want to edit is
slash etsy
and then slash pve
firewall
then cluster.fw
so this config file right here allows me
to enable or disable the firewall for
the entire cluster it's enabled right
now so i'm going to change that to a
zero
and this is nano so we have our options
down here as far as saving files and
whatnot i'm just going to save it ctrl o
and then enter
and then control x
and that should be everything that i'll
need to do
now i have access to the web console
again notice that the connection error
is gone
if i go down here my pings have resumed
so i have restored access to the server
that's pretty cool
so what you just saw was me locking
myself out on purpose
and that just goes to show you that when
you enable the firewall and data center
view it's going to enable it for better
or worse
so we shouldn't actually enable the
firewall until we have the rules created
that are important for us to retain
access to the server
the default policy right here is to drop
traffic this is the input policy
and it's going to drop everything
incoming and that's why i lost access
the default is to drop and well it
dropped my traffic so i guess you could
say that it works
Creating a firewall rule for allowing access to the web console
now what i want to do is create some
rules here just to show you some
examples so i'll click on firewall and
i'll add a rule
so for incoming i'm going to leave it on
accept which is what it is i'm going to
enable this particular rule
the interface i'm going to set it to
vmbr0
that's the default bridge that proxmox
uses if that's different on your end you
might have to type a different interface
name here
for the source i'm going to leave this
blank right here
but if i did want to set a particular
source like an ip address i could do
that here but what i want to do is
actually select the protocol i'll select
tcp
and the destination port is 8006
so essentially what i'm doing is i'm
trying to create a rule right here which
is going to accept traffic that is going
to port 8006
you'll notice that 8006 is in the
address bar right here
so essentially what i'm doing is i'm
creating a rule that is going to allow
access to the web console
i didn't actually type a source or a
destination
so right now i'm allowing everyone
access to the console
in the future i'll probably want to dial
that down and not allow everyone in but
i think it's good enough for now i'm
going to add this rule
and now it's here
now i'm not actually going to lose
access or anything because the firewall
itself
is disabled
as you recall when i enabled this i lost
access pretty much immediately but now i
have a rule that's going to
hypothetically or at least i hope allow
me access to the web console so let's go
ahead and enable the firewall right now
and see what happens
i'll give it a few seconds let's see if
i lose access
to be on the safe side i'm going to
click on something else
now so far it doesn't look like i lost
access i can still click on things
that's a really good sign if i go back
down here to the terminal
well
i did lose access to ping but you know
what
that's actually okay because i do have
access to the web console and i knew
this would happen
because the thing is when i clicked on
firewall right here for the data center
i created this rule right here which is
allowing me or pretty much everyone
access to port 8006 which is of course
the web console
but that does not imply access to ping
Creating a firewall rule for ICMP
or icmp traffic
so what i could do is add yet another
rule
i'll set it to accept
and for the protocol i'll set it to icmp
now let's have a little bit of fun i
want to allow only my laptop to ping the
server
then slash 32
and the slash 32 limits the scope to
that one ip address
so so far so good
i'll enable the rule
and then add it
so we have another rule right here and
actually i should have put the interface
here let me go ahead and adjust that
i'll click ok
and let's drop down
and as you can see pings are restored
so let's go ahead and ssh into the
server let's see if that works it won't
but we may as well try it
so what i'm going to do is attempt an
ssh connection to pve 1 which obviously
won't work
it's just going to time out that's
expected so to allow my laptop access
Creating a firewall rule to allow OpenSSH
what i need to do is add yet another
rule
so protocol is going to be tcp
destination port is going to be 22
that is the port for ssh
and actually
i click up here and scroll down this is
even easier
instead of manually creating it what i
could do is click on ssh right here
then for the source i'll type in yet
again the ip address to my laptop
i'll enable the rule and click add
so we have another rule here
i'm going to cancel out of this
connection attempt right here and try it
again
and would you look at this it's working
now i'm not going to actually connect
via ssh we'll cover that later but we
can see that it's working it's asking
for my password if it wasn't working it
would just continue to time out so that
does mean that the firewall rule that i
created is actually working
now let's see how this is actually
abstracted when i go down another layer
i'm going to actually create some rules
here under pve one
but before i do that i want to remove
this rule right here
and now it's gone
and that should also mean that i won't
be able to ssh into that server anymore
and as you can see i'm no longer able to
use ssh to connect to that server that's
expected
so what i'm going to do under pve 1 is
create that particular rule
i'm already on the firewall section so
i'm going to add a rule
i'm going to accept let's just use the
macro of ssh because that's easier to do
so i'll select that
when i can find it there it is
let's enable it
and again i'll type in my ip address
right here
and there it is
so the interface vmbr0 yet again let's
add it
and it's added
let's cancel out of this
let's try that again
and now it works
so what just happened here
Summary of concepts so far
now so far we understand that in order
for any firewalls to work at all
you have to go here on the data center
view to firewall and then options and
then enable it but you shouldn't
actually enable it until you've created
the rules that you intend on creating
so in the actual firewall section here
i have some rules here that allow me
access to the server so this rule here
icmp allows me to ping the server
so this is going to apply data center
wide so if i added yet another host here
this rule is going to allow me to ping
that host as well
so this saves me from manually adding
this rule right here to every single
host just makes things a little bit
easier
and the same is true for this rule right
here it allows me access to the web
console
because the web console runs on port
8006
now on another level i did have an ssh
option here that's not here now
i created that here under pve one
and that's why i'm able to ssh into pve
one
if i add another server to the cluster
this rule will not be present because i
created this rule underneath this
particular host so it applies to this
particular host it's not going to apply
to pve 2 when i go to add that
if i did want it to apply to the entire
data center i should have created that
rule up here in data center
but because i didn't it applies only to
this server and now that i've added it i
am able to ssh into the server
now we do have this particular server
here
if i go back to the console what is the
ip address let's see
i'll log in
and i'll type the right password this
time
now i'm in so what's the ip address
249.250.
so what i'm going to do is attempt to
ssh directly into the virtual machine
and it actually works
as you can see i was able to ssh
directly into the server
so what i'm going to do is actually
remove this rule right here
and now it's gone
and sometimes it needs a few seconds to
apply but anyway
i'm going to try to connect to that
particular virtual machine
one more time here
and it still works
why does that still work
let's actually make sure that it still
works because again it takes some time
for firewall rules to apply i did remove
it
it still works
so when you get to this level if i add a
firewall rule to pve one it applies to
pve one
but here on the web server
underneath firewall
firewall is disabled
and the reason why i was able to ssh
into the web server despite the fact
that i removed the firewall
was because the firewall was disabled on
web server one so i just enabled that
i'll enable it here as well
and it's enabled so what that should
mean then is i should not be able to ssh
into that server if i go to try it again
and as you can see i'm not able to do
that
if i go back up here to pve one and
re-add that firewall rule that i had
here previously
i'll set it to vmbr0
i'll enable it
now that's enabled
let's cancel out of here
and let's run a little experiment do you
think it's going to work i'll give it a
few seconds to make sure that all the
firewall changes have been applied
i think enough time has passed now let's
try it
it's not working
but wait a minute
i've enabled ssh right here
and i'm allowing traffic from the ip
address for my laptop
that's odd
let's try to ssh into the host again
and that was 249.4
and that works
and the ip address just to make sure
that i'm typing in the correct one
here under web server 1
the ip address is 249.250.
and that was the ip address that i tried
i'm not able to do that
so i'll break out of here let's go back
to the web console and what that's done
is taught us yet another lesson about
the firewall
so when you get down here to this level
basically any level that's not data
center
the firewall rule is going to apply only
for that particular object so when i
enabled ssh right here i'm enabling it
only for pve-1
so if i want to allow access to web
server one
what i need to do is do the same thing
right here and add that firewall rule to
it
so i'll enable the rule and let's go
ahead and choose ssh
i'll select that
and for the source yet again i'll type
the ip address for my laptop
and now it's added
as you can see here i have a password
prompt so that means that i am allowed
to access ssh to this particular server
just to make sure
i typed in the password and now i'm
definitely in
so as a quick summary i want to make
sure that you guys understand this
in order for firewalls to work at all
you have to go to the data center view
right here
and then underneath firewall and then
options you have to enable the firewall
again you shouldn't do that until you
have the rules created that you want to
have created elsewise you risk locking
yourself out so to fix that
again i added these two rules right here
this one here is just a test you don't
have to allow icmp but anyway i have
these two rules right here
and the one that matters the most is
this one
the proxmox web console uses port 8006
so i've enabled that right here
after i did that
i then went to options and then enabled
the firewall
it was safe to do so at that point
because i've already enabled the web
console
so i didn't actually risk locking myself
out so that's pretty cool now down here
on the host itself i have some firewall
rules i can also enable or disable the
firewall it's enabled currently
and now that it's enabled
i created this firewall rule right here
that allows me to ssh into this
particular host
now that does not actually apply to the
vms underneath that host
they have their own firewall settings
but if i actually wanted to use a
firewall on the container i would have
to enable it same for vms
right here it's enabled then after you
enable it
or even before you enable it you create
the rules that you want to have applied
to that server right here so hopefully
that helps you understand how the
firewall rules are abstracted and how
they work
you start at the data center
you enable the ports here that you want
to have enabled especially port 8006
turn on the firewall
and keep just drilling down here and
adding firewall rules as you see fit to
increase the security at the end of the
day it's important to block everything
to all servers unless something actually
needs to connect to a specific server so
hopefully that helps you understand how
the firewall works in proxmox
all right so at this point you guys
should be well on your way to creating
firewall rules to help secure your
proxmox installation that's definitely a
very important thing to do
now in the next class it's going to get
even geekier because we're going to take
a look at the command line in proxmox
which is going to be especially fun for
me because i love the command line
so make sure you click that subscribe
button if you haven't already done so
and that video might already be uploaded
right now so go ahead and check it out
and i'll meet you there
[Music]
you
