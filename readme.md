# 互联网数据集

我的[搜索引擎](https://github.com/RimoChan/sese-engine)已经运行了半年了，收集到了不少有用的数据。

我想，这些数据应该还是挺有价值的，不如就把它们拿出来和大家一起分享吧。


## 数据量

数据量正在持续增长中，截至2022年5月大约有48.9G的数据，包含这些内容——

- 域名数据<sub>(2.7G)</sub>包含6257636个域名，来自1938617个一级域名。

- 网页数据<sub>(6.4G)</sub>包含53294027个网页。其中有标题的网页有48577906个，有介绍的网页有35971682个。

- 反向索引数据<sub>(39.7G)</sub>包含17669628个词，每个词对应1~28000个网页。


## 下载地址

你可以选一个自己喜欢的地方下载: 

- [GitHub Release](https://github.com/RimoChan/internet-dataset/releases)

- [OneDrive](https://v0vxj-my.sharepoint.com/:f:/g/personal/rimochan_v0vxj_onmicrosoft_com/EqRakuQVVjBDqMyU8xd7NnEB3MZrDZxDwPTVXK7tNv5Rqw?e=cXQMod )<sub> (感谢[@skoqaq](https://github.com/skoqaq)帮我传了OneDrive) </sub>


## 数据内容

- 域名级别
  - ip
  - 最后访问时间
  - 访问次数 <sub>(搜索引擎爬取该域名下页面的次数，数值越高，其他的字段越可靠)</sub>
  - 语种 <sub>(fasttext的语种识别结果，对该域名下的所有网页滑动平均)</sub>
  - 链接 <sub>(该域名下的所有网页的指向其他域名的链接，滑动抽样200个左右)</sub>
  - ======下面的属性只针对该域名的首页======
  - 重定向
  - https可用
  - 关键词 <sub>(频率最高的词)</sub>
  - 结构 <sub>(将HTML结构映射到字符串，用于过滤模板生成的大量域名)</sub>

- 网页级别
  - 网页的标题
  - 网页的介绍 <sub>(meta description，截断到256字符)</sub>

注意: 

- ip字段并不完整，基本上是东亚地区的解析结果。

- 如果网站是动态的，关键词就不可靠<sub>(比如腾讯首页)</sub>。中文和英文以外的网站也不可靠。

- 与语言相关的字段都是有偏的。以GitHub语种识别结果为例，实际的中文内容比例达不到`21%`。出现这个差别的原因是因为在选择爬取目标时，中文域名的权重更高，而中文域名链接到GitHub中的中文repo的概率也更高，因此滑动平均的结果上中文的比例会高。

- 有些域名会缺字段，这个是正常的。主要原因是有些字段是后来陆续加上的，没有回扫或者只回扫了一部分。

此外，还有一些没有列出的字段，它们大多是没有意义或者是已经被废弃的字段。看到的话不用去管它们就行了。


## 样例

- `https://github.com/`的网页信息

```json
[
  "GitHub: Where the world builds software · GitHub", 
  "GitHub is where over 83 million developers shape the future of software, together. Contribute to the open source community, manage your Git repositories, review code like a pro, track bugs and features, power your CI/CD and DevOps workflows, and secure cod"
]
```

- `github.com`的域名信息

```json
{
  "https可用": true,
  "ip": ["20.205.243.166"],
  "关键词": ["github", "your", "you", "code", "octocat", "classifier", "all", "actions", "s", "build", "open", "sign", "pull", "up", "learn", "world", "more", "community", "review", "readme", "requests", "security", "merge", "software", "git", "https", "source", "developers", "jump", "can", "repositories", "added", "packages", "cli", "codespaces", "million", "developer", "available", "windows", "cloud"],
  "最后访问时间": 1653115624,
  "结构": "[[20,[[18,[1,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,21,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,1,1,1,3,3,3,1,3]],[19,[[0,[[32,[[0,[[0,[0,[0,[14]]]],[0,[[0,[14]],11,[0,[[0,[[0,[[0,[[16,[[10,[7,7,7,0]]]]]]]]]],0]]]]]]]]]],0,[0,[[38,[[0,[[0,[14,0]]]]]]]],\"include-fragment\",[0,[[44,[[0,[[0,[[0,[[0,[[0,[[0,[30,[16,[[0,[[17,[[15,[10]],[9,[7]]]],7,14]]]],[0,[[0,[[0,[[0,[[0,[4]],[0,[4]],[0,[4]],[0,[5]]]]]]",
  "访问次数": 77611.09999999784,
  "语种": {
    "de": 2.9202289595753074e-144,
    "en": 0.7864020173491018,
    "es": 1.4926505740925807e-174,
    "eu": 4.945433385112884e-144,
    "fa": 4.925068154131393e-158,
    "fr": 4.82696545869921e-22,
    "id": 6.915482390917134e-232,
    "ja": 7.04053776049145e-18,
    "pl": 1.6722448457286058e-146,
    "pt": 7.166986359316283e-264,
    "ru": 1.98435737486779e-25,
    "sk": 4.743657699245051e-30,
    "uk": 1.1930933763516414e-168,
    "zh": 0.2135979826508982
  },
  "链接": ["https://repl.it/github/rust-lang/rustlings", "https://packagist.org/packages/tomsgad/laravel-beem", "https://opensource.guide", "https://github.blog", "https://www.githubstatus.com/", "http://en.wiktionary.org/wiki/bikeshedding", "https://www.githubstatus.com/", "https://github.community", "https://gitter.im/hexo-theme-matery/Lobby?utm_source=badge", "https://codeclimate.com/github/indutny/elliptic", "https://github.blog", "https://github.blog", "https://github.blog", "https://oscarotero.com", "https://github.blog", "https://www.githubstatus.com/", "https://p00q.cn/", "https://opensource.guide", "https://avatars.githubusercontent.com/u/92483627?v=4", "http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html", "https://laravel.com/docs/9.x/notifications", "https://github.blog", "https://spiritree.me", "https://avatars.githubusercontent.com/u/7127720?v=4", "https://github.community", "https://halo.run", "https://opensource.guide", "https://github.blog", "https://entgo.io/blog/2019/10/03/introducing-ent", "https://www.githubstatus.com/", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://opensource.guide", "https://github.co/hiddenchars", "https://avatars.githubusercontent.com/u/6613431?v=4", "http://www.hjljy.cn", "https://opensource.guide", "http://tools.ietf.org/html/rfc6979", "https://github.co/hiddenchars", "https://github.co/hiddenchars", "https://opensource.guide", "https://isoyu.com/?q=%7B$q%7D&si=1&l=zh&s=1&a=1&i=1", "https://github.community", "https://github.blog", "https://github.blog", "https://github.community", "https://github.blog", "https://pypi.python.org/pypi/py2exe/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.community", "https://github.community", "https://vimin.cc/", "https://crt.sh", "https://sourceforge.net/projects/pywin32/files/pywin32/Build%20221/", "https://github.community", "https://www.githubstatus.com/", "https://github.co/hiddenchars", "https://720kb.github.io/angular-datepicker", "http://nodeschool.io/", "https://www.githubstatus.com/", "https://opensource.guide", "https://opensource.guide", "https://github.community", "https://camo.githubusercontent.com/5560d191da93fee2302b31dfce3ac6030ba9566d72a91d4320c619f31214cae5/68747470733a2f2f73332e65752d63656e7472616c2d312e616d617a6f6e6177732e636f6d2f656e74676f2e696f2f6173736574732f676f706865725f67726170682e706e67", "https://opensource.guide", "https://isoyu.com/?q=%7B$q%7D&cr=gbk", "https://camo.githubusercontent.com/bbe521da90754f81af5f5b347384c282e076e360f4f5e4350b0d87e388563b12/68747470733a2f2f706963342e7a68696d672e636f6d2f38302f76322d31363365303636636239373039383132386232386638663666663166646265625f68642e6a7067", "https://github.blog", "https://github.blog", "https://github.co/hiddenchars", "https://camo.githubusercontent.com/67366b97ec46e73f9cad77bf59d6da9991cc912e015c904a58e266432f535732/68747470733a2f2f616530312e616c6963646e2e636f6d2f6b662f48544231316f4370626d6632674b306a535a4650373630736f705861332e706e67", "https://github.community", "https://discord.gg/qZmPgTE6RX", "https://opensource.guide", "https://github.blog", "https://cdpn.io/e/rmBbWe", "https://camo.githubusercontent.com/85fc65cc3b21a418c61b22a0383160879dfc7a656c5df06af146391bc43abd85/68747470733a2f2f6769746875622d726561646d652d73746174732e76657263656c2e6170702f6170692f746f702d6c616e67732f3f757365726e616d653d6e656c6c613137267468656d653d64656661756c74266c61796f75743d636f6d7061637426636172645f77696474683d343435", "https://camo.githubusercontent.com/b8ff2be1b6df10e75a63112bd440bfccc533e86bb659f295c96cf596f5243b5b/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f776568616f782f5479706563686f2d427574746572666c793f636f6c6f723d464635353331", "http://safecurves.cr.yp.to/", "https://github.blog", "http://code.google.com/p/explorercanvas", "https://camo.githubusercontent.com/1a4946c5763eab701e905aba96bdf388397bf80bad3cb6f8492bc5e632466f01/687474703a2f2f692e696d6775722e636f6d2f3935456c4d796b2e676966", "https://coveralls.io/github/indutny/elliptic?branch=master", "https://github.blog", "https://opensource.guide", "https://github.community", "https://opensource.guide", "https://google.com?test=abc", "https://opensource.guide", "https://entgo.io", "https://github.blog", "https://github.community", "https://github.blog", "https://github.community", "http://www.edge-security.com/", "https://www.githubstatus.com/", "https://www.blueskyxn.com/202102/4142.html", "https://camo.githubusercontent.com/ca91ff24a662fc02f64cfed3446fadc7d84dade01a698ebe3dd7b3710926489a/687474703a2f2f7374617469632e626c696e6b666f782e636f6d2f6d61746572792d32303138313230322d312e706e67", "https://camo.githubusercontent.com/3aa25aa8a40740aa4f825987a2ff72f19978d9c18ed8090d3c613645f3255f0d/68747470733a2f2f7777772e7665696c2d6672616d65776f726b2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031332f31322f63726f707065642d5665696c2d53796d626f6c322e706e67", "https://help.eyeo.com/en/adblockplus/how-to-write-filters", "https://opensource.guide", "https://github.community", "https://cash.app/$BlueSkyXN", "https://github.community", "https://spiritree.me/", "https://github.community", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.blog", "https://github.community", "https://dbeaver.com", "https://saucelabs.com/u/gh-indutny-elliptic", "https://spiritree.me/", "https://github.community", "https://github.blog", "https://www.githubstatus.com/", "https://github.community", "https://www.githubstatus.com/", "https://opensource.guide", "https://spiritree.me/archives/typecho-theme-amaze.html", "https://img.xiebruce.top/2019/04/20/bc83005774cf2dca482f290eb5508c5d.mp4", "https://opensource.guide", "https://github.co/hiddenchars", "https://opensource.guide", "https://camo.githubusercontent.com/932c9ef3a7fce4611f3bcf25eb66d3a54247de8381c768d7b6bf65cebb8fd547/68747470733a2f2f706963312e7a68696d672e636f6d2f38302f76322d62386661613633343231303634393833303066363336333964376435363935665f68642e6a7067", "https://github.blog", "http://en.wikiversity.org/wiki/ISO_639-1_language_matrix", "https://lxnchan.cn/super-resolution.html", "https://www.xiebruce.top/634.html", "https://github.blog", "https://opensource.guide", "https://github.blog", "https://dbeaver.com/download/", "https://github.blog", "https://camo.githubusercontent.com/d2dd3096b315ff639bff15e7d9805d393fbd51a6f84e56c6398f8096353c96d9/68747470733a2f2f706963322e7a68696d672e636f6d2f38302f76322d31383938653163643763666233313434333130326533316138353235313933615f68642e6a7067", "https://github.community", "https://gitter.im/nodeschool/discussions?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge", "https://www.githubstatus.com/", "https://camo.githubusercontent.com/3957242b7b7b0313a473b8f019358590add794e2d91356ca856bbcd6ed9ff7e9/68747470733a2f2f6265656d2e6166726963612f77702d636f6e74656e742f75706c6f6164732f323032302f31322f4265656d2d6d656e752d6c6f676f2d30322e737667", "https://opensource.guide", "https://github.blog", "https://opensource.guide", "https://awesome.re/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.blog", "https://binarysearch.com/@/justyy", "https://github.community", "https://www.python.org/downloads/release/python-335/", "https://opensource.guide", "http://nodeschool.io/", "https://packagist.org/packages/tomsgad/laravel-beem", "https://github.community", "http://www.threatcrowd.org", "https://github.community", "https://opensource.guide", "https://adoptopenjdk.net/", "https://avatars.githubusercontent.com/u/7952803?v=4", "https://www.githubstatus.com/", "https://xxyangyoulin.github.io/jquery_headindex/test", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://opensource.guide", "https://opensource.guide", "https://opensource.guide", "https://github.co/hiddenchars", "http://www.edge-security.com/", "https://github.community", "https://lixingyong.com", "https://opensource.guide", "https://www.xiebruce.top/634.html", "https://dbeaver.io", "https://github.co/hiddenchars", "https://opensource.guide", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://opensource.guide", "https://www.githubstatus.com/", "https://github.community", "https://disqus.com/", "https://entgo.io/docs/code-gen/", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://github.community", "https://www.githubstatus.com/", "https://github.community", "https://github.blog", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.community", "https://github.blog", "https://github.community", "https://opensource.guide", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://leanote.com", "http://leanote.org", "http://leanote.org", "http://leanote.org", "https://github.community", "http://leanote.org", "https://opensource.guide", "https://github.blog", "http://leanote.org", "https://opensource.guide", "https://twitter.com/ledoublegui", "https://www.githubstatus.com/", "https://github.blog", "https://avatars.githubusercontent.com/u/3692335?v=4", "https://github.community", "https://github.community", "https://opensource.guide", "https://www.githubstatus.com/", "https://github.blog", "https://github.community", "https://github.blog", "https://opensource.guide", "https://www.githubstatus.com/", "https://github.community", "https://github.blog", "https://opensource.guide", "https://www.githubstatus.com/", "https://wukong.hahack.com/", "http://localhost:5000", "https://www.githubstatus.com/", "https://github.community", "http://snowboy.kitt.ai/", "https://opencollective.com/wukong-robot/contribute/tier/8131-sponsor", "https://opensource.guide", "https://www.hahack.com/wukong-contrib/", "https://wukong.hahack.com/", "https://wukong.hahack.com/", "https://www.minecraft.net/zh-hans/mojang-careers", "https://github.community", "https://opensource.guide", "https://github.blog", "https://www.githubstatus.com/", "https://memoryshadow.github.io/Minecraft-Getting-Started-Guide/"]
}
```

- `github` 的反向索引

```json
[
  [0.1646728515625, "https://zzycreate.github.io/tags/GitHub-Pages/"],
  [0.07293701171875, "https://zzycreate.github.io/abort/"],
  [0.1441650390625, "https://zzy2001.com/index.php/archives/31/"],
  [0.0714111328125, "https://zzbd.org/"],
  [0.0675048828125, "https://zymin.cn/arcticle/hexo-multi-pc.html"],
  [0.15087890625, "https://zykjofficial.github.io/tags/Github"],
  [0.107421875, "https://zykjofficial.github.io/posts/acef0329"],
  [0.15087890625, "https://zykj.vercel.app/tags/Github"],
  [0.24755859375, "https://zykj.vercel.app/posts/ea8e8e59"],
  [0.10772705078125, "https://zykj.vercel.app/posts/acef0329"],
  "(以下略)"
]
```


## 数据格式

首先要把zip包解压缩。

网页数据和域名数据都是被简单压缩过的json格式，所以可以这样读取——

```python
import json
import brotli

print(json.loads(brotli.decompress(open(path, 'rb').read())))
```

反向索引的数据是一个比较奇怪的二进制格式<sub>(由于历史原因还有两种)</sub>，所以读取的代码比较复杂，像是下面这样——

```python
import json
import struct
import brotli


def _load1(b: bytes):
    n = struct.unpack('i', b[:4])[0]
    字符串长度 = struct.unpack(f'{n}h', b[4:4+n*2])
    吸0 = struct.unpack(f'{n}e', b[4+n*2:4+n*4])
    文hint = ''.join([f'{x}s' for x in 字符串长度])
    吸1 = struct.unpack(文hint, b[4+n*4:])
    吸1 = [x.decode('utf8') for x in 吸1]
    return [*zip(吸0, 吸1)]


def _load2(b: bytes):
    assert b[:6] == b'yn0001', '版本不对'
    n = struct.unpack('i', b[6:10])[0]
    吸0 = struct.unpack(f'{n}e', b[10:10+n*2])
    吸1 = json.loads(b[10+n*2:])
    assert len(吸0) == len(吸1), '数据不完整'
    return [*zip(吸0, 吸1)]


def load(b: bytes):
    if b.startswith(b'yn0001'):
        return _load2(b)
    return _load1(b)


print(load(brotli.decompress(open(path, 'rb').read())))
```

## 赞助

如果你觉得互联网数据集对你的工作或学习有帮助，欢迎来当我的女朋友。

要可爱的，最好是白发贫乳傲娇双马尾。
