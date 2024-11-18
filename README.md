# Quatt-sniffer  (c) 2024 M10tech

My first attempt to create a ESPhome component

Purpose is to get info from the Quatt modbus into HomeAssistant

My current idea is to clone modbus and make it catch all messages on the bus, both commands and responses.

Then clone modbus_controller and make it pipe selected registers into HA, provided by the modbus component.

Any reponse that passes CRC is sent up to modbus_controller in on_modbus_message(fc,start_addr,num_reg,data)

### History

#### 0.0.6 introduced sniffer as a role
- this will steer behavior of the underlying systems

#### 0.0.5 use optimized register range
- makes a single read-range that matches the quatt read command
- using git works now as expected in 0.0.4

#### 0.0.4 renamed my_components to components
- seems to allow the use of the external components of source type git
- to be tested after this is committed

#### 0.0.3 Work in sniffer mode and detect commands and responses
- switches between command and response on every good CRC
- this provides the start address and number of registers for each response
- the parsing of messages sent up is not working yet

#### 0.0.2 Rename back to modbus and modbus_controller
- renaming is a non-trivial exercise
- will depend on local components blocking-out built-in ones

#### 0.0.1 Clone modbus and modbus_controller
- they provide a reasonable startpoint
- and a esphome yaml file to match

### Sample
```
01 06 07cf 0000 b881
01 06 07cf 0000 b881
01 06 07da 0000 a945
01 06 07da 0000 a945
01 06 07df 0000 b944
01 06 07df 0000 b944
01 06 0f9f 0000 baf0
01 06 0f9f 0000 baf0
01 03 0833 0028 b7bb
01 03 50 0000 00ea 0000 0000 0000 0000 0000 0000 0064 0000 01f4 191b 15d0 14ef 151a 0000 1800 0094 0093 0000 0000 0000 0000 011e 0072 0002 2e78 0000 0e37 0bb8 0bb8 0000 14a7 14d1 15a2 17f5 160a 0bb8 0000 0000 c907
```
