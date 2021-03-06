## 1. 数据存储的持久性

合同期内承诺每月用户申请实例的数据存储的持久性为 99.9996%。即用户每月每 1,000,000 个实例的存储的文件，每月只有 4 个实例有数据丢失的可能性。

## 2. 数据可销毁性

在用户要求删除数据或在设备弃置、转售前腾讯云将采取磁盘低级格式化操作彻底删除用户所有数据，并无法复原，硬盘到期报废时将进行消磁。

## 3. 数据可迁移性

腾讯云将提供标准的 MySQL 数据库文件格式的数据服务，并支持用户通过腾讯云提供的导入导出工具将数据转存为标准的 SQL 文件，方便用户迁入云数据库，或者迁出到用户的虚拟主机或者本地服务器上。

## 4. 数据私密性

腾讯云通过配置防火墙策略，采用白名单过滤机制进行网络隔离，通过数据库实例的用户名，密码和关闭数据库实例的权限控制机制来保证同一资源池用户数据互不可见。

## 5. 数据知情权

1. 数据存储的数据中心位置（可以通过提交工单进行咨询确认）。
2. 数据备份数量以及备份数据存储的数据中心位置（可以通过提交工单进行咨询确认）。
3. 帮助用户选择网络条件合适的数据中心存储数据，冷备则是根据资源利用情况动态分配，用户默认无需选择数据中心和冷备中心位置，如果需要选择，可以通过提交工单进行咨询确认。
4. 数据中心要遵守的当地的法律和中华人民共和国相关法律（可提交工单进行咨询确认）。
5. 用户所有数据不会提供给任意第三方，除政府监管部门监管审计需要。用户的行为日志会用于数据库运行状态的数据分析，但不会对外呈现用户个人信息数据。

## 6. 数据可审查性

腾讯云在依据现有法律法规体系下，出于配合政府监管部门的监管或安全取证调查等原因的需要，在符合流程和手续完备的情况下，可以提供云数据库相关信息，包括关键组件的运行日志、运维人员的操作记录、用户操作记录等信息。

## 7. 业务功能

腾讯云提供的云数据库实例的服务功能，具体包括 CDB 实例申请、登陆、数据库增删改查、冷备提取、数据回档、数据导入、多线程数据导入导出工具、运维数据查询 AP、密码重置。所有功能均已提供详细的功能介绍和使用说明文档。每项会影响用户数据结果的功能的变更均通过站内信通知用户。

## 8. 业务可用性

1. 云数据库承诺 99.95% 的业务可用性，即用户每月业务可用时间应为 30 天 × 24 小时 × 60 分钟 × 99.95% = 43178.4 分钟，即存在 43200 - 43178.4 = 21.6 分钟的不可用时间，其中业务不可用的统计单元为用户单业务实例。
2. 业务故障的恢复正常时间 5 分钟以下，不计入业务不可用性计算中，不可用时间指业务发生故障开始到恢复正常使用的时间，包括维护时间。

## 9. 业务资源调配能力

腾讯云承诺用户，申请计算资源扩容时，现有资源 50% 以下容量，并且扩容实例资源小于 10 个，1 小时完成；申请资源小于 30 个，24 小时内完成；多于 30 个，请提交工单咨询完成时间。每次单用户最大可扩展 100% 容量，最小 25 GB 的容量。

## 10. 故障恢复能力

腾讯云提供专业团队 7x24 小时帮助维护。
