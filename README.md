# crunchy-docdynamo
Documentation generation engine for crunchy-containers. Source code for the output documentation is adoc (asciidoc) files.

## Setting up the Example Environment
This repository contains a Vagrantfile for building a VM that will automatically pull in the most recent docDynamo and crunchy-containers code from GitHub. **However, until the project is stabilized, the last known working commit from crunchy-containers will be used.**

1. Get the crunchy-docdynamo from Github.
2. cd to the directory on your local machine and run the following:

```
vagrant up
vagrant ssh
```

It will take several minutes to build the VM but once built, the VM can remain running and used continuously.

## Building the Docs
Inside the Vagrant box, running the build script will generate the XML files required by docDynamo. All XML that are specified in the build script can be rebuilt using:

```
/crunchy-docdynamo/./build-docdynamo-docs.sh all create
```

To only generate a specific file or one that is not listed yet in the build script, then use the file name instead of "all"

```
/crunchy-docdynamo/./build-docdynamo-docs.sh containers create
```

Next run docDynamo to build all the HTML, PDF and Markdown files specified in the doc/manifest.xml directory:

```
/docdynamo/bin/docdynamo --doc-path=/crunchy-docdynamo/doc
```

To generate a specific formate, use the --out option. For example, the following will build a markdown file:

```
/docdynamo/bin/docdynamo --doc-path=/crunchy-docdynamo/doc --out=markdown
```

All output will be written to the doc/output directory.

## Refreshing from the Crunchy Containers repository
After having built the VM, if newer source documents have been committed to crunchy-containers, they can be pulled into the VM by performing the following inside the VM.

```
sudo rm -rf /crunchy-containers
sudo git clone https://github.com/CrunchyData/crunchy-containers.git /crunchy-containers
```

If new adoc files have been added, then edit the manifest.xml file and add the name of the new file to the source-list section and as a render-source to the render sections as appropriate.

Then follow the instructions under the section **Building the Docs** above.
