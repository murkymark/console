################################################################################
# VARIABLEN                                                                    #
################################################################################

# Dateien, die durch ein 'clean' gel�scht werden sollen
CLEANABLE_OBJS = dist/hello.gb obj/main.o

ASSEMBLER = wla-gb # Damit wird unser Assemblercode in eine Objektdatei kompiliert
LINKER = wlalink # Dieser 'linkt' unsere Objektdateien in ein ROM
FIXER = tools/gbfix # Repariert bzw. validiert u.a. den Header von unserem ROM
#DEPLOYER = # Legt das Programm fest, um das ROM auf eine Karte zu �bertragen
EMU = gb  # Legt den Emulator fest, mit dem wir unser ROM testen
CC = gcc # C-Compiler
CFLAGS = -Wall -ansi -pedantic -g -O0 # C-Compiler-Argumente
ASSFLAGS = # Argumente f�r den Assembler

################################################################################
# RULES                                                                        #
################################################################################

# 'Phony targets' sind Aktionen und keine Dateien und m�ssen daher immer
# ausgef�hrt werden

.PHONY: all run deploy clean tools

all: dist/hello.gb

dist/hello.gb: tools src/main.asm src/tiles.inc src/memory.asm src/gb.inc ./main.link
	 cd src && $(ASSEMBLER) -vo main.asm ../obj/main.o && cd ..
	 $(LINKER) -vr ./main.link dist/hello.gb
	 $(FIXER) -v dist/hello.gb

tools: tools/gbfix.c
	 $(CC) $(CFLAGS) -o tools/gbfix tools/gbfix.c
   
run: dist/hello.gb
	 $(EMU) dist/hello.gb
  
#deploy: dist/hello.gb
#	$(DEPLOYER) dist/hello.gb

# l�scht alle (durch dieses Makefile) erzeugten Dateien
clean:
	-rm $(CLEANABLE_OBJS)
