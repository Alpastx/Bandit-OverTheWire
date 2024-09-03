# Bandit Level 0 - 10
bottom 👀
## Bandit level 0

- explore ssh man page / help page 
- `ssh username@<ip/url> -p <port>`

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

`password : banit0`

```
ls -al
cat readme
```

## Bandit level 1 

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit1
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

- spaces in filename can be opened using `cat < -`

```
cat < -
```

## Bandit level 2

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit2
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

- spaces in filenames can be accessed using \

```
cat spaces\ in\ this\ filename
```

## Bandit level 3

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit3
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

- always use `cat -al`

```
cd inhere
ls -al
cat ...Hiding-From-You
```

## Bandit level 4

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit4
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

-  multiple file inside `inhere` dir lest read em all

```
cd inhere
cat ./-file01 
or
cat ./*
copy the string and use `reset` if the terminals messedup
```

## Bandit level 5

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit5
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

-  Given conditions for file we haev to find 
	1.human-readable `-readable`
	2.1033 in bytes `-size 1033c`
	3.not executable 
* read manual of find command 

```
find . -type f -readable -size 1033c -exec cat {} \;
```

## Bandit level 6

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit6
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

- conditions :
	- - owned by user bandit7
	- owned by group bandit6
	- 33 bytes in size
*  make a command using find to befit these conditions

```
find / -type f -size 33c -user bandit7 -group banit6 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

## Bandit level 7 

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit7
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

- use grep to fin the word millionth 

```
ls 
cat data.tx | grep millionth
```

## Bandit level 8

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit8
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

- read the desc properly 
- use commands in the hint 

```
sort data.txt | uniq -u
```

## Bandit level 9

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit9
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

-  Read properly

```
strings data.txt | grep "="
```

## Bandit level 10

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit10
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

- use bse64

```
cat data.txt | base64 -d
```

## All passwords 1-11

| Usernames | Passwords                        |
| --------- | -------------------------------- |
| bandit0   | bandit0                          |
| bandit1   | ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If |
| bandit2   | 263JGJPfgU6LtdEvgfWU1XP5yac29mFx |
| bandit3   | MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx |
| bandit4   | 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ |
| bandit5   | 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw |
| bandit6   | HWasnPhtq9AVKe0dmk45nxy20cvUa6EG |
| bandit7   | morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj |
| bandit8   | dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc |
| bandit9   | 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM |
| banit10   | FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey |
| bandit 11 | dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr |


