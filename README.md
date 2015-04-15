# TraPPE-UA and HH-Alkane for GROMACS

James W. Barnett
jbarnet4@tulane.edu

This is a [GROMACS](http://www.gromacs.org) implementation of the TraPPE-UA
force field with HH-Alkane modifications for the C-OW cross interactions. The
modifications can optionally be removed (see below). To install, place
the trapepua.ff folder where GROMACS can find it (like in your GMXLIB directory).
The TIP4P2005 water model is included, and is the only water model that should
be used with the HH-Alkane modifications. If you use this implementation, please
read and cite the following references.

* [M.G. Martin, and J.I. Siepmann, J. Phys. Chem. B, 102, 2569 (1998).](http://dx.doi.org/10.1021/jp972543+)
* [M. G. Martin and J. I. Siepmann, J. Phys. Chem. B 103, 4508 (1999).](http://dx.doi.org/10.1021/jp984742e)
* [B. Chen, J.J. Potoff, and J.I.  Siepmann, J. Phys. Chem. B 105, 3093 (2001).](http://dx.doi.org/10.1021/jp003882x)
* [H.S. Ashbaugh, L. Liu, and L.N. Surampudi. J.Chem. Phys. 135, 054510 (2011).](http://dx.doi.org/10.1063/1.3623267)
* [J. L. F. Abascal and C. Vega, J. Chem. Phys 123 234505 (2005).](http://dx.doi.org/10.1063/1.2121687)

## A few notes

* TrAPPE-UA recommends that a cutoff of 1.4 nm should be used for LJ interactions.
* TraPPE-UA recommends using Ewald summation for long-range electrostatic
  calculations. You should probably use Particle-Mesh Ewald.
* The number of exclusions for intramolecular non-bonded interactions should be
  set to 3 for TraPPE-UA (intramolecular interactions separated by four or more bonds use the
same potential as intermolecular interactions).
* Intramolecular 1-4 LJ and Coulomb interactions are excluded in TraPPE-UA, so you will need
  to remove the `[ pairs ]` list for a molecule. `gen-pairs` is by default "no"
under `[ defaults ]` and no `[ pairtypes ]` section exists, so you'll get an error
about any `[ pairs ]` section.
* When constructing a new molecule for force field, you'll need to use `[
  constraints ]` instead of the normal `[ bonds ]` for the 1-2 bonded interactions.
Constraints type 1 is a bond of fixed length, which is what the TraPPE-UA force
field specifies.
* You can create Residue Template Files (.rtp) to be used with pdb2gmx. Note
  that right now pdb2gmx does not recognize `[ constraints ]`. A workaround is to
simply name the section `[ bonds ]` in the .rtp file and manually fix your generated topology file
by changing the `[ bonds ]` section to `[ constraints ]`. If you leave it as `[ bonds
]` you'll get an error, since there is no `[ bondtypes ]` in the force field (only
`[ constrainttypes ]`).
* You can choose not to use the HH-Alkane modifications by adding `define =
  -DNO_HHALK_MODS` to your mdp files, thus using the original TraPPE-UA force
  field.
* You can choose to turn the fixed bonds (constraints) into regular bonds by using `define =
  -DFLEXIBLE` in your mdp files. This includes the water model.

## Disclaimer

I've done my best in transcribing and converting the parameters for usage with
GROMACS. That said, it is up to the user to ensure that the parameters are
correct and that simulations are set up according to the methods presented in
the papers above. There are several other TraPPE papers out there with more
parameters for different types of molecules - I haven't implemented those yet.
This current implementation only includes linear and branched alkanes and
alcohols. Be sure to check out the [TraPPE website](http://siepmann6.chem.umn.edu/trappe/index.php).
