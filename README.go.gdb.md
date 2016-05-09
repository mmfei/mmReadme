go build -gcflags "-N -l" main.go;
gdb ./main;
source /usr/local/go/src/runtime/runtime-gdb.py;
r

