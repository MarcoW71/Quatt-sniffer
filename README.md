# Quatt-sniffer  (c) 2024 M10tech

My first attempt to create a ESPhome component

Purpose is to get info from the Quatt modbus into HomeAssistant

My current idea is to clone modbus and make it catch all messages on the bus, both commands and responses.

Then clone modbus_controller and make it pipe selected registers into HA, provided by the modbus component.

Any reponse that passes CRC is sent up to modbus_controller in on_modbus_message(fc,start_addr,num_reg,data)

### History

#### 0.0.1 Clone modbus and modbus_controller
- they provide a reasonable startpoint
- and a esphome yaml file to match

#### 0.0.2 Rename back to modbus and modbus_controller
- renaming is a non-trivial exercise
- will depend on local component blocking out build in ones

#### 0.0.3 Work in sniffer mode and detect commands and responses
- switches between command and response on every good CRC
- this provides the start address and number of registers for each response
- the parsing of messages sent up is not working yet

### Sample
01 06 07 cf 00 00 b8 81
01 06 07 cf 00 00 b8 81
01 06 07 da 00 00 a9 45
01 06 07 da 00 00 a9 45
01 06 07 df 00 00 b9 44
01 06 07 df 00 00 b9 44
01 06 0f 9f 00 00 ba f0
01 06 0f 9f 00 00 ba f0
01 03 08 33 00 28 b7 bb
01 03 50 00 00 00 ea 00 00 00 00 00 00 00 00 00 00 00 00 00 64 00 00 01 f4 19 1b 15 d0 14 ef 15 1a 00 00 18 00 00 94 00 93 00 00 00 00 00 00 00 00 01 1e 00 72 00 02 2e 78 00 00 0e 37 0b b8 0b b8 00 00 14 a7 14 d1 15 a2 17 f5 16 0a 0b b8 00 00 00 00 c9 07
