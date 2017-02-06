# vagrant-desktop

Self-installing vagrant-based linux desktop for windows.


## Installation

* Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads), or a virtualization environment of your choice, though I recommend Virtualbox.
* Install [Vagrant](https://vagrantup.com)
* Install the required Vagrant plugins:
    
    ```shell
    $ vagrant plugin install vagrant-hosts-provisioner
    $ vagrant plugin install vagrant-hosts
    ```


## Usage 

```shell
$ vagrant up
```

## Additional notes

vagrant-desktop currently uses (sadly, hardcoded) my [version of dotfiles](https://github.com/mgla/dotfiles). You can easily replace it with your own version or simply comment it out, though.
