
Jeecg-Boot 快速开发平台-jeecg-boot-activiti-online
===============
## 前言

- 本项目是基于 https://github.com/happy-panda/jeecg-boot-activiti 的基础上进行的再次开发，修改了一些代码结构，增加了一些功能，除了增加的代码，主体代码基本都源于原作者，感谢原作者**happy-panda**: https://github.com/happy-panda 的开源贡献。

- 而其根本项目则是基于 https://github.com/jeecgboot/jeecg-boot 开源版。

- 本项目主要在jeecg-boot-activiti的基础上添加了online模块自动添加activiti代码的功能（支持单表，多表等多种风格），并在原版本activiti功能上扩展了一些功能，比如添加表单组件管理页面在页面上进行组件管理，表单支持多表等；其次修复了一些bug，包括原来基础版本和jeecg-boot-activiti的一些bug。

- 由于本人之前参考的基础版本是v.2.4.2，并且本人所做修改已经过去很长时间，所以这里选用的版本也是 v.2.4.2，之后升级的版本理论上应该不会影响activiti的功能。如有升级需求可自行酌情升级。
-  本项目是自己对开源研究的扩展，欢迎大家共同研究。由于主要是对activiti模块的online扩展，所以关于jeecg-boot的问题，请联系jeecg团队，关于activiti的问题，请联系原作者。如有关于activiti online模块的问题，可留言讨论，谢谢！

## 使用说明

> 本使用说明主要聚焦在如何使用本项目提供的online activiti功能使用上，不包含activiti的具体用法，关于activiti，可以参考官方资料或其他资料。

### 启动前数据库和redis相关

#### 配置

本人为了操作方便，在application-dev.yaml文件中使用环境变量替换了数据库和redis的host和ip配置：

```yaml
...
datasource:
  master:
    url: jdbc:mysql://${HOST_IP_PORT}/jeecg-boot...
...
redis:
  database: 0
  host: ${REDIS_HOST_IP}
...
```

如果不准备采用这种方式，可以使用原来基础版的方式。

#### 数据库数据准备

请在按照你的数据库类型在数据库中执行**jeecg-boot-module-activiti**模块db文件夹下的sql文件，第一次使用create文件夹下的，然后执行update.sql，请根据对应的具体数据库执行或修改执行。

### 启动后

#### 菜单授权

给activiti相关菜单授权，现在应该可以在左侧菜单栏看到工作流的菜单了。

#### 创建发布流程模型

这个流程的主要部分和之前没有变化，但是原来版本中需要在文件中配置表单组件，我这里进行了修改，可以在表单组件管理菜单上进行管理，在这个界面点击添加表单组件，按照说明根据你的表单信息填写相应字段即可。

就是在流程模型菜单中创建新的模型，然后在已发布模型菜单中进行编辑，在这里可以预览关联的表单，这里的表单即是上一步你在表单组件管理中创建的表单组件。编辑完成后再按需求进行节点设置，之后启用即可。

#### 申请

原来的版本中，由于不支持online，只能通过我的申请菜单进行申请，并且代码逻辑需要自己去写，包括前端和后端的代码。在这个项目中，我们只需要在online表单开发中，数据库属性增加act_status字段，默认值为**未提交**（这里可以在代码中默认，但是偷懒没改，有兴趣的小伙伴可以提交pr），字段备注大概就是审核状态之类的描述，然后页面属性中表单显示不勾选此字段，列表显示可按大家需求勾选即可。

生成代码后，我们可以发现相比于不加act_status字段的代码有了变化，这些变化即是activiti相关的逻辑。重新部署后，我们在自己项目的表单页面上新增一条数据后，可以在详情下面找到**提交申请**（主表的按钮情况可能不同，但**提交申请**是有的），点击以后的流程和我们在申请菜单中的流程一样。工单的状态会更新到表单数据中的审核状态一列中。

## 结语

最后再次感谢jeecg-boot团队提供的优秀的开源版本，以及happy-panda提供的非常实用的activiti模块，由于本人水平有限，代码比较粗糙，欢迎各位提供pr来优化代码。如有相关使用问题也欢迎提交issue共同讨论。
