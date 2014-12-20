# How to develop vagrant plugins

* https://docs.vagrantup.com/v2/plugins/packaging.html

## Install RVM

* https://rvm.io/rvm/install

```bash
curl -sSL https://get.rvm.io | bash -s stable --ruby
```

Add rvm to `~/.bash_profile`

```bash
if [ -e $HOME/.rvm/scripts/rvm  ]; then
  source ~/.rvm/scripts/rvm
fi
```

## Clone your vagrant plugin

```bash
git clone git@github.com:athak/vagrant-serverspec
cd vagrant-serverspec
bundler
```
