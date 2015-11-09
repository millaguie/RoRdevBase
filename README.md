##  RoR development base 

This is just an example of how to implement a devstack for a RoR application using Vagrant and chef.

### Step 1: Install some nice stuff
First you need VirtualBox, if you don't want to spend extra time tunning vagrant use 4 series of [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

If you're running Mac OS X, you must also install Xcode.

Now you can install [Vagrant](http://www.vagrantup.com/downloads) for your operating sysmte.

If you are not running MacOS, you'll probably need to install [NFS](http://en.wikipedia.org/wiki/Network_File_System) on your computer to work. Running on Linux will require ```nfs-kernel-server``` installation.

### Step 2: Check Out this stuff
Just check out all this code
    git clone https://github.com/millaguie/RoRdevBase.git
and create a directory for your own code
    mkdir mybloodystuff
    cd mybloodystuff
    git co https://github.com/$USER/$PROYECT.git 

### Step 3:  Deploy your brand new development stack
Just run `vagrant up` and grab a nice cup of coffe with cookies.  This will take a while.

And then you are ready to get the fun:
vagrant ssh (to get into the development machine)
cd /vagrant/mybloodystuff (to get into your source code)
bundle  (well... you know...)
rails s (well... you probably also know...(
And you can check your rails server at your own http://localhost:3000

