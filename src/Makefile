SHELL := /bin/bash

FILES=$(wildcard *.lama)
ALL=$(sort $(FILES:.lama=.o))
LAMAC=lamac

.PHONY: all clean

all: Parser.o Lexer.o X86.o SM.o Manifest.o
	$(LAMAC) -I . -o lama-impl Driver.lama

Parser.o: Lexer.o

Builtins.o: World.o

State.o: Lexer.o Parser.o

Expr.o: State.o Builtins.o

SM.o: State.o World.o Expr.o Parser.o Lexer.o Builtins.o

X86.o: SM.o Manifest.o

%.o: %.lama
	$(LAMAC) -I . -c $<

clean:
	rm -Rf *.s *.o *.i *~ *.html *.sm lama-impl

