# Copyright (C) 2006, 2007, 2008, 2009 Free Software Foundation, Inc.
#
# Copying and distribution of this file, with or without modification,
# are permitted in any medium without royalty provided the copyright
# notice and this notice are preserved.
# 
# To use these targets, first do (one time only):
# - ln -s ../*.texi .
# - copy gendocs.sh and gendocs_template from texinfo/util here.
# - then try make a, then make b, then make c
# - if all goes well, see info at end for updating the web.
# - also update gnulib/doc.

# check that makeinfo is happy.  (Best error messages, etc.)
a:
	makeinfo standards

# build everything.
b:
	gendocs.sh standards "GNU coding standards"

# fix cross-manual xrefs.
# be nice to do this more cleanly later, but needs Texinfo config file, etc.
c:
#
# new-style gendocs.sh, but special location.
	perl -pi -e 's,href="(maintain).html,href="/prep/\1/\1.html,g' manual/standards.html 
	perl -pi -e 's,href="\.\./(maintain)/,href="/prep/\1/html_node/,g' manual/html_node/*.html
#
# new-style gendocs.sh
	perl -pi -e 's,href="\.\./texinfo/,href="/software/texinfo/manual/texinfo/html_node/,g' manual/html_node/*.html
	perl -pi -e 's,href="\.\./autoconf/,href="/software/autoconf/manual/html_node/,g' manual/html_node/*.html
#
# makeinfo bug in toc creation of standalone html (for --version/help nodes).
	perl -pi -e 's,#_00,#g_t_00,' manual/standards.html
#
	gzip -9f <manual/standards.html >manual/standards.html.gz
	cd manual/html_node && tar czf ../standards.html_node.tar.gz -- *.html
#
	(cd manual && tar cjf ../s.tbz .)
# then unpack s.tbz in a cvs checkout of www/prep/standards, cvs add any
# new files, cvs remove any old ones, and cvs commit everything.
#
# to copy to a local checkout ($gw).
#	cd manual && for f in `find -type f`; do \
#	  cmp -s $$f $$gw/prep/standards/$$f \
#	  || \cp -f $$f $$gw/prep/standards/$$f -v; done
