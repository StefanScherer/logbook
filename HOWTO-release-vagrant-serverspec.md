# vagrant-serverspec

These are my steps to build a pre-release of vagrant-serverspec

## Merge pull requests

Merge a brilliant good PR into my master branch:

```bash
git remote add vvchik https://github.com/vvchik/vagrant-serverspec
git fetch vvchik
git merge vvchik/ErrorhandlingByAthak
git push
```

## Build the gem

```bash
rake gem:build
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
github-release release --user StefanScherer --repo vagrant-serverspec --tag v0.5.0 --name "serverspec v2 support" --description "Added serverspec v2 support from vvchik and exit status from athak" --pre-release
rake gem:build
github-release upload --user StefanScherer --repo vagrant-serverspec --tag v0.5.0 --name vagrant-serverspec-0.5.0.gem --file pkg/vagrant-serverspec-0.5.0.gem 
```

You can see the result at [my vagrant-serverspec releases](https://github.com/StefanScherer/vagrant-serverspec/releases).

## Install this gem

To install this gem on another machine you can use these steps:

```bash
vagrant plugin uninstall vagrant-serverspec
curl -o vagrant-serverspec-0.5.0.gem -L https://github.com/StefanScherer/vagrant-serverspec/releases/download/v0.5.0/vagrant-serverspec-0.5.0.gem
vagrant plugin install vagrant-serverspec-0.5.0.gem
```
