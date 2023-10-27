# ldmx-genie-splines

Repository for holding GENIE splines used in LDMX eN studies.

### Creating splines

Splines can be created using the `gmkspl` command like so:

```
gmkspl -p 11 -t 1000220500 -o
gxspl_emode_Ti50_G18_02a_02_11b.xml -n 30 -e 10 --tune
G18_02a_02_11b --event-generator-list EM
```

where

  * `-p` option is the pdg code for the probe (11=electron)
  * `-t` option is the nuclear pdg code for the target, of the form
    100ZZZAAA0 where Z is the proton number, and A is the mass number
    (so, 1000220500 --> Z=22, A=50 --> Ti50)
  * `-n` is the number of knots in the spline: default is 30? that's
    what works at least
  * `-e` is the maximum energy to use in the spline (here 10 GeV)
  * `--tune` is used to specify the tune to calculate (see
    https://hep.ph.liv.ac.uk/~costasa/genie/tunes.html)
  * `--event-generator-list` specifies the interaction list to
    consider (here, `EM`)
	
Note with the `ldmxsw` environment setup, one can prepend `ldmx` to
the `gmkspl` command above.

### Combining splines

GENIE provides the `gspladd` utility for combining spline XML files
together:

```
gspladd -d GENIE_v3_04_00 -o gxspl_emode_GENIE_v3_04_00.xml
```

where `-d` specifies the directory (or directories, comma separated)
where the spline XML files are found, and `-o` specifies the combined output
spline file to create.

When new spline files are created for a given version of GENIE, it's
best to combine them. (There should be no issue combining splines with
different tunes, as the XML file tracks which tune each spline belongs to.)
