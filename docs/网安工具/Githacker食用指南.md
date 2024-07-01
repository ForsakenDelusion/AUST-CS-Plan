---
profileName: FskDe7usion
postId: "68"
postType: post
categories:
  - 7
---
设备环境:Macos14.3 MacbookPro2021 14.2 zsh

- `git clone https://github.com/WangYihang/GitHacker`
- `cd GitHacker`
- `python3 -m venv venv`
- `source venv/bin/activate`
- `pip install -r requirements.txt`
- `python3 setup.py`
- `python3 -m pip install -i https://pypi.org/simple/ GitHacker`

博主是按照这个流程来走的,不知道顺序乱了有木有关系

运行的时候要先激活python的虚拟环境

`source venv/bin/activate`

然后输入

`githacker --url url --output-folder foldername`

然后输出的文件就在GitHacker目录下