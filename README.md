This is a [GROMACS](http://www.gromacs.org) implementation of the TraPPE-UA
force field with HH-Alkane modifications for the C-OW cross interactions. Place
the trapepua.ff folder where GROMACS can find it (like in your GMXLIB directory).
The TIP4P2005 water model is included, and is the only water model that should
be used with the HH-Alkane modifications. Note that 1.4 nm cutoffs should be
used with this force field. If you use this implementation, please read and cite
the following references.

* [M.G. Martin, and J.I. Siepmann, J. Phys. Chem. B, 102, 2569 (1998).](http://dx.doi.org/10.1021/jp972543+)
* [M. G. Martin and J. I. Siepmann, J. Phys. Chem. B 103, 4508 (1999).](http://dx.doi.org/10.1021/jp984742e)
* [B. Chen, J.J. Potoff, and J.I.  Siepmann, J. Phys. Chem. B 105, 3093 (2001).](http://dx.doi.org/10.1021/jp003882x)
* [H.S. Ashbaugh, L. Liu, and L.N. Surampudi. J.Chem. Phys. 135, 054510 (2011).](http://dx.doi.org/10.1063/1.3623267)
* [J. L. F. Abascal and C. Vega, J. Chem. Phys 123 234505 (2005).](http://dx.doi.org/10.1063/1.2121687)

I've done my best in transcribing and converting the parameters for usage with
GROMACS. That said, it is YOUR job to make sure that they are correct and that
there are no errors. It is also YOUR job to read the above references and use
this force field and it's modifications in the correct way. 

James W. Barnett
jbarnet4@tulane.edu
