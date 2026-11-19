# mac-quicknotes · 7 天 Devin 主导学习计划

> **模式**：Devin Bot 担任主导师与主开发；你负责提问、验收、合并与复盘；GitHub 是全程唯一的记录源。
> **角色边界**：本机没有可直接调用的 Devin 连接器。Devin 通过 app.devin.ai / Devin Desktop / CLI 使用；这里负责把每日任务卡、验收标准与 GitHub 记录规范准备好，你也可以让我帮你检查 PR 或在本地跑测试。
> **铁律**：Devin 不能创建 GitHub 仓库。动手前必须确认 `LumaCong/mac-quicknotes`（私有）已经存在。

---

## 0. 开场设置（Day 0，约 30 分钟）

- [ ] 确认 `github.com/LumaCong/mac-quicknotes` 私有仓库已创建（若还没有，手动创建，Devin 做不到这一步）
- [ ] 在 Devin 设置中连接 GitHub，授权权限至少包含：`Contents: Read and write`、`Issues: Read and write`、`Metadata: Read only`、`Pull requests: Read and write`
- [ ] 私有仓库需在 GitHub 集成中显式授权给 Devin（Devin 的权限是集成级，不是「按发起用户镜像」）
- [ ] 在 Devin 会话中 `@LumaCong/mac-quicknotes` 提及仓库，走完 Repo Knowledge 引导，让 Devin 建立代码库认知
- [ ] 建立初始提交：README、`.gitignore`、`LEARNING_LOG.md`、`docs/architecture.md`（可让 Devin 第一个会话以 PR 形式提交；空仓库若失败，你手动加 README 后再继续）
- [ ] `main` 分支开启保护：必须 PR + review 才能合并
- [ ] 建 Milestone `7-day-mac-quicknotes`，预建 D1–D7 七个 Issue
- [ ] 会话命名统一为 `learn-d1-xxx`，**每个会话控制在 3 小时以内**，一天一个大任务，超了就拆成第二个会话

---

## 1. 与 Devin 协作的三种提示词模板

### A. 任务卡（每天下给 Devin 的主指令）

```text
@LumaCong/mac-quicknotes
【任务卡 D?：<主题>】

目标：
<用一句话说清今天要实现什么>

背景与已知上下文：
<已完成的模块、表结构、约定；贴关键文件路径>

必须交付：
1. ...
2. ...

验收标准（请自测并在 PR 中给出证据）：
1. ...
2. ...

技术约束：
- Swift 6 / SwiftUI / GRDB.swift，不用 Core Data
- 提交粒度：一个小功能一个 commit，格式 `learn(d?): 动词 + 对象`
- 写完先解释关键概念（面向刚上手的人），再写代码
- 禁止直接 merge 到 main，只开 PR 等我 review
- 不确定的地方先问我，不要自行假设产品行为

自测方式：
<告诉 Devin 它能力范围内可以怎么验证；Xcode GUI 相关验收由我在本地完成>
```

### B. 教学卡（让它先教后写，这是「学习」而非「代写」的关键）

```text
在动手写代码之前，先用 10 行以内讲清楚今天涉及的核心概念：
1. 它解决什么问题？
2. 不用它会怎样？
3. 在这个项目里为什么选它？

讲完等我回复「继续」再开始写。实现完成后，在 PR 描述里写一段「给新手的讲解」，
指出哪三行代码最值得我读懂。
```

### C. 复盘卡（每天收尾，写进 PR）

```text
本次会话结束前，请在 PR 描述末尾追加「今日学习记录」：
- Devin 完成了什么（按 commit 列）
- 我需要掌握的 3 个知识点
- 我容易误解的 1 个点
- 你自测了什么、没测什么（如实说明）
- 明天建议预习的一句话
```

---

## 2. GitHub 全程记录规范

| 载体   | 命名规则                         | 内容                                                         |
| ------ | -------------------------------- | ------------------------------------------------------------ |
| Issue  | `D1 · 地基：跑起来，存得住`      | label `learn, D1, p0`；贴任务卡与验收标准；附 Devin 会话链接 |
| 分支   | `learn/d1-foundation`            | 每天一个分支，从 `main` 开出                                 |
| Commit | `learn(d1): add notes migration` | 小步提交，一天 3–8 个                                        |
| PR     | `D1: SQLite 地基与 NoteStore`    | 含实现清单、教学卡输出、自测证据、今日学习记录               |
| Review | 在 PR 评论 `/devin review`       | 触发 Devin Review 自动查 bug；你再人工过一遍                 |
| 日志   | `LEARNING_LOG.md`                | 每天合并后追加 5 行复盘                                      |
| 架构   | `docs/architecture.md`           | 由 Devin 随代码演进维护                                      |

**每天的闭环**：Issue（任务）→ Devin 开分支写码 → PR → `/devin review` → 你 review 与提问 → Devin 回复评论并修复 → 你 merge → 更新 `LEARNING_LOG.md`。PR 评论 Devin 会自动回复（会话未归档时），所以提问直接写在 PR 里即可。

---

## 3. 一周总览

| 天   | 主题   | 核心交付                          | 分支                  | GitHub 记录        |
| ---- | ------ | --------------------------------- | --------------------- | ------------------ |
| D1   | 地基   | SwiftUI 壳 + SQLite 建表 + 增删改 | `learn/d1-foundation` | Issue/PR D1        |
| D2   | 手感   | Markdown 编辑 + 全局唤起          | `learn/d2-editor`     | Issue/PR D2        |
| D3   | 找得到 | FTS5 搜索 + 标签 + 回收站         | `learn/d3-search`     | Issue/PR D3        |
| D4   | 不丢   | 附件 + 版本 + Keychain + 导出     | `learn/d4-safety`     | Issue/PR D4        |
| D5   | 连得上 | WebDAV 连接 + 变更队列 + 上传     | `learn/d5-upload`     | Issue/PR D5        |
| D6   | 不打架 | 下载 + 冲突副本 + 墓碑 + 诊断     | `learn/d6-sync`       | Issue/PR D6        |
| D7   | 像产品 | 性能 / 无障碍 / README / 复盘     | `learn/d7-polish`     | Issue/PR D7 + 总结 |

---

## 4. 功能范围与技术架构

### P0 · 本周必须完成

- [ ] `⌥Space` 全局悬浮速记窗，输入即存
- [ ] 菜单栏常驻，拖入文件/图片即建笔记
- [ ] 剪贴板速记
- [ ] Markdown 编辑 + 实时预览，任务列表与代码高亮
- [ ] 图片/文件附件，Markdown 内相对路径引用
- [ ] 自动保存（0.5 秒防抖）
- [ ] 多标签、置顶、30 天回收站
- [ ] SQLite FTS5 全文搜索（含中文）
- [ ] 按时间/标签的规则视图
- [ ] SQLite WAL + 外键 + 事务
- [ ] Keychain 存凭据
- [ ] 每日本地快照 + 导出 Markdown / JSON + `integrity_check`
- [ ] WebDAV 连接测试、ETag 增量上传下载
- [ ] 冲突时生成副本，绝不覆盖
- [ ] 删除墓碑、重试退避、诊断日志

### P1 · 有余力就做

- [ ] 三栏布局打磨 / `Cmd+K` 命令面板
- [ ] 版本快照时间线与回滚 UI
- [ ] 仅 Wi-Fi 同步开关
- [ ] 深浅色适配、键盘导航、VoiceOver
- [ ] 语音转写（SFSpeechRecognizer）

### P2 · 之后再说

- [ ] `[[双向链接]]` / 正文 AES-GCM 加密 / 模板系统 / PDF 导出

### 架构约定（Devin 必须遵守）

- 数据库层用 GRDB.swift：`DatabaseQueue` + `Migrator`，WAL 模式
- 表：`notes`、`tags`、`note_tags`、`attachments`、`versions`、`sync_state`、`fts_notes`
- 远端按「每篇笔记一个 `.md` + 附件目录」存储，SQLite 为本地主库与索引
- `sync_state` 记录 `remote_etag`、`local_hash`、`remote_mtime`、`last_synced_at`、`dirty`
- 凭据只进 Keychain，不写 plist，不进导出文件
- 数据目录 `~/Library/Application Support/QuickNotes`

---

## 5. 每日计划

### D1 · 地基：跑起来，存得住

**今日目标**：SwiftUI 空壳 + `notes` 表 + `NoteStore` + 列表增删改。

**GitHub 动作**：Issue `D1 · 地基：跑起来，存得住` → 分支 `learn/d1-foundation` → PR `D1: SQLite 地基与 NoteStore`。

**Devin 任务卡**（套用第 1 节模板 A + B）：

```text
@LumaCong/mac-quicknotes
【任务卡 D1：地基】
目标：建立一个可运行的 SwiftUI macOS 应用骨架，并用 GRDB.swift 完成笔记的本地持久化。
必须交付：
1. Xcode 项目骨架（SwiftUI App，三栏布局占位）
2. Migrator 创建 notes 表（id/title/body/created_at/updated_at/is_deleted）
3. NoteStore 封装插入、更新、软删除、查询
4. 列表页 + 新增/删除交互
5. 三个单元测试（插入/更新/删除）
验收标准：
- 写入后重启应用数据仍在
- 单测全部通过，在 PR 中贴出测试结果
技术约束：Swift 6 / SwiftUI / GRDB.swift；开 WAL；提交格式 learn(d1): ...
自测方式：运行 xcodebuild test；GUI 交互部分给出你的验证步骤，我在本地复核。
先讲清 @State 与 @Observable 的区别、WAL 是什么，等我回复「继续」再写代码。
```

**你要做的**：读 Devin 的概念讲解；在本地 Xcode 打开 PR 分支跑一遍；在 PR 里问「为什么这里用 `@Observable` 而不是 `@StateObject`」。

**验收清单**

- [ ] 改一笔笔记，强制退出再启动仍在
- [ ] 三个 DB 单测通过
- [ ] PR 含「今日学习记录」且 Devin 说明了未测部分

---

### D2 · 手感：编辑器与全局唤起

**今日目标**：Markdown 编辑/预览、防抖自动保存、`⌥Space` 悬浮窗、菜单栏拖拽建笔记。

**GitHub 动作**：Issue `D2 · 手感` → 分支 `learn/d2-editor` → PR `D2: Markdown 编辑器与全局唤起`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D2：编辑器与全局唤起】
目标：让速记应用真正「随手可用」，并完成不丢内容的自动保存。
必须交付：
1. TextEditor + Markdown 预览切换
2. 0.5 秒防抖自动保存，快速切换笔记不能写错对象
3. ⌥Space 全局悬浮速记窗（HotKey 或 Carbon）
4. NSStatusItem 菜单栏常驻，拖入图片/文件生成带附件笔记
5. Cmd+K 命令面板原型
验收标准：
- 快捷键唤起 → 输入 → 关闭 → 重开，内容不丢
- 拖拽图片生成笔记，附件路径可解析
技术约束：沿用 NoteStore；处理 Task 取消与闭包循环引用；提交格式 learn(d2): ...
自测方式：单测覆盖防抖与笔记切换；GUI 部分列出你的验证步骤。
先解释「为什么 NSEvent 全局监听不能拦截按键」再动手。
```

**你要做的**：亲手按快捷键走一遍；在 PR 里问「如果用户连续快速切换笔记，Task 取消的顺序会不会写错？」

**验收清单**

- [ ] 悬浮窗流程内容不丢
- [ ] 拖拽图片生成附件笔记
- [ ] `/devin review` 跑过且你已回复反馈

---

### D3 · 找得到：搜索与归类

**今日目标**：FTS5 全文搜索（含中文）、标签、置顶、回收站、规则视图。

**GitHub 动作**：Issue `D3 · 找得到` → 分支 `learn/d3-search` → PR `D3: FTS5 搜索与标签体系`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D3：搜索与归类】
目标：一万条笔记量级下秒级检索，并支持基本归类。
必须交付：
1. fts_notes 虚拟表 + 增删改触发器
2. 搜索结果高亮
3. 标签多对多表与筛选、置顶、30 天回收站（软删除/恢复）
4. 规则视图：今天 / 有附件 / 未同步
5. 1 万条中英混合假数据 + 基准测试脚本
验收标准：
- 中英文搜索均在 100ms 内，PR 中贴出基准数据
- 回收站恢复后标签关系不丢
技术约束：FTS5；中文分词方案先给我对比 unicode61 / trigram / 自编译 SQLite 再选
自测方式：跑基准测试与数据完整性单测。
```

**你要做的**：看 Devin 的分词方案对比，自己决定选哪个并写进 PR 评论；检查搜索结果中文命中是否合理。

**验收清单**

- [ ] 1 万条数据搜索 < 100ms
- [ ] 标签与回收站行为正确
- [ ] PR 记录了分词方案的选型理由

---

### D4 · 不丢：附件、版本与安全

**今日目标**：附件引用、版本快照、Keychain、导出与备份。

**GitHub 动作**：Issue `D4 · 不丢` → 分支 `learn/d4-safety` → PR `D4: 附件、快照与安全底座`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D4：附件、版本与安全】
目标：任何误操作都能找回数据。
必须交付：
1. 附件目录 + Markdown 相对路径引用
2. versions 表：保存前写快照；时间线与回滚 UI（若时间不够，UI 留到 P1，数据层必做）
3. Keychain 封装（先存占位凭据）
4. 导出 Markdown 文件夹 / JSON
5. 每日快照备份脚本 + 定期 PRAGMA integrity_check
验收标准：
- 插入图片重启后仍在，引用可点开
- 能回滚到 10 分钟前版本
- 导出目录结构与原文一致
技术约束：清洗文件名，防 ../、超长名、非法字符；凭据绝不写 plist 或导出文件
自测方式：写「删掉主库后从快照恢复」的演练脚本并给出结果。
先以安全 reviewer 视角列出路径遍历与文件名注入风险再动手。
```

**你要做的**：在本地真机验证图片重启后仍在；亲自演练一次从快照恢复。

**验收清单**

- [ ] 附件持久化与回滚通过
- [ ] 导出结构正确
- [ ] 恢复演练成功且记录在 PR

---

### D5 · 连得上：WebDAV 上传

**今日目标**：连接测试、`sync_state`、变更队列、批量 PUT、定时/手动触发。

**GitHub 动作**：Issue `D5 · 连得上` → 分支 `learn/d5-upload` → PR `D5: WebDAV 上传链路`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D5：WebDAV 上传】
目标：把本地笔记可靠地推到 WebDAV。
必须交付：
1. 设置页（URL/账号/密码/远程目录）与连接测试（PROPFIND + 写测试文件）
2. sync_state 字段落地（etag/local_hash/mtime/last_synced_at/dirty）
3. 变更检测 + 变更队列 + debounce 2–5 秒批量 PUT
4. 手动/定时同步与状态指示
5. 本地 wsgidav 测试环境脚本与 curl 验证命令
验收标准：
- 远端 .md 可直接用文本编辑器打开
- 断网时队列不丢，恢复后自动继续
技术约束：ETag + If-Match 乐观锁；actor 隔离数据库访问；提交格式 learn(d5): ...
自测方式：对本地 wsgidav 跑上传/断网/恢复测试并贴日志。
先解释 ETag 乐观锁与可能的并发竞态再动手。
```

**你要做的**：在本地用坚果云或 wsgidav 复查一次连通性；在 PR 里问「同步中和用户编辑同时发生会怎样？」

**验收清单**

- [ ] 上传后的远端文件内容正确
- [ ] 断网恢复后队列继续
- [ ] PR 含 curl 验证证据

---

### D6 · 不打架：下载、冲突、删除

**今日目标**：增量下载、三向合并、冲突副本、墓碑删除、重试诊断。

**GitHub 动作**：Issue `D6 · 不打架` → 分支 `learn/d6-sync` → PR `D6: 双向同步与冲突处理`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D6：双向同步与冲突】
目标：两端交替编辑也不丢数据。
必须交付：
1. PROPFIND 扫描远端 → 增量下载
2. base/ours/theirs 三向比较
3. 冲突生成 `xxx (conflict 日期).md` 副本，绝不覆盖任何一方
4. 删除墓碑双向同步
5. 指数退避重试、可读诊断日志、仅 Wi-Fi 开关、诊断页
验收标准：
- 「两端都改」「一端删另一端改」均不丢数据
- 断网重连自动追平，冲突副本可见
技术约束：同步操作幂等；提交格式 learn(d6): ...
自测方式：用 Swift Testing 覆盖至少 5 个冲突场景，贴测试结果。
先列出冲突场景测试表并说明状态机可能丢更新的迁移路径。
```

**你要做的**：人工模拟一次双端冲突，确认两个版本都在；检查诊断日志是否可读。

**验收清单**

- [ ] 冲突场景全部通过，数据无丢失
- [ ] 诊断页能看到上次同步时间与错误
- [ ] `/devin review` 无高危未处理项

---

### D7 · 像产品：打磨与复盘

**今日目标**：性能、无障碍、文档、发布准备与一周总结。

**GitHub 动作**：Issue `D7 · 像产品` → 分支 `learn/d7-polish` → PR `D7: 打磨与文档` → 关闭 Milestone `7-day-mac-quicknotes`。

**Devin 任务卡**：

```text
@LumaCong/mac-quicknotes
【任务卡 D7：打磨与收尾】
目标：让别人能照着 README 跑起来，并完成一周学习闭环。
必须交付：
1. 冷启动与列表滚动优化（1 万条数据）
2. 深浅色适配、空状态、首次引导、键盘导航/VoiceOver 检查
3. README（安装、快捷键、WebDAV 配置、数据恢复）
4. 更新 docs/architecture.md 与 LEARNING_LOG.md（按天汇总）
5. 归档/Release 准备清单
验收标准：
- 1 万条笔记下列表不卡，冷启动 < 1 秒（给出测量方式与数据）
- README 完整可执行
额外：对全部代码做一次 review，按严重程度列出安全/并发/边界问题。
```

**你要做的**：按 README 从零跑一遍；在 Milestone 里写总结；填写一周复盘。

**验收清单**

- [ ] 性能数据达标
- [ ] README 可执行
- [ ] `LEARNING_LOG.md` 有 7 天完整记录
- [ ] Milestone 关闭

---

## 6. Devin 使用守则（来自官方实践）

1. **单会话不超过 3 小时**，大任务拆成多个会话；一条新指令会重置 ACU 上限，但别靠这个硬撑。
2. **给 Devin 你本来知道怎么做的任务**，你才有能力验收——这也是「学习」成立的前提。
3. **明确告诉它如何自测**；它能力边界外的（Xcode GUI、签名、真机）由你在本地做。
4. **需求前置写详细**：任务卡里的验收标准越具体，返工越少。
5. **在 PR 评论里 coaching**：自动回复是开着的，把纠正写进评论会沉淀成 Knowledge。
6. **PR 上用 `/devin review`**：默认查 bug，安全敏感代码可指定更彻底的档位；规则可按路径/分支配置。
7. **合并冲突它不擅长**，出现冲突你手动解决再继续。
8. **权限是集成级的**：私有仓库访问失败先查 GitHub 集成授权，不要以为是 token 过期。
9. **它不能建仓库**：所有仓库准备工作必须由你先完成。

---

## 7. 三个提前避的坑与应急

1. **中文 FTS5**：系统 SQLite 的 `unicode61` 几乎不切中文；`trigram` 要先确认系统库版本，必要时自编译静态链接。让 Devin 在 D3 给出方案对比，别默认它选对。
2. **同步节流**：编辑后 debounce 2–5 秒入队并批量 PUT，避免一请求一个字。
3. **沙盒路径**：数据放 `Application Support/QuickNotes`；手动导出走安全作用域书签。
4. **Devin 跑偏**：在会话 chat 里纠正；纠正无效就停掉，用更小的任务卡重开一个会话，别在一个坏上下文里加码。
5. **成本失控**：每天只开一个主会话，Review 规则按文件/分支收窄，避免每次 push 全量审查。

---

## 8. 项目初期建设 Prompt（Day 0 首个 Devin 会话，可直接复制）

> 前提：私有仓库 `LumaCong/mac-quicknotes` 已存在、`main` 已开保护，Devin 已连接 GitHub 并授权该仓库；仓库内先有一个手动加的 README 以便 Devin 能克隆。
> 用法：在 Devin Web/Desktop 新建会话，粘贴下面整段。

```text
@LumaCong/mac-quicknotes
【项目初期建设 · 首个 Devin 会话】

背景：这是个人 macOS 速记应用 mac-quicknotes 的初始化会话。仓库已存在（私有），main 分支已开启保护。你通过 GitHub 集成操作本仓库，所有变更以 PR 形式提交，禁止直接推送或合并到 main。

目标：把仓库从空壳变成「可开发、可记录、可验收」的起点，为 D1 的 SwiftUI + SQLite 实现做好准备。

必须交付：
1. README.md：项目定位、功能范围（P0/P1/P2 见下）、技术栈、目录结构、快速开始、快捷键占位表、WebDAV 配置占位、数据备份与恢复说明占位。写「占位」的地方明确标注 TODO，不要编造内容。
2. .gitignore：macOS/Xcode/Swift 常用忽略；额外忽略 DerivedData、build/、*.xcuserdata、.env*、Config.plist、Credentials*、以及应用数据目录 QuickNotesData/。
3. LEARNING_LOG.md：7 天复盘模板，每天含日期、Devin 会话链接、PR 链接、学会的/卡住的/帮得好的/给错的一次/明天第一件事。
4. docs/architecture.md：目标架构说明 + Mermaid 图（SwiftUI ↔ SQLite 主库 ↔ WebDAV），列出计划中的表 notes / tags / note_tags / attachments / versions / sync_state / fts_notes 及关键字段，说明 ETag 同步与冲突副本策略。标注「设计稿，待 D1–D6 实现后更新」。
5. 项目约定文件 AGENTS.md（给后续 Devin 会话看）：Swift 6 / SwiftUI / GRDB.swift；提交格式 learn(dN): 动词+对象；分支 learn/dN-主题；每个任务先讲概念再写代码；不在代码或配置里留凭据；GUI 部分如实说明未验证；不确定就先问。
6. Xcode 项目骨架：macOS App、SwiftUI 生命周期、SPM 添加 GRDB.swift、开启 App Sandbox 的「网络客户端」和「用户选择的文件读写」能力；配置 WAL 的占位代码（D1 再做正式迁移）。如果当前环境无法创建或编译 Xcode 项目，明确告诉我哪些步骤需要我在本地做，不要假装完成。
7. GitHub 记录：创建 Milestone 7-day-mac-quicknotes；创建 7 个 Issue（D1 地基：跑起来存得住 / D2 手感：编辑器与全局唤起 / D3 找得到：搜索与归类 / D4 不丢：附件、版本与安全 / D5 连得上：WebDAV 上传 / D6 不打架：双向同步与冲突 / D7 像产品：打磨与复盘），label 用 learn、D1…D7、p0；Issue body 贴对应任务卡的验收要点；为本次初始化开 PR chore: 项目初始化与开发约定。

功能范围：
- P0（本周必做）：全局速记窗、菜单栏拖拽建笔记、剪贴板速记、Markdown 编辑与预览、附件、自动保存、标签/置顶/回收站、FTS5 中文搜索、WAL + Keychain + 快照导出、WebDAV 增量同步与冲突副本、删除墓碑与诊断日志。
- P1：命令面板、版本回滚 UI、仅 Wi-Fi、无障碍、语音转写。
- P2：双向链接、正文加密、模板系统、PDF 导出。

验收标准：
- 上述文件都在 PR 里，README 没有与实际冲突的假信息
- 7 个 Issue 与 1 个 Milestone 建好，PR 描述含文件清单与「待我在本地完成的步骤」
- 你先复述你对项目的理解并列出将创建的文件，等我回复「继续」再动手
- 不要 merge，不要创建凭据文件，不要声称 GUI 已验证

自测方式：检查 Markdown 链接与 Mermaid 语法；如能运行 xcodebuild 就贴出构建结果，否则明确说明无法构建。
```

---

## 9. 每日复盘模板（合并后追加到 `LEARNING_LOG.md`）

```markdown
### D? 复盘（日期：      ，Devin 会话：      ，PR：      ）

- 今天真正学会的：
- 卡住最久的地方：
- Devin 帮得最好的一次：
- Devin 给错/带偏的一次：
- 我在 PR 里提的最有价值的问题：
- 明天第一件事：
```
