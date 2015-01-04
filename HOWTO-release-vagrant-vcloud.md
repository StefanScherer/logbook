# vagrant-vcloud

These are my steps to build a pre-release of vagrant-vcloud

## Merge pull requests

I have merged my branch (literally) into master and

```bash
git clone git@github.com:StefanScherer/vagrant-vcloud
cd vagrant-vcloud
git merge my
vi README.md
vi lib/vagrant-vcloud/version.rb
git add .
git push
```

## Build the gem

```bash
gem build vagrant-vcloud.gemspec
```

## Install `github-release` binary

If you have Go installed, you can just do:

```bash
go get github.com/aktau/github-release
```

## Build the GitHub release

Create a personal access token in your GitHub account. Then export it to environment `GITHUB_TOKEN`.

```bash
export GITHUB_TOKEN=abcef
github-release release --user StefanScherer --repo vagrant-vcloud --tag v0.4.4 --name "Kiah Royal" --description "Added PR#55 to reduce number of GET requests, added PR#104 to add second HDD and use vapp_name, added PR#109 to support TLSv1" --pre-release
github-release upload --user StefanScherer --repo vagrant-vcloud --tag v0.4.4 --name vagrant-vcloud-0.4.4.gem --file vagrant-vcloud-0.4.4.gem 
```

You can see the result at [my vagrant-vcloud releases](https://github.com/StefanScherer/vagrant-vcloud/releases).

## Install this gem

To install this gem on another machine you can use these steps:

```bash
vagrant plugin uninstall vagrant-vcloud
curl -o vagrant-serverspec-0.4.4.gem -L https://github.com/StefanScherer/vagrant-vcloud/releases/download/v0.4.4/vagrant-vcloud-0.4.4.gem
vagrant plugin install vagrant-vcloud-0.4.4.gem
```
