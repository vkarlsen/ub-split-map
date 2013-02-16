# ub-split-map #
## ABOUT ##
The purpose of this module is to create a 1:1 split horizon IP mapping
that will map external IPs to RFC-1918 IPs.  This would be a replacement
for split horizon DNS that would work in a dynamic fashion.

For example, if you had an A record for "www.example.com" that pointed to
an external IP address of 1.2.3.4 that mapped to a web server on your 
192.168.0.10 on your internal network.  Normally you would have to set 
up an internal DNS server to return the 192.168.0.10 address as you wouldn't
be able to route to the 1.2.3.4 address.

## INSTALL ##
### Install Unbound ###
First and foremost, you are going to need to install unbound.  In most
package managers, this is a pretty simple task.  Make sure you install
the python module support along with unbound!

    sudo apt-get install unbound python-unbound

or maybe

    sudo yum install unbound unbound-python

or even

    echo net-dns/unbound python >> /etc/portage/package.use && emerge unbound

If you are building from source, make sure you build it with python module
support.

### Install ub-split-map ###
You can always grab the source or clone the github repository, etc. and do
the good ol:

    sudo python setup.py install

You can also install directly from PyPi with easy_install or pip

    sudo pip install ub-split-map

This is going to install the module in your standard python library location.
If you want it somewhere else, as you have to reference the module in your
unbound.conf, you can copy it wherever you would like.  Otherwise, it's
going to end up somewhere like /usr/lib/python2.7/site-packages/ubsplitmap.py

## CONFIGURATION ##
### Configuring Unbound ###
Note that this configuration does *NOT* cover setting up Unbound in a chroot
environment.  Therefore, if you want this to work, you will want to set the
following in the "server" section. 

    chroot: ""

 This _can_ be run in a chroot, but I will leave that exercise to you...

All you have to add to the unbound.conf file is the _module-config_ and
create a python section.
