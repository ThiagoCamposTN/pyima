# pyima

This python module implements an audio codec IMA ADPCM suitable for use in games or other audio applications. It support 256 bytes compressed blocks with 505 4-bit samples at sample rate 8 KHz mono and 1010 bytes uncompressed blocks with 505 16-bit samples at sample rate 8 KHz mono.
16-bit data samples encoded as 4-bit differences result in 4:1 compression format.

Decoding usage example:

```python
data = b''
with open("./compressed_wav_without_header.bin", "rb") as f:
    data = f.read()

decoded_data = b""

for i in range(int(len(data) / 256)):
    start_index = i * 256
    current_data = data[start_index:start_index+256]
    decoded_data += decode_block(current_data)

with open("./decompressed_wav.raw", "wb") as f:
    f.write(decoded_data)
```