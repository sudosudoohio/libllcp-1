# $Id$

ACLOCAL_AMFLAGS = -I m4

SUBDIRS = doc libllcp test tools examples

dist-hook:
	@if ! grep -qi "$$(LC_ALL=C date +'%d %b %Y')" NEWS; then \
	    printf "\033[31;1mBEWARE!  The first line from the NEWS file does not contain the current date!\033[0m\n"; \
	    sleep 3; \
	fi
	@if test -d "$(srcdir)/.git"; then \
	    echo "Creating ChangeLog..." && \
	    ( cd "$(top_srcdir)" && \
		echo '# Generated by Makefile. Do not edit.'; echo; \
		$(top_srcdir)/missing --run git2cl --authors=AUTHORS --strip-prefix=/trunk/libllcp --stdout ) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(top_distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		echo "Failed to generate ChangeLog" >&2 ); \
	else \
	    echo "A svn checkout is required to generate a ChangeLog" >&2; \
	fi

EXTRA_DIST = HACKING
CLEANFILES = coverage.info
clean-local: clean-local-coverage
.PHONY: clean-local-coverage
clean-local-coverage:
	-rm -rf coverage

style:
	find . -name "*.[ch]" -exec perl -pi -e 's/[ \t]+$$//' {} \;
	find . -name "*.[ch]" -exec astyle --formatted --mode=c --suffix=none \
	    --indent=spaces=2 --indent-switches --indent-preprocessor \
	    --keep-one-line-blocks --max-instatement-indent=60 \
	    --brackets=linux --pad-oper --unpad-paren --pad-header \
	    --align-pointer=name {} \;

