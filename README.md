# simple_115

> 本项目旨在快速搜索番号并提交至115网盘离线下载，简化操作流程，省去繁琐的手动步骤。

### 功能介绍：
- 优先选择SHT中文字幕数据库作为数据源，无资源自动下落 BT 站点
- 自动搜索 BT 站资源并提交番号，目前已支持[sukebei](https://sukebei.nyaa.si/)、[freejavbt](https://freejavbt.com)站点资源自动搜索，后续会继续增加资源站点
- 过滤搜索结果，优先选择中文字幕和高清资源
- 快速提交磁力链接至 115 离线下载，依赖于 Clouddrive2 提供的离线接口
- 支持 iOS 设备通过捷径功能完成以上操作（捷径链接请参见下方）


### 安装
> 0.8版本后不再需要环境变量
#### DockerCli
```shell
docker run --name simple_115 \
    -v ./data:/data \
    -p 5150:5150 \
    --restart unless-stopped \
    -e "CD2_HOST=http://127.0.0.1:19798" \    # cd2的地址
    -e "CD2_USER=user" \                      # cd2的用户
    -e "CD2_PWD=passwd" \                     # cd2的密码
    -e "SAVE_PATH=/115/云下载" \               # 离线路径在cd2中的路径，可填写多个，用英文逗号隔开
    -e "PROXY=http://127.0.0.1:6152" \        # 系统代理
    htnanako/simple_115
```

#### Docker-Compose
```yaml
services:
  simple_115:
    image: htnanako/simple_115
    container_name: simple_115
    volumes:
      - ./data:/data
    ports:
      - 5150:5150
    restart: unless-stopped
    environment:
      CD2_HOST: http://127.0.0.1:19798  # cd2的地址
      CD2_USER: user                    # cd2的用户
      CD2_PWD: passwd                   # cd2的密码
      SAVE_PATH: /115/云下载             # 离线路径在cd2中的路径，可填写多个，用英文逗号隔开
      PROXY: http://127.0.0.1:6152      # 系统代理
```

### 配置
#### 配置文件在映射的data下的config/config.json
> 第一次生成配置文件时，会将环境变量的值保存到配置文件中。
> 
> 请勿直接复制以下内容，json文件不允许注释。
```json
{
    "common": {
        "CD2_HOST": "",       # cd2的地址
        "CD2_USER": "",       # cd2的用户
        "CD2_PWD": "",        # cd2的密码
        "SAVE_PATH": ""       # 离线路径在cd2中的路径，可填写多个，用英文逗号隔开
    },
    "PROXY": {
        "PROXY": "",          # 系统代理
        "timeout": 30         # 超时时间
    },
    "notify": {
        "webhooks": {
            "webhook_url": "",        # webhook通知地址
            "webhook_method": "POST",         # webhook请求方式
            "webhook_params": ""        # webhook请求额外的参数，键与值使用冒号(:)隔开，多组参数间使用英文逗号(,)隔开
        }
    },
    "SHT": {
        "ENABLE": true,        # SHT定时拉取功能开关，关闭修改为false
        "TASK_CRON": "13 0 * * *",        # SHT定时任务cron五位表达式
        "SHT_SAVE_PATH": "/115/测试路径/刮削前",        # SHT任务拉取保存的cd2目录
        "SHT_CATE": "中文字幕,三级"         # SHT任务拉取的类型，共有以下可选，使用英文逗号(,)隔开。国产,动漫,三级,中文字幕,无码,亚洲有码,欧美无码,VR视频,亚洲无码,4K。
    }
}
```

### 捷径下载
- [提交磁链到115](https://www.icloud.com/shortcuts/7ef65b68d71648478b635554ed842e5b)
- [提交番号手动选种下载](https://www.icloud.com/shortcuts/66778e0dd731463c9fe1b40ff9305c52)
- [提交番号自动选种下载](https://www.icloud.com/shortcuts/e669f01a931e4a52856b6e93bf770657)
