ifeq ($(OCAMLC),gcamlc)
OCAMLOPT=
else
OCAMLC=ocamlc
OCAMLOPT=ocamlopt
endif

empty=

ifneq ($(ComSpec),)
RM=del
EXEEXT=.exe
else
RM=rm
EXEEXT=
endif

BUILDDIR=build

export CAML_LD_LIBRARY_PATH=build/stublibs

.PHONY: all clean

SAMPLES=ocurl ominimal opar oput ossl \
	ocurl_test_threads

# omulti.ml requires ocaml-event (http://repo.or.cz/w/ocaml-event.git)

BYTE=$(addprefix $(BUILDDIR)/,$(addsuffix .byte$(EXEEXT),$(SAMPLES)))
OPT=$(addprefix $(BUILDDIR)/,$(addsuffix .opt$(EXEEXT),$(SAMPLES)))

ifneq ($(OCAMLOPT),)
all: $(BYTE) $(OPT)
else
all: $(BYTE)
endif

$(BUILDDIR)/curl.cma $(BUILDDIR)/curl.cmxa:
	make -C ../source install DESTDIR=$(abspath $(BUILDDIR))

$(BUILDDIR)/%.byte$(EXEEXT): %.ml $(BUILDDIR)/curl.cma
	$(OCAMLC) -c -o $(BUILDDIR)/$(basename $<).cmo -thread -I $(BUILDDIR) $<
	$(OCAMLC) -o $@ -thread -I $(BUILDDIR) unix.cma threads.cma curl.cma $(basename $<).cmo

$(BUILDDIR)/%.opt$(EXEEXT): %.ml $(BUILDDIR)/curl.cmxa
	$(OCAMLOPT) -c -o $(BUILDDIR)/$(basename $<).cmx -thread -I $(BUILDDIR) $<
	$(OCAMLOPT) -o $@ -thread -I $(BUILDDIR) unix.cmxa threads.cmxa curl.cmxa $(basename $<).cmx

clean:
	make -C ../source clean uninstall DESTDIR=$(abspath $(BUILDDIR))
	-rmdir build/stublibs
	-$(RM) build/*.o build/*.cm* build/*.byte$(EXEEXT) build/*.opt$(EXEEXT)
	-rmdir build
