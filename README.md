# dotfiles

<!-- ![dotfiles](https://user-images.githubusercontent.com/499192/35094095-9943d7da-fc44-11e7-9dc5-a89b0938eeed.png) -->

.dotfiles, sensible hacker defaults for macOS.

[![Build Status](https://img.shields.io/travis/dotiful/dotfiles/master.svg?style=flat)](https://travis-ci.org/dotiful/dotfiles)
[![License](https://img.shields.io/github/license/dotiful/dotfiles.svg?style=flat)](https://github.com/dotiful/dotfiles/blob/master/LICENSE)

## Bootstrap / Install

There are a few different ways to bootstrap freckles. Depending on the state of your box, your proficiency and your general trust in random people on the internet, you can choose one of the methods below.

The main way of bootstrapping freckles is by utilizing inaugurate.

`inaugurate` supports two modes of install: either using user, or using root permissions.

### without elevated permissions

```sh
curl https://freckles.io | bash -s -- freckelize dotfiles -f gh:dotiful/dots
```

### with elevated permissions

```sh
curl https://freckles.io | sudo bash -s -- freckelize dotfiles -f gh:dotiful/dots
```

## Usage

### ansible-task

This is the most generic frecklecutable, it allows the execution of one Ansible module or role.

#### Create a folder using the file module

```sh
frecklecute ansible-task --task-name file --vars '{"path": "~/cool_folder", "state": "directory"}'
```

#### Install Homebrew on macOS using the geerlingguy.homebrew Ansible role

```sh
frecklecute --ask-become-pass true ansible-task --become --task-name geerlingguy.homebrew
```

> Depending on whether the system we run this on supports password-less sudo or not, we also need to add the –add-become-pass option.

#### Code

```yaml
#! /usr/bin/env frecklecute
doc:
  help: executes an ansible task or role
args:
  task_name:
    arg_name: task-name
    help: the name of the task or role
    required: true
    metavar: "TASK_OR_ROLE"
    is_var: false
  become_root:
    help: whether to become root for this task or not
    arg_name: become
    required: false
    is_flag: true
    default: false
    is_var: false
  vars_file:
    help: a file or json string containing vars for the specified task/role
    arg_name: vars
    multiple: false
    required: false
    is_var: true
    use_value: true
    type: freckles.utils.VarsTypeJson
tasks:
  - meta:
     name: "{{:: task_name ::}}"
     become: "{{:: become_root ::}}"
```

## License

[MIT](LICENSE) © [Dots Util](https://github.com/dotiful)
