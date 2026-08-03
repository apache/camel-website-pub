# camel ask

Ask a question about a running Camel application using AI

## Usage

```bash
camel ask [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--api-key` | API key. Also reads ANTHROPIC\_API\_KEY, OPENAI\_API\_KEY, WATSONX\_APIKEY, or LLM\_API\_KEY env vars |  | String |
| `--api-type` | API type: 'ollama', 'openai', 'anthropic', or 'watsonx' |  | ApiType |
| `--max-iterations` | Maximum number of tool-calling rounds | 10 | int |
| `--model` | Model to use | DEFAULT\_MODEL | String |
| `--name` | Name or PID of the Camel process. Auto-detected when exactly one process is running |  | String |
| `--show-stats` | Show token usage and elapsed time after response |  | boolean |
| `--show-tools` | Show tool calls and results as they happen |  | boolean |
| `--timeout` | Timeout in seconds for LLM response | 120 | int |
| `--url` | LLM API endpoint URL. Auto-detected if not specified. Also reads AZURE\_OPENAI\_ENDPOINT or WATSONX\_URL env vars |  | String |
| `--verbose` | Print debug information: HTTP requests, responses, and parsed results |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |