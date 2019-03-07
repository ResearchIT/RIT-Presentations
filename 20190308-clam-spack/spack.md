# Spack

<img src="images/spack.svg" alt="spack logo" title="Spack"/>

Conference Recap

Levi Baber

http://rit.las.iastate.edu
---
layout: true
class: footer-logo
---

## Software packaging with Spack

[Spack] is a flexible software packaging tool written in python, targeted towards research computing application.

Spack builds packages and creates module files in Lmod, tcl, or dotkit format (we use Lmod).

We've been using [Spack] to build scientific software for about a year and a half

Spack is growing quickly:
<img src="images/spack_contributions.png" alt="photo of cc meeting"/ style="width:40%;float:right;margin:5px">
Currently contains ~3K packages

We got some recoginition during a couple different BoF sessions at SC18 for our contributions
<img src="images/gssi_bof.jpg" alt="photo of cc meeting"/ style="width:50%;float:left;margin:5px">

[Spack]: https://spack.io
---

## Getting Started

Using spack is (generally) as simple as cloning the repo, sourcing a setup script, and running

Few dependencies to get started (a compiler, curl, tar, etc.)

```
yum -y install git python3 gcc gcc-c++ \
gcc-gfortran curl gnupg2 sed patch \
unzip gzip bzip2 \
findutils make vim \
git clone https://github.com/spack/spack.git
. spack/share/spack/setup-env.sh
spack install r
```
---

## Digging a little deeper

The core of spack is the concretizer.  The concretizer is what takes an abstract
specification (spec) like `spack install r` and using a directed acyclic graph [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) algorithm, produces a 'concrete' spec, which 
includes all of the details like which version of r, which options (variants), which version
of all the dependencies, etc.

To get an idea of 
