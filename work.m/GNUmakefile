# Copyright (C) 2006, 2007, 2008 Free Software Foundation, Inc.
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

# check that makeinfo is happy.
a:
	makeinfo maintain

# build everything.
b:
	gendocs.sh maintain "Information for maintainers of GNU software"

# fix cross-manual xrefs.
# be nice to do this more cleanly later, but needs Texinfo config file, etc.
c:
# new-style gendocs.sh
	perl -pi -e 's,href="(texinfo|emacs).html,href="/software/\1/manual/\1/\1.html,g' manual/maintain.html 
	perl -pi -e 's,href="\.\./(texinfo|emacs)/,href="/software/\1/manual/\1/html_node/,g' manual/html_node/*.html
#
# new-style gendocs.sh, but special location.
	perl -pi -e 's,href="(standards).html,href="/prep/\1/\1.html,g' manual/maintain.html 
	perl -pi -e 's,href="\.\./(standards)/,href="/prep/\1/html_node/,g' manual/html_node/*.html
#
# old-style (and not updated for ages)
	perl -pi -e 's,href="(cvs).html,href="/software/\1/manual/html_mono/\1.html,g' manual/maintain.html 
	perl -pi -e 's,href="\.\./(cvs)/,href="/software/\1/manual/\1/html_node/,g' manual/html_node/*.html
#
# elisp
	perl -pi -e 's,href="elisp.html,href="/software/emacs/manual/html_mono/elisp.html,g' manual/maintain.html 
	perl -pi -e 's,href="\.\./elisp/,href="/software/emacs/manual/html_node/elisp/,g' manual/html_node/*.html
#
	gzip -9f <manual/maintain.html >manual/maintain.html.gz
	cd manual/html_node && tar czf ../maintain.html_node.tar.gz -- *.html
#
	cd manual && tar cjf ../m.tbz .

# then unpack m.tbz in a cvs checkout of www/prep/maintain, cvs add any
# new files, cvs remove any old ones, and cvs commit everything.
