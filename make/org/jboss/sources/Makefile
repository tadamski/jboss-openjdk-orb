BUILDDIR = ../../..

PACKAGE = org.omg
PRODUCT = org

include $(BUILDDIR)/common/Defs.gmk

#
# Files
#
JBOSS_JMK_DIRECTORY=$(TOPDIR)/make/org/jboss/minclude/

include $(JBOSS_JMK_DIRECTORY)org_jboss_SSLPolicy.jmk
include $(JBOSS_JMK_DIRECTORY)org_jboss_SASCurrent.jmk

#
# Rules
#

all build gensrc: sslpolicy.compile sascurrent.compile
clean clobber:: sslpolicy.clean sascurrent.clean


#
# These rules are for compiling/cleaning the POA generated stuff
#

SRC_DIR = $(SHARE_SRC)/classes

# IDL Files

SSLPOLICY.IDL = $(SRC_DIR)/org/jboss/iiop/ssl/SSLPolicy.idl
SASCURRENT.IDL = $(SRC_DIR)/org/jboss/iiop/csiv2/SASCurrent.idl

#
# SSLPolicy Files and Rules
#

SSLPOLICYGENERATEDFILES = $(SSLPolicy_java:%=$(GENSRCDIR)/%)

$(SSLPOLICYGENERATEDFILES):: $(SSLPOLICY.IDL)
	$(IDLJ) -td "$(GENSRCDIR)" -i "$(SRC_DIR)/org/omg/CORBA" -corba 3.0 -fallTie -pkgPrefix CORBA org.omg  $(SSLPOLICY.IDL)

sslpolicy.compile: $(SSLPOLICYGENERATEDFILES)

sslpolicy.clean: 
	$(RM) -r $(SSLPOLICYGENERATEDFILES)


#
## SASCurrent Files and Rules
#

SASCURRENTGENERATEDFILES = $(SASCurrent_java:%=$(GENSRCDIR)/%)

$(SASCURRENTGENERATEDFILES):: $(SASCURRENT.IDL)
	$(IDLJ) -td "$(GENSRCDIR)" -i "$(SRC_DIR)/org/omg/CORBA" -i "$(SRC_DIR)/org/omg/CSI" -corba 3.0 -fallTie -pkgPrefix CORBA org.omg -pkgPrefix CSI org.omg $(SASCURRENT.IDL)

sascurrent.compile: $(SASCURRENTGENERATEDFILES)

sascurrent.clean: 
	$(RM) -r $(SASCURRENTGENERATEDFILES)



.PHONY : sslpolicy.compile sslpolicy.clean sascurrent.compile sascurrent.clean

include $(BUILDDIR)/common/Rules.gmk
