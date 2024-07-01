

2024-02-20

[shell](https://yfi.moe/tags/shell) | [python](https://yfi.moe/tags/python) | [教程向](https://yfi.moe/tags/%E6%95%99%E7%A8%8B%E5%90%91) | [环境配置](https://yfi.moe/tags/%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE) | [conda](https://yfi.moe/tags/conda)

Conda 对你的 Shell 做了什么，从而让你可以使用 activate、deactivate 等命令？

从顶向下，本文先说管理环境时最常用的命令 `activate` 是如何作用于 shell 环境的；然后看一看在 shell 的初始化阶段，`conda` 命令和它的环境是如何准备就绪的；了解了以上内容，自然而然就会配置 shell 以使用 conda 了（操作很简单，但是原理还是有些复杂的）。

本文针对在 Unix-like 系统（Linux/macOS）上的 conda 编写，如果是 Windows，建议还是使用 Anaconda Prompt 吧。

Note

本文以在 macOS 上用 Homebrew 安装的 Anaconda ( 2024 年初时候的最新版本 ) 配合 zsh 为例。

如果使用其他 conda，大同小异；只要把安装目录改成自己的就行。（本文中都是 `/opt/homebrew/anaconda3`，替换这个即可）

如果使用 bash，配置过程几乎没有区别；如果使用 fish，则区别较大。

## 开胃菜：activate 做了什么？

简单来说，与本文主题相关的（也是最显而易见的）改变就是改变了 `PATH` 环境变量。

对于 activate，就是在 PATH 最前面加了对应环境的 bin 目录路径。比如，激活 base 环境就是把 `/opt/homebrew/anaconda3/bin` 加到 PATH 最前面；激活 example 环境就是把 `/opt/homebrew/anaconda3/envs/example/bin` 加到 PATH 最前面。

那么 deactivate 做的事情也就很显然了：将对应的路径从 PATH 里删除。

Tip

如果你对 PATH 变量是什么还不了解，一个非常简单的理解就是，输入命令时，shell 会从这些目录里寻找和命令同名的可执行程序运行。

而这个寻找的顺序是从前向后的，找到第一个后即停止。因此，如果在 PATH 中有多个同名的程序，那么会使用在 PATH 靠前的那个。

## 启动 shell 时，发生了什么？

在 2017 年发布的 conda 4.4.0 版本中，对于非 Windows 系统上的 init 流程做了很大的修改；而在 2019 年的 conda 4.6.0 版本中，将原本在 2.x 版本废弃的 `conda init` 命令重新利用了起来，现在是为 conda 配置 shell 的推荐方案。

具体来说，主要的改变在于：

1. 不要在初始化脚本（比如 `~/.zshrc` ）中将 `/opt/homebrew/anaconda3/bin` 放入 PATH，而是使用 `conda init` 命令管理初始化脚本中和 conda 相关的内容
2. 使用 `conda activate env_name` ，而不是 `source activate env_name` 命令。

> 译自 [conda 4.4 Release Notes](https://github.com/conda/conda/releases/tag/4.4.0)
> 
> **conda activate**: The logic and mechanisms underlying environment activation have been reworked. With conda 4.4, `conda activate` and `conda deactivate` are now the preferred commands for activating and deactivating environments. You’ll find they are much more snappy than the `source activate` and `source deactivate` commands from previous conda versions. The `conda activate` command also has advantages of (1) being universal across all OSes, shells, and platforms, and (2) not having path collisions with scripts from other packages like python virtualenv’s activate script.
> 
> **conda activate**：重新设计了环境激活的逻辑和机制。在 conda 4.4 中， `conda activate` 和 `conda deactivate` 现在是激活和停用环境的首选命令。您会发现它们比以前 conda 版本中的 `source activate` 和 `source deactivate` 命令要活泼得多。 `conda activate` 命令还具有以下优点：（1） 在所有操作系统、shell 和平台上都是通用的，并且 （2） 不会与其他软件包（如 python virtualenv 的激活脚本）中的脚本发生路径冲突。

为了保持向后兼容，原本的方法目前都还能用。但是，在新推荐做法发布接近 7 年后，能搜到的大部分教程/笔记依然在用 `source activate` 的老办法，这是非常令人诧异的（也是本文诞生的重要原因之一）。

一步一步来，先看看 conda init 干了什么来帮助我们配置环境。

### conda init 干了什么？

用法就是 `conda init zsh` 或者其他你用的 shell，它便会自动帮你修改好所有相关的脚本。

如果是新安装的 Anaconda，提示找不到 conda 怎么办？直接用安装目录下 `…/condabin/conda` 即可。如 `/opt/homebrew/anaconda3/condabin/conda init zsh`。

运行结果如下：

```
$ conda init zsh
no change     /opt/homebrew/anaconda3/condabin/conda
no change     /opt/homebrew/anaconda3/bin/conda
no change     /opt/homebrew/anaconda3/bin/conda-env
no change     /opt/homebrew/anaconda3/bin/activate
no change     /opt/homebrew/anaconda3/bin/deactivate
no change     /opt/homebrew/anaconda3/etc/profile.d/conda.sh
no change     /opt/homebrew/anaconda3/etc/fish/conf.d/conda.fish
no change     /opt/homebrew/anaconda3/shell/condabin/Conda.psm1
no change     /opt/homebrew/anaconda3/shell/condabin/conda-hook.ps1
no change     /opt/homebrew/anaconda3/lib/python3.11/site-packages/xontrib/conda.xsh
no change     /opt/homebrew/anaconda3/etc/profile.d/conda.csh
modified      /Users/chris/.zshrc

==> For changes to take effect, close and re-open your current shell. <==
```

可以看到，conda 对上面这么多文件进行了检查。对于我们来说，需要操心的只有 `~/.zshrc` 文件，看看 conda 对它做了什么。

打开 `~/.zshrc`，发现多出了如下内容：

```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/opt/homebrew/anaconda3/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/opt/homebrew/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/opt/homebrew/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/opt/homebrew/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

首先是前后两个注释，conda 靠他来定位这段代码的位置，所以你可以把这段代码完整地移到文件的其他位置而不用担心下次 conda init 时 conda 找不到它，以为不存在而重新加一遍。

然后是代码内容。虽然 shell 脚本一直以晦涩难懂知名，但是这段代码逻辑还是很清晰的。用自然语言简单地复述一下大致意思：

- 运行 `/opt/homebrew/anaconda3/bin/conda shell.zsh hook` 这条命令，将命令的输出赋值给变量 `__conda_setup`
- 如果上一条命令的运行是成功的，那么运行 `__conda_setup` 中的内容
- 如果不成功，那么：
    - 检查 `/opt/homebrew/anaconda3/etc/profile.d/conda.sh` 是否存在
    - 存在则运行它
    - 不存在，则将 `/opt/homebrew/anaconda3/bin` 附加到 PATH 前面

可以看出，这里的逻辑主要是错误处理，如果一切正常，那么应该是将 `/opt/homebrew/anaconda3/bin/conda shell.zsh hook` 的输出作为命令运行；而在一切都不正常时，回退到 4.4 版本之前的推荐方式：直接添加 bin 目录到 PATH 中。

此时再打开一个新的 shell，conda 应该就已经准备好工作了！

Tip

**如何应用 `~/.zshrc` 中的更改？**

很多教程/笔记都使用了 `source ~/.zshrc` 的办法，但是这不会清理原本 shell 中的各种乱七八糟的东西，因此 oh-my-zsh 的文档直言这是一个 “common **wrong** suggestion”。  
前往查看 [oh-my-zsh - FAQ - How do I reload the zshrc file?](https://github.com/ohmyzsh/ohmyzsh/wiki/FAQ#how-do-i-reload-the-zshrc-file)

简单来说，正确的方法应该是直接关闭再打开终端，或者运行 `exec zsh` 来重启 zsh。或者，如果你使用 oh-my-zsh，可以直接使用它提供的 `omz reload` 命令。

然而经过我的测试，即使是 `exec zsh` 或是 `omz reload` 命令也不会清理环境变量；因此，如果需要非常严格的“重启”，最好还是关了终端重开。

### 更深入些

此时，我们知道了 eval `conda shell.zsh hook` 命令的输出可以帮助我们配置好 shell 环境。但是，它又是怎么做到的呢？

如果尝试运行一下 `which conda`，发现此时的 conda 既不是 `/opt/homebrew/anaconda3/bin/conda`，也不是 `/opt/homebrew/anaconda3/condabin/conda`，而是一个 shell 函数。

运行 `conda shell.zsh hook`，可以得到以下输出（比较多，有删减）

```
export CONDA_EXE='/opt/homebrew/anaconda3/bin/conda'
...
__conda_activate() {
  ...
}
...
conda() {
  ...
}

if [ -z "${CONDA_SHLVL+x}" ]; then
    \export CONDA_SHLVL=0
    # In dev-mode CONDA_EXE is python.exe and on Windows
    # it is in a different relative location to condabin.
    if [ -n "${_CE_CONDA:+x}" ] && [ -n "${WINDIR+x}" ]; then
        PATH="$(\dirname "$CONDA_EXE")/condabin${PATH:+":${PATH}"}"
    else
        PATH="$(\dirname "$(\dirname "$CONDA_EXE")")/condabin${PATH:+":${PATH}"}"
    fi
    \export PATH
    ...
fi
```

最关键的是提供了 conda 函数，也就是我们 which 出来的那个；这个 conda 函数可以调用其他的类似 `__conda_activate` 的 shell 函数，据说是用于提高性能。

在最后，还有一个 if 段，先查看 CONDA_SHLVL 环境变量有没有被设置，如果没有被设置，就先设为 0，再将安装目录下的 condabin 加进 PATH 里，然后设置下 PS1（shell 提示符）；如果已经被设置了，说明已经初始化过，不做操作。

关于 CONDA_SHLVL 环境变量，简单来说就是目前 conda activate 的嵌套层数，由于与本文主题关系不大，就不展开了。

### 简单总结

在一切都没有错误发生时，启动流程应该是这样的：通过 `conda init` 生成的代码在启动新终端时被调用；其中设置了 conda 这个 shell 函数和 `/opt/homebrew/anaconda3/condabin` 这个 PATH。

其实很简单明了，不是吗？

回头看，当我们在终端中敲下一个 conda 命令然后回车时，实际上有可能调用的是三个不同的 conda：

- 名为 conda 的 shell 函数，如果初始化过程没出问题的话，就是它。
- `/opt/homebrew/anaconda3/condabin/conda` 如果使用 conda init，理论上不可能直接调用到它，但是因为它在 PATH 里，所以如果哪里搞糊了还是有可能调用到它的。
- `/opt/homebrew/anaconda3/bin/conda` 这个文件的内容和上一个其实是一样的。它是在 4.4 版本之前的推荐操作；同时也是现在版本在 init 出问题时候的回退操作。

## 从安装开始的设置指南

对于 macOS，首先 `brew install anaconda`。这样，Anaconda 就被安装到了 `/opt/homebrew/anaconda3` 这个文件夹下（如果使用 Apple Silicon 的机器）。

Note

对于 Linux 用户（和不愿意用 Homebrew 的 macOS 用户），只需要了解自己的安装目录，然后在之后把 `/opt/homebrew/anaconda3` 替换成自己的即可。[参考文档](https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html) 。

而且这些安装脚本一般都有一些选项，选得好的话，直接就把下面调用 conda init 的过程帮你做好了，相当于是开箱即用的状态。  
以 miniconda 在 Linux 下的安装为例，他会问是否希望跑 conda init，这里默认选项是 no，如果输入 yes，那么就自动配好了环境；如果保持默认，按照下面的方法操作即可。

此时，只是安装好了 Anaconda 本身，还没有任何和 shell 相关的事情发生——也就是说，在终端 `conda` 命令还不可用。

Tip

如果使用 Homebrew 安装 miniconda，那么会将 `/opt/homebrew/Caskroom/miniconda/condabin/conda` 符号链接到 `/opt/homebrew/bin`，相当于就有一个开箱即用的 conda 命令；当然，依旧需要运行 init 来使最后的 conda 命令变为一个 shell 函数。

然后，运行 `/opt/homebrew/anaconda3/condabin/conda init zsh` （或者其他你使用的 shell）。

重启终端。此时，base 环境应该已经正确激活！

一共就两个命令；`conda init` 大幅简化了配置体验，现在完全不用手动改 `~/.zshrc` 等配置文件了。

### 卸载

卸载 conda 简单来说就是把安装目录直接 rm 掉就行，如果你没有使用过自定义 prefix 的环境，那么它不会在其他地方拉屎；

不过，推荐在直接 rm 前跑一下 `conda init --reverse --all` 来撤销对所有 shell profile 的更改。

如果你对“卸载干净”这件事很严苛，那么 conda 还会在主目录下留下这些配置文件，可以一并 rm 掉：

```
rm -rf ~/.condarc ~/.conda ~/.continuum
```

## 拓展阅读

- [pyenv 与 conda 双轨制：管理 Python 版本和环境](https://yfi.moe/post/pyenv-conda-together)：我写的另一篇关于 Python 环境的文章，配置了普通 Python 与 Conda 安装的 Python 随意切换的 shell 环境。
- [conda init and conda activate — conda 24.1.2 documentation](https://docs.conda.io/projects/conda/en/stable/dev-guide/deep-dives/activation.html#conda-activate) Conda 文档关于 init | activate 的 “Deep Dive”，可以了解一下；同时也介绍了激活/停用脚本，可以在激活/停用时被调用。

本文难免有遗漏或是错误，如果发现，请一定在评论区指出！