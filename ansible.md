# Ansible

Date: 2015-10-24 22:53
Tags: []
Categories: []

---

## Commands

- SUDO実行

        ansible-playbook hoge.yml -K

- 実行するタグを指定して実行

        ansible-playbook example.yml --tags "configuration,packages"

- スキップするタグを指定して実行

        ansible-playbook example.yml --skip-tags "manual"

- 実行開始するタスクを指定する

        ansible-playbook example.yml --start-at=hoge

- タスクごとに実行するかしないか選択する

        ansible-playbook example.yml --step

## Rules

### Tags

- manual : 手動実行が必要
- slow : 遅い
- fail : エラーになる
