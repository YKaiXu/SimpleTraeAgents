# 全局规则 — SubAgent 委派协议

## 强制规则

1. **每次收到开发任务，必须先检查所有子智能体和技能的描述，判断是否有匹配项，有则立即委派，不得直接上手操作。**

2. **系统运维任务**（系统配置、网络配置、安全加固、故障排查、服务器部署、变更管理）必须优先调用 `sysops-agent` 子智能体。特别注意：所有系统操作前必须先调用该智能体进行调研评估和备份确认。

3. **架构设计任务**（新项目架构设计、系统重构方案、技术选型决策、模块边界划分、架构评审）必须优先调用 `architect-agent` 子智能体。

4. **Python 相关任务**（修复 Bug、添加功能、重构、开发 Web 项目、设计 API、编写测试、代码审查、质量改进）必须优先调用 `python-fullstack` 子智能体。

5. **代码审查**必须调用 `code-reviewer` 子智能体或 `TRAE-code-review` 技能。

6. **UI 设计任务**（页面组件、响应式布局、图片资源生成）必须调用 `ui-designer` 子智能体。

7. **测试编写**（单元测试、集成测试、测试运行与验证）必须调用 `test-engineer` 子智能体。

8. **文档编写**（README、API 文档、架构文档、变更日志）必须调用 `tech-writer` 子智能体。

9. **前置调研**（复杂任务开始前的需求分析、代码现状调研、技术方案对比）必须调用 `research-agent` 子智能体。

10. 不得直接使用 Read/Edit/Write 工具替代子智能体完成上述专业领域任务。

## 自定义说明

### 测试命令

每个项目可能有不同的测试框架和命令。请在项目级 `project_rules.md` 中覆盖以下模板：

```bash
cd $PROJECT_ROOT && pytest tests/ -v
# 或
cd $PROJECT_ROOT && npm test
# 或
cd $PROJECT_ROOT && go test ./...
```

### 编译/代码检查命令

```bash
# Python
cd $PROJECT_ROOT && find . -name "*.py" -not -path "./.venv/*" -exec python3 -m py_compile {} \;

# TypeScript / Node
# cd $PROJECT_ROOT && npm run typecheck

# Go
# cd $PROJECT_ROOT && go build ./...
```

## 使用方式

将本文件复制到项目根目录的 `.trae/rules/` 下，并根据项目实际情况：
1. 更新测试命令中的项目路径和框架
2. 更新代码检查命令
3. 移除不必要的注释和模板

子智能体列表参考：[SimpleTraeAgents](https://github.com/YKaiXu/SimpleTraeAgents)