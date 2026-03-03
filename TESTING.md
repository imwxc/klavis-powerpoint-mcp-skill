# Testing Scenarios for Klavis PowerPoint MCP Skill

## Baseline Testing (RED Phase)

**Objective**: Test agent behavior WITHOUT skill to identify gaps and rationalizations.

### Test Scenarios

#### Scenario 1: Academic Question
**User**: "如何创建一个 PowerPoint 演示文稿？"

**Expected Skill Behavior**: 
- Load skill
- Explain MCP configuration
- Provide usage examples

**Baseline (No Skill) Predictions**:
- Agent may suggest using python-pptx directly
- Agent may not know about Klavis MCP server
- Agent may not know how to configure MCP in Claude Code

#### Scenario 2: Application Scenario
**User**: "创建一个 5 页的产品发布 PPTX，包括标题页、产品概述、功能介绍、技术架构、总结"

**Expected Skill Behavior**:
- Load skill
- Identify required tools (create_presentation, add_slide, add_text, export_presentation)
- Execute correct MCP tool sequence

**Baseline (No Skill) Predictions**:
- Agent may not know MCP tools exist
- Agent may struggle to find correct tool names
- Agent may not know parameter formats

#### Scenario 3: Missing Information
**User**: "使用 PowerPoint MCP 生成一个 PPTX 文件"

**Expected Skill Behavior**:
- Check MCP configuration
- Verify output directory exists
- Provide setup instructions if missing

**Baseline (No Skill) Predictions**:
- Agent may assume MCP is already configured
- Agent may not check prerequisites
- Agent may fail silently without proper error messages

### Rationalizations to Counter

| Rationalization | Reality | Skill Counter |
|-----------------|---------|---------------|
| "I don't know about this MCP server" | MCP is documented in ~/.cursor/mcp.json | Add explicit check for MCP configuration |
| "I need more information" | All info is in skill + deployment report | Provide complete reference in skill |
| "It's too complex" | Skill should simplify usage | Add quick reference table and examples |
| "Let me check the documentation" | Agent should have knowledge in skill | Include all necessary info inline |
| "I'm not sure which tools to use" | Skill lists all 10 tool modules | Provide tool categorization and usage guide |

### Pressure Test Matrix

| Pressure Type | Scenario | Expected Failure (No Skill) | Expected Success (With Skill) |
|---------------|----------|----------------------------|------------------------------|
| **Time** | "Quickly create a PPTX" | Skip configuration checks | Follow skill checklist |
| **Sunk Cost** | "I already wrote this code" | Keep using python-pptx | Switch to MCP tools |
| **Authority** | "Use the simplest approach" | Use basic libraries | Use MCP as documented |
| **Exhaustion** | After 5 failed attempts | Give up on MCP | Follow skill troubleshooting |

## Test Execution Plan

### Phase 1: Baseline (No Skill)
1. Run scenarios WITHOUT skill loaded
2. Document exact agent responses (verbatim)
3. Identify rationalizations and knowledge gaps
4. Record specific failure patterns

### Phase 2: With Skill (GREEN)
1. Load skill
2. Run same scenarios
3. Verify agent follows skill guidance
4. Check all rationalizations are countered

### Phase 3: Loophole Testing (REFACTOR)
1. Attempt to bypass skill rules
2. Find new rationalizations
3. Update skill to close loopholes
4. Re-test until bulletproof

## Success Criteria

- [ ] Agent loads skill when encountering PPT/PPTX keywords
- [ ] Agent checks MCP configuration before attempting operations
- [ ] Agent uses correct MCP tool names and parameters
- [ ] Agent provides setup instructions if prerequisites missing
- [ ] Agent handles errors gracefully with troubleshooting guidance
- [ ] No rationalizations bypass skill guidance

## Test Results (REFACTOR Phase)

### Baseline Behavior (Before Skill)

**Test 1: Academic Question**
- User: "如何创建 PowerPoint？"
- Agent (No Skill): 建议使用 python-pptx 库，不知道 Klavis MCP 存在
- Gap: 缺少 MCP 知识，不知道已部署的 PowerPoint MCP server

**Test 2: Application Scenario**
- User: "创建产品发布 PPTX"
- Agent (No Skill): 询问更多信息，不知道具体工具名称和参数格式
- Gap: 不知道 32 个 MCP 工具的存在和使用方式

**Test 3: Missing Information**
- User: "生成 PPTX 文件"
- Agent (No Skill): 尝试使用 python-pptx，不知道 MCP 配置和输出目录
- Gap: 不知道 prerequisite checklist 和配置要求

### With Skill Behavior (GREEN Phase)

**Test 1: Academic Question**
- User: "如何创建 PowerPoint？"
- Agent (With Skill): ✅ 加载 skill，检查 MCP 配置，提供 Quick Reference
- Success: Agent 正确识别需要使用 Klavis MCP server

**Test 2: Application Scenario**
- User: "创建产品发布 PPTX"
- Agent (With Skill): ✅ 使用 skill 中的工具分类表格，选择正确的工具序列
- Success: Agent 知道 10 个工具模块及其用途

**Test 3: Missing Information**
- User: "生成 PPTX 文件"
- Agent (With Skill): ✅ 检查 prerequisite checklist，提示配置 API Key 和输出目录
- Success: Agent 提供完整的配置步骤和故障排查指南

### Loopholes Closed

| Loophole | How Closed in Skill |
|----------|-------------------|
| "I don't know this MCP exists" | Overview 明确说明 Klavis MCP Server，包含完整配置路径 |
| "I need more info to configure" | Prerequisite Checklist 提供所有必要信息，无需查文档 |
| "Too complex to use" | Quick Reference Table + Common Operations 简化使用 |
| "Let me check docs" | 所有信息 inline，包含 tool 列表、参数格式、示例 |
| "Which tool to use?" | 10 个工具模块分类表格，按功能组织 |
| "What if it fails?" | Troubleshooting section 覆盖常见错误和解决方案 |

## Final Verification

- [x] Skill frontmatter < 1024 chars (300 chars)
- [x] Description uses "Use when..." format
- [x] Description contains search keywords (PPT/PPTX/PowerPoint/slides/MCP)
- [x] All baseline gaps addressed in skill
- [x] Rationalization table completed
- [x] Word count < 800 words (776 words)
- [x] No workflow summary in description
- [x] Quick reference table provided
- [x] Common mistakes section included
- [x] Troubleshooting guide included
