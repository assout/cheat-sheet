# OpenShift

Date: 2015-08-16 18:24
Tags: []
Categories: []

---

## 構築

    rhc setup
    rhc app create management diy-0.1
    cd management
    git remote add github git@github.com:assout/collection-management.git

## Command

- sshログイン

        rhc ssh $app

- ログtail

        rhc tail -a myapp

## TODOs

- 文字コード変換方法

