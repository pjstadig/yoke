Yoke
===

A simple, pure Ruby pairing script for git.  Yoke does not require rubygems or
any additional dependencies.  The first time it runs it will ask you for some
configuration details, which will be stored in ~/.yoke.

To see your current pairing status:

    ~$ yoke
    Missing group email config...
    >> Please enter a group email (i.e. 'safe@sonian.net')
    safe@sonian.net
    You entered 'safe@sonian.net', is this correct? [Y/n] 
    Currently solo

When you try to yoke yourself with a developer that it doesn't know about, it
will ask you for that person's name, which will be stored in ~/.yoke.

To yoke yourself into a pair:

    ~$ yoke paul jim
    Yoking...
    >> I don't know about jim, what is this person's name? 
    Jim Duey
    You entered 'Jim Duey', is this correct? [Y/n] 

    >> I don't know about paul, what is this person's name? 
    Paul Stadig
    You entered 'Paul Stadig', is this correct? [Y/n] 

    Currently pairing with jim (Jim Duey) and paul (Paul Stadig)

To unyoke yourself:

    ~$ yoke -u
    Unyoking...
    Currently solo

Alternatively, if yoke is invoked with the name 'unyoke' it will also perform
the unyoking:

    ~$ ln -s ~/src/yoke/bin/yoke ~/bin/unyoke
    ~$ unyoke
    Unyoking...
    Currently solo

Yoke stores everything in the local git repository config, so you can be yoked
differently in different git repositories.  It can also be used in any directory
in the git repository hierarchy:

    ~$ yoke paul jim
    Yoking...
    Currently pairing with jim (Jim Duey) and paul (Paul Stadig)
    ~$ cd some/sub/dir
    ~/some/sub/dir$ yoke
    Currently pairing with jim (Jim Duey) and paul (Paul Stadig)

When you yoke it modifies the config like so:

    ~$ yoke paul jim
    Yoking...
    Currently pairing with jim (Jim Duey) and paul (Paul Stadig)
    ~$ git config --get-regexp user.*
    user.name 'Jim Duey and Paul Stadig'
    user.email safe+jim+paul@sonian.net

_Note: yoke sorts the developers, so a Gravatar can be created for each unique
pairing.  :)_

Yoke also has a (non-interactive) short status that can be used in scripts.  The
short status is either the empty string, if going solo, or the pair name:

    ~$ yoke -s
    ~$ yoke paul jim
    Missing group email config...
    >> Please enter a group email (i.e. 'safe@sonian.net')
    safe@sonian.net
    You entered 'safe@sonian.net', is this correct? [Y/n] 
    Yoking...
    >> I don't know about jim, what is this person's name? 
    Jim Duey
    You entered 'Jim Duey', is this correct? [Y/n] 
    
    >> I don't know about paul, what is this person's name? 
    Paul Stadig
    You entered 'Paul Stadig', is this correct? [Y/n] 
    
    Currently pairing with jim (Jim Duey) and paul (Paul Stadig)
    ~$ yoke -s
    jim+paul

Installation
===

To install yoke, checkout the project, and link it somewhere on your path:

    ~$ git clone git@github.com:pjstadig/yoke.git
    Initialized empty Git repository in /home/paul/yoke/.git/
    remote: Counting objects: 5, done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 5 (delta 0), reused 0 (delta 0)
    Receiving objects: 100% (5/5), done.
    ~$ cd yoke/
    ~/yoke$ ln -s bin/yoke ~/bin/yoke
    ~/yoke$ ln -s bin/yoke ~/bin/unyoke
