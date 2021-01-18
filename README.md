# 中国滑稽大学(University of Ridiculous of China)健康打卡平台自动打卡脚本

![School](https://img.shields.io/badge/School-URC-blue.svg)![Language](https://img.shields.io/badge/Language-Python3-yellow.svg)![Auto-Report](https://github.com/apylers/URC-ncov-AutoReport/workflows/Auto-Report/badge.svg)

## 说明

**本打卡脚本仅供学习交流使用，请勿过分依赖。开发者对使用或不使用本脚本造成的问题不负任何责任，不对脚本执行效果做出任何担保。**

## 更新记录

- 20210118：重新格式化排版代码，去除多余要素，适配新年。
- 20200827：增加打卡失败重试功能，增加 License。
- 20200826：为配合学校最新规定，切换至 Github Actions 实现一天三次打卡

## 使用方法

1. 将本代码仓库 Fork 到自己的 GitHub。

2. 根据自己的实际情况修改 `data.json` 的数据，参看下文。**这里给出的 `data.json` 仅供参考。**

3. 将修改好的代码 push 至 master 分支。如果不需要修改 `data.json`，请在 `README.md` 里添加一个空格并 push，否则不会触发之后的步骤。

4. 点击 Actions 选项卡，点击 "I understand my workflows, go ahead and enable them"。

5. 点击 Settings 选项卡，点击左侧 Secrets，点击 New secret，创建名为 `STUID`，值为自己学号的 secret。用同样方法，创建名为 `PASSWORD`，值为自己中国滑稽大学统一身份认证密码的 secret。**这两个值不会被公开。**

   ![](imgs/secrets.png)

6. 默认的打卡时间是每天的早上 7: 30、中午 12: 30 和晚上 19: 30，可能会有数分钟的浮动。如需选择其它时间，可以修改 `.github/workflows/report.yml`中的 `cron`，详细说明参见[安排的事件](https://docs.github.com/cn/actions/reference/events-that-trigger-workflows#scheduled-events)，请注意这里使用的是**国际标准时间 UTC**，北京时间的数值比它大 8 个小时。

7. 在 Actions 选项卡可以确认打卡情况。如果打卡失败（可能是临时网络问题等原因），脚本会自动重试，三次尝试后如果依然失败，将返回非零值提示构建失败。

8. 在 GitHub 个人设置页面的 Notifications 下可以设置 GitHub Actions的通知，建议打开 Email 通知，并勾选 "Send notifications for failed workflows only"。

## data.json 数据获取方法

使用 F12 开发者工具抓包之后得到数据，按照 json 格式写入 `data.json` 中。

1. 登录进入 `https://weixine.自动打码.edu.cn/2020/`，打开开发者工具（Chrome 可以使用 F12 快捷键），选中 Network 窗口：

![](./imgs/1.png)

2. 点击确认上报，点击抓到的 `daliy_report` 请求，在 `Headers` 下面找到 `Form Data` 这就是每次上报提交的信息参数。

![](./imgs/2.png)

3. 将找到的 Data 除 `_token` （每次都会改变，所以不需要复制，脚本中会每次获取新的 token 并添加到要提交的数据中）外都复制下来，存放在 `data.json` 中，并参考示例文件转换为对应的格式。

4. 通过 push 操作触发构建任务，检查上报数据是否正确。

## 许可

MIT License

Copyright (c) 2020 BwZhang

Copyright (c) 2020 Violin Wang

Copyright (c) 2021 apylers

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.