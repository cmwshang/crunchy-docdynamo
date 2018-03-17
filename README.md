# crunchy-docdynamo
Documentation generation engine

## Setting up the Environment
1. Get the crunchy-docdynamo from Github.
2. cd to the directory on your local machine and run

```
vagrant up
vagrant ssh
```

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
