# zhr-action-demo

<p align="center">
  <img src="https://user-images.githubusercontent.com/102473739/168511011-7f266047-a437-4ed7-a151-4e8129bf7a1b.png">
</p>

> GitHub Action Demo for https://github.com/upupming/zhr-action

浙江大学健康打卡自动打卡脚本 GitHub Action 例子，只需一步 Fork 即可使用，每天定时帮你自动打卡。

- 🔔 2022.12.25 学校已经不再要求打卡，参考 [zhr-action/#7](https://github.com/upupming/zhr-action/issues/7)，可以自行停用此脚本。

    ```txt
    【关于进一步优化校园疫情防控举措的通知】

    1.本校师生员工不再要求每日打卡，可通过人脸识别、校园卡、身份证等多种方式入校，蓝码逐步停止使用，学校加快开发电子校园卡作为师生移动端身份凭证，过渡期认可凭蓝码进入。师生驾驶已备案机动车（凭通行证）可直接进入校园，如驾驶非备案机动车经身份查验后进入校园。离退休同志参照上述方式进入校园。
    ```

## 使用方法

1. 直接 Fork 本仓库

2. 配置帐号（必须）

   Settings > Actions > General > Workflow permissions，改为 Read and write permissions，这样 Monthly Update Action 才能拥有更新仓库的权限，Monthly Update Action 每月运行一次，会向仓库添加一个新的 commit，是用来防止因为仓库长时间不活跃，而被 GitHub 自动禁用 Actions。

   Settings > Secrets > Actions > New repository secret， 添加 `ZJU_USERNAME`，内容为浙大通行证账号（学号），添加`ZJU_PASSWORD`，内容为浙大通行证密码。

   ![zju_account](https://user-images.githubusercontent.com/24741764/161693671-3659a9d5-aafa-4140-a277-1aa3e6373e48.png)

   如果遇到[登录异常问题](https://github.com/upupming/zhr-action-demo/issues/10)，可添加 `ZJU_COOKIE` 这个 secret，请参考 https://github.com/upupming/zhr-action#%E7%99%BB%E5%BD%95%E5%BC%82%E5%B8%B8 进行配置，`ZJU_PASSWORD` 和 `ZJU_COOKIE` 二选一即可。

3. 配置定时运行时间（可选）

   在 .github/workflows/health-report.yml 中更改时间：

   ```yml
   on:
   workflow_dispatch:
   schedule:
      # `0 23 * * *` 表示UTC 23:00，即北京时间7:00打卡（经测试，实际运行时间比设定时间晚几分钟到几十分钟）。
      # 可以参考 https://crontab.guru/ 进行配置
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

6. 启用 Action（必须）

   Actions > I understand my workflows, go ahead and enable them

   Actions > zhr-action Demo > Enable workflow > Run workflow。

   Actions > Monthly Update Action > Enable workflow > Run workflow。

7. 停用 Action

   Actions > zhr-action Demo > Disable workflow。

   Actions > Monthly Update Action > Disable workflow。
