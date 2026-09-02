# 开源mcp-server-ftp服务Docker项目

**此项目GITHUB源码开源仓库**
URL: [alxspiker/mcp-server-ftp](https://github.com/alxspiker/mcp-server-ftp)

**此仓库代码说明**
- 此项目的源码来源于GITHUB仓库
- 此项目仅用于通过拉取GITHUB代码仓库源码，根据源码中dockerfile进行修改后打包镜像推送镜像仓库
- 此项目修改后的dockerfile，基于supergateway服务，是SSE上运行MCP的一个成熟MCP桥接器服务
- supergateway服务在github的开源地址：[supercorp-ai/supergateway](https://github.com/supercorp-ai/supergateway)

**项目方案**
- 容器内 = stdio 服务 + Streamable HTTP 桥(零改代码)
- 用一个成熟桥接器 supercorp-ai/supergateway 把 stdio 服务转成 Streamable HTTP(当前 MCP 远程标准,端点 /mcp),整个服务跑在同一个容器里:

```text
MCP 客户端 ──HTTP──> supergateway(:8000 /mcp) ──stdio──> mcp-server-ftp ──FTP/SFTP──> 你的 FTP 服务器
```

**此项目目录及文件说明**
```text
|- ./src  # 根据每个版本更新同步github开源代码仓库中原始目录以及下面的文件，不做任何更改
|- ./package.json  # ，不做任何更改
|- ./tsconfig.json  # 根据每个版本更新同步github开源代码仓库中根目录下的原始文件，不做任何更改
|- /dockerfile  # 用于该项目生成直接可用的docker镜像使用的制作镜像文件(基于supergateway服务)
|- /docker-compose.yaml  # 用于直接在部署服务器上进行运行服务的docker-compose文件 
|- /README-Custom.md # 此项目说明文档
```

**容器镜像制作说明**
- build命令
```shell
# chanpin-ftp-mcp-server:latest 其中的latest跟随mcp-server-ftp上github开源release版本
docker build -f ./dockerfile-custom -t chanpin-ftp-mcp-server:v1.2.1
```

- docker-compose部署
```shell
docker compose -f ./docker-compose.yaml up -d
```