# ESP32 Firmware Image to ELF
This tool can be used to convert a flash dump from an ESP32 into an ELF file.

Authors: @lynerc and @\_NickMiles\_

There are three actions:
- **show_partitions** - will display all of the partitions found in an image file.
- **dump_partition** - will dump the raw bytes of a specified partition into a file.
- **create_elf** - reconstruct an ELF file from an 'app' partition (e.g. ota_0).
- **dump_nvs** - will parse a specified NVS partition and dump its contents.

# Setup

There is no setup, just run the scripts with `uv`.

Dump the flash from your chip with `esptool.py -b 921600 read_flash 0 ALL flash_dump.bin`

# Example Usage
## Show all partitions
`$ uv run --script esp32_image_parser.py show_partitions flash_dump.bin`

## Dump a specific partition
Dumps to spiffs_out.bin

`$ uv run --script esp32_image_parser.py dump_partition flash_dump.bin -partition spiffs`

Dumps to spiffs.dump

`$ uv run --script esp32_image_parser.py dump_partition flash_dump.bin -partition spiffs -output spiffs.dump`

## Convert a specific app partition into an ELF file
Converts otadata partition into ELF. Writes to otadata.elf

`$ uv run --script esp32_image_parser.py create_elf flash_dump.bin -partition otadata -output otadata.elf`

## Dump a specific NVS partition
Dumps the nvs partition

`$ uv run --script esp32_image_parser.py dump_nvs esp32_flashdump.bin -partition nvs`

Dumps the nvs partition as a JSON

`$ uv run --script esp32_image_parser.py dump_nvs flashdump/esp32_flashdump.bin -partition nvs -nvs_output_type json`
