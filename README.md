# zju-health-report-action-demo (ZHR demo)

<p align="center" style="display: flex; justify-content: space-between; align-items: center;">
<img src="https://github.githubassets.com/images/modules/site/features/actions-icon-actions.svg" alt="github-actions-logo" height="200" style="padding: 20px 20px 20px; display: inline-block; box-sizing: border-box;"></img>
<img src="https://user-images.githubusercontent.com/102473739/160546748-52ccc565-fc6c-4833-b710-494aacbad18e.png" alt="zju-health-report-logo" height="200"></img>
</p>

> GitHub Action Demo for https://github.com/zju-health-report/action

浙江大学健康打卡自动打卡脚本  GitHub Action 例子，只需一步 Fork 即可使用。

## 使用方法

1. 直接 Fork 本仓库

2. 配置帐号（必须）

   Settings > Actions > General > Workflow permissions，改为 Read and write permissions，这样 Monthly Update Action 才能拥有更新仓库的权限，Monthly Update Action 每月运行一次，会向仓库添加一个新的 commit，是用来防止因为仓库长时间不活跃，而被 GitHub 自动禁用 Actions。

   Settings > Secrets > Actions > New repository secret， 添加 `ZJU_USERNAME`，内容为浙大通行证账号（学号），添加`ZJU_PASSWORD`，内容为浙大通行证密码。

   ![zju_account](https://user-images.githubusercontent.com/24741764/161693671-3659a9d5-aafa-4140-a277-1aa3e6373e48.png)

3. 配置定时运行时间（可选）

   在 .github/workflows/health-report.yml 中更改时间：

   ```yml
   on:
   workflow_dispatch:
   schedule:
      - cron: '0 23 * * *'
   ```

4. 配置钉钉消息通知（可选）

     - 手机版钉钉 > 右上角添加 > 面对面建群 > 创建之后得到只有你一个人的群聊
     - 电脑版钉钉 > 群设置 > 智能群助手 > 添加机器人 > 自定义，名字随便填，安全设置选择`自定义关键字`，填`ZHR`，然后下一步复制Webhook。
     - Settings > Secrets > Actions > New repository secret， 添加`DINGTALK_TOKEN`，内容为刚才复制的Webhook中 `access_token=` 后面的内容。

5. 配置多人打卡（可选）

   在 .github/workflows/health-report.yml 中添加一组，自行添加对应的Secrets。

   ```yml
      - username: ZJU_USERNAME
        password: ZJU_PASSWORD
        dingtalk_token: DINGTALK_TOKEN
      - username: ZJU_USERNAME2
        password: ZJU_PASSWORD2
        dingtalk_token: DINGTALK_TOKEN2
   ```

6. 测试

   Actions > I understand my workflows, go ahead and enable them
   
   Actions > @zju-health-report/action Demo > Enable workflow > Run workflow。

   Actions > Monthly Update Action > Enable workflow > Run workflow。

7. 停用

   Actions > @zju-health-report/action Demo > Disable workflow。

   Actions > Monthly Update Action > Disable workflow。
