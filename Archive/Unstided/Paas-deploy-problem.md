# PaaS部署与升级问题:20200213第一次讨论记录

1. AKE：Python 脚本部署，配置单独拆分出来，部署脚本可以复用 ansiblo Playbook，比 shell 可用性更高些
2. 客户环境本身会更复杂（可以继续沟通）：
3. 版本升级：我们版本升级并验证（增加测试验收）
    * 功能层面上的，部署应用等都出现问题
    * 部署包里默认的环境变量是错误的
    * Redis、Kafka、ES 等无法做平滑升级
        * 版本跨度大，无法升级，要有明确的告知
4. 版本的维护（定制功能）
    * 需要单独的验证规则
    * 定制功能清单列表等
5. 部署文档、升级手册里可以提供一个完整的验证成功标准
    * 自动化测试验证 ？ — 操作比较复杂，实施同事不容易上手
    * 组件测试工具 — 运维验证
    * 收集项目上线升级过程中的验证功能 — 海涛
6. 流水线可能会有版本不兼容，产品侧本身不兼容的部分，需要暴露
7. 发版、测试距离品控还是有一定的距离：
    * 功能不好用，可能跟什么有关系 — 运维了解
    * 功能如何使用 — 测试了解
    * 私有部署、升级包测试缺失；可能验证不完整。
8. 发版验证可以验证保证平台部署成功；责任人需要明确 — 部署测试
9. 产品版本信息报漏：组件版本等信息
10. 升级等文档变更（频繁，导致 PSD 获取消息不及时
11. 部署文档（歧义部分：可能需要调整结构；部署文档参数及产品说明等
12. 部署文档需要增加测试用例，需要明确的验收标准 
13. Confluence or jira 等核心业务推动在生产环境上使用
14. 运维能力：业务组件及运维管理
15. 组件部署的 Request Limit 值，初始化数据以及推荐等
16. 部署白皮书有些方案，措辞需要优化
    * 高可用依赖域名，变更 IP or 域名 变更需要重新部署
    * 长域名到短域名的切换
    * 项目POC阶段使用 IP 会比较多，不能变更 Host，只能用 IP
    * 域名：客户真正实施的时候可以提前要求，未来将来做容灾
    * Https + IP ，通过私钥认证，推动所有客户端都
17. 产品升级以后对应产品变更需要测试验证 — Harbor 支持 https
18. 产品用法改变，需要在 Release note
19. Https+ip 等4种部署方式，升级是否验证过（AMP、AML 是否有验证过） — 杜维维