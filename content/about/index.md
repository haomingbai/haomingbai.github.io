---
title: "About"
---

{{< katex >}}

# 关于我

白昊明，西北工业大学软件工程本科生（2023.09—2027.06），关注高吞吐网络服务、事件驱动架构与异步 I/O。

## 联系方式

- 手机：(+86) 138-1817-5845
- 邮箱：[haomingbai@mail.nwpu.edu.cn](mailto:haomingbai@mail.nwpu.edu.cn)
- GitHub：[github.com/haomingbai](https://github.com/haomingbai)

## 教育经历

**西北工业大学** · 软件工程，软件学院（在读） · 2023.09—2027.06

- GPA：3.44/4.1；本科从 0 开始自学 C++，加入校 ACM 基地，系统训练算法与数据结构，夯实工程基础。
- ICPC 2025 陕西省赛银牌、CCPC 2025 郑州站铜牌、2026 美赛 ICM Honorable Mention。
- 开源维护 [C++ 算法模板库](https://github.com/haomingbai/algorithm_example)（GitHub 29 stars），实现 B+ 树、AC 自动机、可持久化线段树、SA-IS 等。

## 技术能力

- **语言**：C++20（主要）、C；熟悉 JavaScript；了解 Java、Python；CET-4 603 / CET-6 568。
- **方向**：高吞吐网络服务、事件驱动架构、异步 I/O、并发控制、性能压测与调优；熟悉 Linux 系统编程与调试。
- **工作流**：Linux（6 年）、Shell、Git、CMake、Podman、Vim/VS Code、GitHub Actions、$\LaTeX$。

## 工作经历

### 腾讯科技（深圳）有限公司 · 技术工程事业群 · 云架构平台部（实习生）｜2026.07—2026.10

- 针对 AI Agent 产品 WorkBuddy 的 MCP/消息同步延迟瓶颈，参与边缘加速探索，两个月内收敛出可落地方案。
- 提出网页抓取、边缘代码执行、边缘消息队列三个方向；独立设计与实现前两者并完成实验验证，纳入远期规划。
- 负责边缘消息队列的实验，参与架构讨论；围绕延迟目标与工程取舍评估候选方案，输出结论支撑选型。
- 国内消息同步延迟实测降低约 50%，海外 P99 按链路测算 &lt; 200 ms；支撑方案通过并进入开发排期。

### 深圳市大数据研究院（香港中文大学（深圳））（实习生）｜2026.01—2026.02

- 参与水电站水库调度优化系统综述的框架设计、撰写与修改工作，相关论文目前在投 [Engineering Management](https://link.springer.com/journal/42524)。
- 系统调研 2016—2026 年 138 篇水电站调度优化文献，梳理强化学习、遗传算法、粒子群优化与动态规划等方法。
- 学习 Branch & Bound、列生成等精确计算方法，并分析其在实际调度问题中的适用性、实现难点与计算代价。

## 项目经历

### [bnio](https://github.com/haomingbai/bnio) · C++20 异步 I/O 库（独立开发，开源）｜2026.06—至今

- C++20 缺少统一异步 I/O 抽象、C++26 std::execution 未落地；[自研 P2300 子集](https://github.com/haomingbai/bexec)并构建 bnio，统一异步编程模型。
- 采用 sender/receiver 调度模型，将 I/O、定时器、DNS、TLS 统一为惰性、可组合的异步操作，屏蔽平台差异。
- 每 worker 独占 io_uring/kqueue 事件循环，提交与收割本地化，避免多线程共享环的同步与跨核提交。
- 线程本地任务队列减少竞争，跨线程批量投递摊薄同步开销，降低缓存失效与调度抖动，提升多核扩展性。
- 定时器与任务调度按需加锁，减少热路径内存分配与锁竞争，在低延迟与高并发场景下保持调度稳定与低开销。
- 分层模块化设计，统一跨平台 API，明确模块边界，分离接口与实现，降低耦合，便于上层组合、替换与扩展。
- 提供跨平台构建、打包与 CI；Linux/macOS 构建与测试、Linux 包消费测试通过，保证多平台交付一致性。
- [TCP echo 对比 Asio/epoll](https://github.com/haomingbai/bnio/blob/main/docs/benchmark/io_uring.md)：整体 1.046 倍、4 worker 1.13 倍、峰值 1.25 倍（1.0M vs 0.80M req/s）。

### [bsrvcore](https://github.com/haomingbai/bsrvcore) · 轻量级 C++20 异步 HTTP 服务器框架（独立开发，开源）｜2025.09—2026.06

- Servlet 模型基于同步 IO、每请求占用 worker 线程；bsrvcore 以 Reactor 多核架构承载 Servlet 式编程模型。
- 提供 AOP、路由、会话、生命周期管理与插件化能力，支持跨语言嵌入与配置驱动部署，形成可扩展框架。
- 采用多 reactor 分片与端口复用，将连接按核分流，降低 accept 竞争与跨核调度开销，提升多核吞吐。
- 结合连接亲和与缓存友好的内存分配，减少跨线程调度、缓存失效与内存同步开销，提升多核吞吐稳定性。
- 连接级写队列与超时管理，读写生命周期按连接维护，支持长连接与流式写入，兼顾内存占用与响应及时性。
- 建立自动化构建、测试与发布流程，支持 DEB/RPM 打包；Linux/macOS 构建与包消费测试通过。
- [同机回环微基准 70 万以上 RPS](https://github.com/haomingbai/bsrvcore/blob/main/docs/benchmark-results/benchmark-report.md)（峰值 85 万），覆盖多核扩展与饱和点验证，支撑高吞吐服务。

### [西瓜报名](https://github.com/haomingbai/program_test) · 校内程序设计考试报名系统（独立开发）｜2024.03—至今

- 针对校内课程考试报名集中开放时容易超卖的问题，构建校内投产的报名系统并保证名额一致性与流程完整性。
- 基于微信云开发与 NoSQL 数据库，用事务将空闲名额检查与报名写入原子化，避免并发超卖，保证数据一致。
- 接入校内 CAS 统一认证，实现报名、退选、签到、考场管理、数据导入与签到表导出，服务学生与管理端。
- 单场考试 3000+ 用户报名，系统在校内投产使用；前端基于小程序原生框架与 ColorUI，覆盖学生与管理员端。

## 个人总结

- 热爱新技术，关注 C++ 协程、execution、ranges 等新特性与软件抽象架构；在异步 I/O 与性能优化上追求极致。
- 认同科技向善，关注技术的社会影响与工程伦理，希望以扎实的工程能力解决真实问题、持续创造社会价值。

## 简历下载

- [中文简历 PDF](/resume.pdf)
- [English Resume PDF](/resume-en.pdf)
