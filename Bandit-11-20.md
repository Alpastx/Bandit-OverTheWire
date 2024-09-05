## Walkthrough for bandit 11 - 20
## Bandit 11

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit11
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

- The uppercase and lowercase have are rotated by 13 chars (simple hint for rot13 cipher method )
- can use cyberchef to solve this but we are built different 😏😏

```bash
alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"
cat data.txt | rot13
```

## Bandit 12

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit12
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

- 1st hint multiple compression types
- use file to see the file type 
- hexdump is available reverse it?
- act like a detective 🔍👀
- we have to work in tmp dir 

```bash
mkdir /tmp/Alpastx
cd /tmp/Alpastx
cp ~/data.txt /tmp/Alpastx/
cat data.txt

#the file is a hexdump (google whoe to reverse it ?)
file data.tx 

#says ascii text but ik its hexdump so we reverse it 
xxd -r data.txt > reved
file reved

#says it was a gzip
cp reved reved.tar.gz
gzip -d reved.tar.gz
file reved.tar

# says it was a bzip2 format
bzip2 -d reved.tar
file reved.tar.out 

# says it was a gzip again repeat 
cp reved.tar.out reved.tar.gz
gzip -d revedgzip.tar.gz
file revedgzip.tar

# shows it was a TAR archive
tar -xf revedgzip.tar
file data5.bin

# shows its a tar file
tar -xf data5.bin
file data6.bin

# its a bzip2 file
bzip2 -d data6.bin
file data6.bin.out

# its a tar file (at this time am tired 😭)
tar -xf data6.bin.out
file data8.bin

# its a gzip file
cp data8.bin data8.tar.gz
gzip -d data8.tar.gz
file data8.tar

# its a ascii text
cat data8.tar
```

## Bandit 13

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit13
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

- super easy we havea  private key rather than a passsword 
- we cant read the passwor din the mentioned dir `/etc/bandit_pass/bandit14`
- just copy paste the key on your local system and login using it 

```
cat sshkey.private
#copyit
save it in notepad and name it banitkey.private
```

## Bandit 14

```
ssh bandit14@bandit.labs.overthewire.org -p 2220 -i banitkey.private
```

- we need to copy the password form the file `/etc/bandit_pass/bandit14`
```
cat /etc/bandit_pass/bandit14
nc localhost 30000
#paste the passwd of leevl14
```

## Bandit 15

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit15
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

- We have to use anything using ssl 
- what's better than open ssl?

```
 openssl s_client -quiet -connect localhost:30001
 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

## Bandit 16
```
ssh bandit.labs.overthewire.org -p 2220 -l bandit16
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

- find ports listening between 31000-32000
- find the ones with ssl 

```bash
nmap localhost -p 31000-32000
# got open ports now a version scan on them 
nmap -sV localhost -p 31046,31518,31691,31790,31960
#or you can try brute each port lmao
openssl s_client -quiet -connect localhost:31790
#got a privatekeylets use it for nect level

```

## Bandit 17

```
ssh bandit17@bandit.labs.overthewire.org -i bandit17 -p 2220
```

-  find the difference

```
diff passwords.old passwords.new
```

## Bandit 18

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit18
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

- getting logged out instatnly ?
- read the man page of ssh we can execute commands as ssh

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit18 cat readme
```

## Bandit 19

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit19
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

- run the setup to make the setup word as bandit20 

```
./bandit20-do cat /etc/bandit_pass/bandit20
```

## Bandit20

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

- using the binary we can use multiple ssh session's to send banit20 password 

```
#open up new terminal and ssh into bandit 20 with 2 sessions 
session1
nc -lvnp 4567
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

#session2 
./suconnect 4567

#you will get the pass for next level
```

## All passwords 

| Username  | Password                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bandit11  | dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit12  | 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit 13 | FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit14  | -----BEGIN RSA PRIVATE KEY-----<br>MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+<br>gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB<br>ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb<br>ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV<br>ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7<br>jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA<br>J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE<br>pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67<br>xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS<br>nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD<br>o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe<br>ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf<br>laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS<br>M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU<br>1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH<br>PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s<br>8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+<br>xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1<br>GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J<br>3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY<br>iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby<br>9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD<br>qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0<br>kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN<br>/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==<br>-----END RSA PRIVATE KEY-----<br><br>OR <br><br>MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS |
| banit15   | 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit16  | kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit17  | -----BEGIN RSA PRIVATE KEY-----<br>MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ<br>imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ<br>Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu<br>DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW<br>JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX<br>x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD<br>KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl<br>J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd<br>d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC<br>YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A<br>vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama<br>+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT<br>8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx<br>SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd<br>HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt<br>SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A<br>R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi<br>Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg<br>R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu<br>L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni<br>blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU<br>YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM<br>77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b<br>dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3<br>vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=<br>-----END RSA PRIVATE KEY-----                                                        |
| bandit18  | x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit19  | cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit20  | 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bandit21  | EeoULMCra2q0dSkYj561DX7s1CpBuOBt                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
