# Data Model of Unomi

![Data model overview](/unomi/data-model-overview.jpg)

Official documentation: https://unomi.apache.org/manual/latest/#_data_model_overview

## Scope

域, 举例来说, 域的值可以是是 CMS 的域名, 用作划分业务. 系统默认值是 `systemscope` , 表示所有域共享的内容.

## Item

所有 data 的泛型, 包含了 `id`, `itemType`, `scope` 这些基础属性.

## MetadataItem

泛型, 存储一个对象的额外信息. 包含一个 `metadata`

### MetaData

里面存储了所需要的 plugin 支持, 一些业务开关, tags...

## Event

事件, 在某个时刻(时间戳)发生的事, 用来记录用户操作(点击, 表单提交, 登入, 浏览页面等...).

用 `eventType` 表示类型, 用 `properties` 键值对记录对应 `eventType` 的详细信息.

事件还包含了 Profile 和 Session.

### Built-in Event types

- Login
- View (打开某个页面)
- Form (提交表单)
- Update properties (如:用户修改自己的信息)
- Identify (类似 update properties, 但是用户输入相对不可信, 切这一改动是公共可见的, 详情请查阅官方文档)
- Session created (当新 Session 被创建)
- Goal (当一个 Profile 达成一个 Goal)
- Modify consent (当用户修改 Consent, e.g. 取消订阅邮件)

## Profile

处理 Event 时, Unomi 会建立 Profile 为用户行为建模.

Profile 包含了描述用户的常用字段: 姓名 年龄 email 等...

Profile 也包含了一些用户评分和用户分类, 也鼓励增加更多定制化数据.

同一个用户会在各个服务留下多个 Profile, Unomi 会在检测到这些 Profile 的共同特征后将他们合并.

### Persona

继承自 Profile, 但没有自己独立的 fields, 就是一类特殊的, 有代表性的 Profile.

并不是某个具体的用户, 而是某一类用户.

## Consent

同意条款, 记录用户是否 同意了某项条款/打开了某个开关, 比如接收 marketing email.

## Session

会话, 关联一个 Profile, 并且会保存一个 Profile 当时的副本 (记录历史变化? denormalization?).

Session 以松散的方式管理了一系列连续的 Event, 记录了此次会话的时常, 和最后一个 Event 的时间戳.

## Segment

用户分割/分类, 包含 Condition, 根据条件为 Profile 分类(Profile 有`segments`字段,有点像打 tag).

## Condition

条件, 出现于众多 Unomi 的 data model 里:

- Segments
- Rules
- Queries
- Campaigns
- Goals
- Profile filters (用于搜索 Profiles)

Unomi 提供了许多内置的 condition type, 并且用 `and`, `or`, `not` 操作符构建复杂查询.

Condition 得到的结果总是一个 boolean.

(此处参考官方 example 更能说明如何组织复杂查询):

```json
{
  "condition": {
    "type": "booleanCondition",
    "parameterValues": {
      "operator": "or",
      "subConditions": [
        {
          "type": "eventTypeCondition",
          "parameterValues": {
            "eventTypeId": "sessionCreated"
          }
        },
        {
          "type": "eventTypeCondition",
          "parameterValues": {
            "eventTypeId": "sessionReassigned"
          }
        }
      ]
    }
  }
}
```

## Rule

规则, 可以想像成 hook, 每有新的 Event, 这个 Event 都会被所有 Rules 校验. 如果 Rule 通过校验, 就会执行对应的 Action.

Rule 与 Action 被设计得足够灵活, 可以编写插件(Connectors)来增加更多功能.

### Action

动作, 由 Rule 触发的一系列操作中的一个.

## List

列表, 对比 Segment, List 更偏向‘人工定义的’列表.

和 Segment 一样, List 本身不存储一个 Profile 数组, 而是在 Profile 里的`systemProperties.lists`做标记, 很像 tagging.

## Goal

目标, 根据 Event, 设置了起始和目标 Conditions, 当一个 Profile 有符合起始 Condition 的 Event, 并且接下来的 Event 触发了目标 Condition, Goal 就会被触发, Profile 的 `systemProperties.goals` 会增加对应 Goal 达成的时间戳.

Goal 还可以和 Campaign 绑定.

## Campaign

活动, Campaign 包含了持续时间, Profile 的入场 Condition, 金钱成本, 以及重要指标 Goal.

## Scoring Plan

评分方案, 包含一组 Condition 和他们对应的评分, 当 Condition 被满足, 相应的 Profile 就会被修改对应的评分.
