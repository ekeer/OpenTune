基础
请用中文语言思维方式完成所有任务，必须先用Best-Engineering技能，积极调用子代理。
### 规划与执行
1. 规划前必看 `.planning/codebase/` 记忆文档，获得最新现状。"记忆说 X 存在" ≠ "X 现在存在"。如果记忆提到文件路径，用 Glob/Read 验证；如果提到函数，用 Grep 确认是否还在
2. 接到任务后必用相关skill。。`test-driven-spec` 技能来设计和进行测试阶段
3. **执行前必读**: `.planning/PROJECT.md`、`.planning/REQUIREMENTS.md`、`.planning/ROADMAP.md`、`.planning/STATE.md`
4. Debug可以看日志目录：C:\Users\当前系统用户名\AppData\Roaming\OpenTune\Logs。Debug、代码审查参考Oracle意见，但不要全信，它的意见多有防御性和兜底冗余，损害代码简洁性。
编译：VS + CMake  MSBuild，禁 ninja 或手写脚本。

## Kill List (eliminate on sight)

| Anti-pattern | What it looks like |
|---|---|
| Band-aid (止血) | Patches symptom, not root cause |
| Minimal-change workaround (最小改动) | Avoids proper refactor |
| Defensive programming (防御性编程) | Unnecessary null checks, try-catch soup, "just in case" guards |
| Fallback/safety-net (兜底) | Redundant backup path masking real bugs |
| Parallel structures (并行结构) | Old+new paths coexisting during incomplete migration |
| Compatibility layer (兼容层) | Shims for removed/obsolete code |

## Common Mistakes

| Mistake | Fix |
|---|---|
| Fixing symptom not cause | Trace to requirement, find structural root |
| "Just in case" defensive code | Remove guard; fix the source of bad state |
| Keeping dead code "for reference" | Delete; git has history |
| Adding fallback instead of fixing caller | Fix caller; remove fallback |
| Partial migration (old+new coexist) | Complete migration, delete old path |

VST3 规则
UI 隔离：Standalone/PluginEditor.* 属 Standalone；Plugin/PluginEditor.* 属 VST3。用 JucePlugin_Build_Standalone 隔离。
Processor 共享：PluginProcessor.* 两格式共用，修改时保证 JucePlugin_Build_Standalone 和 JucePlugin_Enable_ARA 分支正确。