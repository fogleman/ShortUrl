## Short URL Generator

Python module for generating tiny URLs.

### Sample Usage

    >>> import short_url
    >>> short_url.encode_url(123)
    '9epgb'
    >>> short_url.decode_url('9epgb')
    123
    >>> short_url.encode_url(124)
    '2yy2m'
    >>> short_url.decode_url('2yy2m')
    124

### Implementation Details

A bit-shuffling approach is used to avoid generating URLs in a consecutive,
predictable order. However, the algorithm is deterministic and guarantees that
no collisions will occur.

The URL alphabet is fully customizable and may contain any number of
characters. By default, digits and lower-case letters are used, with some
removed to avoid confusion between characters like o, O and 0. The default
alphabet is shuffled and has a prime number of characters to further improve
the results of the algorithm.

The block size specifies how many bits will be shuffled. The lower BLOCK_SIZE 
bits are reversed. Any bits higher than BLOCK_SIZE will remain as is.
BLOCK_SIZE of 0 will leave all bits unaffected and the algorithm will simply 
be converting your integer to a different base. BLOCK_SIZE is necessary to
establish an upper-bound for the bit reversal and to generate the URLs at an
appropriate length.

The intended use is that incrementing, consecutive integers will be used as 
keys to generate the short URLs. For example, when creating a new URL, the 
unique integer ID assigned by a database could be used to generate the URL 
by using this module. Or a simple counter may be used. As long as the same 
integer is not used twice, the same short URL will not be generated twice.

The module supports both encoding and decoding of URLs. The min_length 
parameter allows you to pad the URL if you want it to be a specific length.

Use the functions in the top-level of the module to use the default encoder. 
Otherwise, you may create your own UrlEncoder object and use its encode_url 
and decode_url methods.
