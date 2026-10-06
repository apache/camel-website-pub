# camel tui

Camel TUI

> **Note**
> This command is provided by the `tui` plugin. Install it with `camel plugin add tui`.

## Usage

```bash
camel tui [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [monitor](camel-jbang-tui-monitor.md) | Live dashboard for monitoring Camel integrations |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--mcp` | Enable embedded MCP server for AI agent access to the TUI |  | boolean |
| `--mcp-port` | MCP server port | 8123 | int |
| `--record` | Replay a .tape file inside the TUI and record to an Asciinema .cast file |  | String |
| `--record-duration` | Maximum duration in milliseconds captured by --record | 120000 | int |
| `--record-fps` | Frames per second captured by --record | 10 | int |
| `--record-size` | Size of the recorded terminal for --record, as <cols>x<rows> | 200x50 | String |
| `--refresh` | Refresh interval in milliseconds | 100 | long |
| `--theme` | Color theme: dark or light (overrides persisted preference for this session) |  | String |
| `--web` | Enable browser-accessible terminal (WebSocket) server |  | boolean |
| `--web-port` | Web terminal server port | 8090 | int |
| `-h,--help` | Display the help and sub-commands |  | boolean |