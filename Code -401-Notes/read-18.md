One of the earliest encryption techniques is the Caesar Cipher, invented by Julius Caesar more than two thousand years ago to communicate messages to his allies.
The Caesar Cipher is a great introduction to encryption, decryption, and code cracking, thanks to its simplicity.

Encrypting a message
Imagine Caesar wants to send this message:
SECRET MEETING AT THE PALACE
Here's what that might look like encrypted:
YKIXKZ SKKZOTM GZ ZNK VGRGIK
That looks an awfully lot like gobbledygook at first, but this encrypted message is actually very related to the original text.
The Caesar Cipher is a simple substitution cipher which replaces each original letter with a different letter in the alphabet by shifting the alphabet by a certain amount.
To make the encrypted message above, I shifted the alphabet by 6 and used this substitution table:
A	B	C	D	E	F	G	H	I	J	K	L	M	N	O	P	Q	R	S	T	U	V	W	X	Y	Z
G	H	I	J	K	L	M	N	O	P	Q	R	S	T	U	V	W	X	Y	Z	A	B	C	D	E	F
S shifts 6 letters over to Y, E shifts 6 letters over to K, etc. Here's the first word and its shifts:
S	E	C	R	E	T
Y	K	I	X	K	Z

Decrypting a message
According to historical records, Caesar always used a shift of 3. As long as his message recipient knew the shift amount, it was trivial for them to decode the message.
Imagine Caesar sends this message to a comrade:
EHZDUH EUXWXV
The comrade uses this substitution table, where the alphabet is shifted by 3:
A	B	C	D	E	F	G	H	I	J	K	L	M	N	O	P	Q	R	S	T	U	V	W	X	Y	Z
D	E	F	G	H	I	J	K	L	M	N	O	P	Q	R	S	T	U	V	W	X	Y	Z	A	B	C
They can then decode the message with certainty. The first letter "E" was shifted by 3 from "B", the second letter "H" was shifted by 3 from "E", etc. The result is this ominous message:
BEWARE BRUTUS
