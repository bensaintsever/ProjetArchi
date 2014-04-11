CC=gcc
CFLAGS=-Wall -O2

ISADIR = ../misc
YAS=$(ISADIR)/yas
YIS=$(ISADIR)/yis
PIPE=../pipe/psim
SEQ=../seq/ssim
SEQ+ =../seq/ssim+

YSFILES = $(wildcard *.ys)
YOFILES = $(YSFILES:.ys=.yo)

PIPEFILES = $(YSFILES:.ys=.pipe)

SEQFILES = $(YSFILES:.ys=.seq)

SEQ+FILES = $(YSFILES:.ys=.seq+)

.SUFFIXES:
.SUFFIXES: .c .s .o .ys .yo .yis .pipe .seq .seq+

all: $(YOFILES) 

test: testpsim testssim testssim+

testpsim: $(PIPEFILES)
	grep "ISA Check" *.pipe
	rm $(PIPEFILES)

testssim: $(SEQFILES)
	grep "ISA Check" *.seq
	rm $(SEQFILES)

testssim+: $(SEQ+FILES)
	grep "ISA Check" *.seq+
	rm $(SEQ+FILES)

.ys.yo:
	$(YAS) $*.ys

.yo.yis: $(YIS)
	$(YIS) $*.yo > $*.yis

.yo.pipe: $(PIPE)
	$(PIPE) -t $*.yo > $*.pipe

.yo.seq: $(SEQ)
	$(SEQ) -t $*.yo > $*.seq

.yo.seq+: $(SEQ+)
	$(SEQ+) -t $*.yo > $*.seq+

clean:
	rm -f *.o *.yis *~ *.yo *.pipe *.seq *.seq+ core
