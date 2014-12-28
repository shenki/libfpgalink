
## Existing HDMI2USB USB endpoint usage

FIXME: Check this is correct!!!

| Endpoint | Direction | Transfer type | Used? | Comments                              |
| -------- | --------- | ------------- | ----- | --------------------------------------|
|     0    |     -     | CONTROL       | No    | USB Reserved                          |
|     1    |     -     | -             | No    | Unused, can be freed                  |
|     2    |    OUT    | BULK          | Yes   | Used for UART TX                      |
|     4    |    IN     | BULK          | Yes   | Used for UART RX                      |
|     6    |    IN     | BULK          | Yes   | Used for sending UVC camera data      |
|     8    |     -     | -             | No    | Unused, can be freed                  |


## What Cypress FX2LP supports

| Endpoint | Direction  | Transfer type | Comments |
|     0    |      -     | Control       | Reserved |
|     1    | IN and OUT | INT/BULK      | 64-byte buffers for smaller payloads |
|     2    | IN or OUT  | BULK/ISO/INT  | 512 or 1024 byte buffers for larger payloads |
|     4    | IN or OUT  | BULK/ISO/INT  |  |
|     6    | IN or OUT  | BULK/ISOINT   |  |
|     8    | IN or OUT  | BULK/ISO/INT  |  |


# Building

`make clean; make AS8051=sdas8051 FLAGS="-DDEBUG" USE_16K=1`

Compile fx2lib in ../../../../3rd/fx2lib/ with
`make clean; make SDCCFLAGS="-DDEBUG_EPUTILS -DDEBUG_SETUPDAT`

Flash with;
`sudo ./lin.x64/dbg/fx2loader -v 0925:3881 ../../libs/libfpgalink/firmware/fx2/firmware.hex ram`

# TODO

 - [ ] Finish the set interface stuff in uvc.c
 - [ ] Set up the endpoint FIFOs correctly
 - [ ] Get TD_poll stuff working
