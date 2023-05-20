# 互联网数据集

我的[搜索引擎](https://github.com/RimoChan/sese-engine)已经运行了1年多了，收集到了不少有用的数据。

我想，这些数据应该还是挺有价值的，不如就把它们拿出来和大家1起分享吧。


## 数据量

数据量正在持续增长中，截至2022年5月大约有48.9G的数据，包含这些内容——

- 域名数据<sub>(5.8G)</sub>包含14,000,000个域名，来自4,000,000个1级域名。

- 网页数据<sub>(24.9G)</sub>包含115,000,000个网页。

- 反向索引数据<sub>(99.7G)</sub>包含22,000,000个词，每个词对应1~30000个网页。


## 下载地址

你可以选1个自己喜欢的地方下载: 

- [GitHub Release](https://github.com/RimoChan/internet-dataset/releases)

- [OneDrive](https://v0vxj-my.sharepoint.com/:f:/g/personal/rimochan_v0vxj_onmicrosoft_com/EqRakuQVVjBDqMyU8xd7NnEB3MZrDZxDwPTVXK7tNv5Rqw?e=cXQMod )<sub> (感谢[@skoqaq](https://github.com/skoqaq)帮我传了OneDrive，但是这是2022年的数据) </sub>


## 数据内容

- 域名级别
  - ip
  - 最后访问时间
  - 访问次数 <sub>(搜索引擎爬取该域名下页面的次数，数值越高，其他的字段越可靠)</sub>
  - 语种 <sub>(fasttext的语种识别结果，对该域名下的所有网页滑动平均)</sub>
  - 链接 <sub>(该域名下的所有网页的指向其他域名的链接，滑动抽样200个左右)</sub>
  - 重定向 <sub>(该域名下的所有网页被重定向的情况，滑动抽样40个左右)</sub>
  - ======下面的属性只针对该域名的首页======
  - https可用
  - 关键词 <sub>(频率最高的词)</sub>
  - 结构 <sub>(将HTML结构映射到字符串，用于过滤模板生成的大量域名)</sub>

- 网页级别
  - 网页的标题
  - 网页的介绍 <sub>(meta description，截断到256字符)</sub>
  - 网页的文本 <sub>(截断到256字符)</sub>
  - 最后访问时间

注意: 

- ip字段并不完整，基本上是东亚地区的解析结果。

- 如果网站是动态的，关键词就不可靠<sub>(比如新闻网站的首页)</sub>。中文和英文以外的网站也不可靠。

- 与语言相关的字段都是有偏的。出现这个差别的原因是因为在选择爬取目标时，包含更多中文网页的域名的权重更高，而这些域名链接到其他域名的中文网页的概率也更高，因此滑动平均的结果上中文的比例会偏高。

- 有些域名会缺字段，这个是正常的。主要原因是有些字段是后来陆续加上的，没有回扫或者只回扫了1部分。

此外，还有1些没有列出的字段，它们大多是没有意义或者是已经被废弃的字段。看到的话不用去管它们就行了。


## 样例

- `https://github.com/`的网页信息

```json
[
  "GitHub: Let’s build from here · GitHub",
  "GitHub is where over 100 million developers shape the future of software, together. Contribute to the open source community, manage your Git repositories, review code like a pro, track bugs and features, power your CI/CD and DevOps workflows, and secure co",
  "Skip to content Toggle navigation Sign up Product Actions Automate any workflow Packages Host and manage packages Security Find and fix vulnerabilities Codespaces Instant dev environments Copilot Write better code with AI Code review Manage code changes Is",
  1683401341
]
```

- `github.com`的域名信息

```json
{
  "https可用": true,
  "ip": ["20.205.243.166"],
  "关键词": ["github", "your", "you", "code", "octocat", "classifier", "all", "actions", "s", "build", "open", "sign", "pull", "up", "learn", "world", "more", "community", "review", "readme", "requests", "security", "merge", "software", "git", "https", "source", "developers", "jump", "can", "repositories", "added", "packages", "cli", "codespaces", "million", "developer", "available", "windows", "cloud"],
  "成功率": 0.9450735409551977,
  "最后访问时间": 1683429300,
  "结构": "[[20,[[18,[1,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,21,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,1,1,1,3,3,3,1,3]],[19,[[0,[[32,[[0,[[0,[0,[0,[14]]]],[0,[[0,[14]],11,[0,[[0,[[0,[[0,[[16,[[10,[7,7,7,0]]]]]]]]]],0]]]]]]]]]],0,[0,[[38,[[0,[[0,[14,0]]]]]]]],\"include-fragment\",[0,[[44,[[0,[[0,[[0,[[0,[[0,[[0,[30,[16,[[0,[[17,[[15,[10]],[9,[7]]]],7,14]]]],[0,[[0,[[0,[[0,[[0,[4]],[0,[4]],[0,[4]],[0,[5]]]]]]",
  "访问次数": 556694.9000000316,
  "语种": {
    "ar": 0.00012560604452730657,
    "bg": 5.067841852608503e-11,
    "cs": 2.5e-323,
    "de": 3.7523861649975535e-10,
    "el": 1.0593663757620937e-07,
    "en": 0.9744931624632813,
    "eo": 2.5e-323,
    "es": 4.333235886036386e-05,
    "eu": 2.5e-323,
    "fa": 1.0508114267205955e-12,
    "fr": 7.0824680275658e-05,
    "hu": 0.0004203567032961541,
    "id": 2.5e-323,
    "it": 3.063911176630927e-15,
    "ja": 0.0017088828225574997,
    "ko": 0.0015900679303152115,
    "ne": 2.5e-323,
    "nl": 0.0005624524911557625,
    "pl": 1.717507063606e-312,
    "pt": 4.0744963011521734e-06,
    "ru": 0.0009116465126009326,
    "sk": 2.5e-323,
    "th": 0.000237629139099449,
    "tr": 2.830707100472314e-05,
    "uk": 1.9260313777921886e-12,
    "vi": 2.5e-323,
    "zh": 0.019803550921189992
  },
  "重定向": {"http://github.com/5iux/": "https://github.com/5iux/", "http://github.com/brianmario/yajl-ruby": "https://github.com/brianmario/yajl-ruby", "http://github.com/cch123": "https://github.com/cch123", "http://github.com/composer/packagist": "https://github.com/composer/packagist", "https://github.com/FriendsOfPHP/PHP-CS-Fixer": "https://github.com/PHP-CS-Fixer/PHP-CS-Fixer", "https://github.com/Homebrew/homebrew": "https://github.com/Homebrew/legacy-homebrew", "https://github.com/Laravelium/laravel-sitemap": "https://github.com/LaraPalCom/laravel-sitemap", "https://github.com/Nikschavan/header-footer-elementor": "https://github.com/brainstormforce/header-footer-elementor", "https://github.com/Redsmin/redsmin": "https://github.com/Redsmin/proxy", "https://github.com/TralahM/pympesa/pull/": "https://github.com/TralahM/pympesa/pulls", "https://github.com/UsersWP/userswp/": "https://github.com/AyeCode/userswp", "https://github.com/Vtrois/Kratos": "https://github.com/seatonjiang/kratos", "https://github.com/Xhofe/alist": "https://github.com/alist-org/alist", "https://github.com/apps/dependabot": "https://docs.github.com/github/managing-security-vulnerabilities/configuring-dependabot-security-updates", "https://github.com/apps/github-actions": "https://github.com/features/actions", "https://github.com/bollnh/hexo-theme-material": "https://github.com/iblh/hexo-theme-material", "https://github.com/bryan31/tlog-homepage/edit/master/docs/10.%E6%96%87%E6%A1%A3/210.%E5%AF%B9Soul%E7%BD%91%E5%85%B3%E7%9A%84%E6%94%AF%E6%8C%81.md": "https://github.com/dromara/tlog-homepage/edit/master/docs/10.%E6%96%87%E6%A1%A3/210.%E5%AF%B9Soul%E7%BD%91%E5%85%B3%E7%9A%84%E6%94%AF%E6%8C%81.md", "https://github.com/business": "https://github.com/enterprise", "https://github.com/contact": "https://support.github.com?tags=dotcom-direct", "https://github.com/creationix/nvm": "https://github.com/nvm-sh/nvm", "https://github.com/easydigitaldownloads/easy-digital-downloads/issues/7130": "https://github.com/awesomemotive/easy-digital-downloads/issues/7130", "https://github.com/github/feedback": "https://github.com/community/community", "https://github.com/gojek/feast": "https://github.com/feast-dev/feast", "https://github.com/greensock/GreenSock-JS/": "https://github.com/greensock/GSAP", "https://github.com/hackmdio/hackmd/issues/720": "https://github.com/hackmdio/codimd/issues/720", "https://github.com/iceb0y/winjudge": "https://github.com/iceboy233/winjudge", "https://github.com/indyplanets/flexnav": "https://github.com/mrjasonweaver/flexnav", "https://github.com/iteufel/nwjs-ffmpeg-prebuilt/releases": "https://github.com/nwjs-ffmpeg-prebuilt/nwjs-ffmpeg-prebuilt/releases", "https://github.com/kubernetes-sigs/federation-v2/blob/master/docs/userguide.md": "https://github.com/kubernetes-retired/kubefed/blob/master/docs/userguide.md", "https://github.com/kubernetes/test-infra/blob/master/images": "https://github.com/kubernetes/test-infra/tree/master/images", "https://github.com/mereithhh/van-blog": "https://github.com/Mereithhh/vanblog", "https://github.com/mperham/sidekiq": "https://github.com/sidekiq/sidekiq", "https://github.com/nuxt-community/i18n-module": "https://github.com/nuxt-modules/i18n", "https://github.com/pinggod/hexo-theme-apollo": "https://github.com/chongshengsun/hexo-theme-apollo", "https://github.com/rtfd/readthedocs.org": "https://github.com/readthedocs/readthedocs.org", "https://github.com/rtfd/sphinx_rtd_theme": "https://github.com/readthedocs/sphinx_rtd_theme", "https://github.com/rx-ts/prettier": "https://github.com/un-ts/prettier", "https://github.com/site/privacy": "https://docs.github.com/site-policy/privacy-policies/github-privacy-statement", "https://github.com/sourcemeta/json-size-benchmark/blob/master/benchmark/esmrc": "https://github.com/sourcemeta/json-size-benchmark/tree/master/benchmark/esmrc", "https://github.com/spatie/larabank-event-projector-aggregates": "https://github.com/spatie/larabank-aggregates", "https://github.com/uptrace/bun/blob/v1.1.12/example": "https://github.com/uptrace/bun/tree/v1.1.12/example", "https://github.com/users/hzoo/sponsorship": "https://github.com/sponsors/hzoo", "https://github.com/wikimedia/php-excimer": "https://github.com/wikimedia/mediawiki-php-excimer", "https://github.com/wowchemy/wowchemy-hugo-modules": "https://github.com/wowchemy/wowchemy-hugo-themes", "https://github.com/xb2016/kratos": "https://github.com/seatonjiang/kratos", "https://github.com/xingrz/bs-map-editor": "https://github.com/xingrz/rdt-editor", "https://github.com/xuegao-tzx/2048-HarmonyOS": "https://github.com/xuegao-tzx/2048-HarmonyOS-Lite", "https://github.com/xuperchain/xuperunion/wiki": "https://github.com/xuperchain/xuperchain/wiki", "https://github.com/yarnpkg/berry/blob/master/packages/yarnpkg-core": "https://github.com/yarnpkg/berry/tree/master/packages/yarnpkg-core"},
  "链接": ["https://github.blog", "https://avatars.githubusercontent.com/u/7133698?v=4", "https://neko-dev.github.io/material-theme-docs/", "https://github.blog", "https://twitter.com/palkan_tula", "https://github.blog", "http://blog.cocoapods.org/CocoaPods.org-Two-point-Five/", "https://twitter.com/github", "https://packagist.org/packages/brunocfalcao/larapush", "https://leeoniya.github.io/uPlot/demos/zoom-wheel.html", "https://developer.apple.com/xcode/", "https://www.githubstatus.com/", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://usthe.com/sureness", "https://github.blog", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://formbold.com/templates", "https://nodejs.org/en/", "https://cloudburstmc.org", "https://formbold.com/", "https://www.apache.org/licenses/LICENSE-2.0.html", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://anarchyinstaller.org/", "https://evilmartians.com/chronicles/system-of-a-test-setting-up-end-to-end-rails-testing", "https://github.co/hiddenchars", "https://evilmartians.com/chronicles/hotwire-reactive-rails-with-no-javascript", "https://github.blog", "https://www.githubstatus.com/", "https://www.npmjs.com/package/errorhandler", "https://github.blog", "https://github.blog", "https://github.blog", "https://noti.st/palkan/jWy57U/weaving-seaming-mocks", "https://www.npmjs.com/package/raw-body", "https://git.sr.ht/~emersion/gamja/", "https://www.githubstatus.com/", "https://actions.github.io/humans.txt", "https://github.blog", "https://www.busybox.net/", "https://github.blog", "https://laravel.com/docs/collections", "https://github.blog", "https://wordpress.org/plugins/userswp-recaptcha/", "https://developer.apple.com/xcode/", "https://github.blog", "https://www.bitlbee.org/", "https://github.blog", "https://github.co/hiddenchars", "https://github.blog", "https://www.mdpi.com/2078-2489/11/2/125", "https://github.blog", "https://github.co/hiddenchars", "https://github.blog", "https://gyoogle.dev/", "https://www.githubstatus.com/", "https://developer.apple.com/xcode/", "https://jsonapi.org", "https://www.irccloud.com/", "https://formbold.com/", "https://github.blog", "https://userswp.io/downloads/verified-users/", "https://www.githubstatus.com/", "https://www.electronjs.org", "https://laravel.com/docs/eloquent-relationships", "https://www.archlinux.org", "https://xxxx.com/pc/js/manifest.e90b779b12a4f25606f0.js", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.npmjs.com/package/chartjs-adapter-spacetime", "https://userswp.io/downloads/wp-job-manager/", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.buymeacoffee.com/gyoogle", "https://github.blog", "https://demos.ayecode.io/userswp/", "https://github.blog", "https://github.blog", "https://link.springer.com/chapter/10.1007/978-3-030-55789-8_60", "https://github.blog", "https://www.githubstatus.com/", "https://jsonapi.org/format/", "https://en.wikipedia.org/wiki/Open_source", "https://www.npmjs.com/package/spacetime", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "http://issues.npcap.org/226", "https://github.co/hiddenchars", "https://userswp.io/downloads/multisite-creator/", "https://github.blog", "https://openjsf.org/", "https://packagist.org/packages/tightenco/collect", "https://www.githubstatus.com/", "https://userswp.io/downloads/mailchimp/", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://github.co/hiddenchars", "https://berlin.social/@lutki95", "https://github.blog", "https://www.producthunt.com/posts/github-metrics?utm_source=badge-featured&utm_medium=badge&utm_source=badge-github-metrics", "https://www.npmjs.com/package/cookie-session", "https://github.blog", "https://github.blog", "https://github.co/hiddenchars", "https://www.johnsmith.com", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://github.blog", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://weechat.org/", "https://www.githubstatus.com/", "https://albumentations.ai/docs/", "https://www.npmjs.com/package/serve-favicon", "https://github.blog", "https://github.blog", "https://npmjs.org/package/connect", "https://github.blog", "https://twitter.com/thephpleague", "https://userswp.io/downloads/private-messages/", "https://github.blog", "https://sdrausty.github.io/TermuxArch/docs/install", "https://github.blog", "https://www.apache.org/licenses/LICENSE-2.0.html", "https://github.blog", "https://developer.apple.com/xcode/", "https://search.maven.org/artifact/com.usthe.sureness/sureness-core", "https://camo.githubusercontent.com/559879cbb14f47ebeb2da8aeaa8a4c61db62b9d484fd94e569e2e75e4af51469/68747470733a2f2f6769746875622d726561646d652d73746174732e76657263656c2e6170702f6170692f746f702d6c616e67732f3f757365726e616d653d70696e757373696c76657374727573266c61796f75743d636f6d7061637426686964655f7469746c653d3126636172645f77696474683d333030", "https://github.blog", "https://www.githubstatus.com/", "https://github.co/hiddenchars", "https://beta-metrics.lecoq.io", "https://www.githubstatus.com/", "https://lineicons.com/", "https://www.githubstatus.com/", "https://packagist.org/packages/brunocfalcao/larapush", "https://noti.st/palkan/VWPOSd/between-monoliths-and-microservices", "https://github.blog", "https://github.blog", "https://userswp.io/downloads/advanced-search/", "https://github.blog", "https://www.npmjs.com/package/chart.js", "https://flight-manual.atom.io/hacking-atom/sections/debugging/", "https://twitter.com/lutki95", "https://github.blog", "https://www.npmjs.com/package/cookie-parser", "https://www.npmjs.com/package/lineicons", "https://www.githubstatus.com/", "https://avatars.githubusercontent.com/u/113136203?v=4", "https://avatars.githubusercontent.com/u/21816?v=4", "https://www.githubstatus.com/", "https://twitter.com/feelinglucky", "https://github.blog", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://actions.github.io/humans.txt", "https://github.blog", "https://www.githubstatus.com/", "https://t.me/pornbaike", "https://github.co/hiddenchars", "https://github.blog", "https://spec.matrix.org/v1.4/client-server-api/", "https://stackoverflow.com/questions/tagged/chart.js", "https://devblogs.microsoft.com/dotnet/dotnet-maui-dotnet-7/", "https://brew.sh", "https://camo.githubusercontent.com/626c2f3093027bc493aa25c73cf7f445e87e3e35f33885abf5407be37c862a94/68747470733a2f2f696d67732e786b63642e636f6d2f636f6d6963732f7465616d5f636861742e706e67", "https://github.blog", "https://coveralls.io/r/senchalabs/connect?branch=master", "https://github.blog", "https://github.blog", "https://github.blog", "https://discuss.atom.io/c/faq", "https://www.linkedin.com/in/niklas-kiefer-9249341a2/", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://github.blog", "https://huww98.github.io/TimeChart/docs/performance", "https://developer.apple.com/xcode/", "https://www.githubstatus.com/", "https://www.githubstatus.com/", "https://json-schema.org", "https://flight-manual.atom.io/hacking-atom/sections/debugging/", "https://github.blog", "https://www.deviantart.com/dartty/art/Kanaya-364815353", "https://github.blog", "https://www.githubstatus.com/", "https://www.facebook.com/whitehat", "https://github.blog", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://demo.stack.jimmycai.com", "https://dev.stack.jimmycai.com", "https://user-images.githubusercontent.com/5889006/190859553-5b229b4f-c476-4cbd-928f-890f5265ca4c.png", "https://stack.jimmycai.com", "https://developer.apple.com/xcode/", "https://www.githubstatus.com/", "https://ko-fi.com/jimmycai", "https://stack.jimmycai.com", "https://user-images.githubusercontent.com/5889006/190859441-141b5f81-8483-40d2-bd96-ebf85616a46d.png", "https://cssnano.co/", "https://gitter.im/postcss/postcss", "https://vk.com/postcss", "https://plugins.jetbrains.com/plugin/8578-postcss", "https://postcss.org/api/", "https://parceljs.org", "https://www.postcss.parts/", "https://evilmartians.com/?utm_source=postcss", "https://postcss.org", "https://atom.io/packages/source-preview-postcss", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://github.co/hiddenchars", "https://github.co/hiddenchars", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://www.githubstatus.com/", "https://github.blog", "https://github.blog", "https://router.vuejs.org/guide/advanced/meta.html", "https://developer.mozilla.org/en-US/docs/Web/API/ScrollToOptions", "https://developer.mozilla.org/en-US/docs/Web/API/History/state", "https://www.githubstatus.com/", "https://router.vuejs.org/api/interfaces/routelocationoptions.html", "https://github.blog", "https://mathiasbynens.be/notes/css-escapes", "https://developer.mozilla.org/en-US/docs/Web/API/ScrollToOptions/behavior", "https://pinia.vuejs.org", "https://github.blog"]
}
```


## 数据格式

首先要把zip包解压缩。

网页数据和域名数据都是被简单压缩过的json格式，所以可以这样读取——

```python
import json
import brotli

print(json.loads(brotli.decompress(open(path, 'rb').read())))
```

反向索引的数据是1个比较奇怪的2进制格式<sub>(由于历史原因还有两种)</sub>，所以读取的代码比较复杂，像是下面这样——

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
