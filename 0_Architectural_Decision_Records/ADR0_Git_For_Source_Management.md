# Git for Source Code Management

ADR 0: 使用Git进行源代码管理

- 状态：采用
- 决定者：PM - 陈欣洋
- 日期：2020-02-16

## 背景

20人团队，3组，每组内3层技术栈，进行敏捷开发。该过程需要一个高效的源代码管理与协作方式。

## 可选方案

- 纯文件分享
  - 优势：学习成本低。
  - 劣势：本身不包含版本管理，难以维持团队内版本统一。
  - 劣势：组与组之间、技术栈之间需要进行大量额外协调。

- Git：单一Repo
  - 优势：强大的版本管理、分支、合并功能，降低协调成本。
  - 优势：带有版本历史，可以前进/回退到特定版本以便找到新引进的问题。
  - 优势：对接DevOps管线，自动测试&部署。
  - 劣势：较高的学习成本。

- Git：多Repo
  - 区别：使每个团队拥有自己独立的Repo
  - 优势：简化分支合并
  - 劣势：增加复杂度，同一更改可能在多个Repo中都需出现

## 结果

选择GitHub上的单一Repo进行源代码管理。
