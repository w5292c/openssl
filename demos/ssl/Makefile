all: client server

server: serv.cpp
	gcc ./serv.cpp `pkg-config --libs --cflags libssl` -o srv

client: cli.cpp
	gcc ./cli.cpp `pkg-config --libs --cflags libssl` -o cli
