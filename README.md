# sci-titan.unitn.it Documentation

Documentation for sci-titan.

This repo contains the markdown sources of the manfile installed in the system.
Please announce new man file `banner.net` and update manually `/usr/local/banner.net`.

All files will be under **7.Miscellanea**.

Please prefix all files with `titan-`, thse are the **only files that are compiled**

## List of files

 * **titan-intall**: guide on how to setup the system from scratch
 * titan-tensorflow: TBD
 * titan-torch: TBD
 * titan-sshfs: TBD
 * titan-cuda: TBD
 * titan-caffe: TBD

## Compile and install
`rake` and `pandoc` are required for compilation.

Use Rakefile for compilation and installation:
```
rake
```
will compile all markdown and md files in manfiles.
```
rake install
```
will install manuals in `/usr/local/man/man7` and will trigger `mand` refreshing.

To visualize a compiled manfile without installing it:
```
man -l titan-file.7
```

## License

Guide and man files are released under GPL License.

Matteo Ragni and Paolo Bosetti 2016, University of Trento.
