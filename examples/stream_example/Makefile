#
# Example program
#
# Makefile used to build the software
#
# Copyright 2016 Nicolas Mora <mail@babelouest.org>
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the MIT License
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#
CC=gcc
CFLAGS=-c -Wall -D_REENTRANT $(ADDITIONALFLAGS)
ULFIUS_LOCATION=../../src
LIBS=-lc -lulfius -L$(ULFIUS_LOCATION)

all: stream_example stream_client

clean:
	rm -f *.o stream_example stream_client

debug: ADDITIONALFLAGS=-DDEBUG -g -O0

debug: stream_example stream_client

libulfius.so:
	cd $(ULFIUS_LOCATION) && $(MAKE) debug

stream_example.o: stream_example.c
	$(CC) $(CFLAGS) stream_example.c -DDEBUG -g -O0

stream_example: libulfius.so stream_example.o
	$(CC) -o stream_example stream_example.o $(LIBS)

stream_client.o: stream_client.c
	$(CC) $(CFLAGS) stream_client.c -DDEBUG -g -O0

stream_client: libulfius.so stream_client.o
	$(CC) -o stream_client stream_client.o $(LIBS)

test: stream_example stream_client
	LD_LIBRARY_PATH=$(ULFIUS_LOCATION):${LD_LIBRARY_PATH} ./stream_example
