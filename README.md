# Lesson 2: A digest

The second lesson is about writing an engine with only a digest implementation

## Build

Build as follows:

    $ gcc -fPIC -o rfc1321/md5c.o -c rfc1321/md5c.c
	$ gcc -fPIC -o e_md5.o -c e_md5.c
	$ gcc -shared -o e_md5.so -lcrypto e_md5.o rfc1321/md5c.o

A quick and easy test goes like this:

    $ openssl engine -t -c `pwd`/e_md5.so
	 A simple md5 engine for demonstration purposes
	Loaded: (emd5) A simple md5 engine for demonstration purposes
 	[MD5]
     [ available ]

	$ echo whatever | openssl dgst -engine `pwd`/e_md5.so -md5
	engine "emd5" set.
	(stdin)= d8d77109f4a24efc3bd53d7cabb7ee35

	$ echo whatever | openssl dgst -md5
	(stdin)= d8d77109f4a24efc3bd53d7cabb7ee35
