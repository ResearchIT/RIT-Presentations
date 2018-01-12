# Tools & Methods for Reproducibile Research

Levi Baber : http://rit.las.iastate.edu

### Topics

* Why reproducibility & replicability matter
* Methods & Data
* Technical considerations
* Tools and resources available to help
* References

---

# Why reproducibility and replicability matter

Reproducibility:

Replicability:


Funding agencies & publishers
Effectiveness
Efficiency

---

# Methods and Data

Keeping close track of your research methods is a key
to producing reproducibile research, but so is your data.

Ideally, your published project should contain

---

# Technical considerations

Creating reproducibile research

Why is this so hard:
* Software dependencies are complicated
* Hardware differences
* Numerical reproducibility (floating point errors)

---

# Technical considerations

---

# Tools and resources available to help
### Project management with [OSF]

The Open Science Framework is a free and open source
tool that makes it easy for researchers to manage the full research cycle from
conception through publication.

Features include:
* Separate projects
* Collaboration with permission controls
* Wiki
* Data tracking
* Version control
* Integration with common tools like Box, GitHub, [figshare], etc.
* Ability to share results, raw data, generate [DOI]'s, etc.

For more information on how to use [OSF] at Iowa State: http://researchit.las.iastate.edu/open-science-framework

[OSF]:https://osf.io/
[figshare]: https://figshare.com
[DOI]: https://www.doi.org/

---

# Tools and resources available to help
### Package Management with [Spack]

A variety of tools are available to help make software installation
and management easier, with different focuses (ease of use, compatibility, reproducibility, etc.)

* [Spack] is the best option we've found for scientific reproducibility and ease of use
* Research IT has contributed several hundred packages so far
* We're currently installing a new software tree for the University based on Spack
* You can also use [Spack] in your home directory as an easy way to install
packages

---
# Tools and resources available to help
### Package Management with [Spack]

[Spack] creates a package spec & hash via a dependency graph for each package based on its
dependencies and configuration options.  You can use the spec to verify installations
on another system, or to share with colleagues attempting to reproduce your research.

The graph:
```
o  samtools
|\
| o  htslib
| |\
| | |\
| o | |  zlib
|  / /
| o |  xz
|  /
o |  ncurses
o |  pkg-config
 /
o  bzip2
```
---
# Tools and resources available to help
### Package Management with [Spack]

The spec:
```
Concretized
--------------------------------
vjstbcc  samtools@1.6%gcc@6.4.1 arch=linux-fedora25-x86_64
3e2nn4i      ^htslib@1.6%gcc@6.4.1 arch=linux-fedora25-x86_64
dmvuk2s          ^bzip2@1.0.6%gcc@6.4.1+shared arch=linux-fedora25-x86_64
wpfddzd          ^xz@5.2.3%gcc@6.4.1 arch=linux-fedora25-x86_64
ct3ya7h          ^zlib@1.2.11%gcc@6.4.1+optimize+pic+shared arch=linux-fedora25-x86_64
ovacyo2      ^ncurses@6.0%gcc@6.4.1 patches=4110a40613b800da2b2888c352b64c75a82809d48341061e4de5861e8b28423f,f84b2708a42777aadcc7f502a261afe10ca5646a51c1ef8b5e60d2070d926b57 ~symlinks~termlib arch=linux-fedora25-x86_64graph & hash
u6vweto          ^pkg-config@0.29.2%gcc@6.4.1+internal_glib arch=linux-fedora25-x86_64
```
While Spack is very good, it's not trivially reproducibile since there can
be dependencies on external packages and libraries that may vary by system.

[Spack]: http://spack.readthedocs.io/
---

# Tools and resources available to helpgraph & hash
### Containers


---


# References

* HARRIS, RICHARD. [RIGOR MORTIS]: How Sloppy Science Creates Worthless Cures, Crushes Hope, and Wastes Billions. BASIC BOOKS, 2017.
* FIRESTEIN, STUART. [FAILURE]: Why Science Is so Successful. Oxford University Press, 2016.
* Todd Gamblin, Matthew P. LeGendre, Michael R. Collette, Gregory L. Lee, Adam Moody, Bronis R. de Supinski, and W. Scott Futral. [The Spack Package Manager]: Bringing Order to HPC Software Chaos. In Supercomputing 2015 (SC’15), Austin, Texas, November 15-20 2015. LLNL-CONF-669890.
* Ivo Jimenez, Michael Sevilla, Noah Watkins, Carlos Maltzahn, Jay Lofstead, Kathryn Mohror, Andrea Arpaci-Dusseau and Remzi Arpaci-Dusseau. [The Popper Convention]: Making Reproducible Systems Evaluation Practical. In 2017 IEEE International Parallel and Distributed Processing Symposium Workshops (IPDPSW), 1561–70, 2017. https://doi.org/10.1109/IPDPSW.2017.157.

[RIGOR MORTIS]: http://www.worldcat.org/title/rigor-mortis-how-sloppy-science-creates-worthless-cures-crushes-hope-and-wastes-billions/oclc/958798220?referer=br&ht=edition
[FAILURE]: http://www.worldcat.org/title/failure-why-science-is-so-successful/oclc/965392747
[The Spack package manager]: https://www.computer.org/csdl/proceedings/sc/2015/3723/00/2807623.pdf
[The Popper Convention]: http://falsifiable.us

---

# Reproducibility / Replicability

* I went to several sessions on this topic
* Tools like [Spack] and [Singularity] will make this easier for the researchers
* Post upgrade testing - saw several tools, none of which were perfect / production ready
  * Can we use Singularity or Spack with CI to do this testing more effectively?
  * Purdue plans to release their [Testpilot] tool as open source
* Some concern about cpu arch & compiler differences
* Most concern about software stack and access to data & methods
* [Open Science Framework] got some small mention, but more focus on [Popper]

[Spack]:http://spack.readthedocs.io
[Singularity]: http://singularity.lbl.gov/
[Testpilot]: https://dl.acm.org/citation.cfm?doid=3152493.3152555

[Popper]:http://falsifiable.us/

---

# Containers

* Lot of attention for ease of software install & replicability
* [Docker], [Shifter], and [Charliecloud], but Singularity seems to have the most momentum
  * [Singularity]: No daemon, runs in userland, allows for untrusted containers, seems to have best MPI support
  * 2.4 adds support for [SCI-F] which provides better modularity
  * Could encrypted container images help meet compliance guidelines for standards like NIST800-171 ?
  * Future:
      * Checkpoint restarting that will be added as a layer to the sci-f file
      * Native Kubernetes support
      * OSX and Windows support
  * Nextflow which supports Docker and Singularity images looks interesting
* Portability for people moving from local compute to Xsede or other national resources is a big benefit

[Shifter]:https://github.com/NERSC/shifter
[Charliecloud]: https://github.com/hpc/charliecloud
[Singularity]: http://singularity.lbl.gov
[Docker]: https://www.docker.com/
[SCI-F]: http://containers-ftw.org/SCI-F/
[Nextflow]: https://www.nextflow.io/

---

# Interactivity / UX

### Interactivity
* Need for interactive jobs growing as data & visualization needs outgrow desktops
* Setting different expectations for cluster utilization (how much science got done vs. being 90% utilized)
* [MIT Lincoln Lab] runs independent servers for interactive use (much like BioCrunch, Speedy, etc.)

### User Experience / Training / Onboarding
* General consensus that HPC needs to be easier for new users
* Some ideas:
  * Paired up mentoring with experienced users
  * [Parallware] & [HPC Sonar] to help with code parallelization
* Developing a [HPC Carpentry] curriculum for new user training
  * Provide some incentive for completion (badges, higher queue priority, etc.)
* Growing demand for tools like Jupyter Notebook

[Parallware]: https://www.parallware.com/
[HPC Sonar]: http://www.hpcsonar.com/
[HPC Carpentry]:https://github.com/hpccarpentry
[MIT Lincoln Lab]: https://www.ll.mit.edu/about/about.html
---
