---
layout: post
title: Git 配置多个 SSH Key
categories: SSH Git
---

以前使用 git 经常遇到这样的问题：
项目A 位于 github ，使用 ssh key A 提交代码；
项目B 位于 gitlab ，使用 ssh key B 提交代码。
这样本地就存储了两个私钥，在来回切换项目并提交代码的时候怎么办呢？

## 使用 ssh config 映射文件
在 `~/.ssh/` 文件下创建 `config` 文件，内容如下：
```shell
# github user
  Host github.com
  HostName github.com
  User git
  IdentityFile /Users/brandon/.ssh/id_rsa_github

# gitlab user
  Host gitlab.com
  HostName gitlab.com
  User git
  IdentityFile /Users/brandon/.ssh/id_rsa_gitlab
```
### 文件内容格式：

标签|描述
-|-
Host|仓库主机，对应具体项目下的`.git/config`中的`url`中的主机名
HostName|仓库主机名称
User| 用户名，对于 git 来说就是固定值 git
IdentityFile|ssh 私钥 路径

如上面描述的一样，`Host` 对应的是项目中的`.git`目录中`config`文件中的远程仓库url 的主机名，这样可以解决一个问题：假如项目 A 和项目 C 都位于 github，但是使用了不同的 ssh key 。
这种情况下可以使用如下配置：
- 项目 A 配置, 同上
- 项目 C 配置:
  - 项目 C/.git/config

  ```
  [remote "origin"]
	url = git@github2:brandon/project-c.git
  ```

 - ~/.ssh/config

  ```
  # github user
  Host github.com
  HostName github.com
  User git
  IdentityFile /Users/brandon/.ssh/id_rsa_github

  Host github2
  HostName github.com
  User git
  IdentityFile /Users/brandon/.ssh/id_rsa_github_2

  # gitlab user
  Host gitlab.com
  HostName gitlab.com
  User git
  IdentityFile /Users/brandon/.ssh/id_rsa_gitlab
  ```
## 验证 ssh key
使用如下命令可以验证配置是否正确:

```shell
ssh -T github.com
```

## 补充

之前切换仓库地址的时候经常使用`ssh-add`命令来添加私钥，
假如从 github 切换到 gitlab
```shell
# 删除 github 私钥
ssh-add -d /Users/brandon/.ssh/id_rsa_gitlab.pub
# 添加 gitlab 私钥
ssh-add /Users/brandon/.ssh/id_rsa_gitlab
```
__但是有了 `ssh config` 文件之后就不用这么麻烦了。__
