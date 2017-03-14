
## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
Ok... This is encrypted some how. They give us the key. The challenge must be to find the encryption method. I ran it through some common classical ciphers, but then realized the ciphertext all seemed to be hex characters. It must be a modern cipher. 

I wrote this to run in through all possible ciphers with openssl:
```
<?php
$ciphers             = openssl_get_cipher_methods();
$ciphers_and_aliases = openssl_get_cipher_methods(true);
$cipher_aliases      = array_diff($ciphers_and_aliases, $ciphers);

$key =  hex2bin("0d5d127cfbc9d8ef12ae22c2edca3fb5cf4fcdbcc9668461bddfab975c5dbdff");
$ciphertext = hex2bin("63098d7dab14f5ac126b85e0ae814f889c635f4a7a683e2481ac641b1153a66e45c8861fc1f26dd4dec123841ffeb288c7f7be032a833883b5637d88a894e4b12644dca0aaea941f6997920492085919ddf7d2ec2744362195bcb2ffed7f6eab");
print_r($ciphers);

print_r($cipher_aliases);

foreach($ciphers as $i){
	print_r("\n");
	echo openssl_decrypt($ciphertext,$i,$key, $options = OPENSSL_RAW_DATA);
}

	print_r("\n\nend");
?>
```

Sweet. Run it:
```
$ php decode.php
V�EI���c{�BsF8��0�T�>ZS����
4��;Hv�^.3�f��g�)�{��lw�\.��e�

if you spend all day shuffling words around, you can make anything sound bad, Morty

;	75�
           �nk�rq��
```
Basically it gives you a bunch of junk until it hits the right cipher, then it prints ot the good text and keeps going.

Sweet!
## Key
if you spend all day shuffling words around, you can make anything sound bad, Morty
