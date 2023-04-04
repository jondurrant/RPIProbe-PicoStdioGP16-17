# RPIProbe-PicoStdioGP16-17
Moving stdio from GP0&amp;1 to GP16&amp;17 to use the RPI Probe on Pico.

I've got lots of projects that predate the RPI Probe. Back in the old days I used to 
use stdio over USB as by telematry for debut. There are some caviates with this that are
not ideal. With the RPI Probe I now want to move to use STDIO over UART for telematry.

That is easy right as we just put 
```
pico_enable_stdio_uart(${NAME} 1) 
```
in our cmake file. But wait that will turn stdio on for GPIO 0 and GPIO 1, I've already 
used those ports for LEDs or Switches or I2C interfaces. Doh.

But wait moving this to another GPIO is easy. We just need to define the appropriate UART0 
GP pad numbers. It is limited to particular pad that we can use UART0 on, but is as simple as adding the following to the cmake file.
```
target_compile_definitions(${NAME} PRIVATE
    PICO_DEFAULT_UART_RX_PIN=16
    PICO_DEFAULT_UART_TX_PIN=17
)
```
