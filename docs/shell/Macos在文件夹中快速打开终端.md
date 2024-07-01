---
profileName: FskDe7usion
postId: "66"
postType: post
categories:
  - 7
---
使用自动操作+AppleScript的方法

[参考文章](https://blog.csdn.net/weixin_43093163/article/details/131074213?ops_request_misc=%25257B%252522request%25255Fid%252522%25253A%252522170688932316800192259225%252522%25252C%252522scm%252522%25253A%25252220140713.130102334.pc%25255Fall.%252522%25257D&request_id=170688932316800192259225&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-131074213-null-null.142%5Ev99%5Epc_search_result_base5&utm_term=mac%2520%25E6%2596%2587%25E4%25BB%25B6%25E5%25A4%25B9%2520%25E7%25BB%2588%25E7%25AB%25AF&spm=1018.2226.3001.4187)

- 打开`自动操作`
- 新建应用程序
- 切换实用工具
- 运行AppleScript
- 贴代码

```script
on run {input, parameters}

tell application "Finder"

set currFolder to (POSIX path of (folder of the front window as string))

end tell

tell application "Terminal"

activate

do script ("cd " & "'" & currFolder & "'")

end tell

end run
```