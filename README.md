# Telkomsel Orbit API Decryption Tool - AES-256

Tool ini dapat digunakan untuk melakukan decryption API response pada website myorbit.id sehingga memungkinkan kita untuk mengetahui isi dari API Respone tersebut.

Tool dapat diakses pada [https://andrew-susanto.github.io/Telkomsel-Orbit-API-Decryption-Tool/decrypt.html](https://andrew-susanto.github.io/Telkomsel-Orbit-API-Decryption-Tool/decrypt.html). Tool ini melakukan decryption dengan javascript dan dilakukan pada client-side sehingga tidak ada encrypted data maupun token yang dikirim ke server manapun. 

## Cara Penggunaan

- Buka tab Network pada Inspect Element untuk memonitor API Call yang akan dilakukan website myorbit.id.
- Sambil membuka tab Network, buka website myorbit.id dan login seperti biasa.
- Perhatikan beberapa API Call yang dilakukan ke endpoint https://api.myorbit.id (terutama untuk endpoint /membernew/v2/members/device-router atau /membernew/v2/members)
- Salin response data dan token dari salah satu API Call tersebut ke decryption tool.
- Tekan tombol decrypt untuk melihat hasil decrytion.

## Contoh encryption data yang dilakukan myorbit.id

![Encrypted Data](/Encrypted-Data.png?raw=true "Encrypted Data")

## Encryption Details

Encryption yang digunakan pada website myorbit adalah AES-256 dengan key dan iv.

Pada website myorbit, key dan iv yang digunakan merupakan potongan dari JWT Token pada header Authentication. Dengan Key dan IV berupa : 

- Key : 32 karakter terakhir JWT Token - AES-256 membutuhkan 32 karakter key
- IV : 16 Karakter pertama JWT Token

Key dan IV ini ternyata juga diikutsertakan pada API response di pada bagian token.

Beberapa endpoint yang diketahui melakukan encryption pada data yang dikirim adalah :

- https://api.myorbit.id/membernew/v2/members/device-router
- https://api.myorbit.id/membernew/v2/members

Dengan melakukan decryption ini, maka memungkinkan kita untuk mengetahui isi sebenarnya dari API Response tersebut.

## Side Notes

Not really sure the reason behind Telkomsel Orbit doing this kind of encryption to some of their API endpoint.

