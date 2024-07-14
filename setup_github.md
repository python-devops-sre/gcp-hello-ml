## Steps to setup Github

1.  Create a public repo:
  * check Public
  * Initialize with a READM
  * add .gitignore PYthon
  * Add licence MIT
![github hello](https://user-images.githubusercontent.com/58792/58992683-58739e00-87a0-11e9-9b77-2e13116c2d35.png)

*Note on .gitignore*

It allows you to ignore frequently modified garbage files.  You probably will need to continuously update things in the file.  For example, if you use VSCode, it will create files you should ignore.  If you open in OS X finder, it will create .DS_Store and you should ignore.

2.  Clone locally repo:  two options:  https and ssh

`git clone `

* ssh method.  Set up ssh key
A.  `ssh-keygen -t rsa` press return several times
B.  Save file in `~/.ssh/id_rsa.pub`
C.  Print out public key to stdout

```
cat ~/.ssh/id_rsa.pub
```

Will look like this:

```
i4mQCVoMgB6MBTLuKrQNkYCRPI8
i4mQCVoMgB6MBTLuKrQNkYCRPI8
blah...
```
D.  go to profile and add ssh-key (public key!!!).
E.  git clone your repo using ssh.

* How to do this in Cloud Shell

AA. Launch cloudshell
BB. create src directory: `mkdir -p src && cd src`
CC. do same steps as above



3.  Create a python virtual environment

if on cloud shell could be similar to:

```virtualenv  ~/.hello-github```
```source ~/.hello-github/bin/activate```

Optional add this to ```~/.bashrc``` and then ```source ~/.bashrc```

```bash
#alias
alias hello-github="cd ~/src/hello-github && source ~/.hello-github/bin/activate"

```


4.  Create a Makefile
5.  Create a requirements.txt

```
touch Makefile && touch requirements.txt
```
get inspiration from this repo:  https://github.com/noahgift/myrepo


fill out requirements.txt

```
pylint
pytest
black
jupyter
```

then install:

```make install```

6.  Check everything into github

this should show two files need to be added: ```Makefile``` and ```requirements```
```git status```

to add:

```git add *```
```git status```
```git commit -m "adding makefile"```
```git push``` #note you may need to configure your name and email.  Go ahead and do this.


7.  Create circleci account and add project

run these commands in shell:
```
mkdir -p .circleci && touch .circleci/config.yml
```

8.  Cut and paste sample config.yml file from site


```
# Python CircleCI 2.0 configuration file
#
version: 2
jobs:
  build:
    docker:
      - image: circleci/python:3.6.1

    working_directory: ~/repo

    steps:
      - checkout

      # Download and cache dependencies
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "requirements.txt" }}
            # fallback to using the latest cache if no exact match is found
            - v1-dependencies-

      - run:
          name: install dependencies
          command: |
            python3 -m venv venv
            . venv/bin/activate
            make install

      - save_cache:
          paths:
            - ./venv
          key: v1-dependencies-{{ checksum "requirements.txt" }}

      # run lint!

      - run:
          name: run lint
          command: |
            . venv/bin/activate
            make lint
```

Make a very simple hello script:
```touch hello.py```

```python
def say():
    return "hello"
print(say())
```



