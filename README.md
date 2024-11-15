<p align="center">
  <a href="https://nonebot.dev/docs/next/best-practice/alconna/"><img src="https://v2.nonebot.dev/logo.png" width="200" height="200" alt="nonebot"></a>
</p>



<div align="center">

# NoneBot Plugin Alconna

_✨ Alconna 支持 NoneBot2 ✨_

_✨ 接收全部信息 | 发送全部信息 ✨_

</div>

<p align="center">
  <a href="https://raw.githubusercontent.com/nonebot/plugin-alconna/master/LICENSE">
    <img src="https://img.shields.io/github/license/nonebot/plugin-alconna.svg" alt="license">
  </a>
  <a href="https://pypi.python.org/pypi/nonebot-plugin-alconna">
    <img src="https://img.shields.io/pypi/v/nonebot-plugin-alconna.svg" alt="pypi">
  </a>
  <img src="https://img.shields.io/badge/python-3.9+-blue.svg" alt="python">
</p>


<div align="center">

# 文本信息

</div>

<details markdown='1'><summary>[普通]ALC 通用代码 发送文本信息 </summary>

```python
# NCSO_Menu 是 功能 ID
# 当用户在聊天发送 菜单 或者 Menu
# Bot 就会发送 菜单 = """菜单内容"""
NCSO_Menu = on_alconna(Alconna("菜单"), aliases={"Menu", "menu"})
@NCSO_Menu.handle()
async def NCSO_Menu_handle():
    菜单 = """哔哩哔哩 | 剪辑软件
温玉项目 | 音乐功能
帮助中心 | 呼叫客服
Whois查询  | IP查询"""
     await NCSO_Menu.send(UniMessage.template(f"{菜单}"))
```
</details>

****

<details markdown='1'><summary>[进阶] Args 变量使用 + if: else:</summary>

```python
NCSO_BT_CHN = on_alconna(Alconna("帮助",Args["方法指令", str]),aliases={"help","HELP"})
@NCSO_BT_CHN.handle()
#在 async的(添加 方法指令: Match[str]) 读取 [帮助 你好] 取值 [你好]
async def NCSO_BT_CHN_handle(方法指令: Match[str]):
    # 假设指令参数是通过某种方式解析得到的
    帮助判断 = f"{方法指令.result}"
    
    # 定义宝塔相关的帮助文档
    帮助文档_宝塔 = """>·>·帮助-宝塔-菜单·<·<
宝塔 + 安装宝塔
宝塔 + 主机安全系统安装脚本
宝塔 + 云WAF安装脚本"""
    # 根据用户输入的指令选择相应的帮助文档
    if 帮助判断 == "宝塔":
        帮助文档C = 帮助文档_宝塔
    else:
        帮助文档C = "宝宝～\n请输入正确指令"
    
    # 发送帮助文档
    帮助文档 = f"{帮助文档C}"
    await NCSO_BT_CHN.send(UniMessage.template(帮助文档))
```
</details>

****

<details markdown='1'><summary>[进阶] Args 变量使用 使用API</summary>

```python
NCSO_whois_Parsing = on_alconna(Alconna("Whois查询", Args["web域名", str]), aliases={"Whois", "whois"})
@NCSO_whois_Parsing.handle()
# 在 async 中写入 你的 Args web域名: Match[str]
# 写入后 代码就可以引入 {web域名.result}
async def NCSO_whois_Parsing_handle(web域名: Match[str]):
    域名 = f"{web域名.result}"
    appkey = "b7a782741f667201b54880c925faec4b"
    # API的URL
    url = "https://api.gumengya.com/Api/Whois"
    # 查询参数
    params = {
        "format": "json",
        "domain": 域名,
        "appkey": appkey
    }
    try:
        # 发送GET请求
        response = requests.get(url, params=params)
        # 检查响应状态码
        if response.status_code == 200:
            # 解析响应内容为JSON
            data = response.json()
            # 检查返回码
            if data['code'] == 200:
                # 提取需要的信息
                domain_info = data['data']
                查询结果 = f""">·>·>·「温玉」·<·<·<
询域名：{domain_info['domain']}
注册商：{domain_info['registrar']}
注册时间：{domain_info['registrationTime']}
域名到期时间：{domain_info['expirationTime']}
名称服务器：{domain_info['nameServer']}"""
            else:
                查询结果 = f"请求失败，错误信息：{data['msg']}"
        else:
            查询结果 = f"请求失败，HTTP状态码：{response.status_code}"
        
        await NCSO_whois_Parsing.send(查询结果)
    except requests.RequestException as e:
        await NCSO_whois_Parsing.send(f"请求异常：{e}")

```
</details>


<div align="center">

# 图片信息

</div>

<details markdown='1'><summary>[普通]ALC 通用代码 发送图片信息</summary>

```python
#很直白没什么可介绍的
@wenyu_sb.handle()
async def wenyu_sb_handle():
  await UniMessage.image(url = "https://image.wycun.shop/Laugh-at-you.jpg").send()

```
</details>

