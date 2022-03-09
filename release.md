# 如何发布将自己的片段发布到vscode市场呢
> mac-token: uvyllmuwan2ndfqf6uplpouaojsde2r7iidnfei63ehyi4dadpqq

## 1. 全局安装依赖

### vsce 包管理工具

```bash
npm install -g vsce
```

### 项目脚手架

```bash
npm install -g yo generator-code
```

## 2. 快速创建项目

```bash
yo code
```

### 选择 new code snippets

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/36a5f690dac34b39bbb9b6b5c644b385~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

按提示输入包名、描述等生成项目

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2e50cb2410824ec0a584bce59fdf523b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)


## 3. 获取个人访问令牌

1. 首先，在 Azure DevOps[登录 Azure DevOps](https://app.vssps.visualstudio.com/_signedin) 中创建您自己的组织

2. 选择"新建组织"

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ae0bcaa9f05d4f7c944369d6ab77d3db~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

3. 创建组织成功

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2662959fa41418787b5e9258bf00c31~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

4. 创建项目

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67dcbdc3b7e143dea8e374b30823c5ab~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

5. 从组织的主页选择个人访问token

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ff494534ab184c5ab99bc46e0d6868a4~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

- 设置token名字

- 将组织设置为所有可访问的组织

- 可选择延长其到期日

- 将范围设置为自定义，然后选择市场 > 管理范围

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3ae59f8792264c8aa07cedb20f3e2a48~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

生成Token成功

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/989a30ce65564d779d5c0985b17d08f9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

## 4. 创建发布者

执行 vsce login 命令

```bash
vsce login <publisher name>
```

输入之前创建的token

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bcdcbed936b0495c972ec59db8280a5b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)


## 5. 开发snippets且发布

```bash
vsce publish    //拓展发布
vsce publish 2.0.1  //拓展发布至指定版本
vsce publish minor   //自动增加扩展版本
vsce unpublish (publisher name).(extension name) //取消发布扩展

```

## 6.敲重点的一节来了package.json属性含义讲解

package.json 文件图解


- version(红色区域)：版本号每次有修改且需要发布时一定要修改版本号不然发不上去（此坑踩过）
- engines(蓝色区域)：最低vscode版本号支持，就是vscode1.28.0版本以上的才能使用此拓展
- repository(黄色区域): 远程仓库地址
- contributes(白色区域): snippets配置项可设置language、以及aliases设置别名等等

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12459fa45d41450e8f1666d64eb57f26~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

## 7. 发版失败(vsce publish)常见的错误

- 错误1：Error:Missing publisher name. Learn more:[https://code.visualstudio.com...](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#publishing-extensions)
解决方式：在package.json中将刚刚创建好的发布账号配置进去"publisher":"your name",

- 错误2：Error:Make sure to edit the README.md file before you publish your extension
解决方式：看下README.md文件中是否有http地址

- 错误3：A ‘repository’field is missing from the 'package.josn' manifest file .Do you want to continue? [y/n]
解决方式：y

- 错误4：vsce publish 成功，但是在 [https://marketplace.visualstudio.com/manage/publishers/win](https://marketplace.visualstudio.com/manage/publishers/win) 上没有真正发布成功，最终发现是 README.md 存在问题，但是没找到具体原因，故最好不要更改现有的 README.md 文件文案格式结构。
具体错误：
