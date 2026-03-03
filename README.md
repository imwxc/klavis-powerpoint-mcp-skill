# Klavis PowerPoint MCP Skill

[![GitHub](https://img.shields.io/badge/GitHub-imwxc%2Fklavis--powerpoint--mcp--skill-blue)](https://github.com/imwxc/klavis-powerpoint-mcp-skill)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> AI-powered PowerPoint/PPTX generation skill for Claude Code and OpenCode

## ✨ Features

- **32 MCP Tools** - Full-featured PowerPoint manipulation
- **Dual Platform Support** - Works with both Claude Code and OpenCode
- **Enterprise API Compatible** - Supports custom OpenAI-compatible APIs (e.g., Kuaishou Wanqing)
- **Token Optimized** - 776 words skill content
- **TDD Verified** - Complete test scenarios and rationalization table

## 🚀 Quick Start

### Prerequisites

1. **Klavis PowerPoint MCP Server** installed and configured
   - Project path: `~/klavis/mcp_servers/local/powerpoint/`
   - MCP config: `~/.cursor/mcp.json`

2. **API Key** configured in MCP settings
   - Replace `your-api-key-here` with real API key
   - Output directory: `~/Documents/PPTX-Output`

### Installation

#### Claude Code

```bash
# Skill auto-loads from ~/.claude/skills/klavis-powerpoint-mcp/
mkdir -p ~/.claude/skills/klavis-powerpoint-mcp
cd ~/.claude/skills/klavis-powerpoint-mcp
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/SKILL.md
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/TESTING.md
```

#### OpenCode

```bash
# Copy to OpenCode skills directory
mkdir -p ~/.agents/skills/klavis-powerpoint-mcp
cd ~/.agents/skills/klavis-powerpoint-mcp
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/SKILL.md
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/TESTING.md
```

## 📖 Usage

### Trigger Keywords

The skill auto-activates when you use these keywords:

- `PPT`, `PPTX`, `PowerPoint`
- `presentation`, `slides`
- `演示文稿`, `幻灯片` (Chinese)

### Example Commands

```
# Simple
"创建一个关于项目介绍的 PPT"

# Detailed
"生成一个 10 页的技术方案演示文稿，包含架构图和数据图表"

# Edit existing
"打开 /path/to/presentation.pptx，添加一页总结"
```

## 🛠️ Tool Modules (10 Categories)

| Module | Description | Key Tools |
|--------|-------------|-----------|
| **Presentation** | Create/open/save presentations | `create_presentation`, `open_presentation`, `save_presentation` |
| **Content** | Add text/images/tables | `add_text_slide`, `add_image`, `add_table` |
| **Structural** | Slide layout/shapes | `add_shape`, `duplicate_slide`, `delete_slide` |
| **Professional** | Themes/masters | `apply_theme`, `set_master_slide` |
| **Template** | Template operations | `apply_template`, `list_templates` |
| **Chart** | Create charts | `add_chart` |
| **Hyperlink** | Hyperlink management | `add_hyperlink`, `remove_hyperlink` |
| **Connector** | Connector tools | `add_connector` |
| **Master** | Slide masters | `edit_master_slide` |
| **Transition** | Transitions | `set_transition` |

## 📁 File Structure

```
klavis-powerpoint-mcp-skill/
├── SKILL.md          # Main skill file (776 words)
├── TESTING.md        # TDD test scenarios
├── README.md         # This file
└── LICENSE           # MIT License
```

## 🔧 Configuration

### MCP Settings (Claude Code/OpenCode)

```json
{
  "mcpServers": {
    "powerpoint": {
      "command": "/path/to/python",
      "args": ["/path/to/ppt_mcp_server.py"],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here",
        "OPENAI_BASE_URL": "https://your-api-endpoint",
        "OPENAI_MODEL_ID": "your-model-id",
        "OUTPUT_DIR": "/Users/you/Documents/PPTX-Output"
      }
    }
  }
}
```

## 🧪 Testing

See `TESTING.md` for:
- 3 pressure test scenarios
- 5 rationalization patterns
- Complete test matrix

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

## 🔗 Related Projects

- [Klavis AI](https://github.com/Klavis-AI/klavis) - Original MCP Server
- [python-pptx](https://github.com/scanny/python-pptx) - PowerPoint library

## 📝 Changelog

### v1.0.0 (2026-03-03)
- Initial release
- 32 MCP tools across 10 modules
- Dual platform support (Claude Code + OpenCode)
- Enterprise API compatibility
- TDD verified

---

**Made with ❤️ by [imwxc](https://github.com/imwxc)**
