# 总览

<!-- markdownlint-disable MD026 -->
## Argo CD是什么?
<!-- markdownlint-enable MD026 -->

Argo CD是Kubernetes的一个声明性的GitOps持续交付工具。

![Argo CD UI](assets/argocd-ui.gif)

<!-- markdownlint-disable MD026 -->
## 为什么是Argo CD?
<!-- markdownlint-enable MD026 -->

应用程序的定义，配置和环境应该是声明性的，并且受版本控制。
应用程序的部署和生命周期管理应该是自动化的，可审核的且易于理解的。

## 入门

### 快速开始

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

遵循我们的[入门指南](getting_started.md)。 提供了更多有关其他功能的面向用户的[文档](user-guide/)。 如果你要升级ArgoCD，请参阅[升级指南](./operator-manual/upgrading/overview.md)。面向开发人员的[文档](developer-guide/)可供有兴趣构建第三方集成的人员使用。

## 如何工作

Argo CD遵循**GitOps**模式，该模式使用Git仓库作为定义所需应用程序状态的事实来源。of using Git repositories as the source of truth for defining
the desired application state. Kubernetes资源可以通过几种方式指定：

* [kustomize](https://kustomize.io) 应用
* [helm](https://helm.sh) charts
* [ksonnet](https://ksonnet.io) 应用
* [jsonnet](https://jsonnet.org) 文件
* YAML/json资源的普通目录
* 任何配置为配置管理插件的自定义配置管理工具

Argo CD可在指定的目标环境中自动部署所需要的应用程序状态。应用程序的部署能够追踪Git分支，标签的变更，或者通过指定某个Git提交绑定到具体版本的资源。有关可用的不同跟踪策略的更多详细信息，请参阅[跟踪策略](user-guide/tracking_strategies.md)。


10分钟快速浏览Argo CD，查看展示给Sig Apps社区的演示：


[![Argo CD Overview Demo](https://img.youtube.com/vi/aWDIQMbp1cc/0.jpg)](https://youtu.be/aWDIQMbp1cc?t=1m4s)

## 架构

![Argo CD 架构](assets/argocd_architecture.png)

Argo CD被实现为Kubernetes控制器，持续监控运行的应用程序，并比较当前实时的状态和期望的目标状态（在Git仓库中指定的）。实时状态偏离目标状态的已部署应用程序被视为`OutOfSync`。Argo CD报告并可视化差异，同时提供了自动或手动将实时状态同步回期望的目标状态。任何对Git仓库中的期望状态的修改都能够被自动地应用并反映在指定的目标环境中。

更多的细节, 请参阅[架构总览](operator-manual/architecture.md).

## 功能

* 自动部署应用程序到指定的目标环境中
* 支持多个配置管理/模板工具(Kustomize, Helm, Ksonnet, Jsonnet, plain-YAML)
* 管理和部署多个集群的能力
* 集成SSO (OIDC, OAuth2, LDAP, SAML 2.0, GitHub, GitLab, Microsoft, LinkedIn)
* 多租户和RBAC授权策略
* 回滚/任意回滚到Git仓库中的任何应用程序配置
* 应用程序资源的健康状态分析
* 自动检测和可视化配置偏移
* 自动或手动同步应用程序到期望状态
* 提供实时应用程序视图的Web UI
* CLI用于自动化和CI集成
* Webhook集成 (GitHub, BitBucket, GitLab)
* 用于自动化的Access tokens
* PreSync, Sync, PostSync钩子用于支持复杂应用程序的发布(比如，蓝/绿和金丝雀升级)
* 应用程序事件和API调用的审计跟踪
* Prometheus指标
* 参数覆盖用来覆盖Git中ksonnet/helm参数

## 开发状态

社区一直积极开发Argo CD。 在[这里](https://github.com/argoproj/argo-cd/releases)可以找到我们所有的发布。

## 采用

从[这里](https://github.com/argoproj/argo-cd/blob/master/USERS.md)可以找到已经官方采用Argo CD的组织。