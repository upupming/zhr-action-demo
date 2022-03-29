# zju-health-report-action-demo

![logo](https://user-images.githubusercontent.com/102473739/160546748-52ccc565-fc6c-4833-b710-494aacbad18e.png)

> Demo for https://github.com/zju-health-report/action

浙江大学健康打卡自动打卡脚本  GitHub Action 例子。可以直接 fork，按照 [@zju-health-report/action](https://github.com/zju-health-report/action) 的说明配置好 secrets 之后手动触发一下两个 Action 就可以使用了。

## 使用方法

1. 直接 Fork 本仓库

2. 配置定时运行时间（可选）

   在 .github/workflows/action.yml 中更改时间：

   ```yml
   on:
   workflow_dispatch:
   schedule:
      - cron: '0 23 * * *'
   ```

3. 配置帐号（必须）

   Settings > Secrets > New repository secrets， 添加 `ZJU_USERNAME`，内容为浙大通行证账号（学号），添加`ZJU_PASSWORD`，内容为浙大通行证密码。

   ![zju_account](https://user-images.githubusercontent.com/102473739/160592128-4ae2f655-3e6e-4373-b655-9433ac4fb0c9.png)

4. 配置多人打卡（可选）

   在 .github/workflows/action.yml 中添加一组，自行添加对应的Secrets。

   ```yml
      - username: ZJU_USERNAME
        password: ZJU_PASSWORD
      - username: ZJU_USERNAME2
        password: ZJU_PASSWORD2
   ```

5. 测试

   Actions > @zju-health-report/action Demo > Enable workflow > Run workflow。

   Actions > Monthly Action > Enable workflow > Run workflow。

6. 停用

   Actions > @zju-health-report/action Demo > Disable workflow。

   Actions > Monthly Action > Disable workflow。
