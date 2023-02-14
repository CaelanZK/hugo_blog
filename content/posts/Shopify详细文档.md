---
title: "Shopify详细文档"
subtitle: ""
date: 2023-02-13T11:35:21+08:00
draft: false
author: ""
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- BlockChain
- Shopify
- Tokengate
categories:
- 区块链

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []


# See details front matter: https://fixit.lruihao.cn/theme-documentation-content/#front-matter
---

<!--more-->
## 区块链相关

> 构建支持区块链的商业：发现 UI 组件、强大的 API 以开发您的下一个令牌驱动的应用程序、提高忠诚度、促进品牌合作、增强社区能力等
> 区块链应用程序被定义为向商家展示区块链资产或功能的任何应用程序，包括但不限于加密货币、铸币、代币生成和赠送
> Shopify 上的所有区块链应用程序都必须符合区块链应用程序要求

### 概述

#### NFT发行

1. 商家可能出于各种原因决定出售或赠送 NFT。销售 NFT 的商家必须先获得 Shopify 的批准，然后才能通过 Shopify Payments 进行销售。支持商家进行 NFT 分发的开发人员需要控制此功能，并限制铸造、赠送或列出 NFT 以出售给获准商家的能力
2. 代表商家上架和铸造 NFT 的开发人员必须遵守 Shopify 应用商店中对应用的要求，包括区块链应用合作伙伴要求，并特别注意 NFT 分发应用的要求

#### 代币化和忠诚度

1. 代币化商务让商家可以向拥有特定NFT（Token）的客户提供对其商店中的产品
   1. 进行折扣或者独家购买
   2. 品牌还可以进行Token化，让基于品牌Token的其他产品与用户建立忠诚度
2. Tokengating

#### 加密支付

- Shopify支持加密货币进行支付（[加密货币 · Shopify 帮助中心](https://help.shopify.com/zh-CN/manual/payments/additional-payment-methods/cryptocurrency)）

![image.png](https://uss.useenet.cn/picgo/note/202302132236563.png)

### NFT发行

#### 概述

##### NFT发行

> 商家可能会决定出售或赠送 NFT。目前，NFT 最常用于展示数字艺术等媒体的所有权，但它们对商家和客户还有许多其他用途

1. 商家可能会考虑通过以下方式在他们的 Shopify 商店中使用 NFT：
   1. 通过他们的Shopify商店出售NFT
   2. 提供免费的NFT以奖励其客户的购买、参与和忠诚度
   3. 通过代币化商业，根据某些NFT的所有权提供独家产品、折扣和产品发布的早期访问权
   4. 通过您的在线商店或者现场活动与其他品牌进行代币化合作，增加潜在受众
   5. 根据NFT所有权创建客户群，以进行以进行营销获取和保留活动
   6. 在客户购买时提供正品证书或者NFT收据
2. 销售 NFT 的商家必须先获得 Shopify 的批准，然后才能通过`Shopify Payments`进行销售。支持商家进行 NFT 分发的开发人员需要控制此功能，并限制铸造、赠送或列出 NFT 以出售给获准商家的能力

##### 开发商代表商家上市和铸造NFT

1. 支持商家铸造、赠送或上架 NFT 以供销售的开发人员必须满足以下要求
   1. 在应用程序的安装过程中或在应用程序内向商家显示申请表，当商家尝试访问这些功能但尚未获得批准状态时重定向到申请表
      - 如果您希望在安装应用程序期间显示表单，则应用程序开发人员不需要进行额外的开发工作。
      - 如果您希望重定向到应用内的申请表，您必须根据商家的当前状态验证是否需要显示该表单，并在相关情况下将商家引导至`https://{shop}.myshopify.com/admin/nft-application`
      - 在应用程序批准过程中，应用程序开发人员将被问及他们希望申请表显示在何处的偏好。如果您决定改变关于申请表显示位置的想法，请发送电子邮件至<blockchain-partners@shopify.com>
   2. 当 Shopify Payments 在商店中处于活动状态时，阻止商家列出 NFT，直到商家获得[SellApproved](https://shopify.dev/apps/blockchain/nft-distribution/nft-sales-eligibility#possible-api-responses)（`sellApproved`：true）和/或[GiftingApproved](https://shopify.dev/apps/blockchain/nft-distribution/nft-sales-eligibility#possible-api-responses)（`giftingApproved`：true）
   3. 遵守[区块链应用合作伙伴要求](https://shopify.dev/apps/store/requirements#a-blockchain-app-requirements)

#### 检查NFT销售资格（开发文档）

- [Check NFT sales eligibility](https://shopify.dev/docs/apps/blockchain/nft-distribution/nft-sales-eligibility)

#### 商家资格

> [Merchant eligibility](https://shopify.dev/docs/apps/blockchain/nft-distribution/merchant-eligibility)

- 需要通过[Shopify Payments](https://help.shopify.com/manual/payments/shopify-payments)销售 NFT 的商家必须在销售前获得 Shopify 的批准

### Tokengating

#### 概述

> Tokengating 允许商家为符合条件的代币持有者提供对产品和折扣的独家访问权

##### 运行方式

1. Tokengating是对Token要求的定义，用于确定谁可以解锁它，主要由一个`字段`和一个`反应`组成
   1. 字段：定义了哪些Token持有者可以通过验证他们的Token所有权来通过`Tokengating`
   2. 反应：则是通过`Tokengating`的结果，例如特定产品的折扣等
2. Tokengating应用程序可以指导商家完成入口配置过程（包括定义入口要求和相应的反应），最后将他们与钱包连接体验一起展示给店面的客户
3. 示例流程图：
   1.
   ![image.png](https://uss.useenet.cn/picgo/note/202302141420235.png)

##### Tokengate应用职责

1. Configuration 配置
   1. 该应用程序如何用于配置商户定义的`Tokengate`以及要求
   2. 图片示例
      1.
   ![image.png](https://uss.useenet.cn/picgo/note/202302141704752.png)
2. Presentation 演示
3. `GateConfiguration` 详细信息（如状态和要求）如何呈现给客户。表示层也是客户连接钱包的地方
4. 图片示例
   1.
   ![image.png](https://uss.useenet.cn/picgo/note/202302141706478.png)
5. Evaluation 评估
   1. 应用程序如何根据 `GateConfiguration` 检查客户的钱包内容并做出相应反应。例如，应用程序可能会通过打折做出反应。为确保您的`Tokengate`具有服务器端验证，您应该使用 Shopify Function
   2. 图片示例
      1.
      ![](https://uss.useenet.cn/picgo/note/202302141707473.png)

#### 构建Tokengate应用程序

- [Overview](https://shopify.dev/docs/apps/blockchain/tokengating/build-a-tokengating-app)
- [Create gates](https://shopify.dev/docs/apps/blockchain/tokengating/build-a-tokengating-app/create-gates-admin)
- [Show gates](https://shopify.dev/docs/apps/blockchain/tokengating/build-a-tokengating-app/show-gates-storefront)
- [Apply discount](https://shopify.dev/docs/apps/blockchain/tokengating/build-a-tokengating-app/shopify-function-gate-reaction)

#### 用户体验指南

1. 客户体验
   - 客户应该清楚地了解什么是被限制的，他们可以如何采取行动，以及他们在连接钱包后的资格状态是什么。
   1. 在客户连接他们的钱包之前，传达解锁`Tokengate`所需的内容（最好是视觉上的）
   2. 如果客户没有，请提供获取所需Token的路径
   3. 清楚地传达`Tokengate`解锁的内容（反应）
   4. 当产品被门控时，隐藏只有在`Tokengate`被解锁时才具有功能的控件（变体、购买按钮、数量选择器）
   5. 支持尽可能多的钱包，即使您想提升某些钱包的体验
   6. 如果客户的连接钱包不包含符合条件的代币，则将其传达给他们。如果需要令牌组合的话，则显示客户缺少哪些令牌
   7. 不需要在单个购买会话中连接多个钱包。连接钱包后，店面上的所有门都应该根据它进行评估
   8. 如果`Tokengate`内容不再可用，则在`Tokengate`锁定状态下将其传达给客户。例如，如果门禁产品售罄，则在客户连接钱包之前显示该产品已售罄
   9. 当`Tokengate`解锁时，通过显示客户符合条件的令牌来个性化体验
   10. 使客户能够轻松断开他们的钱包
   11. 通过将样式与主题相匹配，让代币体验成为商家店面的原生体验

2. `Tokengate`的状态例子
   1. 客户尚未连接钱包。`Tokengate`已锁定，`Tokengate`内容已隐藏
   2. 客户连接了一个没有有效令牌的钱包。`Tokengate`锁定，`Tokengate`内容已隐藏
   3. 客户已将钱包与有效令牌相关联。`Tokengate`被解锁，`Tokengate`内容被显示（购买表格）
   4.
   ![image.png](https://uss.useenet.cn/picgo/note/202302141908133.png)

3. 商家体验
   - 为商家提供清晰的说明、丰富的预览和全面的错误验证。尽量避免技术性语言和操作
   1. 为获得最佳商家体验，请直接在 Shopify 后台构建您的应用，并遵循构建 Shopify 应用的最佳实践
   2. 尽量减少使用不太熟悉区块链技术的商家可能不理解的技术术语。例如，限制智能合约、元数据和 ERC-1155 等术语的使用
   3. 配置`Tokengate`时，允许商户使用通俗易懂的语言查询和可视化搜索结果来搜索代币集合
   4. 提供尽可能多的细分选项，以便商家可以细化他们的客户定位。例如，您可以让商家根据特征、代币 ID 或代币组合对客户进行细分
   5. 在配置过程中提供`Tokengate`的动态预览
   6. 允许商家自定义任何面向客户的组件的样式以匹配他们的主题
   7. 如果您的`Tokengate`仅适用于在线商店，请确保商家了解将门控产品发布到其他渠道可能出现的问题，例如门规避或结账失败

4. 商家管理员用户体验示例
   1. ## Token collection search 代币收藏搜索
      - 
       ![image.png](https://uss.useenet.cn/picgo/note/202302142008917.png)
   2. ## Dynamic gate preview 动态门预览
      - 
      ![image.png](https://uss.useenet.cn/picgo/note/202302142009738.png)

### 开发区块链应用程序要求

[Requirements for apps in the Shopify App Store](https://shopify.dev/docs/apps/store/requirements#a-blockchain-app-requirements)

> 区块链应用程序被定义为向商家展示区块链资产或功能的任何应用程序，包括但不限于加密货币、铸币、代币生成和赠送。

#### 区块链应用要求

1. 需要联系`blockchain-partners@shopify.com`进行申请流程
2. 确保没有个人数据写入或存储在链上
3. 只有获得`Shopify Payments`团队批准的支付合作伙伴，否则不能出售、转让或者修改可替代令牌
   1. crypto.com
4. 应用程序目前只支持 NFT 在Shopify 上的初级销售
5. 应用程序在任何情况下都不应促进代表或有资格作为证券或其他受监管金融工具的 NFT 的销售或营销，或与证券或其他受监管金融工具相关的活动。
6. 1. 应用程序必须确保没有二次版税（例如，非创作者版税）写入 NFT。

#### NFT分发应用程序要求

> NFT 铸造应用程序允许商家在 Shopify 上创建和销售 NFT。 NFT 赠送应用程序允许商家免费分发 NFT，并包括购买实体产品的免费 NFT、免费将 NFT 列为产品或追溯空投给客户

##### NFT创建

1. 商家能够从 Shopify 后台维护他们提供的所有NFT的上下文（请求和创建）
2. 所有 NFT 变体都必须使用产品元字段以编程方式表示其 NFT 状态

##### NFT 产品元字段

- 任何包含一个或多个 NFT 变体的产品都必须使用产品元字段在产品对象中列出 NFT 变体 ID

![image.png](https://uss.useenet.cn/picgo/note/202302131136311.png)

##### NFT的分发

1. 关注铸造方法，商家在Shopify后台中的NFT履行的操作必须<mark style="background: #FFB86CA6;">及时向客户发送</mark>`Claim`消息
2. 需要一个<mark style="background: #FFB86CA6;">单独界面</mark>向商家提供每个<mark style="background: #FFB86CA6;">NFT执行操作</mark>以及<mark style="background: #FFB86CA6;">后续情况</mark>
3. 再每笔交易需要给客户提供
   1. 区块链交易ID（tracking_numbers）
   2. 区块链浏览器链接（tracking_urls）
   3. 具体是那条区块链（tracking_company）
4. 应用程序必须给客户提供一种请求钱包的方式，如果他们需要的话
   1. 客户必须对其NFT有完全的自我保管，可以链上直接铸造，必须向用户明确说明，且不收取费用
5. 不能分发受金融机构监管的NFT
6. 应用程序必须获得商家的批准，商店才能够铸造、赠送、创造或者列出NFT产品，或者使用有销售资格的API来确定商店的批准状态
7. 在没有确认的情况下，应用程序不能将NFT的`claim`链接发送到其他人

##### 端到端验证测试

- Shopify必须能够对NFT分发应用程序进行端到端的测试，包阔必要时创建、铸造和交付NFT，以验证应用程序功能

#### 代币化应用程序要求

> Shopify 上的令牌化应用程序允许商家根据客户 Web3 钱包的内容来控制对产品、促销和内容的访问

##### 代币化订单元字段

- 任何通过 gate 添加或者打折的订单必须通过使用指定的元字段将订单项 ID 添加到订单对象来识别

![image.png](https://uss.useenet.cn/picgo/note/202302131949977.png)

##### 代币化产品元字段

- 任何包含一个或多个 gated variants 的产品都必须使用产品元字段在产品对象中列出 gated variants ID

![](https://uss.useenet.cn/picgo/note/202302131958312.png)
