# Basic coding tools - Git, Latek, and others



## Git

### Setup

*First* you need to install it.

```shell
sudo apt-get -y install git
```

*Then* to configure it :

```shell
git config --global user.name "name"
git config --global user.email "mail"
git config --global push.default current 
git config --global url."https://".insteadOf git://
```

The last line is useful if you are behind a firewall. **push.default current** will create a new remote branch with the same name as your local branch and connect them automatically when you push a new branch.

*Lastly* you need to automate your accesses to your online repositories.

Create a new pair of ssh key in ~/.ssh/ with :

```shell
ssh-keygen #generate a new new pair of asymetric key.
ssh-agent #start an agent that will automatically give the password of the privatekey for as long as it lives
ssh-add ~/.shh/id_rsa #enter password at this point to give the password to the agent
```

Now you have to give your public key to your online repos (in 'settings' for github and bitbucket for example).

You can copy your public-key with :

```shell
sudo apt-get install xclip
xclip -sel clip < ~/.ssh/id_rsa.pub
```

If you have a github account, you can *test* your configuration with :

```
ssh -T git@github.com #should output  You've successfully authenticated!
```

### Usecase

* view a previous commit in detached head

* ```shell
  git checkout 6e23a6a
  git checkout mybranch #tocomeback
  ```



# Latek

I will consider you don't lack space on your machine.

```shell
sudo apt-get install texlive-full qtikz
sudo apt-get install perl-tk --no-install-recommends ##for tlmgr
tlmgr init-usertree
```

You're basically ready...

You can use the gui tlmgr to install packages.

```shell
tlmgr --gui
```

### Usecase

I like using Makefiles to compile my tex documents (I got the idea from [Lilian Besson](http://perso.crans.org/besson/index.fr.html). They look like :

```bash
# Quick Makefile to compile easily the poster, uses PDFLaTeX (pdflatex) and BibTeX (bibtex)
all: clean pdf evince clean

pdf:
	pdflatex -synctex=1 my_doc.tex
	pdflatex -synctex=1 my_doc.tex
	# bibtex my_doc 
	# pdflatex -synctex=1 my_doc.tex
	# pdflatex -synctex=1 my_doc.tex

evince:
	-evince my_doc.pdf >/dev/null 2>/dev/null &

clean:
	-rm -rfv *.fls *.fdb_latexmk *.ps *.dvi *.htoc *.tms *.tid *.lg *.log *.id[vx] *.vrb *.toc *.snm *.nav *.htmp *.aux *.tmp *.out *.haux *.hidx *.bbl *.blg *.brf *.lof *.ilg *.ind *.meta *.fdb_latexmk *.fls *.synctex.gz*

# Download my script from https://bitbucket.org/lbesson/bin/src/master/PDFCompress
compress:
	PDFCompress my_doc.pdf
```



# Markdown

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
# add Typora's repository
sudo add-apt-repository 'deb https://typora.io ./linux/'
sudo apt-get update
sudo apt-get install typora
sudo apt-get install pandoc #for latex in markdown
```

It's the Best !

# Sublime

It's detailled [here](https://github.com/ThibaultGROUEIX/workflow_and_installs/tree/master/initial_steps.md)!



[![Analytics](https://ga-beacon.appspot.com/UA-91308638-2/github.com/ThibaultGROUEIX/workflow_and_installs/basic_coding_tools.md?pixel)](https://github.com/ThibaultGROUEIX/workflow_and_installs/)