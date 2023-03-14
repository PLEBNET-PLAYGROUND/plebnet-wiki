SHELL                                   := /bin/bash
PWD 									?= pwd_unknown
TIME 									:= $(shell date +%s)
export TIME

HOMEBREW                                := $(shell type -P brew)
export HOMEBREW

PYTHON                                  := $(shell which python)
export PYTHON
PYTHON2                                 := $(shell which python2)
export PYTHON2
PYTHON3                                 := $(shell which python3)
export PYTHON3

PIP                                     := $(notdir $(shell which pip))
export PIP
PIP2                                    := $(notdir $(shell which pip2))
export PIP2
PIP3                                    := $(notdir $(shell which pip3))
export PIP3

ifeq ($(PYTHON3),/usr/local/bin/python3)
PIP                                    := pip
PIP3                                   := pip
export PIP
export PIP3
endif

PYTHON_VENV                             := $(shell python  -c "import sys; sys.stdout.write('1') if hasattr(sys, 'base_prefix') else sys.stdout.write('0')")
PYTHON3_VENV                            := $(shell python3 -c "import sys; sys.stdout.write('1') if hasattr(sys, 'real_prefix') else sys.stdout.write('0')")
export PYTHON_VENV
export PYTHON3_VENV
ifeq ($(PYTHON_VENV),0)
USER_FLAG:=--user
else
USER_FLAG:=	
endif

ifeq ($(project),)
PROJECT_NAME							:= $(notdir $(PWD))
else
PROJECT_NAME							:= $(project)
endif
export PROJECT_NAME
TWITTER_API=$(PWD)/TwitterAPI
export TWITTER_API
ifeq ($(port),)
PORT									:= 0
else
PORT									:= $(port)
endif
export PORT

#GIT CONFIG
GIT_USER_NAME							:= $(shell git config user.name || echo $(PROJECT_NAME))
export GIT_USER_NAME
GH_USER_NAME							:= $(shell git config user.name || echo $(PROJECT_NAME))
#MIRRORS
GH_USER_REPO							:= $(GH_USER_NAME).github.io
GH_USER_SPECIAL_REPO					:= $(GH_USER_NAME)
KB_USER_REPO							:= $(GH_USER_NAME).keybase.pub
#GITHUB RUNNER CONFIGS
ifneq ($(ghuser),)
GH_USER_NAME := $(ghuser)
GH_USER_SPECIAL_REPO := $(ghuser)/$(ghuser)
endif
ifneq ($(kbuser),)
KB_USER_NAME := $(kbuser)
KB_USER_REPO := $(kbuser).keybase.pub
endif
export GIT_USER_NAME
export GH_USER_REPO
export GH_USER_SPECIAL_REPO
export KB_USER_REPO

GIT_USER_EMAIL							:= $(shell git config user.email || echo $(PROJECT_NAME))
export GIT_USER_EMAIL
GIT_SERVER								:= https://github.com
export GIT_SERVER
GIT_SSH_SERVER							:= git@github.com
export GIT_SSH_SERVER
GIT_PROFILE								:= $(shell git config user.name || echo $(PROJECT_NAME))
export GIT_PROFILE
GIT_BRANCH								:= $(shell git rev-parse --abbrev-ref HEAD 2>/dev/null || echo $(PROJECT_NAME))
export GIT_BRANCH
GIT_HASH								:= $(shell git rev-parse --short HEAD 2>/dev/null || echo $(PROJECT_NAME))
export GIT_HASH
GIT_PREVIOUS_HASH						:= $(shell git rev-parse --short master@{1} 2>/dev/null || echo $(PROJECT_NAME))
export GIT_PREVIOUS_HASH
GIT_REPO_ORIGIN							:= $(shell git remote get-url origin 2>/dev/null || echo $(PROJECT_NAME))
export GIT_REPO_ORIGIN
GIT_REPO_NAME							:= $(PROJECT_NAME)
export GIT_REPO_NAME
GIT_REPO_PATH							:= $(HOME)/$(GIT_REPO_NAME)
export GIT_REPO_PATH

BASENAME := $(shell basename -s .git `git config --get remote.origin.url` || echo $(PROJECT_NAME))
export BASENAME

NODE_VERSION                           :=v16.19.1
export NODE_VERSION
NODE_ALIAS                             :=v16.19.0
export NODE_ALIAS
NVM_DIR                                :=$(HOME)/.nvm
export NVM_DIR
PACKAGE_MANAGER                        :=yarn
export PACKAGE_MANAGER
PACKAGE_INSTALL                        :=add
export PACKAGE_INSTALL


# Force the user to explicitly select public - public=true
# export KB_PUBLIC=public && make keybase-public
ifeq ($(public),true)
KB_PUBLIC  := public
else
KB_PUBLIC  := private
endif
export KB_PUBLIC

ifeq ($(libs),)
LIBS  := ./libs
else
LIBS  := $(libs)
endif
export LIBS

SPHINXOPTS            =
SPHINXBUILD           = sphinx-build
PAPER                 =
BUILDDIR              = _build
PRIVATE_BUILDDIR      = _private_build

# Internal variables.
PAPEROPT_a4           = -D latex_paper_size=a4
PAPEROPT_letter       = -D latex_paper_size=letter
ALLSPHINXOPTS         = -d $(BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) $(SPHINXOPTS) .
PRIVATE_ALLSPHINXOPTS = -d $(PRIVATE_BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) $(SPHINXOPTS) .
# the i18n builder cannot share the environment and doctrees with the others
I18NSPHINXOPTS  = $(PAPEROPT_$(PAPER)) $(SPHINXOPTS) .

-:
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?##/ {printf "\033[36m%-15s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

.PHONY: init
.ONESHELL:
init:## 	DL pandoc & pip install requirements.txt
	type -P pandoc || \
		type -P curl && \
		curl -LJO https://github.com/jgm/pandoc/releases/download/3.1/pandoc-3.1-macOS.pkg | echo ""
	type -P pandoc || \
		type -P curl && \
		curl -LJO https://github.com/jgm/pandoc/releases/download/3.1/pandoc-3.1-linux-arm64.tar.gz | echo ""
	type -P pandoc || \
		type -P curl && \
		curl -LJO https://github.com/jgm/pandoc/releases/download/3.1/pandoc-3.1-linux-amd64.tar.gz | echo ""
	$(PYTHON3) -m pip install $(USER_FLAG) --upgrade pip
	$(PYTHON3) -m pip install $(USER_FLAG) -r $(PWD)/requirements.txt
	#pandoc -f mediawiki --metadata title="" -t html -s export/Welcome_to_Plebnet.wiki -o index.en.wiki
	#pandoc -f mediawiki --metadata title="" -t html5 -s index.en.wiki -o index.en.html
	#pandoc -f mediawiki --metadata title="" -t html5 -s index.en.wiki -o index.en.html
	sed -i .bak '1d' index.en.html
#<p>&lt;!DOCTYPE html&gt;</p>
	sed 's/<p>&lt;!DOCTYPE html&gt;<\/p>/ /' index.en.html > index.html

help:## 	verbose help
	@echo verbose $@
	@sed -n 's/^##//p' ${MAKEFILE_LIST} | column -t -s ':' |  sed -e 's/^/ /'
get-plebnet-wiki:## 	python3 exportMediaWiki2Html.py --url https://plebnet.wiki
	python3 exportMediaWiki2Html.py --url https://plebnet.wiki
wiki:## 	make wiki...
	#@for i in ./export/*.html; do echo $i; done
	@for i in ./export/*.html; do pandoc -f html -t mediawiki -s $$i > $$i.wiki; done;
twitter-api:pyjq## 	twitter-api
	#@echo pip3 install $(USER_FLAG) twint
	echo pip3 install $(USER_FLAG) TwitterAPI
	[ -d "$(PWD)/TwitterAPI" ] && pushd $(PWD)/TwitterAPI && $(PYTHON3) setup.py install $(USER_FLAG) || git clone https://github.com/geduldig/TwitterAPI.git && pushd $(PWD)/TwitterAPI && $(PYTHON3) setup.py install $(USER_FLAG)
.PHONY: report
report:
	@echo ''
	@echo '[ENV VARIABLES]	'
	@echo ''
	@echo 'TIME=${TIME}'
	@echo 'BASENAME=${BASENAME}'
	@echo 'PROJECT_NAME=${PROJECT_NAME}'
	@echo 'TWITTER_API=${TWITTER_API}'
	@echo 'PYTHON_VENV=${PYTHON_VENV}'
	@echo 'PYTHON3_VENV=${PYTHON3_VENV}'
	@echo ''
	@echo 'NODE_VERSION=${NODE_VERSION}	'
	@echo 'NODE_ALIAS=${NODE_ALIAS}	'
	@echo ''
	@echo 'HOMEBREW=${HOMEBREW}'
	@echo ''
	@echo 'GIT_USER_NAME=${GIT_USER_NAME}'
	@echo 'GH_USER_REPO=${GH_USER_REPO}'
	@echo 'GH_USER_SPECIAL_REPO=${GH_USER_SPECIAL_REPO}'
	@echo 'KB_USER_REPO=${KB_USER_REPO}'
	@echo 'GIT_USER_EMAIL=${GIT_USER_EMAIL}'
	@echo 'GIT_SERVER=${GIT_SERVER}'
	@echo 'GIT_PROFILE=${GIT_PROFILE}'
	@echo 'GIT_BRANCH=${GIT_BRANCH}'
	@echo 'GIT_HASH=${GIT_HASH}'
	@echo 'GIT_PREVIOUS_HASH=${GIT_PREVIOUS_HASH}'
	@echo 'GIT_REPO_ORIGIN=${GIT_REPO_ORIGIN}'
	@echo 'GIT_REPO_NAME=${GIT_REPO_NAME}'
	@echo 'GIT_REPO_PATH=${GIT_REPO_PATH}'

.PHONY: super
super:
ifneq ($(shell id -u),0)
	@echo switch to superuser
	@echo cd $(TARGET_DIR)
	#sudo ln -s $(PWD) $(TARGET_DIR)
#.ONESHELL:
	sudo -s
endif

.PHONY: docs
docs:##
	#@echo docs
	bash -c 'if pgrep MacDown; then pkill MacDown; fi'
	bash -c 'cat $(PWD)/export/HEADER.md                >  $(PWD)/README.md'
	bash -c 'cat $(PWD)/export/COMMANDS.md              >> $(PWD)/README.md'
	bash -c 'cat $(PWD)/export/FOOTER.md                >> $(PWD)/README.md'
	@if hash pandoc 2>/dev/null; then echo; fi || $(HOMEBREW) install pandoc
	bash -c 'pandoc -s README.md -o index.html'
	git add --ignore-errors export/*.md
	git add --ignore-errors *.md
	#git ls-files -co --exclude-standard | grep '\.md/$\' | xargs git

checkbrew:## 	checkbrew
ifeq ($(HOMEBREW),)
	@/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
else
	@type -P brew
endif

submodules:checkbrew## 	submodules
	@git submodule update --init --recursive
#	@git submodule foreach --recursive "git submodule update --init --recursive"

.PHONY: nvm
.ONESHELL:
nvm: ## 	nvm
	@curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash || git pull -C $(HOME)/.nvm && export NVM_DIR="$(HOME)/.nvm" && [ -s "$(NVM_DIR)/nvm.sh" ] && \. "$(NVM_DIR)/nvm.sh" && [ -s "$(NVM_DIR)/bash_completion" ] && \. "$(NVM_DIR)/bash_completion"  && nvm install $(NODE_VERSION) && nvm use $(NODE_VERSION)
	# @source ~/.bashrc && nvm alias $(NODE_ALIAS) $(NODE_VERSION)

clean-nvm: ## 	clean-nvm
	@rm -rf ~/.nvm

.PHONY: clean
.ONESHELL:
clean: touch-time touch-global## 	clean
	bash -c "rm -rf $(BUILDDIR)"

.PHONY: serve
.ONESHELL:
serve:## 	serve
	bash -c "$(PYTHON3) -m http.server $(PORT) -d . &"

include venv.3.11.mk
include venv.3.10.mk
include venv.3.8.mk
include venv.3.7.mk
