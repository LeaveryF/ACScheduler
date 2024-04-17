# About Git

> Q: 为什么要在文档里面包含 git 的内容?
> 
> A: 菜

## submodule

### 添加 git 子模块

``` shell
git submodule add url path/to/submodule
```

### 更新 git 子模块

``` shell
git submodule update --remote path/to/submodule
```

### 子模块与 `.gitmodules` 同步

``` shell
git submodule sync
```

### 指定 submodule 的 branch

在 `.gitmodules` 中指定 `branch`, 然后使用 `git submodule sync`

``` plaintext
[submodule "submodule_name"]
    path = submodule_path
    url = submodule_repository_url
    branch = branch_name

```

### 指定 submodule 的 commit

在 `.gitmodules` 中指定 `branch`, 然后使用 `git submodule sync`

``` plaintext
[submodule "submodule_name"]
    path = submodule_path
    url = submodule_repository_url
    commit = commit_hash
```
