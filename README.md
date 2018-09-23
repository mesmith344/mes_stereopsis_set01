# mes_stereopsis_set01
Ten thousand (10000) Blender-generated paired image files of random polyhedra at random distances from two different vantage points (left and right), simulating stereopsis (aka binocular vision). The image pairs are meant to be used to train a computer model to estimate distances via stereopsis, an ability which is a component of depth perception.

As such, the distance for each image pair is also provided as a dimensionless ratio of two distances, the distance to the object over the distance between the two vantage points. These values, called R, are provided both in the filenames of the image files themselves, and in the file r_values.csv

The generated paired image files have names in this format:

    iiiiiX_(RR.RRR).png

where
    iiiii  = a five digit index number with leading zeroes (00000, 00001, 00002, etc.)
    X      = either the letter L or R, meaning "left" or "right", indicating that the
             image was taken from the left or right vantage point.
    RR.RRR = a floating point number R, with 5 significant digits and a decimal point,
             indicating the approximate distance between the center of the two vantage
             points and the nearest surface of the polyhedron. This number is a dimensionless
             ratio of that distance and the distance between the two vantage points.
             Thus, R is given by:
             
                 R = Ds / Dv
                 
                 where
                     Ds is the approximate distance to the nearest surface of the polyhedron
                     Dv is the distance between the vantage points
                     
             NOTE: R need not always have two digits to the left of the decimal point and three
			             to the right of it. It could be in the form R.RRRR, RR.RRR, RRR.RR, etc.
			 
A few examples of typical paired image file names are:
    00007L_(15.947).png
    00007R_(15.947).png
    00135L_(2.3118).png
    00135R_(2.3118).png

If the distance between the vantage points Dv were known, as it would be in a robot with two
camera eyes, then Ds could be derived from R and Dv.

The reason the Ds distance is approximate is because the polyhedra have various random shapes,
and are not perfect spheres, (although many are close to being spheres) but this was simplified
by treating all of the polyhedra as spheres. The impact of these approximations are expected to
more significant at lower values of R (where the polyhedron size is close to Ds).

The polyhedra are varied in shape, color, size, light source direction, and light intensity, so that
the computer model learns that those are not relevant to stereopsis. Varying the size is especially
important; if the polyhedra size was constant, the model could use the apparent size to estimate
distance, instead of learning stereopsis.

The background color is also varied so that the model doesn't inadvertantly learn that backgrounds
are always a certain color.
