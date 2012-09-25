archblocks
==========

ArchBlocks - a minimal, modular, manual install framework

## WHAT:

ArchBlocks is a very lightweight framework for creating quick, modular, *non-interactive* Arch Linux install scripts tailored to specific systems. It is accessible via a single quick curl downloadable script (from, for example, github).

## WHERE:

Example repo at https://github.com/altercation/archblocks

## EXAMPLE:

    curl -sfL http://git.io/ > install.sh
    sh install.sh

(this then sources the blocks of code remotely and configures the system based on the specific blocks called and variables set in its configuration)

## WHAT IT ISN'T:

ArchBlocks is not an interactive general purpose script that asks you what you'd like. You *must* customize it (or its blocks) as much as any other install script. ArchBlocks simply makes this process easier to maintain as a single project that is applicable for multiple systems.

## WHY:

Many somewhat experienced Arch users end up building lightweight install scripts to set up their systems. I've been wanting to modularize my own install scripts such that multiple, different system types (laptop/server/desktop/headless) can reuse most of the common elements easily and swap out blocks of code as needed.

AND YET it's easy to make something like this far too complex. To paraphrase the Ruby community: Arch is Simple so Our Utilities Are Simple. ArchBlocks kickstarts off a *single* "configuration" script and loads blocks from a *single* directory (remote or local, doesn't matter).

(I've previously written extensive additions to AIF before it was frozen in carbonite, and that experience convinced me of the value of non-interactive, simple install script based approach).

## NO REALLY, WHY NOT JUST MONOLITHIC INSTALL SCRIPTS, WHY MODULAR:

There is install code that may be impacted by changes to Arch, or I sometimes want to improve the way I handle some part of the installation. This may impact multiple systems. Rather than update and maintain five different manual install scripts, modular is better approach. A simple example is the various `NETWORK_*` blocks. I can keep using the default network setup method in most of my scripts and use a light weight / minimal network install method by just swapping out a block. This minimal install script can be revised and all systems that I install with it in future will make use of the revision.

## EXAMPLE:

curl -sfL http://git.io/ > install.sh
sh install.sh

## DETAILS:

Each system I install gets a single config file (the "tau" script in the example above is a laptop). This script loads a few very lightweight helper functions (maintained in a lib file for reuse across "config" scripts) and then loads blocks from the (surprise) blocks directory (local or remote). These blocks are almost all just simple blocks of bash script. The only exceptions should be very clear from the example: there are a few functions that are very specific to the filesytem configuration that must be sprinkled throughout the code. These functions and their intended sequence in the script are easily identified by name such as FILESYSTEM_PRE_BASEINSTALL (in this case FILESYSTEM_PRE_BASEINSTALL is either a null function or does something as defined in the FILESYSTEM block).

A config script (the only script you need to manually execute) looks like this:

That's it, really. Nothing fancy. Comprehensible, reusable, modular.

If you want to use something like this, fork away.


