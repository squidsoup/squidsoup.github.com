---
layout: post
title: "Provisioning Oracle Java on Ubuntu with Vagrant and Puppet"
description: ""
category: devops 
tags: [puppet, vagrant, java, ubuntu]
---
{% include JB/setup %}


![Vagrant](http://www.vagrantup.com/images/logo_vagrant-81478652.png)


In the course of working on my current project, a clinical decision support service in Clojure, I needed to introduce Memcached as a kv store for CCDA documents (XML). When you reach the point of having to introduce external services as dependenies in your project, it's a good time to think about moving your local development environment to [Vagrant](http://www.vagrantup.com/). Given that most web projects involve a database of some kind, you'll most likely want to be doing this from the outset.

Vagrant allows you to easily spin up a VM and provision it using [Chef Solo](http://docs.vagrantup.com/v2/provisioning/chef_solo.html), [Ansible](http://docs.vagrantup.com/v2/provisioning/ansible.html) or [Puppet](http://docs.vagrantup.com/v2/provisioning/puppet_apply.html). One of the biggest wins with Vagrant is that you can effectively mirror your production and development environments, ensuring consistency. The provisioning tools are also a big win, and make it easy for another developer to get up and running quickly without having to manually install services. As your infrastructure to support your application grows, you can later consider introducing a Puppet Master or Chef Server.

### Puppet provisioning in Vagrant

In order to enable puppet provisioning, uncomment the following in your projects *Vagrantfile*:

{% highlight ruby %}
# Vagrantfile
config.vm.provision :puppet do |puppet|
   puppet.manifests_path = "manifests"
   puppet.manifest_file  = "default.pp"
end
{% endhighlight %}
 
#### Provisioning Oracle Java

Unfortunately, the Oracle JDK isn't available be default in Ubuntu and must be installed from a PPA. Automated installation is also further complicated by the Oracle Java7 installer prompting for user acceptance of the license agreement.

The following puppet manifest adds the webupd8 java ppa, authorises the ppa key, updates the apt package and key stores, and finally installs oracle-java7.

{% highlight puppet %}
# default.pp - puppet provisioning

  # define a variable for the webupd8team ppa sources list
  $webupd8src = '/etc/apt/sources.list.d/webupd8team.list'
 
  # Ensure the sources list exists
  # See http://stackoverflow.com/a/10463734/428876 for sharing files and configuring a puppet fileserver
  file { $webupd8src:
    content => "deb http://ppa.launchpad.net/webupd8team/java/ubuntu lucid main\ndeb-src http://ppa.launchpad.net/webupd8team/java/ubuntu lucid main\n",
  } ->
  # Authorise the webupd8 ppa
  # At the time of writing this key was correct, but check the PPA page on launchpad!
  # https://launchpad.net/~webupd8team/+archive/java
  exec { 'add-webupd8-key':
    command => 'apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886',
    path => '/usr/bin/',
  } ->
  # update the apt keystore
  exec { 'apt-key-update':
    command => 'apt-key update',
    path => '/usr/bin/',
  } ->
  # update apt sources 
  exec { 'apt-update':
    command => 'apt-get update',
    path => '/usr/bin/',
  } ->
  # set license acceptance with debconf
  # thanks to Gert van Dijk on http://askubuntu.com/a/190674
  exec { 'accept-java-license':
    command => '/bin/echo /usr/bin/debconf shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections;/bin/echo /usr/bin/debconf shared/accepted-oracle-license-v1-1 seen true | sudo /usr/bin/debconf-set-selections;',
  } ->
  # finally install the package
  # oracle-java6-installer and oracle-java8-installer also available from the ppa
  package { 'oracle-java7-installer':
    ensure => present,
  }
{% endhighlight %}

Finally, if your VM is already running, run the following to have vagrant kick off the provisioning:

{% highlight bash %}
$ vagrant provision
{% endhighlight %}

Vagrant will also run provisioning after a **vagrant up**.


#### Less bloody-minded approaches

A simpler approach is to just use the OpenJDK locally, even if you're deploying to the Oracle JVM in production. In practice, I suspect there is no harm in doing this, but I feel more comfortable having parity with production.  

{% highlight puppet %}
package { 'openjdk-7-jdk':
  ensure => present,
}
{% endhighlight %}

Alternatively, you could use Redhat linux, which has the Oracle JDK available in the yum repos.

If anyone has suggestions for improving my puppet-foo, by all means leave a comment. :)
