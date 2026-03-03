---
name: klavis-powerpoint-mcp
description: Use when creating PPT/PPTX/PowerPoint files, users mention presentations/demonstrations/slides, or when PowerPoint MCP configuration/setup is needed. Covers Klavis MCP server with 32 tools for slide creation, text editing, charts, templates, and PPTX export.
---

# Klavis PowerPoint MCP

## Overview

Klavis PowerPoint MCP Server provides 32 tools for creating, editing, and exporting PPTX files through Model Context Protocol (MCP). Use this skill to configure MCP in Claude Code/OpenCode and generate professional presentations.

**Core principle**: MCP server must be configured before use. Always check configuration and prerequisites first.

## When to Use

Use this skill when:
- User wants to create, edit, or export PowerPoint/PPTX files
- User mentions "PPT", "PPTX", "PowerPoint", "演示文稿", "幻灯片"
- MCP configuration for PowerPoint is needed
- Presentation generation fails or tools not found

## MCP Configuration

### Claude Code Configuration

Edit `~/.claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "powerpoint": {
      "command": "/Users/wangxianchen/klavis/mcp_servers/local/powerpoint/.venv/bin/python",
      "args": [
        "/Users/wangxianchen/klavis/mcp_servers/local/powerpoint/ppt_mcp_server.py"
      ],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here",
        "OPENAI_BASE_URL": "https://wanqing-api.corp.kuaishou.com/api/gateway/v1/endpoints",
        "OPENAI_MODEL_ID": "ep-trfdr9-1772437647576223172",
        "OUTPUT_DIR": "/Users/wangxianchen/Documents/PPTX-Output"
      }
    }
  }
}
```

### OpenCode Configuration

Edit `~/.config/opencode/mcp.json`:

```json
{
  "mcpServers": {
    "powerpoint": {
      "command": "/Users/wangxianchen/klavis/mcp_servers/local/powerpoint/.venv/bin/python",
      "args": [
        "/Users/wangxianchen/klavis/mcp_servers/local/powerpoint/ppt_mcp_server.py"
      ],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here",
        "OPENAI_BASE_URL": "https://wanqing-api.corp.kuaishou.com/api/gateway/v1/endpoints",
        "OPENAI_MODEL_ID": "ep-trfdr9-1772437647576223172",
        "OUTPUT_DIR": "/Users/wangxianchen/Documents/PPTX-Output"
      }
    }
  }
}
```

### Configuration Checklist

- [ ] API Key: Replace `your-api-key-here` with actual key
- [ ] Output Directory: Create with `mkdir -p ~/Documents/PPTX-Output`
- [ ] Restart IDE after configuration changes

## Quick Reference

### 10 Tool Modules (32 Tools Total)

| Module | Tools | Purpose |
|--------|-------|---------|
| **presentation_tools** | create, open, save, export, close | Presentation lifecycle |
| **content_tools** | add_text, add_title, add_content | Text and content |
| **structural_tools** | add_slide, delete_slide, duplicate_slide | Slide management |
| **professional_tools** | add_chart, add_smartart | Advanced graphics |
| **template_tools** | apply_template, create_from_template | Template handling |
| **hyperlink_tools** | add_hyperlink, add_action | Interactive elements |
| **chart_tools** | add_chart, update_chart_data | Data visualization |
| **connector_tools** | add_connector, add_line | Diagram connectors |
| **master_tools** | edit_master, create_layout | Slide masters |
| **transition_tools** | add_transition, set_timing | Animations |

### Common Operations

```python
# Create presentation
create_presentation(width, height)

# Add slides
add_slide(presentation_id, layout_index)

# Add text
add_text(presentation_id, slide_index, left, top, width, height, text)

# Export
export_presentation(presentation_id, output_path, format="pptx")
```

## Usage Workflow

### 1. Check Prerequisites

```bash
# Verify MCP server exists
ls -la ~/klavis/mcp_servers/local/powerpoint/ppt_mcp_server.py

# Verify Python environment
ls -la ~/klavis/mcp_servers/local/powerpoint/.venv/bin/python

# Verify output directory
ls -la ~/Documents/PPTX-Output
```

### 2. Verify MCP Configuration

Check if `powerpoint` server is in MCP configuration file.

### 3. Create Presentation

```python
# Step 1: Create presentation
presentation_id = create_presentation(width=10, height=7.5)

# Step 2: Add slides
add_slide(presentation_id, layout_index=0)  # Title slide
add_slide(presentation_id, layout_index=1)  # Title + Content
add_slide(presentation_id, layout_index=6)  # Blank

# Step 3: Add content
add_title(presentation_id, slide_index=0, text="Product Launch")
add_text(presentation_id, slide_index=1, left=1, top=1, 
         width=8, height=5, text="Key Features")

# Step 4: Export
export_presentation(presentation_id, 
                   output_path="~/Documents/PPTX-Output/presentation.pptx")
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| "MCP tools not found" | Check MCP configuration in config file |
| "API Key invalid" | Replace `your-api-key-here` with real key |
| "Output directory not found" | Run `mkdir -p ~/Documents/PPTX-Output` |
| "Import python-pptx directly" | Use MCP tools instead, don't bypass MCP |
| "Tool name incorrect" | Check exact tool name in quick reference |

## Red Flags - Check These First

- [ ] MCP configuration file exists
- [ ] `powerpoint` server in MCP config
- [ ] API Key is not `your-api-key-here`
- [ ] Output directory exists
- [ ] Python environment at `~/klavis/mcp_servers/local/powerpoint/.venv/bin/python`

If ANY flag fails → Fix before proceeding.

## Troubleshooting

### MCP Tools Not Visible

1. Check configuration file path is correct
2. Restart IDE after config changes
3. Verify Python environment exists
4. Check MCP server logs for errors

### Tool Execution Fails

1. Verify API Key is valid
2. Check network connectivity to API endpoint
3. Ensure output directory has write permissions
4. Review error message for specific guidance

### Configuration Issues

1. Verify paths use absolute paths (no `~` or `.`)
2. Check JSON syntax is valid
3. Ensure all required environment variables are set
4. Test Python environment manually

## Real-World Impact

**Before MCP**: Manual python-pptx coding, 50+ lines per presentation
**After MCP**: 4-5 MCP tool calls, declarative approach

**Time saved**: ~80% reduction in code for standard presentations

## Deployment Information

- **Repository**: `~/klavis/`
- **Server Path**: `~/klavis/mcp_servers/local/powerpoint/`
- **Virtual Environment**: `~/klavis/mcp_servers/local/powerpoint/.venv/`
- **Config Files**: `~/.claude/claude_desktop_config.json` (Claude Code), `~/.config/opencode/mcp.json` (OpenCode)
- **Output Directory**: `~/Documents/PPTX-Output/`

## Related Skills

- **superpowers:brainstorming** - Use before creating complex presentations
- **superpowers:verification-before-completion** - Verify presentation exported successfully

---

**Remember**: Always check configuration first. MCP server must be configured before tools are available.
