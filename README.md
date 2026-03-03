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

## 🤖 For AI Agent - Local Deployment Guide

> **This section is for AI agents** who need to deploy Klavis PowerPoint MCP Server from scratch.

### Environment Requirements

- **OS**: macOS / Linux / Windows
- **Python**: 3.8+
- **Git**: Installed
- **IDE**: Cursor / Claude Code / OpenCode
- **API**: OpenAI-compatible API key

### Step-by-Step Deployment

#### 1. Clone Repository

```bash
# Clone Klavis AI repository
cd ~
git clone https://github.com/Klavis-AI/klavis.git
cd klavis/mcp_servers/local/powerpoint
```

#### 2. Setup Python Environment

```bash
# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
# macOS/Linux:
source .venv/bin/activate
# Windows:
# .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. Configure Environment Variables

Create `.env` file in the powerpoint directory:

```bash
# Create .env file
cat > .env << 'EOF'
# OpenAI API Configuration
OPENAI_API_KEY=your-api-key-here
OPENAI_BASE_URL=https://api.openai.com/v1
OPENAI_MODEL_ID=gpt-4

# Output Configuration
OUTPUT_DIR=/Users/you/Documents/PPTX-Output

# Template Path (optional)
PPT_TEMPLATE_PATH=./templates:./assets
EOF
```

**For Enterprise APIs** (e.g., Kuaishou Wanqing):

```bash
cat > .env << 'EOF'
OPENAI_API_KEY=your-enterprise-api-key
OPENAI_BASE_URL=https://your-enterprise-api-endpoint
OPENAI_MODEL_ID=your-model-id
OUTPUT_DIR=/Users/you/Documents/PPTX-Output
EOF
```

#### 4. Create Output Directory

```bash
mkdir -p ~/Documents/PPTX-Output
```

#### 5. Configure MCP Client

##### For Cursor IDE

Edit `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "powerpoint": {
      "command": "/Users/you/klavis/mcp_servers/local/powerpoint/.venv/bin/python",
      "args": [
        "/Users/you/klavis/mcp_servers/local/powerpoint/ppt_mcp_server.py"
      ],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here",
        "OPENAI_BASE_URL": "https://api.openai.com/v1",
        "OPENAI_MODEL_ID": "gpt-4",
        "OUTPUT_DIR": "/Users/you/Documents/PPTX-Output"
      }
    }
  }
}
```

##### For Claude Code

Edit `~/.claude/config.json` or create MCP configuration:

```json
{
  "mcpServers": {
    "powerpoint": {
      "command": "/Users/you/klavis/mcp_servers/local/powerpoint/.venv/bin/python",
      "args": [
        "/Users/you/klavis/mcp_servers/local/powerpoint/ppt_mcp_server.py"
      ],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here",
        "OPENAI_BASE_URL": "https://api.openai.com/v1",
        "OPENAI_MODEL_ID": "gpt-4",
        "OUTPUT_DIR": "/Users/you/Documents/PPTX-Output"
      }
    }
  }
}
```

#### 6. Verify Installation

```bash
# Test MCP Server startup (stdio mode)
cd ~/klavis/mcp_servers/local/powerpoint
source .venv/bin/activate
python ppt_mcp_server.py

# Should see: "Starting PowerPoint MCP Server..."
# Press Ctrl+C to stop
```

#### 7. Install Skill (Optional)

If you want AI agents to auto-activate this skill:

```bash
# Claude Code
mkdir -p ~/.claude/skills/klavis-powerpoint-mcp
cd ~/.claude/skills/klavis-powerpoint-mcp
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/SKILL.md

# OpenCode
mkdir -p ~/.agents/skills/klavis-powerpoint-mcp
cd ~/.agents/skills/klavis-powerpoint-mcp
curl -O https://raw.githubusercontent.com/imwxc/klavis-powerpoint-mcp-skill/main/SKILL.md
```

### Troubleshooting

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| `Permission denied` | Check file permissions or use `chmod +x` |
| `API connection failed` | Verify `OPENAI_API_KEY` and `OPENAI_BASE_URL` |
| `Output directory not found` | Create with `mkdir -p ~/Documents/PPTX-Output` |
| MCP not connecting | Restart IDE, check `mcp.json` syntax |

### Architecture

```
MCP Client (Cursor/Claude Code)
    ↓
PowerPoint MCP Server (Local Python)
    ↓
python-pptx (Local Library)
    ↓
OpenAI API (Cloud, for content generation)
    ↓
.pptx files (Local output)
```

---

## 🚀 Quick Start (Skill Installation)

### Prerequisites

1. **Klavis PowerPoint MCP Server** deployed (see above)
2. **API Key** configured in MCP settings

### Skill Installation

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
