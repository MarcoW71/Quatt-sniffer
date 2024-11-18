# Quatt-sniffer  (c) 2024 M10tech

My first attempt to create a ESPhome component

Purpose is to get info from the Quatt modbus into HomeAssistant

My current idea is to clone modbus to modbus_sniffer and make it catch all messages on the bus, both commands and responses.

Then clone modbus_controller to modbus_parser and make it pipe selected registers into HA, provided by the modbus_sniffer.

As for the sniffer, I think the message intake loop can be a lot more robust if we actively use the 3.5t concept of modbus to partition the messages.

Then each message can be defined irrespective of parsing and CRC checked right away.
Any message that passes CRC is sent up to modbus_parser.

### History

#### 0.0.1 Clone modbus and modbus_controller
- they provide a reasonable startpoint
- and a esphome yaml file to match
