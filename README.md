# WeChat Mini Program Jump Relay Page (微信小程序跳转中继页)

## 项目简介 (Project Introduction)

本项目是一个部署在 **微信云开发 (WeChat CloudBase)** 静态网站托管环境下的中继页面。其主要作用是作为 **作品集项目小程序** 与 **目标小程序** 之间的跳转桥梁。

通过对接微信开放标签（WeChat Open Tags）与云开发免鉴权机制，实现在微信环境内（如小程序 Webview、微信内置浏览器）流畅地跳转至指定的小程序页面。

## 核心功能 (Core Features)

*   **中继跳转**：作为中间页，接收来自“作品集项目”小程序的跳转请求。
*   **微信能力对接**：集成 `wx-open-launch-weapp` 开放标签，实现小程序间的无缝唤起。
*   **云开发集成**：利用 CloudBase 静态托管特性，实现免鉴权（Identityless）调用微信 JS-SDK，简化签名流程。

## 工作流程 (Workflow)

1.  **触发入口**：用户在“作品集项目”小程序的卡片或链接中点击跳转。
2.  **页面加载**：请求被重定向至当前托管在 CloudBase 的静态页面 (`jump-mp.html`)。
3.  **环境初始化**：页面加载 `cloud.js` 并初始化云开发环境，自动完成微信 JS-SDK 的鉴权配置。
4.  **渲染跳转按钮**：页面展示 `<wx-open-launch-weapp>` 开放标签（通常表现为一个点击按钮或透明覆盖层）。
5.  **完成跳转**：用户点击或自动触发后，微信客户端唤起目标小程序。

## 部署信息 (Deployment Information)

*   **代码仓库**：GitHub
*   **部署环境**：微信云开发 (WeChat CloudBase) - 静态网站托管
*   **依赖服务**：
    *   微信 JS-SDK (`jweixin-1.6.0.js`)
    *   云开发 Web SDK (`cloud.js`)
*   **访问策略**：
    *   必须通过云开发分配的特定域名或绑定的自定义域名访问，以确保免鉴权机制生效。
    *   仅支持在微信客户端环境（MicroMessenger）中运行，非微信环境将显示提示信息。
