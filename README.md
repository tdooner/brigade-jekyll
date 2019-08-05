# Brigade Jekyll Meetup Demo
This is a demo repo of building a Jekyll site for your Brigade.

## Installation
```
bundle install

```
generate a deploy key:
1. generate the key:
ssh-keygen -m PEM -t rsa -b 4096 -C "circleci" -f circleci
(no passphrase)

copy the private key into CircleCI
circleci project > project settings > ssh permissions > add ssh key

copy the public key into github
github repo > Settings > Deploy Keys
