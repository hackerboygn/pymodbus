# Pymodbus REPL

## Dependencies

Depends on [prompt_toolkit](https://python-prompt-toolkit.readthedocs.io/en/stable/index.html) and [click](http://click.pocoo.org/6/quickstart/)

Install dependencies
```
$ pip install click prompt_toolkit --upgarde
```

Or
Install pymodbus with repl support
```
$ pip install pymodbus[repl] --upgrade
```

## Usage Instructions
RTU and TCP are supported as of now
```
bash-3.2$ pymodbus.console
Usage: pymodbus.console [OPTIONS] COMMAND [ARGS]...

Options:
  --version       Show the version and exit.
  --verbose       Verbose logs
  --support-diag  Support Diagnostic messages
  --help          Show this message and exit.

Commands:
  rtu
  tcp


```
TCP Options
```
bash-3.2$ pymodbus.console tcp --help
Usage: pymodbus.console tcp [OPTIONS]

Options:
  --host TEXT     Modbus TCP IP
  --port INTEGER  Modbus TCP port
  --help          Show this message and exit.




```

RTU Options
```
bash-3.2$ pymodbus.console rtu --help
Usage: pymodbus.console rtu [OPTIONS]

Options:
  --method TEXT          Modbus Serial Mode (rtu/ascii)
  --port TEXT            Modbus RTU port
  --baudrate INTEGER     Modbus RTU serial baudrate to use. Defaults to 9600
  --bytesize [5|6|7|8]   Modbus RTU serial Number of data bits. Possible
                         values: FIVEBITS, SIXBITS, SEVENBITS, EIGHTBITS.
                         Defaults to 8
  --parity [N|E|O|M|S]   Modbus RTU serial parity.  Enable parity checking.
                         Possible values: PARITY_NONE, PARITY_EVEN, PARITY_ODD
                         PARITY_MARK, PARITY_SPACE. Default to 'N'
  --stopbits [1|1.5|2]   Modbus RTU serial stop bits. Number of stop bits.
                         Possible values: STOPBITS_ONE,
                         STOPBITS_ONE_POINT_FIVE, STOPBITS_TWO. Default to '1'
  --xonxoff INTEGER      Modbus RTU serial xonxoff.  Enable software flow
                         control.Defaults to 0
  --rtscts INTEGER       Modbus RTU serial rtscts. Enable hardware (RTS/CTS)
                         flow control. Defaults to 0
  --dsrdtr INTEGER       Modbus RTU serial dsrdtr. Enable hardware (DSR/DTR)
                         flow control. Defaults to 0
  --timeout FLOAT        Modbus RTU serial read timeout. Defaults to 0.025 sec
  --write-timeout FLOAT  Modbus RTU serial write timeout. Defaults to 2 sec
  --help                 Show this message and exit.
```

To view all available commands type `help`

```
$ pymodbus.console tcp --host 192.168.128.126 --port 5020

> help
Available commands:
client.change_ascii_input_delimiter          Diagnostic sub command, Change message delimiter for future requests
client.clear_counters                        Diagnostic sub command, Clear all counters and diag registers
client.clear_overrun_count                   Diagnostic sub command, Clear over run counter
client.force_listen_only_mode                Diagnostic sub command, Forces the addressed remote device to its Listen Only Mode
client.get_clear_modbus_plus                 Diagnostic sub command, Get or clear stats of remote modbus plus device
client.get_com_event_counter                 Read  status word and an event count from the remote device's communication event counter
client.get_com_event_log                     Read  status word, event count, message count, and a field of event bytes from the remote device.
client.mask_write_register                   Mask content of holding register at `address` with `and_mask` and `or_mask`
client.read_coils                            Reads `count` coils from a given slave starting at `address`
client.read_device_information               Read the identification and additional information of remote slave
client.read_discrete_inputs                  Reads `count` number of discrete inputs starting at offset `address`
client.read_exception_status                 Read the contents of eight Exception Status outputs in a remote device.
client.read_holding_registers                Read `count` number of holding registers starting at `address`
client.read_input_registers                  Read `count` number of input registers starting at `address`
client.readwrite_registers                   Read `read_count` number of holding registers starting at `read_address`  and write `write_registers` starting at `write_address`
client.report_slave_id                       Report information about remote slave ID
client.restart_comm_option                   Diagnostic sub command, initialize and restart remote devices serial interface and clear all of its communications event counters .
client.return_bus_com_error_count            Diagnostic sub command, Return count of CRC errors received by remote slave
client.return_bus_exception_error_count      Diagnostic sub command, Return count of Modbus exceptions returned by remote slave
client.return_bus_message_count              Diagnostic sub command, Return count of message detected on bus  by remote slave
client.return_diagnostic_register            Diagnostic sub command, Read 16-bit diagnostic register
client.return_iop_overrun_count              Diagnostic sub command, Return count of iop overrun errors by remote slave
client.return_query_data                     Diagnostic sub command , Loop back data sent in response
client.return_slave_bus_char_overrun_count   Diagnostic sub command, Return count of messages not handled  by remote slave due to character overrun condition
client.return_slave_busy_count               Diagnostic sub command, Return count of server busy exceptions sent  by remote slave
client.return_slave_message_count            Diagnostic sub command, Return count of messages addressed to remote slave
client.return_slave_no_ack_count             Diagnostic sub command, Return count of NO ACK exceptions sent  by remote slave
client.return_slave_no_response_count        Diagnostic sub command, Return count of No responses  by remote slave
client.write_coil                            Write `value` to coil at `address`
client.write_coils                           Write `value` to coil at `address`
client.write_register                        Write `value` to register at `address`
client.write_registers                       Write list of `values` to registers starting at `address`
result.decode                                Decode the register response to known formatters
result.raw                                   Return raw result dict
```

Every command has auto suggetion on the arguments supported , supply arg and value are to be supplied in `arg=val` format.
```

> client.read_holding_registers count=4 address=9 unit=1
{
    "registers": [
        60497,
        47134,
        34091,
        15424
    ]
}
```

The last result could be accessed with `result.raw` command
```
> result.raw
{
    "registers": [
        15626,
        55203,
        28733,
        18368
    ]
}
```

For Holding and Input register reads, the decoded value could be viewed with `result.decode`
```
> result.decode word_order=little byte_order=little formatters=float64
28.17

>
```

## DEMO

[![asciicast](https://asciinema.org/a/y1xOk7lm59U1bRBE2N1pDIj2o.png)](https://asciinema.org/a/y1xOk7lm59U1bRBE2N1pDIj2o)
