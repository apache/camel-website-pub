# camel kubernetes

Manage Camel applications running on Kubernetes

> **Note**
> This command is provided by the `kubernetes` plugin. Install it with `camel plugin add kubernetes`.

## Usage

```bash
camel kubernetes [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [delete](camel-jbang-kubernetes-delete.md) | Delete Camel application from Kubernetes. This operation will delete all resources associated to this app, such as: Deployment, Routes, Services, etc. filtering by label app.kubernetes.io/name=<name>. |
| [export](camel-jbang-kubernetes-export.md) | Export as Maven project that contains a Kubernetes deployment manifest |
| [logs](camel-jbang-kubernetes-logs.md) | Print the logs of a Kubernetes pod |
| [run](camel-jbang-kubernetes-run.md) | Run Camel application on Kubernetes |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--kube-config` | Path to the kube config file to initialize Kubernetes client |  | String |
| `--name` | The integration name. Use this when the name should not get derived otherwise. |  | String |
| `--namespace,-n` | Namespace to use for all operations |  | String |
| `-h,--help` | Display the help and sub-commands |  | boolean |