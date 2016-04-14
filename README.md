# cpp-sha1
sha1 checksum library for C++

This library is based upon code that I found here: http://www.tamale.net/sha1/ 

I needed a way to create diverse, procedurally-generated data sets with only a bit of variation in my function's input, so sha1 fit the bill nicely. However, the page where I got the code hasn't been maintained since 2005, and the library itself threw a mess of warnings for being non-standards compliant, hence the reason I'm forking the code here. It has been cleaned up and should now compile in gcc without complaining.

While sha1 will also work for many cryptography applications, I recommend thorough research before using sha1 in any role that requires strong cryptographic security. To quote Wikipedia: "Microsoft, Google, and Mozilla have all announced that their respective browsers will stop accepting SHA-1 SSL certificates by 2017."

## Class Usage

The class is called SHA1. The API consists of four methods:

`SHA1::SHA1()` is the class constructor

`void SHA1::addBytes( const char* data, int num )` processes bytes into the hash.

data is a pointer to the first byte to be added. The bytes are not modified.
num is the number of bytes to process. 

`unsigned char* SHA1::getDigest()` completes the hashing process and returns the final hash. The SHA1 instance should not be used after calling this method.

Returns a pointer to a 20-byte hash. Release the memory with free(). 

`static void SHA1::hexPrinter( unsigned char* c, int l )` prints bytes to stdout in hexadecimal format.

c is a pointer to the first byte to be printed. The bytes are not modified.
l is the number of bytes to print. 

Example

The following program will print one line to stdout:

 a9 99 3e 36 47 06 81 6a ba 3e 25 71 78 50 c2 6c 9c d0 d8 9d

```C++
#include <string.h>
#include <stdlib.h>
#include "sha1.h"
int main(int argc, char *argv[])
{
	#define BYTES "abc"
	SHA1* sha1 = new SHA1();
	sha1->addBytes( BYTES, strlen( BYTES ) );
	unsigned char* digest = sha1->getDigest();
	sha1->hexPrinter( digest, 20 );
	delete sha1;
	free( digest );
}
```
## TO DO

- [ ] Implement method that returns a pointer to a C string containing the hex representation of the digest