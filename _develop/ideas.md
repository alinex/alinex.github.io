Ideas and Comments
=================================================

This document collects some Ideas of what may be developed and what may be used
in the further packages and versions.


Generators
-------------------------------------------------

It's purpose is mainly to make callback hell better. The same is true with the
use of CoffeeScript and Async.js or some Promise Framework.

Because generators are not widely supported it is not possible at the moment
to use them in production code.
I personally will wait till they are everythere supported and give me some
real benefit.


Webserver Framework
-------------------------------------------------

Based on nodes http module some other frameworks help to come to a full blown
web application.

### [ExpressJS](http://expressjs.com/)

Express is a minimal and flexible node.js web application framework, providing
a robust set of features for building single and multi-page, and hybrid web
applications.

### [Koajs](http://koajs.com/)

Next generation web framework like express implemented with generics. This
makes it only accessible with node 0.11 and --harmony flag or 0.12 version.
At the moment of this writing the stable coffeeScript is also impossible to work
with generators.


Icon Sets
-------------------------------------------------

It is possible to use PNG, Fonts or SVG graphics.

### PNG Icons

Have to be loaded each on it's own, not scalable.

### Icon Font

Only monochrome but loads at once and are scalable but problems with antialiasing
and Retina display.

### SVG Icons

Best choice but not for older browsers before MSIE 9.
