# hashcat

## Introduction

Hashcat est un outil qui permet de cracker des mots de passe. Certains de ses modes d’attaque utilisent un dictionnaire.&#x20;

Hashcat is the world’s fastest CPU-based password recovery tool. While it's not as fast as its GPU counterpart oclHashcat, large lists can be easily split in half with a good dictionary and a bit of knowledge of the command switches.

#### Terms to be aware of

* **cracking chain** The entire set of tools (both hardware and software) used to crack hashes
* **hash** A fixed-length output of data that represents a plaintext value after it has been placed through a hash function
* **mask** A specific set of rules used to tell your cracking utility which parts of a key space should be used
* **plaintext** The input for a hash function. For example, a password.

{% embed url="https://www.unix-ninja.com/search/t/Hashcat" %}

{% embed url="https://hashcat.net/hashcat/" %}

{% embed url="https://null-byte.wonderhowto.com/how-to/crack-shadow-hashes-after-getting-root-linux-system-0186386/" %}

{% embed url="https://hashcat.net/wiki/doku.php?id=rule_based_attack" %}



## Attack mode

* 0 = Straight&#x20;
* 1 = Combination
* 3 = Brute-force
* 6 = Hybrid Wordlist + Mask
* 7 = Hybrid Mask + Wordlist

### Brute force

Tries all combinations from a given Keyspace. It is the easiest of all the attacks. In Brute-Force we specify a Charset and a password length range. The total number of passwords to try is Number of Chars in Charset ^ Length.

### &#x20;Mask attack

The reason for doing this and not to stick to the traditional Brute-Force is that we want to **reduce** the password candidate **keyspace** to a more efficient one.

&#x20;Here is a single example. We want to crack the password: _Julia1984_

&#x20;In traditional Brute-Force attack we require a charset that contains all upper-case letters, all lower-case letters and all digits (aka “mixalpha-numeric”). The Password length is 9, so we have to iterate through 62^9 (13.537.086.546.263.552) combinations. Lets say we crack with a rate of 100M/s, this requires more than **4 years** to complete.

&#x20;In Mask attack we know about humans and how they design passwords. The above password matches a simple but common pattern. A name and year appended to it. We can also configure the attack to try the upper-case letters only on the first position. It is very uncommon to see an upper-case letter only in the second or the third position. To make it short, with Mask attack we can reduce the keyspace to 52\*26\*26\*26\*26\*10\*10\*10\*10 (237.627.520.000) combinations. With the same cracking rate of 100M/s, this requires just **40 minutes** to complete.

### Dictionnary attack

&#x20;The dictionary attack, or “straight mode,” is a very simple attack mode. It is also known as a “Wordlist attack”.

&#x20;All that is needed is to read line by line from a textfile (aka “dictionary” or “wordlist”) and try each line as a password candidate.

### Combinatory attack

#### Description

&#x20;Each word of a dictionary is appended to each word in a dictionary.

#### Input

&#x20;If our dictionary contains the words:

```
pass
12345
omg
Test
```

#### Output

&#x20;Hashcat creates the following password candidates:

```
passpass
pass12345
passomg
passTest
12345pass
1234512345
12345omg
12345Test
omgpass
omg12345
omgomg
omgTest
Testpass
Test12345
Testomg
TestTest
```

## Syntaxe

hashcat-binary attack-mode hash-file mask

* **hashcat-binary** This should be obvious. It's the path to the hashcat binary itself&#x20;
* **attack-mode** For mask attacks, this will always be -a3
* **hash-file** Similar to a dictionary attack, this will be the location of the file with all of your hashes
* **mask** The mask can either be the actual mask you want to use, or the location of a file with multiple masks inside of it. Either one is fine, but you must supply one of them ( and only one )

```bash
hashcat [options][hash|hashfile|hccapxfile] [mask|dictionary|directory]
```

### Options

| Paramètre          | Description                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `-m`               | Type de hash (voir la section hash type)                                                                                                      |
| `-a`               | mode d'attaque                                                                                                                                |
| `-o`               | Défini un fichier de sortie                                                                                                                   |
| `-h`               | Affiche l'aide (très utile)                                                                                                                   |
| `-p`               | Séparateur pour un fichier de hash                                                                                                            |
| `-d`               | device: permet de choisir un périphérique                                                                                                     |
| `-i`               | incrementer la taille du masque. On peut aussi spécifier la borne inférieure et supérieure: -`-increment-min=min` et le `--increment-max=max` |
| `-r`               | Utiliser une règle                                                                                                                            |
| `[filename\|hash]` | Spécifie un fichier contenant les hash que l'on veut exploiter                                                                                |

### Masque

* `?l = abcdefghijklmnopqrstuvwxyz`
* `?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ`
* `?d = 0123456789`
* ``?s =  !"#$%&'()*+,-./:;<=>?@[]^_`{|}~``
* `?a = ?l?u?d?s`

### Hash type

[https://hashcat.net/wiki/doku.php?id=example\_hashes](https://hashcat.net/wiki/doku.php?id=example\_hashes)

* 0 = MD
* 20 = md5($salt.$pass)
* 30 = md5(unicode($pass).$salt)&#x20;
* 40 = md5($salt.unicode($pass))
* 50 = HMAC-MD5 (key = $pass)
* 60 = HMAC-MD5 (key = $salt)
* 100 = SHA1&#x20;
* &#x20;110 = sha1($pass.$salt)
* 120 = sha1($salt.$pass)
* 130 = sha1(unicode($pass).$salt
* 140 = sha1($salt.unicode($pass))
* 150 = HMAC-SHA1 (key = $pass)
* 160 = HMAC-SHA1 (key = $salt)
* 200 = MySQL323
* 300 = MySQL4.1/MySQL5
* 400 = phpass, MD5(Wordpress), MD5(phpBB3), MD5(Joomla)
* 500 = md5crypt, MD5(Unix), FreeBSD MD5, Cisco-IOS MD5&#x20;
* 510 = md5($pass.$salt)
* 900 = MD4&#x20;
* 1000 = NTLM&#x20;
* 1100 = Domain Cached Credentials (DCC), MS Cache
* 1400 = SHA256&#x20;
* 1410 = sha256($pass.$salt)
* 1420 = sha256($salt.$pass)&#x20;
* 1430 = sha256(unicode($pass).$salt)
* 1431 = base64(sha256(unicode($pass)))
* 1440 = sha256($salt.unicode($pass))&#x20;
* 1450 = HMAC-SHA256 (key = $pass)
* 1460 = HMAC-SHA256 (key = $salt)
* 1600 = md5apr1, MD5(APR), Apache MD5&#x20;
* 1700 = SHA512 1710 = sha512($pass.$salt)&#x20;
* 1720 = sha512($salt.$pass)
* 1730 = sha512(unicode($pass).$salt)
* 1740 = sha512($salt.unicode($pass))&#x20;
* 1750 = HMAC-SHA512 (key = $pass)&#x20;
* 1760 = HMAC-SHA512 (key = $salt)
* 1800 = SHA-512(Unix)&#x20;
* 2400 = Cisco-PIX MD5&#x20;
* 2410 = Cisco-ASA MD5&#x20;
* 2500 = WPA/WPA2&#x20;
* 2600 = Double MD5
* 3200 = bcrypt, Blowfish(OpenBSD)
* 3300 = MD5(Sun)
* 3500 = md5(md5(md5($pass)))
* 3610 = md5(md5($salt).$pass)
* 3710 = md5($salt.md5($pass))
* 3720 = md5($pass.md5($salt))
* 3800 = md5($salt.$pass.$salt)
* etc...

### Permutation attack-mode options Outfile formats&#x20;

* 1 = hash\[:salt]&#x20;
* 2 = plain
* 3 = hash\[:salt]:plain
* 4 = hex\_plain
* 5 = hash\[:salt]:hex\_plain
* 6 = plain:hex\_plain
* 7 = hash\[:salt]:plain:hex\_plain
* 8 = crackpos
* 9 = hash\[:salt]:crack\_pos&#x20;
* 10 = plain:crack\_pos
* 11 = hash\[:salt]:plain:crack\_pos
* 12 = hex\_plain:crack\_pos
* 13 = hash\[:salt]:hex\_plain:crack\_pos
* 14 = plain:hex\_plain:crack\_pos
* 15 = hash\[:salt]:plain:hex\_plain:crack\_pos

## Utilisation

```bash
hashcat -a 3 file.hash ?l?l?l?l?d?d
```

