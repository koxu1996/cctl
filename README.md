Updating public image:

```sh
docker build . -t cspr-cctl/release-1.5.6
docker tag cspr-cctl/release-1.5.6 koxu1996/casper-cctl:1.5.6
docker push koxu1996/casper-cctl:1.5.6
```

---

cctl
===============

Bash application to work with a **local** casper-node network.  Stripped down sucessor to nctl.

What is cctl ?
--------------------------------------

cctl is a bash utility that allows a developer to work with a local casper-node network.

Why cctl ?
--------------------------------------

Developers & community users need to spin up small local throwaway networks.  

Who uses cctl ?
--------------------------------------

CSPR network community.  This encompasses developers, validators, evaluators ... etc.

Setup
--------------------------------------

See [here](docs/setup.md) for setup details.

Usage
--------------------------------------

See [here](docs/usage.md) for usage details.

Installation
--------------------------------------

To install upon a virtual machine execute the one step install script. 

```
curl https://github.com/casper-network/cctl/blob/main/installer | bash
```
