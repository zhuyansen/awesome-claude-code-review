# Awesome Claude Code Review

[English](README.md)

给 Claude Code、Codex 等 agent 用的开源 **AI 代码审查 skill 和工具**:审查 skill、本地与命令行审查、PR 机器人与 CI、多 agent 互审、安全审查、自托管平台。共 185 个仓库,每个都由 [Agent Skills Hub (agentskillshub.top)](https://agentskillshub.top?utm_source=github&utm_medium=awesome-list) 读过 README 并做了安全评级。

带类型筛选的在线页面:**[https://agentskillshub.top/best/code-review/](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list)** · 每 8 小时刷新

## 到底装哪个

我们实跑了其中 16 个(13 个出了结果),结论如下。[完整实测结果](#tested)在下面。

- 🥇 **只想加一个审查 skill: [code-review-skill](https://github.com/awesome-skills/code-review-skill)**  
  八个埋入的缺陷全部找到，干净 PR 上零误报，约一分钟，每个 PR 不到两条发现。这和不装任何东西的 Claude Code 一样：它带来的是成文的检查清单和固定的报告格式，不是更强的检出。
- 🥈 **想让每次提交自动被审: [roborev](https://github.com/kenn-io/roborev)**  
  你提交时它在后台审；这次换了一个模型（gpt-6-astra）来读，仍然八个全中，每个 PR 不到一条发现。比较慢：12 个 PR 用了 13 分钟。
- 🥉 **宁可多等也不想看噪音: [adamsreview](https://github.com/adamjgmiller/adamsreview)**  
  审完的部分一个没漏，也是最安静的：每个 PR 0.5 条发现，完成的七个带缺陷 PR 全部找到。我们给的 30 分钟内差一个没审完。

**先弄清这几个不查什么:** brooks-lint (只查设计劣化；把卡号写进日志的 PR 给了 100/100); bug-hunter (不看测试文件，被削弱的测试会放过).

不管选哪个，最难抓的缺陷不在业务代码里：13 个里有 4 个放过了悄悄削弱测试断言的 PR。测试的改动要自己看。

*按找到的缺陷数、再按耗时排列。这套题分不出头部名次：不装任何工具的 Claude Code 一分钟找全 8 个缺陷、零误报，有 6 个工具结果相同。自带模型的工具用 gpt-6-astra 审，skill 用 Claude Opus 5.5 审，两组之间的差距可能来自模型。*


## 这些审查工具长什么样

<table>
<tr>
<td align="center" valign="top" width="33%"><b>🔁 PR 机器人与 CI</b><br><sub>39 个仓库</sub><br><br><a href="https://github.com/truongnh1992/gemini-ai-code-reviewer"><img src="assets/previews/truongnh1992__gemini-ai-code-reviewer.jpg" width="260" alt="truongnh1992/gemini-ai-code-reviewer"></a><br><sub>在每个 PR 上发评论的机器人和 CI。</sub><br><a href="#type-pr_bot"><b>查看列表 →</b></a></td>
<td align="center" valign="top" width="33%"><b>🧩 Agent Skill</b><br><sub>30 个仓库</sub><br><br><a href="https://github.com/Continuum-AI-Corp/Orca-Code-Review"><img src="assets/previews/Continuum-AI-Corp__Orca-Code-Review.gif" width="260" alt="Continuum-AI-Corp/Orca-Code-Review"></a><br><sub>让 Claude Code、Codex 审查 diff 的 skill 和插件。</sub><br><a href="#type-skill"><b>查看列表 →</b></a></td>
<td align="center" valign="top" width="33%"><b>⌨️ 本地与命令行</b><br><sub>65 个仓库</sub><br><br><a href="https://github.com/persiyanov/herdr-reviewr"><img src="assets/previews/persiyanov__herdr-reviewr.gif" width="260" alt="persiyanov/herdr-reviewr"></a><br><sub>在本地对分支或 diff 运行的审查工具。</sub><br><a href="#type-cli"><b>查看列表 →</b></a></td>
</tr>
<tr>
<td align="center" valign="top" width="33%"><b>🛡 安全审查</b><br><sub>16 个仓库</sub><br><br><a href="https://github.com/DeepCodeAI/vscode-extension"><img src="assets/previews/DeepCodeAI__vscode-extension.gif" width="260" alt="DeepCodeAI/vscode-extension"></a><br><sub>专找漏洞的 agent,有些在沙箱里复现。</sub><br><a href="#type-security"><b>查看列表 →</b></a></td>
<td align="center" valign="top" width="33%"><b>👥 多 Agent 互审</b><br><sub>26 个仓库</sub><br><br><a href="https://github.com/syabro/rejudge"><img src="assets/previews/syabro__rejudge.gif" width="260" alt="syabro/rejudge"></a><br><sub>多个审查者或模型看同一个改动。</sub><br><a href="#type-multi"><b>查看列表 →</b></a></td>
<td align="center" valign="top" width="33%"><b>🏗 自托管平台</b><br><sub>9 个仓库</sub><br><br><a href="https://github.com/imDarshanGK/AI-dev-assistant"><img src="assets/previews/imDarshanGK__AI-dev-assistant.jpg" width="260" alt="imDarshanGK/AI-dev-assistant"></a><br><sub>在团队所有仓库上跑审查的自托管服务。</sub><br><a href="#type-platform"><b>查看列表 →</b></a></td>
</tr>
</table>

## 目录

- [🧪 端到端实测](#tested)
- [🔁 PR 机器人与 CI](#type-pr_bot) (39)
- [🧩 Agent Skill](#type-skill) (30)
- [⌨️ 本地与命令行](#type-cli) (65)
- [🛡 安全审查](#type-security) (16)
- [👥 多 Agent 互审](#type-multi) (26)
- [🏗 自托管平台](#type-platform) (9)

## 什么样的仓库能上榜

1. 它用 AI 模型审查代码:一段 diff、一个 PR 或一个代码库,找 bug、安全问题或质量问题。只写代码的工具、不带模型的 linter、通用编程 agent 不算。
2. 它是能安装或运行的软件,不是链接合集或空仓库。
3. 它有 README。没有 README 就没法评级。
4. 50 星及以上只看是否切题;50 星以下还要过 README 质量线(展示效果、一条命令上手、说清产出、文档完整),并且至少 5 星。

这些问题由决策模型逐个读 README 回答,不是人工挑选。卡在线上的仓库可能判到任一边,归错了请提 issue。

<a id="tested"></a>
## 🧪 端到端实测

2026-10-10 我们实跑了其中 16 个，跑成 13 个。每个在用完即删的沙箱里审同样的 12 个 PR（一个小型 Python 服务）：8 个各埋了一个缺陷（差一错误、SQL 注入、卡号写进日志、漏掉权限检查、永不结束的重试、吞掉的异常、写反的条件、被削弱的测试），4 个是干净的。按 SWR-Bench 的做法每个工具给两个数：找到几个缺陷、在干净 PR 上报了几条阻塞问题。评审是 gpt-6-astra，三遍取多数。不装任何工具的 Claude Code 做了同样的事，作为对照。

**发现:** 没有工具超过对照组。不装任何东西的 Claude Code 约一分钟找全 8 个缺陷、零误报（每个 PR 1.8 条发现）；6 个工具与它持平，没有更好的。工具之间真正的差别是噪音（每个 PR 0.5 到 7.2 条发现）和耗时（1 到 30 分钟）。漏得最多的是被削弱的测试：13 个里有 4 个放过了。

| # | 工具 | ★ | 找到缺陷（共 8 个） | 4 个干净 PR 上的误报 | 每个 PR 发现数 | 耗时 | 审查模型 |  |
|---|---|---|---|---|---|---|---|---|
| 1 | [code-review-skill](https://github.com/awesome-skills/code-review-skill) | 1,914 | 8/8 | 0 | 1.8 | 1 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/awesome-skills__code-review-skill.html) |
| 2 | [guard-skills](https://github.com/amElnagdy/guard-skills) | 1,153 | 8/8 | 0 | 1.4 | 2 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/amElnagdy__guard-skills.html) |
| 3 | [review-forge](https://github.com/vikingmute/review-forge) | 220 | 8/8 | 0 | 1.3 | 2 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/vikingmute__review-forge.html) |
| 4 | [clean-architecture-skills](https://github.com/nathankim0/clean-architecture-skills) | 90 | 8/8 | 0 | 2.7 | 2 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/nathankim0__clean-architecture-skills.html) |
| 5 | [open-code-review](https://github.com/spencermarx/open-code-review) | 331 | 8/8 | 0 | 7.2 | 11 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/spencermarx__open-code-review.html) |
| 6 | [roborev](https://github.com/kenn-io/roborev) | 1,746 | 8/8 | 0 | 0.9 | 13 分钟 | gpt-6-astra | [证据](https://agentskillshub.top/best-runs/review/kenn-io__roborev.html) |
| 7 | [adamsreview](https://github.com/adamjgmiller/adamsreview) | 243 | 7/7 | 0 | 0.5 | 30 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/adamjgmiller__adamsreview.html) |
| 8 | [bug-hunter](https://github.com/codexstar69/bug-hunter) | 487 | 7/8 | 0 | 0.8 | 3 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/codexstar69__bug-hunter.html) |
| 9 | [open-code-review](https://github.com/alibaba/open-code-review) | 43,912 | 7/8 | 0 | 0.6 | 7 分钟 | gpt-6-astra | [证据](https://agentskillshub.top/best-runs/review/alibaba__open-code-review.html) |
| 10 | [vet](https://github.com/imbue-ai/vet) | 519 | 7/8 | 0 | 1.1 | 18 分钟 | gpt-6-astra | [证据](https://agentskillshub.top/best-runs/review/imbue-ai__vet.html) |
| 11 | [brooks-lint](https://github.com/hyhmrright/brooks-lint) | 1,506 | 5/8 | 0 | 0.9 | 3 分钟 | Claude Opus 5.5 | [证据](https://agentskillshub.top/best-runs/review/hyhmrright__brooks-lint.html) |
| 12 | [gentleman-guardian-angel](https://github.com/Gentleman-Programming/gentleman-guardian-angel) | 1,180 | 5/8 | 见说明 | 6.0 | 9 分钟 | gpt-6-astra | [证据](https://agentskillshub.top/best-runs/review/Gentleman-Programming__gentleman-guardian-angel.html) |
| 13 | [warden](https://github.com/getsentry/warden) | 414 | 4/8 | 0 | 0.5 | 25 分钟 | gpt-6-astra | [证据](https://agentskillshub.top/best-runs/review/getsentry__warden.html) |

**未能实测:** cynical-sally (它把 diff 发到自己的托管服务，当时返回服务不可用。); git-lrc (它把 diff 发给 LiveReview 服务器，本地没有可用的。); claude-pr-review (它通过 Bitbucket API 审 Bitbucket 上的 PR，审不了本地分支。)

[全部结果、提示词和脚本](https://github.com/zhuyansen/agent-skills-hub/blob/main/ops/review-runs/RESULTS.md) · [https://agentskillshub.top/best/code-review/#test-results](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#test-results)

<a id="type-pr_bot"></a>
## 🔁 PR 机器人与 CI

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-pr_bot)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/The-PR-Agent/pr-agent"><img src="assets/previews/The-PR-Agent__pr-agent.jpg" width="260" alt="The-PR-Agent/pr-agent"></a><br><sub><a href="https://github.com/The-PR-Agent/pr-agent">The-PR-Agent/pr-agent</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/Nayjest/Gito"><img src="assets/previews/Nayjest__Gito.jpg" width="260" alt="Nayjest/Gito"></a><br><sub><a href="https://github.com/Nayjest/Gito">Nayjest/Gito</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/sturdy-dev/codeball-action"><img src="assets/previews/sturdy-dev__codeball-action.jpg" width="260" alt="sturdy-dev/codeball-action"></a><br><sub><a href="https://github.com/sturdy-dev/codeball-action">sturdy-dev/codeball-action</a></sub></td>
</tr></table>

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [The-PR-Agent/pr-agent](https://github.com/The-PR-Agent/pr-agent) | 13.6k | PR Agent：开源 PR 审查工具，不是 Qodo 免费版。 | [SAFE](https://agentskillshub.top/skill/The-PR-Agent/pr-agent/?utm_source=github&utm_medium=awesome-list) |
| [mattzcarey/shippie](https://github.com/mattzcarey/shippie) | 2.5k | 可扩展的代码审查与 QA agent 🚢 | [SAFE](https://agentskillshub.top/skill/mattzcarey/shippie/?utm_source=github&utm_medium=awesome-list) |
| [sourcery-ai/sourcery](https://github.com/sourcery-ai/sourcery) | 1.9k | 即时 AI 代码审查 | [SAFE](https://agentskillshub.top/skill/sourcery-ai/sourcery/?utm_source=github&utm_medium=awesome-list) |
| [vercel-labs/openreview](https://github.com/vercel-labs/openreview) | 1.7k | 由 Vercel 驱动的开源、自托管 AI 代码审查机器人 | [SAFE](https://agentskillshub.top/skill/vercel-labs/openreview/?utm_source=github&utm_medium=awesome-list) |
| [villesau/ai-codereviewer](https://github.com/villesau/ai-codereviewer) | 1.0k | AI Code Reviewer：使用 OpenAI 的 GPT-4 API 为 pull request 提供代码审查反馈和建议，提升代码质量并节省开发时间。 | [SAFE](https://agentskillshub.top/skill/villesau/ai-codereviewer/?utm_source=github&utm_medium=awesome-list) |
| [Nikita-Filonov/ai-review](https://github.com/Nikita-Filonov/ai-review) | 598 | GitHub、GitLab、Bitbucket Cloud、Bitbucket Server、Azure DevOps、Gitea 的 AI 代码审查工具 | [SAFE](https://agentskillshub.top/skill/Nikita-Filonov/ai-review/?utm_source=github&utm_medium=awesome-list) |
| [Nayjest/Gito](https://github.com/Nayjest/Gito) | 453 | 使用大语言模型进行代码审查，检测高置信度、高影响的问题，如安全漏洞、错误和可维护性问题。 | [SAFE](https://agentskillshub.top/skill/Nayjest/Gito/?utm_source=github&utm_medium=awesome-list) |
| [cirolini/genai-code-review](https://github.com/cirolini/genai-code-review) | 372 | 使用 LLM 审查 Pull Request 差异并在 PR 中发布评论的 GitHub Action | [SAFE](https://agentskillshub.top/skill/cirolini/genai-code-review/?utm_source=github&utm_medium=awesome-list) |
| [sturdy-dev/codeball-action](https://github.com/sturdy-dev/codeball-action) | 327 | Codeball – 发现代码错误并加快审查流程的 AI 代码审查工具 | [SAFE](https://agentskillshub.top/skill/sturdy-dev/codeball-action/?utm_source=github&utm_medium=awesome-list) |
| [gitbito/bitoai](https://github.com/gitbito/bitoai) | 300 | 在 GitHub、GitLab、Bitbucket pull requests 或 IDE 中获取代码库感知的反馈。 | [SAFE](https://agentskillshub.top/skill/gitbito/bitoai/?utm_source=github&utm_medium=awesome-list) |
| [Cloudflare-Studio/ask-bonk](https://github.com/Cloudflare-Studio/ask-bonk) | 267 | Bonk 是基于 Cloudflare Workers 和 OpenCode 的代码与文档 agent，可代你构建、审查和分流。 | [SAFE](https://agentskillshub.top/skill/Cloudflare-Studio/ask-bonk/?utm_source=github&utm_medium=awesome-list) |
| [truongnh1992/gemini-ai-code-reviewer](https://github.com/truongnh1992/gemini-ai-code-reviewer) | 257 | 使用 Google Gemini AI 自动审查 Pull Request 的 GitHub Action | [SAFE](https://agentskillshub.top/skill/truongnh1992/gemini-ai-code-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [spherical-up/Easy-AI-CodeReview](https://github.com/spherical-up/Easy-AI-CodeReview) | 243 | Code Review 工具，提供智能比对、注释建议、变更摘要和代码质量提示，帮助理解提交内容并发现潜在问题。 | [SAFE](https://agentskillshub.top/skill/spherical-up/Easy-AI-CodeReview/?utm_source=github&utm_medium=awesome-list) |
| [flows-network/github-pr-summary](https://github.com/flows-network/github-pr-summary) | 229 | 使用 LLM 总结和审查 GitHub Pull Request | [SAFE](https://agentskillshub.top/skill/flows-network/github-pr-summary/?utm_source=github&utm_medium=awesome-list) |
| [presubmit/ai-reviewer](https://github.com/presubmit/ai-reviewer) | 187 | 面向 Pull Request 的上下文感知 AI 审查工具，提供摘要、逐行评论和标题生成等功能 | [SAFE](https://agentskillshub.top/skill/presubmit/ai-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [Juror-AI/juror](https://github.com/Juror-AI/juror) | 117 | Cheaper and better Greptile alternative runs on your own github actions. | [SAFE](https://agentskillshub.top/skill/Juror-AI/juror/?utm_source=github&utm_medium=awesome-list) |
| [octopusreview/octopus](https://github.com/octopusreview/octopus) | 114 | AI-powered PR review tool — multi-armed code analysis, no bug escapes 🐙 | [SAFE](https://agentskillshub.top/skill/octopusreview/octopus/?utm_source=github&utm_medium=awesome-list) |
| [mr-karan/hodor](https://github.com/mr-karan/hodor) | 112 | 用于 GitHub PR 和 GitLab MR 的智能代码审查工具，通过多步推理和自主工具编排发现需跨文件分析的错误。 | [SAFE](https://agentskillshub.top/skill/mr-karan/hodor/?utm_source=github&utm_medium=awesome-list) |
| [qiniu/reviewbot](https://github.com/qiniu/reviewbot) | 106 | 自托管的自动化代码质量分析与审查 | [SAFE](https://agentskillshub.top/skill/qiniu/reviewbot/?utm_source=github&utm_medium=awesome-list) |
| [nfacha/OpenAI-Gitlab-PR-Review](https://github.com/nfacha/OpenAI-Gitlab-PR-Review) | 94 | GitLab Webhook 原型，将代码提交给 OpenAI 审查 | [SAFE](https://agentskillshub.top/skill/nfacha/OpenAI-Gitlab-PR-Review/?utm_source=github&utm_medium=awesome-list) |
| [Usagi-org/ai-code-review-helper](https://github.com/Usagi-org/ai-code-review-helper) | 92 | 自动化代码审查工具，通过 GitHub、GitLab Webhook 使用 LLM 分析代码变更并反馈结果。 | [SAFE](https://agentskillshub.top/skill/Usagi-org/ai-code-review-helper/?utm_source=github&utm_medium=awesome-list) |
| [buxuku/ai-code-reviewer](https://github.com/buxuku/ai-code-reviewer) | 90 | 使用 OpenAI API 审查 GitLab Merge Request 的小工具 | [SAFE](https://agentskillshub.top/skill/buxuku/ai-code-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [feiskyer/ChatGPT-Reviewer](https://github.com/feiskyer/ChatGPT-Reviewer) | 90 | 使用 ChatGPT 自动审查拉取请求并分类处理问题。 | [SAFE](https://agentskillshub.top/skill/feiskyer/ChatGPT-Reviewer/?utm_source=github&utm_medium=awesome-list) |
| [zixingtangmouren/mr-agent](https://github.com/zixingtangmouren/mr-agent) | 89 | mr-agent：Node.js 服务，接收 Git merge request webhook 事件后自动触发 AI 代码审查，集成 GitHub/GitL… | [SAFE](https://agentskillshub.top/skill/zixingtangmouren/mr-agent/?utm_source=github&utm_medium=awesome-list) |
| [adshao/chatgpt-code-review-action](https://github.com/adshao/chatgpt-code-review-action) | 80 | 使用 OpenAI ChatGPT 进行代码审查的 GitHub Action | [SAFE](https://agentskillshub.top/skill/adshao/chatgpt-code-review-action/?utm_source=github&utm_medium=awesome-list) |
| [ccsert/opencode-review-gitea](https://github.com/ccsert/opencode-review-gitea) | 76 | 基于 OpenCode 的 Gitea/Forgejo PR 审查工具，在 Gitea Actions 运行，获取差异并发布结构化审查。支持 Docker 或… | [SAFE](https://agentskillshub.top/skill/ccsert/opencode-review-gitea/?utm_source=github&utm_medium=awesome-list) |
| [truskovskiyk/pr-reviewer](https://github.com/truskovskiyk/pr-reviewer) | 73 | 使用 LLM 协助进行 PR 审查 | [SAFE](https://agentskillshub.top/skill/truskovskiyk/pr-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [gitbito/CodeReviewAgent](https://github.com/gitbito/CodeReviewAgent) | 67 | 按需、结合上下文的 AI 代码审查，可在 Git 工作流或 IDE 中进行。 | [SAFE](https://agentskillshub.top/skill/gitbito/CodeReviewAgent/?utm_source=github&utm_medium=awesome-list) |
| [gitpack-ai/gitpack-ai](https://github.com/gitpack-ai/gitpack-ai) | 67 | 用 AI 自动审查 Pull Request | [SAFE](https://agentskillshub.top/skill/gitpack-ai/gitpack-ai/?utm_source=github&utm_medium=awesome-list) |
| [Integral-Healthcare/robin-ai-reviewer](https://github.com/Integral-Healthcare/robin-ai-reviewer) | 65 | Robin 是以 GitHub Action 形式提供的 AI pull request 审查工具。 | [SAFE](https://agentskillshub.top/skill/Integral-Healthcare/robin-ai-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [furudo-erika/codingfox](https://github.com/furudo-erika/codingfox) | 64 | 开源 AI 代码审查工具 | [SAFE](https://agentskillshub.top/skill/furudo-erika/codingfox/?utm_source=github&utm_medium=awesome-list) |
| [snarktank/ai-pr-review](https://github.com/snarktank/ai-pr-review) | 62 | 使用 Amp 或 Claude Code 提供 AI 代码审查的 GitHub Actions 工作流 | [SAFE](https://agentskillshub.top/skill/snarktank/ai-pr-review/?utm_source=github&utm_medium=awesome-list) |
| [Aestheticsuraj234/chai-ai-code-reviewer](https://github.com/Aestheticsuraj234/chai-ai-code-reviewer) | 59 | Chai AI Code Reviewer 自动分析 GitHub PR 变更，使用 Next.js、向量搜索、Vercel AI SDK 和 OpenRou… | [SAFE](https://agentskillshub.top/skill/Aestheticsuraj234/chai-ai-code-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [aryanbrite/openrabbit](https://github.com/aryanbrite/openrabbit) | 59 | 免费、完全在 GitHub Actions 中运行的 AI PR 审查工具，无需托管。 | [SAFE](https://agentskillshub.top/skill/aryanbrite/openrabbit/?utm_source=github&utm_medium=awesome-list) |
| [Factory-AI/droid-code-review](https://github.com/Factory-AI/droid-code-review) | 54 | Droid 代码审查 | [SAFE](https://agentskillshub.top/skill/Factory-AI/droid-code-review/?utm_source=github&utm_medium=awesome-list) |
| [ellenhp/auditlm](https://github.com/ellenhp/auditlm) | 52 | 可自行托管的 AI 代码审查工具，适用于 Forgejo | [SAFE](https://agentskillshub.top/skill/ellenhp/auditlm/?utm_source=github&utm_medium=awesome-list) |
| [electricsheephq/evaos-code-review-bot-neondiff](https://github.com/electricsheephq/evaos-code-review-bot-neondiff) | 51 | NeonDIFF 是面向团队的本地优先 AI PR 审查工具，可审查代码并补充问题信息，无需将每个 diff 交给托管审查 SaaS。 | [SAFE](https://agentskillshub.top/skill/electricsheephq/evaos-code-review-bot-neondiff/?utm_source=github&utm_medium=awesome-list) |
| [selimozten/elek](https://github.com/selimozten/elek) | 19 | 仅供审查的 GitHub PR AI 代码审查，可行内评论但不能批准、合并或关闭。 | [SAFE](https://agentskillshub.top/skill/selimozten/elek/?utm_source=github&utm_medium=awesome-list) |
| [diffpal/diffpal](https://github.com/diffpal/diffpal) | 9 | 开源、不绑定提供商的拉取请求 AI 审查工具。 | [SAFE](https://agentskillshub.top/skill/diffpal/diffpal/?utm_source=github&utm_medium=awesome-list) |

<a id="type-skill"></a>
## 🧩 Agent Skill

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-skill)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/hyhmrright/brooks-lint"><img src="assets/previews/hyhmrright__brooks-lint.gif" width="260" alt="hyhmrright/brooks-lint"></a><br><sub><a href="https://github.com/hyhmrright/brooks-lint">hyhmrright/brooks-lint</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/fivetaku/insane-review"><img src="assets/previews/fivetaku__insane-review.jpg" width="260" alt="fivetaku/insane-review"></a><br><sub><a href="https://github.com/fivetaku/insane-review">fivetaku/insane-review</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/nathankim0/clean-architecture-skills"><img src="assets/previews/nathankim0__clean-architecture-skills.jpg" width="260" alt="nathankim0/clean-architecture-skills"></a><br><sub><a href="https://github.com/nathankim0/clean-architecture-skills">nathankim0/clean-architecture-skills</a></sub></td>
</tr></table>

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | 34.6k | 使用 Claude Code 中的 Codex 审查代码或委派任务。 | [SAFE](https://agentskillshub.top/skill/openai/codex-plugin-cc/?utm_source=github&utm_medium=awesome-list) |
| [awesome-skills/code-review-skill](https://github.com/awesome-skills/code-review-skill) | 2.1k | Claude Code 的代码审查 skill，涵盖 React 19、Vue 3、Rust、TypeScript、TanStack Query v5 等。 | [SAFE](https://agentskillshub.top/skill/awesome-skills/code-review-skill/?utm_source=github&utm_medium=awesome-list) |
| [hyhmrright/brooks-lint](https://github.com/hyhmrright/brooks-lint) | 1.5k | 基于12本经典工程书籍的AI代码审查：引用书籍、严重性标签的代码腐化风险诊断，以及包括全量扫描自动修复在内的6种分析模式 | [SAFE](https://agentskillshub.top/skill/hyhmrright/brooks-lint/?utm_source=github&utm_medium=awesome-list) |
| [amElnagdy/guard-skills](https://github.com/amElnagdy/guard-skills) | 1.3k | 为 coding agents 提供守护 skill，检测代码、测试和文档中的 AI 生成问题 | [SAFE](https://agentskillshub.top/skill/amElnagdy/guard-skills/?utm_source=github&utm_medium=awesome-list) |
| [hamelsmu/claude-review-loop](https://github.com/hamelsmu/claude-review-loop) | 726 | Claude Code 插件：使用 Codex 的自动化代码审查循环 | [SAFE](https://agentskillshub.top/skill/hamelsmu/claude-review-loop/?utm_source=github&utm_medium=awesome-list) |
| [AsyncFuncAI/AsyncReview](https://github.com/AsyncFuncAI/AsyncReview) | 459 | 受 DevinReview 启发的开源智能体代码审查工具，使用 Recursive Language Models（RLM） | [SAFE](https://agentskillshub.top/skill/AsyncFuncAI/AsyncReview/?utm_source=github&utm_medium=awesome-list) |
| [greptileai/skills](https://github.com/greptileai/skills) | 427 | 用于检查 PR 审查评论、状态检查和描述完整性的 agent skill | [SAFE](https://agentskillshub.top/skill/greptileai/skills/?utm_source=github&utm_medium=awesome-list) |
| [vikingmute/review-forge](https://github.com/vikingmute/review-forge) | 223 | review-forge 是用于结构化、可审计代码审查流程的 Agent Skill | [SAFE](https://agentskillshub.top/skill/vikingmute/review-forge/?utm_source=github&utm_medium=awesome-list) |
| [Continuum-AI-Corp/Orca-Code-Review](https://github.com/Continuum-AI-Corp/Orca-Code-Review) | 180 | OrcaCode Review——开源代码审查工具。多模型审查、合并门禁，无标记。仅支付推理费用。 | [SAFE](https://agentskillshub.top/skill/Continuum-AI-Corp/Orca-Code-Review/?utm_source=github&utm_medium=awesome-list) |
| [fivetaku/insane-review](https://github.com/fivetaku/insane-review) | 125 | 在 Claude Code 中使用 GPT-5.5 Pro（仅网页端，无 API），用 repomix 打包代码并发送至 ChatGPT Pro 获取审查结果… | [SAFE](https://agentskillshub.top/skill/fivetaku/insane-review/?utm_source=github&utm_medium=awesome-list) |
| [win4r/agent-skills-code-review-router](https://github.com/win4r/agent-skills-code-review-router) | 124 | 根据技术栈、复杂度和变更特征，在 Gemini CLI 与 Codex CLI 间分配代码审查的 Agent Skill。 | [SAFE](https://agentskillshub.top/skill/win4r/agent-skills-code-review-router/?utm_source=github&utm_medium=awesome-list) |
| [nathankim0/clean-architecture-skills](https://github.com/nathankim0/clean-architecture-skills) | 108 | 用于依据 Clean Architecture 原则审查和设计代码的 Claude Code skill | [SAFE](https://agentskillshub.top/skill/nathankim0/clean-architecture-skills/?utm_source=github&utm_medium=awesome-list) |
| [w1ckedxt/cynical-sally](https://github.com/w1ckedxt/cynical-sally) | 101 | 面向 Claude Code、Cursor、Windsurf 和终端的代码审查：评分、证据支持的问题与可用修复方案。 | [SAFE](https://agentskillshub.top/skill/w1ckedxt/cynical-sally/?utm_source=github&utm_medium=awesome-list) |
| [rediga/Salesforce-Code-Review-Agent](https://github.com/rediga/Salesforce-Code-Review-Agent) | 100 | Salesforce DX 代码审查：Apex、LWC、Flows、安全性（CRUD/FLS）、governors 和 Bugbot。 | [SAFE](https://agentskillshub.top/skill/rediga/Salesforce-Code-Review-Agent/?utm_source=github&utm_medium=awesome-list) |
| [akkie76/code-review-skills](https://github.com/akkie76/code-review-skills) | 89 | 基于证据的 Codex 和 Claude Code 代码审查技能 | [SAFE](https://agentskillshub.top/skill/akkie76/code-review-skills/?utm_source=github&utm_medium=awesome-list) |
| [mberneti/clab](https://github.com/mberneti/clab) | 54 | 开源 Claude skill，用于自动审查 GitLab MR，支持可配置 lint 规则、语义分析和行内评论。 | [SAFE](https://agentskillshub.top/skill/mberneti/clab/?utm_source=github&utm_medium=awesome-list) |
| [aidankinzett/claude-git-pr-skill](https://github.com/aidankinzett/claude-git-pr-skill) | 52 | Claude Code 的 GitHub PR 审查 skill，支持待处理审查、代码建议和用户批准流程 | [SAFE](https://agentskillshub.top/skill/aidankinzett/claude-git-pr-skill/?utm_source=github&utm_medium=awesome-list) |
| [turingmindai/turingmind-code-review](https://github.com/turingmindai/turingmind-code-review) | 50 | Claude Code 代码审查 skill | [SAFE](https://agentskillshub.top/skill/turingmindai/turingmind-code-review/?utm_source=github&utm_medium=awesome-list) |
| [Aurite-ai/agent-verifier](https://github.com/Aurite-ai/agent-verifier) | 45 | Agent Verifier 是在发布前按组织政策、代码质量、安全要求和框架最佳实践验证代码的 coding agent skill，支持 Claude Co… | [SAFE](https://agentskillshub.top/skill/Aurite-ai/agent-verifier/?utm_source=github&utm_medium=awesome-list) |
| [mturac/simulacra](https://github.com/mturac/simulacra) | 43 | 幽灵角色在代码发布前审查代码，发现边界情况、竞态条件和业务逻辑错误。 | [SAFE](https://agentskillshub.top/skill/mturac/simulacra/?utm_source=github&utm_medium=awesome-list) |
| [drafthq/draft](https://github.com/drafthq/draft) | 40 | Claude Code、Cursor、GitHub Copilot、Gemini 的上下文驱动开发插件 | [SAFE](https://agentskillshub.top/skill/drafthq/draft/?utm_source=github&utm_medium=awesome-list) |
| [SomeStay07/code-review-agent](https://github.com/SomeStay07/code-review-agent) | 29 | Claude Code 代码审查 agent。单个 .md 文件，涵盖 14 类审查、4 个严重级别、自动修复和 OWASP 安全检查。零依赖。 | [SAFE](https://agentskillshub.top/skill/SomeStay07/code-review-agent/?utm_source=github&utm_medium=awesome-list) |
| [Teycir/Assumptions](https://github.com/Teycir/Assumptions) | 20 | 将代码差异转化为有证据支持的隐藏假设、失败模式和证伪测试清单的 skill | [SAFE](https://agentskillshub.top/skill/Teycir/Assumptions/?utm_source=github&utm_medium=awesome-list) |
| [Lykhoyda/ask-llm](https://github.com/Lykhoyda/ask-llm) | 18 | 用于 AI 间协作的 MCP server，连接 Claude、Gemini、Codex 和其他 LLM，进行代码审查、征求第二意见和讨论计划 | [SAFE](https://agentskillshub.top/skill/Lykhoyda/ask-llm/?utm_source=github&utm_medium=awesome-list) |
| [whitequeen306/code-cortex-loop](https://github.com/whitequeen306/code-cortex-loop) | 15 | 一条命令完成 AI 代码审查、安全、测试、性能、简化与清理，含健康评分和 CI 门禁，支持 Cursor、Claude Code、Qoder、Trae】【。 | [SAFE](https://agentskillshub.top/skill/whitequeen306/code-cortex-loop/?utm_source=github&utm_medium=awesome-list) |
| [lohani-mohit/shipcheck](https://github.com/lohani-mohit/shipcheck) | 12 | Claude Code 的 Senior-QA 审查 skill：并行运行回归检查和变更审查，基于文件:行号证据给出只读的 SIGN OFF/DO NOT S… | [SAFE](https://agentskillshub.top/skill/lohani-mohit/shipcheck/?utm_source=github&utm_medium=awesome-list) |
| [VoDaiLocz/Design-Patterns](https://github.com/VoDaiLocz/Design-Patterns) | 11 | 全面设计模式 skill：检测反模式，诊断架构债务，生成生产级重构代码。GoF、SOLID、DDD、CQRS、Microservices。 | [SAFE](https://agentskillshub.top/skill/VoDaiLocz/Design-Patterns/?utm_source=github&utm_medium=awesome-list) |
| [wxmb01/review-skill](https://github.com/wxmb01/review-skill) | 11 | 基于证据的审查 skill，面向 diff、项目和制品，涵盖代码、就绪度、架构、需求和风险。 | [SAFE](https://agentskillshub.top/skill/wxmb01/review-skill/?utm_source=github&utm_medium=awesome-list) |
| [barlevysh/code-smells-skill](https://github.com/barlevysh/code-smells-skill) | 7 | 🦨 120+种代码异味及前后示例，覆盖C/C++/C#/Java/Python/Go/Rust/JS/TS/SQL，助力开发与代码审查的AI agent sk… | [SAFE](https://agentskillshub.top/skill/barlevysh/code-smells-skill/?utm_source=github&utm_medium=awesome-list) |
| [victorserpa/objection](https://github.com/victorserpa/objection) | 7 | 反对！供 AI 编程 agent 使用的 skill 和插件（Claude Code、Codex、Cursor、Gemini）：控方、辩方和法官审查 PR，审… | [SAFE](https://agentskillshub.top/skill/victorserpa/objection/?utm_source=github&utm_medium=awesome-list) |

<a id="type-cli"></a>
## ⌨️ 本地与命令行

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-cli)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/alibaba/open-code-review"><img src="assets/previews/alibaba__open-code-review.jpg" width="260" alt="alibaba/open-code-review"></a><br><sub><a href="https://github.com/alibaba/open-code-review">alibaba/open-code-review</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/tirth8205/code-review-graph"><img src="assets/previews/tirth8205__code-review-graph.jpg" width="260" alt="tirth8205/code-review-graph"></a><br><sub><a href="https://github.com/tirth8205/code-review-graph">tirth8205/code-review-graph</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/kenn-io/roborev"><img src="assets/previews/kenn-io__roborev.jpg" width="260" alt="kenn-io/roborev"></a><br><sub><a href="https://github.com/kenn-io/roborev">kenn-io/roborev</a></sub></td>
</tr></table>

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [alibaba/open-code-review](https://github.com/alibaba/open-code-review) | 48.3k | 混合架构代码审查工具：确定性流水线+LLM Agent，支持行级评论、多语言规则集及OpenAI和Anthropic兼容接口。 | [SAFE](https://agentskillshub.top/skill/alibaba/open-code-review/?utm_source=github&utm_medium=awesome-list) |
| [tirth8205/code-review-graph](https://github.com/tirth8205/code-review-graph) | 32.4k | 本地优先的代码智能图，支持 MCP 和 CLI，持久化映射代码库，让 AI 编程工具读取相关代码。 | [SAFE](https://agentskillshub.top/skill/tirth8205/code-review-graph/?utm_source=github&utm_medium=awesome-list) |
| [kenn-io/roborev](https://github.com/kenn-io/roborev) | 1.8k | 面向 agent 的持续后台代码审查数据库，追踪每行生成代码的责任归属。 | [SAFE](https://agentskillshub.top/skill/kenn-io/roborev/?utm_source=github&utm_medium=awesome-list) |
| [HexmosTech/git-lrc](https://github.com/HexmosTech/git-lrc) | 1.5k | 微型 AI 代码审查，随 Git 提交运行 | [SAFE](https://agentskillshub.top/skill/HexmosTech/git-lrc/?utm_source=github&utm_medium=awesome-list) |
| [sashiko-dev/sashiko](https://github.com/sashiko-dev/sashiko) | 1.4k | 基于 agent 的 Linux Kernel 代码变更审查 | [SAFE](https://agentskillshub.top/skill/sashiko-dev/sashiko/?utm_source=github&utm_medium=awesome-list) |
| [Gentleman-Programming/gentleman-guardian-angel](https://github.com/Gentleman-Programming/gentleman-guardian-angel) | 1.2k | Gentleman Guardian Angel (gga)：支持 Claude、Gemini、Codex 和 Ollama 的 AI 代码审查工具，用于执行… | [SAFE](https://agentskillshub.top/skill/Gentleman-Programming/gentleman-guardian-angel/?utm_source=github&utm_medium=awesome-list) |
| [persiyanov/herdr-reviewr](https://github.com/persiyanov/herdr-reviewr) | 946 | 在终端窗格审查 coding agent 的差异，并将逐行评论发送回 Claude Code、Codex、OpenCode 或 Pi。herdr 插件。 | [SAFE](https://agentskillshub.top/skill/persiyanov/herdr-reviewr/?utm_source=github&utm_medium=awesome-list) |
| [nilbuild/diffity](https://github.com/nilbuild/diffity) | 894 | 用于审查你或 agent 编写代码的 Mac 应用，支持 Claude 参与。 | [SAFE](https://agentskillshub.top/skill/nilbuild/diffity/?utm_source=github&utm_medium=awesome-list) |
| [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | 691 | 基于 TypeSafe Jev 构建的分阶段代码审查工作流和本地仪表板。 | [SAFE](https://agentskillshub.top/skill/devagrawal09/jev-review/?utm_source=github&utm_medium=awesome-list) |
| [imbue-ai/vet](https://github.com/imbue-ai/vet) | 511 | 发现值得关注的问题。 | [SAFE](https://agentskillshub.top/skill/imbue-ai/vet/?utm_source=github&utm_medium=awesome-list) |
| [taovc/pr-cockpit](https://github.com/taovc/pr-cockpit) | 485 | 本地 AI PR 工作台：在隔离的 Git worktree 中进行 Claude/Codex 审查，GitHub 评论需人工审核 | [SAFE](https://agentskillshub.top/skill/taovc/pr-cockpit/?utm_source=github&utm_medium=awesome-list) |
| [getsentry/warden](https://github.com/getsentry/warden) | 418 | 你的代码由新的管理者接管。审查代码的 agent。 | [SAFE](https://agentskillshub.top/skill/getsentry/warden/?utm_source=github&utm_medium=awesome-list) |
| [lakeday-org/perch](https://github.com/lakeday-org/perch) | 352 | 使用 Jev 进行语义代码检查 | [SAFE](https://agentskillshub.top/skill/lakeday-org/perch/?utm_source=github&utm_medium=awesome-list) |
| [TheMorpheus407/RepoLens](https://github.com/TheMorpheus407/RepoLens) | 302 | 多视角代码审计工具，支持代码审查、安全测试和基础设施审计 | [SAFE](https://agentskillshub.top/skill/TheMorpheus407/RepoLens/?utm_source=github&utm_medium=awesome-list) |
| [ReviewStage/stage-cli](https://github.com/ReviewStage/stage-cli) | 274 | 用于按小章节查看本地代码变更，适用于任何 AI agent。 | [SAFE](https://agentskillshub.top/skill/ReviewStage/stage-cli/?utm_source=github&utm_medium=awesome-list) |
| [NiazMorshed2007/jev-review](https://github.com/NiazMorshed2007/jev-review) | 246 | 基于 Jev 的本地优先 MCP 插件，用于 AI 编程 agent 持续审查软件质量。 | [SAFE](https://agentskillshub.top/skill/NiazMorshed2007/jev-review/?utm_source=github&utm_medium=awesome-list) |
| [openqa-cn/codexqa](https://github.com/openqa-cn/codexqa) | 235 | 11个Agent Skills：Cursor、Claude Code、Codex、OpenClaw；变更分析、AI审查、缺陷扫描、用例生成、浏览回放、RCA。 | [SAFE](https://agentskillshub.top/skill/openqa-cn/codexqa/?utm_source=github&utm_medium=awesome-list) |
| [wong2/diffx](https://github.com/wong2/diffx) | 217 | 用于编码 agent 工作流的本地代码审查工具 | [SAFE](https://agentskillshub.top/skill/wong2/diffx/?utm_source=github&utm_medium=awesome-list) |
| [Ataraxy-Labs/inspect](https://github.com/Ataraxy-Labs/inspect) | 208 | 实体级代码审查。通过跨文件依赖图和理解语义的 LLM，按结构风险分流 PR。 | [SAFE](https://agentskillshub.top/skill/Ataraxy-Labs/inspect/?utm_source=github&utm_medium=awesome-list) |
| [tshemsedinov/reslop](https://github.com/tshemsedinov/reslop) | 188 | 审查 AI 生成的代码并规划修改 | [SAFE](https://agentskillshub.top/skill/tshemsedinov/reslop/?utm_source=github&utm_medium=awesome-list) |
| [puemos/lareview](https://github.com/puemos/lareview) | 182 | 代码审查工作台。 | [SAFE](https://agentskillshub.top/skill/puemos/lareview/?utm_source=github&utm_medium=awesome-list) |
| [egma-ai/jev-code-reviewer](https://github.com/egma-ai/jev-code-reviewer) | 148 | 审查行为，而不只是差异。Jev 优先利用人的注意力；OpenAI 解释变更。支持本地 CLI、agent skill 和 GitHub 扩展。 | [SAFE](https://agentskillshub.top/skill/egma-ai/jev-code-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [Gil2015/code-gate](https://github.com/Gil2015/code-gate) | 127 | 智能 Git 提交代码审查工具，支持 Ollama、DeepSeek、OpenAI、Anthropic 模型及 CLI 界面。 | [SAFE](https://agentskillshub.top/skill/Gil2015/code-gate/?utm_source=github&utm_medium=awesome-list) |
| [vuphongle/oss-pr-reviewer](https://github.com/vuphongle/oss-pr-reviewer) | 114 | AI 驱动的 CLI，用于审查 GitHub pull request，检测潜在 bug、安全风险、回归和缺失测试，并生成结构化 Markdown 报告。 | [SAFE](https://agentskillshub.top/skill/vuphongle/oss-pr-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [nicobailon/pi-review-loop](https://github.com/nicobailon/pi-review-loop) | 113 | 面向 Pi coding agent 的自动化代码审查循环扩展 | [SAFE](https://agentskillshub.top/skill/nicobailon/pi-review-loop/?utm_source=github&utm_medium=awesome-list) |
| [Ali-Marandi/AI-Code-Reviewer](https://github.com/Ali-Marandi/AI-Code-Reviewer) | 109 | AI 驱动的代码审查与质量分析工具 | [SAFE](https://agentskillshub.top/skill/Ali-Marandi/AI-Code-Reviewer/?utm_source=github&utm_medium=awesome-list) |
| [reviu-dev/reviu](https://github.com/reviu-dev/reviu) | 97 | 用于审查 agent 编写代码的应用。基于 Rust/GPUI 的原生桌面应用，支持真实 Git 工作流。 | [SAFE](https://agentskillshub.top/skill/reviu-dev/reviu/?utm_source=github&utm_medium=awesome-list) |
| [hyperb1iss/lucidity-mcp](https://github.com/hyperb1iss/lucidity-mcp) | 90 | 基于 MCP 的代码质量分析，帮助 AI 助手通过结构化提示检查 Git 变更中的复杂度和安全问题等。 | [SAFE](https://agentskillshub.top/skill/hyperb1iss/lucidity-mcp/?utm_source=github&utm_medium=awesome-list) |
| [snakyvine/codex-maintainer](https://github.com/snakyvine/codex-maintainer) | 85 | 基于证据的问题分流、拉取请求审查和发布说明，面向 GitHub 维护者。CLI + GitHub Action。 | [SAFE](https://agentskillshub.top/skill/snakyvine/codex-maintainer/?utm_source=github&utm_medium=awesome-list) |
| [mikker/semantic-review](https://github.com/mikker/semantic-review) | 82 | coding agent 的语义差异审查 | [SAFE](https://agentskillshub.top/skill/mikker/semantic-review/?utm_source=github&utm_medium=awesome-list) |
| [katarmal-ram/codemoot](https://github.com/katarmal-ram/codemoot) | 78 | 多模型协作开发平台——Claude 与 GPT 共同讨论、审查和构建 | [SAFE](https://agentskillshub.top/skill/katarmal-ram/codemoot/?utm_source=github&utm_medium=awesome-list) |
| [n24q02m/crg](https://github.com/n24q02m/crg) | 76 | 面向节省 token 的代码审查知识图谱，支持整个代码库的语义搜索和调用图解析。 | [SAFE](https://agentskillshub.top/skill/n24q02m/crg/?utm_source=github&utm_medium=awesome-list) |
| [in-the-loop-labs/pair-review](https://github.com/in-the-loop-labs/pair-review) | 70 | AI辅助代码审查，人工参与 | [SAFE](https://agentskillshub.top/skill/in-the-loop-labs/pair-review/?utm_source=github&utm_medium=awesome-list) |
| [simion/reviewd](https://github.com/simion/reviewd) | 70 | 本地 AI pull request 审查工具，直接在终端审查 GitHub 和 BitBucket PR，支持 Claude Code、Gemini 和 C… | [SAFE](https://agentskillshub.top/skill/simion/reviewd/?utm_source=github&utm_medium=awesome-list) |
| [kunkka19xx/lgtm](https://github.com/kunkka19xx/lgtm) | 64 | 说 LGTM 前先阅读 agent 写的内容。用 Zig 编写的快速 TUI，支持 vim 操作审查代码。 | [CAUTION](https://agentskillshub.top/skill/kunkka19xx/lgtm/?utm_source=github&utm_medium=awesome-list) |
| [bobmatnyc/ai-code-review](https://github.com/bobmatnyc/ai-code-review) | 56 | 支持 Gemini、Claude、OpenAI 的 AI 代码审查 CLI，含语义分块、7 种审查类型、多语言、交互式修复和开发者 skill 评估。 | [SAFE](https://agentskillshub.top/skill/bobmatnyc/ai-code-review/?utm_source=github&utm_medium=awesome-list) |
| [kodehash/katichai](https://github.com/kodehash/katichai) | 52 | 具备上下文感知和 AI 辅助的代码审查 CLI 工具，避免生成多余代码、检测重复逻辑、落实架构模式并保障工程质量 | [CAUTION](https://agentskillshub.top/skill/kodehash/katichai/?utm_source=github&utm_medium=awesome-list) |
| [get-tmonier/argot](https://github.com/get-tmonier/argot) | 51 | 基于代码仓库历史构建的统计代码分析器。 | [SAFE](https://agentskillshub.top/skill/get-tmonier/argot/?utm_source=github&utm_medium=awesome-list) |
| [giorgiop/AICodePal](https://github.com/giorgiop/AICodePal) | 51 | AI 管理的开源代码审查与辅助工具，帮助开发者编写更高效、更安全的代码。 | [SAFE](https://agentskillshub.top/skill/giorgiop/AICodePal/?utm_source=github&utm_medium=awesome-list) |
| [ScanLineDev/scanline](https://github.com/ScanLineDev/scanline) | 50 | 代码审查：在 CLI 中运行 Scanline，查找竞态条件、逻辑错误、安全风险和优化点 | [SAFE](https://agentskillshub.top/skill/ScanLineDev/scanline/?utm_source=github&utm_medium=awesome-list) |
| [dbachelder/slop-review](https://github.com/dbachelder/slop-review) | 50 | Claude Code、Codex CLI、pi 的 /slop-review 窗口，支持 Monaco 行内评论，agent 可读取。 | [SAFE](https://agentskillshub.top/skill/dbachelder/slop-review/?utm_source=github&utm_medium=awesome-list) |
| [killop/code-review-skill](https://github.com/killop/code-review-skill) | 50 | Code Review Skill：用于通用代码工程的定期代码质量审查。 | [SAFE](https://agentskillshub.top/skill/killop/code-review-skill/?utm_source=github&utm_medium=awesome-list) |
| [xieziyu/duetlens](https://github.com/xieziyu/duetlens) | 50 | 在 macOS 上与 Codex agent 协作审查 PR 或本地分支，可询问任意代码行而非只读结果。 | [SAFE](https://agentskillshub.top/skill/xieziyu/duetlens/?utm_source=github&utm_medium=awesome-list) |
| [DiffoHQ/diffo](https://github.com/DiffoHQ/diffo) | 42 | 面向 AI 时代的本地实时代码审查，阅读 agent 编写的内容并直接反馈 | [SAFE](https://agentskillshub.top/skill/DiffoHQ/diffo/?utm_source=github&utm_medium=awesome-list) |
| [raye-deng/open-code-review](https://github.com/raye-deng/open-code-review) | 40 | AI生成代码质量门禁，检测虚构包、幽灵依赖、过时API等，提供MCP Server、CLI和CI/CD Action。 | [SAFE](https://agentskillshub.top/skill/raye-deng/open-code-review/?utm_source=github&utm_medium=awesome-list) |
| [WillNigri/Agentic-Tool-Optimization](https://github.com/WillNigri/Agentic-Tool-Optimization) | 34 | 本地优先的多运行时 AI 驾驶舱（CLI + 桌面端 + MCP）。作战室、审查回执、开放的多模型编码基准。MIT。 | [SAFE](https://agentskillshub.top/skill/WillNigri/Agentic-Tool-Optimization/?utm_source=github&utm_medium=awesome-list) |
| [amix/dunk](https://github.com/amix/dunk) | 31 | 在终端 UI 中审查 diff、添加行内评论，并让 coding agents 修复问题 | [SAFE](https://agentskillshub.top/skill/amix/dunk/?utm_source=github&utm_medium=awesome-list) |
| [logi-cmd/agent-guardrails](https://github.com/logi-cmd/agent-guardrails) | 27 | 在合并前检查 AI 生成的代码变更：范围、验证、风险、审查证据及可选的 Verity 凭证。 | [SAFE](https://agentskillshub.top/skill/logi-cmd/agent-guardrails/?utm_source=github&utm_medium=awesome-list) |
| [ispuppy/ai-pre-commit-reviewer](https://github.com/ispuppy/ai-pre-commit-reviewer) | 24 | AI 驱动的 Git pre-commit hook，按自定义规则自动进行代码审查。 | [SAFE](https://agentskillshub.top/skill/ispuppy/ai-pre-commit-reviewer/?utm_source=github&utm_medium=awesome-list) |
| [ahoybuoy/buoy](https://github.com/ahoybuoy/buoy) | 20 | 代码设计系统守护工具，检测 React/Vue/Tailwind 偏离并自动审查 PR。开源项目免费。 | [SAFE](https://agentskillshub.top/skill/ahoybuoy/buoy/?utm_source=github&utm_medium=awesome-list) |
| [itsmesherry/claude-audit](https://github.com/itsmesherry/claude-audit) | 15 | AI 代码库审计工具。使用 Claude。 | [CAUTION](https://agentskillshub.top/skill/itsmesherry/claude-audit/?utm_source=github&utm_medium=awesome-list) |
| [umitkavala/revet](https://github.com/umitkavala/revet) | 12 | 代码审查 agent | [SAFE](https://agentskillshub.top/skill/umitkavala/revet/?utm_source=github&utm_medium=awesome-list) |
| [CommitBrief/commitbrief](https://github.com/CommitBrief/commitbrief) | 11 | 本地 LLM 代码审查 CLI：在终端审查已暂存/未暂存更改、任意 git diff 范围或 GitHub PR | [SAFE](https://agentskillshub.top/skill/CommitBrief/commitbrief/?utm_source=github&utm_medium=awesome-list) |
| [DanielT777/sieve](https://github.com/DanielT777/sieve) | 11 | 在进入代码库前筛掉 AI 垃圾代码，为 AI 生成代码提供结构化人工审查流程。 | [SAFE](https://agentskillshub.top/skill/DanielT777/sieve/?utm_source=github&utm_medium=awesome-list) |
| [alxnddr/reviewer](https://github.com/alxnddr/reviewer) | 11 | 用于 agent 生成代码审查的界面 | [SAFE](https://agentskillshub.top/skill/alxnddr/reviewer/?utm_source=github&utm_medium=awesome-list) |
| [matheusfillipe/diffler](https://github.com/matheusfillipe/diffler) | 11 | 面向 AI 编程 agent 的终端代码审查，支持实时 diff、评论回复、PR review 和内置 MCP。 | [SAFE](https://agentskillshub.top/skill/matheusfillipe/diffler/?utm_source=github&utm_medium=awesome-list) |
| [narghev/askdiff](https://github.com/narghev/askdiff) | 11 | 在 Git diff 查看器中询问 AI 关于其代码改动的问题。 | [SAFE](https://agentskillshub.top/skill/narghev/askdiff/?utm_source=github&utm_medium=awesome-list) |
| [zanetworker/highstakes](https://github.com/zanetworker/highstakes) | 11 | AI 写代码快于你的审查速度。HighStakes 读取代码库，按影响范围为每个文件评分，指出需人工审查和可交给 AI 处理的部分。 | [SAFE](https://agentskillshub.top/skill/zanetworker/highstakes/?utm_source=github&utm_medium=awesome-list) |
| [mantacron/manta](https://github.com/mantacron/manta) | 10 | 20 个 AI agent 审查 Git：提交拦截密钥、注入缺陷和不安全迁移，推送检查性能与覆盖率；编码前设 GO/NO-GO 闸门，生成代码、Wiki、代码… | [SAFE](https://agentskillshub.top/skill/mantacron/manta/?utm_source=github&utm_medium=awesome-list) |
| [jsliapark/preflight](https://github.com/jsliapark/preflight) | 8 | Preflight——提交 PR 前的 AI 代码审查，多 agent 系统为 git diff 提供资深级反馈。 | [SAFE](https://agentskillshub.top/skill/jsliapark/preflight/?utm_source=github&utm_medium=awesome-list) |
| [verabravo/diffback](https://github.com/verabravo/diffback) | 8 | 用于审查 AI 生成的代码更改并生成结构化反馈提示的本地 Web 界面 | [SAFE](https://agentskillshub.top/skill/verabravo/diffback/?utm_source=github&utm_medium=awesome-list) |
| [voodootikigod/adversarial-review](https://github.com/voodootikigod/adversarial-review) | 8 | 对 git diff 或分支进行审慎的发布与否对抗式代码审查，支持任意 LLM（API 或本地 CLI agent） | [SAFE](https://agentskillshub.top/skill/voodootikigod/adversarial-review/?utm_source=github&utm_medium=awesome-list) |
| [witold-andelie/revio](https://github.com/witold-andelie/revio) | 8 | 代码审查CLI：LangGraph编排13分析器，覆盖23种语言含工业PLC；Grounding validator防虚构路径；RAG；dedup--fix可… | [SAFE](https://agentskillshub.top/skill/witold-andelie/revio/?utm_source=github&utm_medium=awesome-list) |
| [agent-0x/claude-codex-review](https://github.com/agent-0x/claude-codex-review) | 7 | 双 AI 自动代码审查：Codex 发现问题，Claude 修复，循环直到通过。 | [SAFE](https://agentskillshub.top/skill/agent-0x/claude-codex-review/?utm_source=github&utm_medium=awesome-list) |
| [Open-Document-Alliance/Agent-Review-CLI](https://github.com/Open-Document-Alliance/Agent-Review-CLI) | 6 | 用于编排并行 AI 编程 agent，审查、修复并交付代码变更的 CLI | [SAFE](https://agentskillshub.top/skill/Open-Document-Alliance/Agent-Review-CLI/?utm_source=github&utm_medium=awesome-list) |

<a id="type-security"></a>
## 🛡 安全审查

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-security)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/agentgg-dev/agentgg"><img src="assets/previews/agentgg-dev__agentgg.jpg" width="260" alt="agentgg-dev/agentgg"></a><br><sub><a href="https://github.com/agentgg-dev/agentgg">agentgg-dev/agentgg</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/tanviet12/vbsec"><img src="assets/previews/tanviet12__vbsec.jpg" width="260" alt="tanviet12/vbsec"></a><br><sub><a href="https://github.com/tanviet12/vbsec">tanviet12/vbsec</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/Addepar/RedFlag"><img src="assets/previews/Addepar__RedFlag.gif" width="260" alt="Addepar/RedFlag"></a><br><sub><a href="https://github.com/Addepar/RedFlag">Addepar/RedFlag</a></sub></td>
</tr></table>

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [lintsinghua/DeepAudit](https://github.com/lintsinghua/DeepAudit) | 7.2k | DeepAudit：开源代码漏洞挖掘多智能体系统，支持自主审计、沙箱 PoC 验证、Ollama 私有部署和报告生成。 | [SAFE](https://agentskillshub.top/skill/lintsinghua/DeepAudit/?utm_source=github&utm_medium=awesome-list) |
| [anthropics/claude-code-security-review](https://github.com/anthropics/claude-code-security-review) | 6.6k | 使用 Claude 分析代码变更安全漏洞的 AI 安全审查 GitHub Action。 | [SAFE](https://agentskillshub.top/skill/anthropics/claude-code-security-review/?utm_source=github&utm_medium=awesome-list) |
| [google/mantis](https://github.com/google/mantis) | 2.5k | 面向 AI 编程代理的模块化、与技术栈无关的工具包，可自主发现、复现并修复漏洞。 | [SAFE](https://agentskillshub.top/skill/google/mantis/?utm_source=github&utm_medium=awesome-list) |
| [arm/metis](https://github.com/arm/metis) | 888 | Metis 是一个开源的 AI 驱动安全代码审查工具 | [SAFE](https://agentskillshub.top/skill/arm/metis/?utm_source=github&utm_medium=awesome-list) |
| [agentgg-dev/agentgg](https://github.com/agentgg-dev/agentgg) | 442 | 开源智能体 SAST，支持分析代码仓库或 PR diff，并可自选模型。 | [SAFE](https://agentskillshub.top/skill/agentgg-dev/agentgg/?utm_source=github&utm_medium=awesome-list) |
| [tanviet12/vbsec](https://github.com/tanviet12/vbsec) | 309 | 适用于 Claude Code、Codex 和 Antigravity 的安全扫描 skill，发现 AI 编写代码中 21 种常见漏洞并说明修复方法。 | [SAFE](https://agentskillshub.top/skill/tanviet12/vbsec/?utm_source=github&utm_medium=awesome-list) |
| [AgriciDaniel/claude-cybersecurity](https://github.com/AgriciDaniel/claude-cybersecurity) | 255 | 面向 Claude Code 的 AI 网络安全代码审查 skill，含 8 个专用 agent，支持 OWASP 2025、CWE Top 25、MITRE… | [SAFE](https://agentskillshub.top/skill/AgriciDaniel/claude-cybersecurity/?utm_source=github&utm_medium=awesome-list) |
| [Addepar/RedFlag](https://github.com/Addepar/RedFlag) | 163 | RedFlag 使用 AI 识别高风险代码变更，可在批处理模式或 CI 流程中标记 PR 并添加审阅者。 | [SAFE](https://agentskillshub.top/skill/Addepar/RedFlag/?utm_source=github&utm_medium=awesome-list) |
| [EastSword/skill-dfyx_code_security_review](https://github.com/EastSword/skill-dfyx_code_security_review) | 144 | 东方隐侠团队的代码审计 skill | [SAFE](https://agentskillshub.top/skill/EastSword/skill-dfyx_code_security_review/?utm_source=github&utm_medium=awesome-list) |
| [DeepCodeAI/vscode-extension](https://github.com/DeepCodeAI/vscode-extension) | 129 | Visual Studio Code 的 DeepCode 扩展 | [SAFE](https://agentskillshub.top/skill/DeepCodeAI/vscode-extension/?utm_source=github&utm_medium=awesome-list) |
| [momenbasel/vulnhawk](https://github.com/momenbasel/vulnhawk) | 90 | AI 驱动的 SAST 扫描器，发现 Semgrep/CodeQL 漏掉的认证绕过、IDOR 和逻辑漏洞。免费 GitHub Action，支持 Python… | [SAFE](https://agentskillshub.top/skill/momenbasel/vulnhawk/?utm_source=github&utm_medium=awesome-list) |
| [shivamsaraswat/SeCoRA](https://github.com/shivamsaraswat/SeCoRA) | 58 | 安全代码审查 AI Agent（SeCoRA）- AI SAST | [SAFE](https://agentskillshub.top/skill/shivamsaraswat/SeCoRA/?utm_source=github&utm_medium=awesome-list) |
| [fabriziosalmi/brutal-coding-tool](https://github.com/fabriziosalmi/brutal-coding-tool) | 27 | 审查你的 vibecode，让它更稳固。 | [SAFE](https://agentskillshub.top/skill/fabriziosalmi/brutal-coding-tool/?utm_source=github&utm_medium=awesome-list) |
| [oscaar90/OpsGuard-AI](https://github.com/oscaar90/OpsGuard-AI) | 17 | GitHub Actions 的上下文感知安全门，使用 Hybrid Analysis 验证部署。 | [SAFE](https://agentskillshub.top/skill/oscaar90/OpsGuard-AI/?utm_source=github&utm_medium=awesome-list) |
| [win4r/jev-security-scan](https://github.com/win4r/jev-security-scan) | 11 | 使用 TypeSafe Jev 审查 Agent Skill 与 MCP 代码，提供静态证据并说明覆盖缺口 | [SAFE](https://agentskillshub.top/skill/win4r/jev-security-scan/?utm_source=github&utm_medium=awesome-list) |
| [vikram-codes-hub/codesense-ai](https://github.com/vikram-codes-hub/codesense-ai) | 7 | 代码审查平台，自动分析 GitHub PR 的安全漏洞、错误和复杂度问题，并发布行内评论。 | [CAUTION](https://agentskillshub.top/skill/vikram-codes-hub/codesense-ai/?utm_source=github&utm_medium=awesome-list) |

<a id="type-multi"></a>
## 👥 多 Agent 互审

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-multi)

<table><tr>
<td align="center" valign="top"><a href="https://github.com/codexstar69/bug-hunter"><img src="assets/previews/codexstar69__bug-hunter.jpg" width="260" alt="codexstar69/bug-hunter"></a><br><sub><a href="https://github.com/codexstar69/bug-hunter">codexstar69/bug-hunter</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/chorus-codes/chorus"><img src="assets/previews/chorus-codes__chorus.gif" width="260" alt="chorus-codes/chorus"></a><br><sub><a href="https://github.com/chorus-codes/chorus">chorus-codes/chorus</a></sub></td>
<td align="center" valign="top"><a href="https://github.com/spencermarx/open-code-review"><img src="assets/previews/spencermarx__open-code-review.jpg" width="260" alt="spencermarx/open-code-review"></a><br><sub><a href="https://github.com/spencermarx/open-code-review">spencermarx/open-code-review</a></sub></td>
</tr></table>

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [Agent-Field/pr-af](https://github.com/Agent-Field/pr-af) | 657 | #1 open-source code reviewer on Code-Review-Bench | [SAFE](https://agentskillshub.top/skill/Agent-Field/pr-af/?utm_source=github&utm_medium=awesome-list) |
| [codexstar69/bug-hunter](https://github.com/codexstar69/bug-hunter) | 537 | 对抗式 AI 漏洞猎手，支持 Claude Code、Cursor、Codex CLI 等，自动发现并在安全分支修复安全漏洞、逻辑错误和运行时错误。 | [SAFE](https://agentskillshub.top/skill/codexstar69/bug-hunter/?utm_source=github&utm_medium=awesome-list) |
| [chorus-codes/chorus](https://github.com/chorus-codes/chorus) | 534 | 面向代码决策的多 LLM 同行评审。使用自己的 CLI，Chorus 发布前召集 2-4 个 LLM 评审。 | [SAFE](https://agentskillshub.top/skill/chorus-codes/chorus/?utm_source=github&utm_medium=awesome-list) |
| [spencermarx/open-code-review](https://github.com/spencermarx/open-code-review) | 380 | AI 驱动的多智能体代码审查，模拟可定制的工程师团队进行内置讨论式审查。 | [SAFE](https://agentskillshub.top/skill/spencermarx/open-code-review/?utm_source=github&utm_medium=awesome-list) |
| [adamjgmiller/adamsreview](https://github.com/adamjgmiller/adamsreview) | 244 | Claude Code 的多视角代码审查流程：深度审查、自动修复循环、交互式演练、外部发现注入。 | [SAFE](https://agentskillshub.top/skill/adamjgmiller/adamsreview/?utm_source=github&utm_medium=awesome-list) |
| [99xAgency/GodModeSkill](https://github.com/99xAgency/GodModeSkill) | 240 | Claude Code 多 LLM 交叉审查工作流。/work 编排规划、实现和修复，每个关卡由 3 个不同模型系列投票。 | [SAFE](https://agentskillshub.top/skill/99xAgency/GodModeSkill/?utm_source=github&utm_medium=awesome-list) |
| [syabro/rejudge](https://github.com/syabro/rejudge) | 167 | 面向 AI 编程 agent 的独立多模型评测 | [SAFE](https://agentskillshub.top/skill/syabro/rejudge/?utm_source=github&utm_medium=awesome-list) |
| [amElnagdy/review-skills](https://github.com/amElnagdy/review-skills) | 160 | 双模型辩论审查 PR 和 MR，另有 babysitter 管理审查轮次。适用于任何 coding agent 的 skill。 | [SAFE](https://agentskillshub.top/skill/amElnagdy/review-skills/?utm_source=github&utm_medium=awesome-list) |
| [VirtusLab/tulip](https://github.com/VirtusLab/tulip) | 131 | 使用 LLM 以易于理解的方式解释 GitHub PR。 | [SAFE](https://agentskillshub.top/skill/VirtusLab/tulip/?utm_source=github&utm_medium=awesome-list) |
| [minetechnic2012-lang/claude-ops-inspector](https://github.com/minetechnic2012-lang/claude-ops-inspector) | 120 | Claude AI Code Networks 的子代理验证 2026 | [SAFE](https://agentskillshub.top/skill/minetechnic2012-lang/claude-ops-inspector/?utm_source=github&utm_medium=awesome-list) |
| [Mte90/linus-torvalds-skill](https://github.com/Mte90/linus-torvalds-skill) | 116 | 从 kernel newsletter 约3.2万封邮件中提炼的 Code Reviewer skill/soul | [SAFE](https://agentskillshub.top/skill/Mte90/linus-torvalds-skill/?utm_source=github&utm_medium=awesome-list) |
| [GGGODLIN/claude-pr-review](https://github.com/GGGODLIN/claude-pr-review) | 114 | Claude Code 的多维 PR 审查编排：5 个独立审查视角、对称交叉验证、确定性覆盖断言 | [SAFE](https://agentskillshub.top/skill/GGGODLIN/claude-pr-review/?utm_source=github&utm_medium=awesome-list) |
| [huoji120/code_review_agent](https://github.com/huoji120/code_review_agent) | 113 | 代码审计 agent | [SAFE](https://agentskillshub.top/skill/huoji120/code_review_agent/?utm_source=github&utm_medium=awesome-list) |
| [umputun/revmux](https://github.com/umputun/revmux) | 108 | 多智能体代码审查，可监督、可审计 | [SAFE](https://agentskillshub.top/skill/umputun/revmux/?utm_source=github&utm_medium=awesome-list) |
| [ZJunCher/mr-agent](https://github.com/ZJunCher/mr-agent) | 93 | 用于 GitLab MR 代码审查、治理和 CI 自动修复的开源多 agent 平台。 | [SAFE](https://agentskillshub.top/skill/ZJunCher/mr-agent/?utm_source=github&utm_medium=awesome-list) |
| [dalemoncayo/fullcase-web](https://github.com/dalemoncayo/fullcase-web) | 93 | AI 代码审查实际集成示例，使用 Next.js 和 Firebase，展示结构化提示、可复用 review skill，以及 Claude Code 和 O… | [CAUTION](https://agentskillshub.top/skill/dalemoncayo/fullcase-web/?utm_source=github&utm_medium=awesome-list) |
| [csy-csy123/pr-review-agent-council](https://github.com/csy-csy123/pr-review-agent-council) | 87 | 基于 learn-claude-code 的 PR Review Agent：实现 Debate Council 多 Agent 审查、Tool Callin… | [SAFE](https://agentskillshub.top/skill/csy-csy123/pr-review-agent-council/?utm_source=github&utm_medium=awesome-list) |
| [kevinten-ai/ai-agent-agentscope-codereview](https://github.com/kevinten-ai/ai-agent-agentscope-codereview) | 68 | 基于 AgentScope Java SDK 的代码审查 Agent，涵盖 ReAct、工具系统和多 Agent 协作。 | [SAFE](https://agentskillshub.top/skill/kevinten-ai/ai-agent-agentscope-codereview/?utm_source=github&utm_medium=awesome-list) |
| [MaxwellCCC/autonomous-qa-loop](https://github.com/MaxwellCCC/autonomous-qa-loop) | 65 | 用于发现 bug、避免偏见自检的便携式 fresh-agent QA 循环提示词/SKILL | [SAFE](https://agentskillshub.top/skill/MaxwellCCC/autonomous-qa-loop/?utm_source=github&utm_medium=awesome-list) |
| [addyosmani/adverse](https://github.com/addyosmani/adverse) | 62 | 适用于任意 coding agent 的多智能体对抗式代码审查 | [SAFE](https://agentskillshub.top/skill/addyosmani/adverse/?utm_source=github&utm_medium=awesome-list) |
| [AaronZ345/codebase-argus](https://github.com/AaronZ345/codebase-argus) | 58 | 多 agent 代码库审查，涵盖 PR、CI 和下游 fork 同步。 | [CAUTION](https://agentskillshub.top/skill/AaronZ345/codebase-argus/?utm_source=github&utm_medium=awesome-list) |
| [ncoevoet/claude-review-all](https://github.com/ncoevoet/claude-review-all) | 44 | Claude Code 的多智能体代码审查 | [SAFE](https://agentskillshub.top/skill/ncoevoet/claude-review-all/?utm_source=github&utm_medium=awesome-list) |
| [leocder07/spectra](https://github.com/leocder07/spectra) | 19 | 8 个 AI agent 从 6 个维度评估整个仓库，生成可签名、可验证的 A+ 至 F 审计报告 | [SAFE](https://agentskillshub.top/skill/leocder07/spectra/?utm_source=github&utm_medium=awesome-list) |
| [ZephyrDeng/pi-review](https://github.com/ZephyrDeng/pi-review) | 16 | 从命令行进行隔离的 AI 代码和计划审查 | [SAFE](https://agentskillshub.top/skill/ZephyrDeng/pi-review/?utm_source=github&utm_medium=awesome-list) |
| [FreHu/claude-maintainability-review](https://github.com/FreHu/claude-maintainability-review) | 11 | Claude Code 工作流：由人工和大语言模型评估项目可维护性 | [SAFE](https://agentskillshub.top/skill/FreHu/claude-maintainability-review/?utm_source=github&utm_medium=awesome-list) |
| [wdnmd1265/Audison](https://github.com/wdnmd1265/Audison) | 11 | 不要依赖单一 AI 输出。用于 LLM 质量控制的反幻觉框架，支持双脑仲裁、多模型审计和证据链。 | [SAFE](https://agentskillshub.top/skill/wdnmd1265/Audison/?utm_source=github&utm_medium=awesome-list) |

<a id="type-platform"></a>
## 🏗 自托管平台

[在在线页面打开这一类,按星数排序 →](https://agentskillshub.top/best/code-review/?utm_source=github&utm_medium=awesome-list#type-platform)

| 仓库 | 星数 | 做什么 | 安全评级 |
|---|---:|---|---|
| [px0-ai/px0](https://github.com/px0-ai/px0) | 1.9k | px0 是审查 AI 生成代码的 IDE，将浏览器变为低延迟控制台，集成 Git、GitHub，支持大型代码库搜索，并可交接到本地 AI 编程工具。 | [SAFE](https://agentskillshub.top/skill/px0-ai/px0/?utm_source=github&utm_medium=awesome-list) |
| [kodustech/kodus-ai](https://github.com/kodustech/kodus-ai) | 1.5k | 开源、自托管的 AI 代码审查，支持自带 LLM。 | [SAFE](https://agentskillshub.top/skill/kodustech/kodus-ai/?utm_source=github&utm_medium=awesome-list) |
| [miracodeai/mira](https://github.com/miracodeai/mira) | 378 | 自托管 AI 代码审查工具，支持索引 PR 审查、代码讲解、漏洞扫描、依赖图、自定义规则和学习循环。 | [SAFE](https://agentskillshub.top/skill/miracodeai/mira/?utm_source=github&utm_medium=awesome-list) |
| [domvwt/chatgpt-code-review](https://github.com/domvwt/chatgpt-code-review) | 289 | ChatGPT Code Review：分析 GitHub 仓库代码并提供改进建议。 | [SAFE](https://agentskillshub.top/skill/domvwt/chatgpt-code-review/?utm_source=github&utm_medium=awesome-list) |
| [FelixNg1022/cf_ai_code_review](https://github.com/FelixNg1022/cf_ai_code_review) | 168 | 基于 Cloudflare Workers 的 AI 代码审查应用 | [SAFE](https://agentskillshub.top/skill/FelixNg1022/cf_ai_code_review/?utm_source=github&utm_medium=awesome-list) |
| [devarshishimpi/codra](https://github.com/devarshishimpi/codra) | 124 | 基于 Cloudflare Workers 的 GitHub Pull Request 自托管 AI 代码审查工具。 | [SAFE](https://agentskillshub.top/skill/devarshishimpi/codra/?utm_source=github&utm_medium=awesome-list) |
| [seoes/proval](https://github.com/seoes/proval) | 118 | 面向 GitLab、Forgejo 和 GitHub 的自托管 LLM 代码审查 agent，支持本地 LLM | [SAFE](https://agentskillshub.top/skill/seoes/proval/?utm_source=github&utm_medium=awesome-list) |
| [imDarshanGK/AI-dev-assistant](https://github.com/imDarshanGK/AI-dev-assistant) | 83 | 代码分析工具，可检测错误、解释代码并提供建议。 | [SAFE](https://agentskillshub.top/skill/imDarshanGK/AI-dev-assistant/?utm_source=github&utm_medium=awesome-list) |
| [HexmosTech/LiveReview](https://github.com/HexmosTech/LiveReview) | 68 | 面向业务关键系统的影响范围感知 AI 代码审查 | [CAUTION](https://agentskillshub.top/skill/HexmosTech/LiveReview/?utm_source=github&utm_medium=awesome-list) |

**安全评级**是 Agent Skills Hub 对仓库 README 和安装步骤的评级。*待评级*表示目录还没评到它。

预览图是各项目 README 里图片的缩小副本,只收录采用宽松许可证的项目,版权归原作者所有。来源和许可证见 [assets/previews/NOTICE.md](assets/previews/NOTICE.md)。如需移除请提 issue。

## 相关合集

- [zhuyansen/awesome-claude-video-skills](https://github.com/zhuyansen/awesome-claude-video-skills), [zhuyansen/awesome-codex-ppt-skills](https://github.com/zhuyansen/awesome-codex-ppt-skills) —— 同样做法的合集。

## 推荐仓库

提一个 issue 附上 GitHub 链接。它会走和每个条目一样的评审;决定上不上榜的是上面的规则,不是星数。

---

机器可读版本:[`data/skills.json`](data/skills.json)。生成于 2026-10-26。
