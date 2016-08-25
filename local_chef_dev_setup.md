## Local Development Setup for Chef

### Install git

Linux: `sudo yum install git`
Mac: [Download](http://git-scm.com/download/mac)
Windows: [Download](http://git-scm.com/download/win)
- posh-git: A set of PowerShell scripts that provide Git/PowerShell integration
- [Download posh-git](https://github.com/dahlbyk/posh-git)



### Download and install

[chef-dk](https://downloads.chef.io/chef-dk)

[virtual box](https://www.virtualbox.org/wiki/Downloads)

[vagrant](http://www.vagrantup.com/downloads.html)

### Use these instructions to install the chefdk
[docs.chef.io installation instructions](https://docs.chef.io/install_dk.html)

### If you are not able to run chef-dk check out this blog post by Mischa Taylor:
[Set Up a Sane Ruby Cookbook Authoring Environment for Chef on Mac OS X, Linux and Windows](http://misheska.com/blog/2013/12/26/set-up-a-sane-ruby-cookbook-authoring-environment-for-chef/)

### Don't forget to set the embedded ruby shipped with Chef first in your PATH
`echo 'export PATH="/opt/chefdk/embedded/bin:$PATH"' >> $HOME/.bash_profile`

### Make sure ruby is installed and working
`which ruby && ruby -v`

### Install kitchen-vagrant gem if not already present
`chef gem install kitchen-vagrant`

### Install Text Editor

[atom](https://github.com/atom/atom)
- atom plugins:
- vim-mode
- language-chef
- linter
- linter-foodcritic
- linter-rubocop
- remote-sync
- linter-package-json-validator
- colorful-json

[sublime text](https://www.sublimetext.com/)

[VisualStudio Code](https://code.visualstudio.com/download)

## Local cookbook development workflow

### create new cookbook using the `chef generate` command
`chef generate cookbook your-cookbook`

### list test-kitchen VM's
`kitchen list`

### use Berkshelf to download dependency cookbooks
`berks install` if applicable

### Modify .kitchen.yml to specify platforms, run-list, verifier,
```
---
driver:
  name: vagrant

provisioner:
  name: chef_zero

# Uncomment the following verifier to leverage Inspec instead of Busser (the
# default verifier)
# verifier:
#   name: inspec

platforms:
  - name: ubuntu-14.04
  - name: centos-7.1

suites:
  - name: default
    run_list:
      - recipe[your-cookbook::default]
    attributes:
```

### Modify .kitchen.yml to add cpu/memory and port forwarding if needed
```
driver:
  network:
  - ["forwarded_port", {guest: 8080, host: 8080}]
  customize:
    memory: 2048
    cpus: 2
```

### Show all kitchen instances
`kitchen list`

### Run VM for CentOS 7.1 and converge with configuration
`kitchen converge centos`

### see git status of files added and modified
`git status`

### add all files
`git add .`

### commit all changes
`git commit -m "initial commit of cookbook"`

### link to Chef tutorials
[Chef tutorials](https://learn.chef.io/tutorials/)
