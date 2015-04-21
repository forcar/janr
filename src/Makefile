#CREATED_F=janr_main.F
#LIBNAMES  = $(MAIN_DIRECTORY)$(DEBUG) 
#LIBNAMES=  janr03 $(GSIM_INT_LIBS) $(GSIM_INT_MD_LIBS)
#SHARED_LIBS=$(GSIM_INT_SHARED_LIBS)
#include $(CLAS_CMS)/Makefile


.PHONY: all clean

#CXXFLAGS = -pipe -Wall -Wextra -Weffc++ -pedantic -ggdb

FC = gfortran
FCFLAGS =  -O -fno-automatic  -ffixed-line-length-none -fno-second-underscore -funroll-loops -fomit-frame-pointer -fPIC 

SRCS = $(wildcard *.F)
OBJS_TEMP = $(patsubst %.F,%.o,$(SRCS))
OBJS = $(filter-out janr_main.o,$(OBJS_TEMP))
OBJS += abort_rut.o
all: janr 

lib: $(OBJS)
		#gcc -c abort_rut.c
		ar rv libjanr.a $(OBJS) 

clean:
		rm -fv $(OBJS) janr

%.o: %.F
		$(FC) $(FCFLAGS) -c $^ 

%.o: %.c
		gcc -c $^

janr:
		$(FC) janr_main.F -L/sw/lib -lpawlib -lgraflib -lgrafX11 -lpacklib -lphtools -lmathlib -lkernlib -L./ -ljanr  -lgfortran -L/opt/X11/lib/ -lX11 -o $@
display:
	  @echo "$(SRCS)"	
		@echo "$(OBJS)"
