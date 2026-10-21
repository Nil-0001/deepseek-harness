# 连云港开发文档

## 本地模型

llm访问地址：http://miluoinfo.cn/v1
密钥：gpustack_60576a0a8f0b19c3_9f64c82c2bd78c5dceeeeb9f4217aa06
模型名称：
qwen3.8:27b
bge-reranker-v2-m3
bge-m3

10.20.16.14：8188   comfyui上面

{"data":[{"id":"qwen3.8-27b","created":1787203843,"object":"model","owned_by":"gpustack","meta":null},{"id":"bge-m3","created":1791442994,"object":"model","owned_by":"gpustack","meta":null}],"object":"list"}

## 运行

```bash
pnpm install
pnpm run typecheck
pnpm run build
```

网页端
```bash
pnpm dsh web
```

桌面端
```bash
pnpm run start:desktop
```

## 挂载插件

```bash
pnpm dsh plugin --profile web add "D:\Desktop\BaiduSyncdisk\Miluo\LYG_agent\LYG_ui"  # 添加插件

pnpm dsh plugin --profile web list  # 插件列表

pnpm dsh plugin --profile web remove @nilwang/dsh-client-ui-theme  # 卸载插件
```

## 更新

### 远端更新

```bash
git pull upstream master
git push origin master
```

### 本地更新

```bash
git pull origin master
git push -u origin master
```

## 结构

```txt
deepseek-harness
│
├── vendor/                   👉 【真正的 Cordis 微内核】（底座发动机，负责统筹与调度）
│   ├── cordis                (Context、Service、Fiber 核心运行时)
│   ├── loader                (插件依赖加载器)
│   ├── include               (YAML 补丁与动态表达式)
│   └── schemastery           (配置 Schema 校验)
│
├── apps/                     👉 【宿主外壳与启动器】（拉起 Cordis 引擎并提供入口）
│   ├── cli                   (dsh 命令行入口)
│   ├── desktop               (Electron 桌面壳)
│   └── web                   (Vite 静态打包)
│
├── native/                   👉 【C++ 底层系统扩展】（Landlock 沙箱、文件锁驱动）
├── patches/                  👉 【第三方依赖补丁】（pnpm patch 修复上游 node-pty、pkg 等 bug）
├── scripts/                  👉 【构建与门禁脚本】（CI 流水线、代码生成器、质量检查）
├── benchmarks/               👉 【性能基准测试工程】（长会话内存、启动耗时、终端吞吐压测）
├── python/                   👉 【Python 跨语言包装】（Python SDK 与运行时 wheel）
├── snapshots/                👉 【录制会话快照资产】（预先录制的真实 Session 会话回放流）
├── docs/ & website/          👉 【架构文档与官网】（Markdown 文档源文件与 VitePress 站点）
├── .agents/ & .claude/       👉 【智能体工程记忆库】（架构决策记录 ADR 与开发专属技能 Skills）
├── .github/                  👉 【CI/CD 与审查策略】（Actions 工作流、PR Review 权限）
├── .dsh-build/               👉 【构建环境元数据缓存】（编译版本与 Git Commit 记录）
├── lyg/                      👉 【本地开发者工作区】（个人笔记与常用同步脚本）
│
└── packages/                 👉 【核心业务积木（绝大部分是 Cordis 插件）】
    ├── core/                 (核心脊椎：agent-loop, session, tools, system-prompt 插件)
    ├── llm/                  (模型接入插件：deepseek, openai, anthropic 适配器)
    ├── fs/ · shell/ · pty/   (环境能力插件：文件工具、终端执行、持久化 PTY)
    ├── ptc-runtime/ · subagent (高级特性插件：代码化调用、子代理委派)
    └── util/ · scope/        (少数纯函数工具库，非插件)
```