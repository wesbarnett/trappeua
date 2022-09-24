# TraPPE-UA and HH-Alkane for GROMACS

James W. Barnett
jbarnet4@tulane.edu

This is a [GROMACS](http://www.gromacs.org) implementation of the TraPPE-UA
force field with optional HH-Alkane modifications for the C-OW cross
interactions (see below). 

To install, place the `trapepua.ff` folder where GROMACS can find it, like in
a directory pointed to by the environmental variable `GMXLIB`:

    git clone https://github.com/wesbarnett/trappeua.git
    cd trappeua
    cp -r trappeua.ff $GMXLIB/

Then include `trappeua.ff/forcefield.itp` in your topology file like you do for other
forcefields. An example topology file is found
[here](https://gist.github.com/wesbarnett/479925865f9575464165).

The TIP4P2005 water model is included, and is the only water model that should
be used with the HH-Alkane modifications. Ethanol is also included as solvent
(HH-Alkane modifications don't apply here). 

There are several git branches in this repo, some with personal modifications to
the force field. The only branch that has the official TraPPE-UA parameters
along with the HH-Alkane modifications is the `master`.

Lastly, if you use this implementation, please read and cite the following references.

* [M.G. Martin, and J.I. Siepmann, J. Phys. Chem. B, 102, 2569 (1998).](http://dx.doi.org/10.1021/jp972543+)
* [M. G. Martin and J. I. Siepmann, J. Phys. Chem. B 103, 4508 (1999).](http://dx.doi.org/10.1021/jp984742e)
* [B. Chen, J.J. Potoff, and J.I.  Siepmann, J. Phys. Chem. B 105, 3093 (2001).](http://dx.doi.org/10.1021/jp003882x)
* [H.S. Ashbaugh, L. Liu, and L.N. Surampudi. J.Chem. Phys. 135, 054510 (2011).](http://dx.doi.org/10.1063/1.3623267)
* [J. L. F. Abascal and C. Vega, J. Chem. Phys 123 234505 (2005).](http://dx.doi.org/10.1063/1.2121687)

## A few implementation notes

* TrAPPE-UA recommends that a cutoff of 1.4 nm should be used for LJ interactions.
* TraPPE-UA recommends using Ewald summation for long-range
electrostatic calculations. You should probably use Particle-Mesh Ewald.
* The number of exclusions for intramolecular non-bonded interactions should be
  set to 3 for TraPPE-UA (intramolecular interactions separated by four or more
bonds use the same potential as intermolecular interactions). This is pretty
typical.
* Intramolecular 1-4 LJ and Coulomb interactions are excluded in TraPPE-UA, so
  you will need to remove the `[ pairs ]` list for a molecule. `gen-pairs` is by
default "no" under `[ defaults ]` and no `[ pairtypes ]` section exists, so
you'll get an error about any `[ pairs ]` section.
* Currently two .rtp files are included in the force field directory. Only a few
  molecules are present at the time. Note that you can easily create linear
alkanes / alcohols by specifying the end groups with residue `CH3` and the interior groups
as residue `CH2`, as long as each atom has the name `C`.

**NOTE**: Please read the following carefully.

* You should set constraints to `all-bonds`, since TraPPeUA bonds are fixed. If
  you do not, bonds will be flexible and an arbitrarily large spring constant is
set in the force field.
* You can choose use the HH-Alkane modifications by adding `define =
-DWITH_HHALK_MODS` to your mdp files, thus using the original TraPPE-UA force
field. The HHALK modifications only affect water-oxygen carbon cross
interactions.


## Disclaimer

I've done my best in transcribing and converting the parameters for usage with
GROMACS. That said, it is up to the user to ensure that the parameters are
correct and that simulations are set up according to the methods presented in
the papers above. There are several other TraPPE papers out there with more
parameters for different types of molecules - I haven't implemented those yet.
This current implementation only includes linear and branched alkanes and
alcohols. Be sure to check out the [TraPPE website](http://trappe.oit.umn.edu/).
