PREFIX = /usr

install:
	mkdir -p $(DESTDIR)$(PREFIX)/bin/
	cp -f cp-p $(DESTDIR)$(PREFIX)/bin/
	cp -f mv-p $(DESTDIR)$(PREFIX)/bin/

uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/cp-p
	rm -f $(DESTDIR)$(PREFIX)/bin/mv-p

.PHONY: install uninstall
