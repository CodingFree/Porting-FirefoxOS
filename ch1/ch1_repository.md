# Prepare your repository #
## Warning 1 ##
The following manifest is not part of the main repository of B2G (yet).

- TODO: Merge needed manifest: [Bugzilla: 1211870](https://bugzilla.mozilla.org/show_bug.cgi?id=1211870)

Manifests mentioned below can be found on [github.com/cm-b2g](https://github.com/cm-b2g/).

## Warning 2 ##
Downloading all of these repositories, many of which are **several gigabytes**, will take a while so we recommend doing this overnight on a slow connection, or just before lunch on a faster connection.

Try to not interrupt the download, it may break your repostories or it may result in strange errors during the compilation eventually.

## Setup ##

We have several useful tools for building Firefox OS, all contained in a single repository. Download these tools via git to create your working directory:

    git clone https://github.com/cm-b2g/B2G.git && cd B2G

Now we need to download the source code:

    ./config.sh cm-porting

The **config.sh** initializes the repo tool using the **base-l-cm.xml** manifest found in the **b2g-manifest** repository. This XML file is a list of repositories needed to build Firefox OS. The config.sh will download those repositories.

*This step also creates a **.config** file which you will edit later.*