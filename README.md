# RackNerd搭建WordPress：两条路线从购买到上线的完整步骤，附套餐价格与真实成本对比

在 RackNerd 上搭 WordPress，实际只有两条路：买它的 cPanel 共享主机，用 Softaculous 一键安装，付款到上线半小时以内；或者买一台 KVM VPS，自己装面板、用 Docker 部署，便宜得多，但系统层面的事全归你管。这篇文章把两条路线的套餐、价格、安装步骤和容易踩的坑一次讲清，你只需要判断自己属于哪类用户。

> **选购速览**：只想把网站跑起来、不想碰命令行 → 选 Shared 30 GB（$5.59/月，LiteSpeed + LSCache，Softaculous 半分钟装完 WordPress，几百篇文章的站够用）。愿意自己当管理员、想把成本压到最低 → 入门 KVM VPS 年付促销价约 $11/年。👉 [查看 RackNerd 共享主机三档套餐与当前结算价](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting)

## 先分清楚：用共享主机还是 VPS 搭 WordPress

判断标准只有一条：你想不想自己管服务器。

共享主机是托管环境。RackNerd 负责服务器、系统、cPanel 面板和每日备份，你只管网站本身，WordPress 靠 Softaculous 一键装出来。博客、企业站、作品集、几个客户站，这类需求全部可以走这条路。

VPS 给你的则是一台空机器：KVM 虚拟化、完整 root 权限、1 Gbps 端口、RAID-10 SSD、独立 IPv4，配 SolusVM 面板做重启和重装。没有 cPanel，没有 Softaculous，WordPress 要自己装——用免费面板（CloudPanel、WordOps、FastPanel、SlickStack）、付费管理面板（xCloud、RunCloud、ServerAvatar），或者 Docker Compose。

真实成本账值得算一下。共享主机 30 GB 档月付 $5.59，月付一年大约 67 美元；而按 RackNerd 当前的新年促销，入门 VPS 年付低到约 11 美元，第一年价差在六倍左右。代价也明摆着：装面板、配防火墙、备份和升级都变成你的事。官方博客把安装流程写成了教程，跟着做半天能跑起来，可之后的日常维护还是落在自己头上。

网站是要紧事、时间比钱贵，选共享主机；折腾本身是乐趣，或者已经有运维经验，VPS 才是它该待的位置。

## RackNerd 共享主机套餐怎么选

三档套餐的唯一区别是存储和流量，功能完全一致。

| 套餐 | SSD 存储 | 月流量 | 域名/数据库 | 月付价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| Shared 30 GB | 30 GB | 2 TB | 不限 | $5.59/月 | [ 开通 Shared 30 GB](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting) |
| Shared 100 GB | 100 GB | 3 TB | 不限 | $9.59/月 | [ 开通 Shared 100 GB](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting) |
| Shared 200 GB | 200 GB | 5 TB | 不限 | $15.59/月 | [ 开通 Shared 200 GB](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting) |

每一档都包含同一套东西：

- LiteSpeed Web Server + LSCache——WordPress 的 LSCache 插件可以直接启用，整页缓存随主机免费提供
- CloudLinux、免费 Let's Encrypt SSL（自动签发）
- JetBackup 每日异地备份
- DDoS 防护、KernelCare 免重启内核更新
- 免费 cPanel 到 cPanel 迁移
- Softaculous 一键安装 380+ 应用

机房在洛杉矶、纽约、德国、法国、新加坡之间选，下单时确定，建议选离主要访客近的。付款方式上，月付无合约；购物车里也可以选年付、两年付或三年付，月均成本会再降一截，具体折扣以结账页显示为准。

至于要不要往 100 GB 或 200 GB 跳：30 GB 装几百篇文章加常规图库绰绰有余，月流量 2 TB 对绝大多数小站根本用不到 100 GB。真正需要升档的信号是多店铺、视频内容多，或者大量邮箱账户在吃磁盘。起步阶段多花的钱基本是白花的。👉 [前往共享主机商店页确认三档套餐的当前价格](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting)

## 路线一：Softaculous 一键安装 WordPress

付款后大约 5–15 分钟开通，cPanel 登录信息几分钟内发到邮箱。登录之后流程是这样：

1. 在 cPanel 的 Software 区域找到蓝色方块图标 "Softaculous Apps Installer"，点进去。
2. 在 Blogs 分类里选 WordPress（列表第一个）。
3. 点蓝色 Install 按钮。注意别点旁边灰色的 Import——那是给迁移现有站点用的，新装站点点它会一头雾水。
4. 选协议和域名。SSL 已经自动签发的话选 https://，www 与否按你的习惯。
5. 目录留空就是装在域名根目录；填 /blog 则是子目录安装。大多数情况留空。
6. 填站点名称、描述和管理员账号。管理员用户名别用 admin，这是被爆破扫描最多的用户名。
7. 展开高级选项，勾上限制登录尝试和自动升级，两项都值得开。
8. 备份频率选每周。每日备份不是不行，只是存储消耗快得多。

装完页面会给出后台地址，用第 6 步的账号直接登录，开始写第一篇文章就行。

Softaculous 能做的事不止安装。它可以把现有站点克隆到测试地址改主题、按你设定的计划自动更新程序和插件，还能从别的主机远程导入 WordPress——从其他 cPanel 主机搬家时，不需要手动导出数据库再重建。

## 路线二：在 RackNerd VPS 上搭 WordPress

VPS 开通后你拿到的是一台干净的 Ubuntu、Debian 或 AlmaLinux，WordPress 需要自己装。欢迎邮件里有 SolusVM 面板地址、VPS IP 和 root 登录信息；想换系统就进 SolusVM 用 Reinstall 重装，重装会清空整台机器的数据。主流做法有三种。

### 用服务器管理面板（以 xCloud 为例）

前提条件：全新安装的 Ubuntu 24.04 LTS x64、至少 1 GB 内存、放行 TCP 22/80/443 端口、可用的 root SSH 权限。

流程：在 xCloud 添加服务器时选 Other Providers → 填服务器名和公网 IPv4 → 选 NGINX 或 OpenLiteSpeed 技术栈 → 用密码或公钥完成认证（私钥永远不要贴进任何表单）→ 提交后等几分钟自动部署。

两个容易翻车的地方：xCloud 只接受全新服务器，上面不能已经有网站、数据库或别的管理面板；部署进行中别装软件包、别改防火墙规则，动了容易导致部署中断。真不符合条件就先去 SolusVM 重装一遍再连。部署完成后在 xCloud 里选 Add New Site → Install New WordPress Website，填站点标题和管理员账号创建站点，再把域名 A 记录指向 VPS IP，解析生效后签发 SSL。

### 用 Docker Compose

RackNerd 官方频道出过完整的 Docker Compose 教程：先放行防火墙的 OpenSSH、http、https，装好 Docker 和 Compose 插件，然后在 /opt/wordpress 目录下放 docker-compose.yml 和 .env 文件（里面是数据库名、用户名、密码、root 密码四个变量），执行 `docker compose up -d` 拉起容器，最后绑域名、配 SSL。这条路的吸引力在于整站就是几个容器，备份和迁移都在文件层面完成，适合愿意维护配置文件的人。

### 用免费控制面板

RackNerd 官方博客陆续发布过 CloudPanel、CentOS Web Panel（CWP）的 WordPress 安装教程，第三方常见的还有 WordOps、FastPanel、SlickStack。这类面板自动配好 Nginx 或 LiteSpeed 加 MySQL 加 PHP 的整套环境，装 WordPress 的点击次数和 Softaculous 已经相差无几。想要更精致的图形界面，可以看 ServerAvatar、RunCloud 这类付费选项。

一个年付 11 美元左右的 VPS 加上免费面板，在很多场景下响应速度反而好过月付十美元的共享主机——前提是你愿意自己处理更新、备份和故障排查。👉 [查看 RackNerd KVM VPS 当前促销与可选配置](https://bit.ly/my-rn)

## 域名解析与 SSL

无论走哪条路线，收尾步骤都一样：在域名的 DNS 管理处把 A 记录指向服务器 IP（共享主机在 cPanel 里能看到自己的 IP，VPS 看欢迎邮件），如果这个主机名原来指向别处，把冲突的 A 或 AAAA 记录删掉。解析生效需要一点时间，可以先改动再等；确认解析到位后，用面板签发 Let's Encrypt SSL 证书，浏览器里确认 https 能正常打开、WordPress 后台能登录，整个搭建过程才算闭环。

## 常见问题

**RackNerd 共享主机付款后多久能开通？**
官方流程大约 5–15 分钟内完成，cPanel 凭据几分钟内发到邮箱，不用等人工审核。

**Shared 30 GB 真的够用吗？**
对一个几百篇文章、图库正常的 WordPress 站来说够。需要跳档的信号是多店铺、视频托管或大量邮箱占用磁盘，而不是文章数量。

**已有的 WordPress 站能搬过来吗？**
两种方式：Softaculous 的远程导入功能直接从原主机拉取站点并重新配置；或者用免费的 cPanel 到 cPanel 迁移服务，都不用手动导数据库。

**RackNerd 的 VPS 大概什么价位？**
促销期入门档年付约 11 美元，KVM 虚拟化、1 Gbps 端口、RAID-10 SSD、独立 IPv4，带 SolusVM 面板。注意它不带 cPanel 和 Softaculous，软件栈完全自己装。

**出问题找谁？**
支持是 24/7 的，官方给出的平均响应时间约 10 分钟。

## 怎么选，最后帮你捋一遍

今晚就想让网站上线，之后的时间花在写内容上——共享主机 30 GB，Softaculous 流程走完也就十分钟的事。

手里已经有别的 cPanel 主机在跑 WordPress——共享主机加免费迁移，搬家不用碰数据库导出。

预算压到极限、享受折腾，或者需要多个隔离环境——年付入门 VPS 配一个免费面板，代价是自己管更新和备份。

下单前确认两件事就够：机房位置（洛杉矶、纽约、德国、法国、新加坡）和计费周期（月付无合约，年付更省，折扣在结账页能看到）。👉 [选好路线后前往 RackNerd 开通套餐](https://my.racknerd.com/aff.php?aff=16470&rp=/store/shared-hosting)
