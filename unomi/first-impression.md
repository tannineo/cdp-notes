# First impression

以下都是没有尝试过 Unomi 的胡言乱语:

Unomi 感觉更像是基于 Event 触发各种过程的系统, 这些过程包括用户建模, 分类, 评分, 以及一系列其他操作(自定义 Action, 据文档描述 Salesforce 的 Connector 其实就是一些列额外定义的 Action).

参考官方文档: https://unomi.apache.org/manual/latest/#_how_profile_tracking_works

## Import & Export Profiles

我们现在的问题:

> 手头已经有一系列用户的信息, 并且会定期从别的来源获取用户信息, 如果考虑集成 Unomi, 就需要考虑如何导入用户 Profile.

Unomi RESTful API 提供了 Profile 的导入导出: https://unomi.apache.org/manual/latest/#_profile_import_export

## 老板说的 Standard? 和 GDPR Compliance

`ctrl-f` `standard` 只找到这个说明: [Customer Experience Digital Data Layer](https://www.w3.org/2013/12/ceddl-201312.pdf) , 好像是描述如何在 webpage 通过 js 追踪用户的. 数据库的设计并没有遵循什么已有业界标准. 只能说 Unomi 的数据库设计可以作为参考, 的确有所启发:

- 我们的业务 ACID 要求并不严格, 考虑到数据一旦入库, 搜索需求更大, Elasticsearch 可能相对传统 SQL 更符合我们的场景. (Elasticsearch as document database, 对比 mongoDB 有啥区别?需要研究)
- campaign, event, goal... 这些现有的业务模型, 对于我这种初次接触 marketing 行业的人来说值得参考.

至于 GDPR Compliance, 因为有一个统一的 Consent 模型存储, 应该能做到用户选择, 且根据用户的记录执行全文查询, 删除对应记录应该也不困难.
