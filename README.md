# simple_115

> 本项目旨在快速搜索番号并提交至115网盘离线下载，简化操作流程，省去繁琐的手动步骤。

### 功能介绍：
- 优先选择SHT中文字幕数据库作为数据源，无资源自动下落 BT 站点
- 自动搜索 BT 站资源并提交番号，目前已支持[sukebei](https://sukebei.nyaa.si/)、[freejavbt](https://freejavbt.com)站点资源自动搜索，后续会继续增加资源站点
- 过滤搜索结果，优先选择中文字幕和高清资源
- 快速提交磁力链接至 115 离线下载，依赖于 Clouddrive2 提供的离线接口
- 支持 iOS 设备通过捷径功能完成以上操作（捷径链接请参见下方）


### 安装
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

### 捷径下载
- [提交磁链到115](https://www.icloud.com/shortcuts/7ef65b68d71648478b635554ed842e5b)
- [提交番号手动选种下载](https://www.icloud.com/shortcuts/58f6f77d023c4aab970d3bb123fb28d3)
- [提交番号自动选种下载](https://www.icloud.com/shortcuts/9c34ef3a71c3486f813ecd217ccf4b2e)
