# Elasticsearch Curator Helm Chart

This directory contains a Kubernetes chart to deploy the [Elasticsearch Curator](https://github.com/elastic/curator).

## Prerequisites Details

* Elasticsearch

* The `elasticsearch-curator` cron job requires [K8s CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) support:
    > You need a working Kubernetes cluster at version >= 1.8 (for CronJob). For previous versions of cluster (< 1.8) you need to explicitly enable `batch/v2alpha1` API by passing `--runtime-config=batch/v2alpha1=true` to the API server ([see Turn on or off an API version for your cluster for more](https://kubernetes.io/docs/admin/cluster-management/#turn-on-or-off-an-api-version-for-your-cluster)).

## Chart Details

This chart will do the following:

* Create a CronJob which runs the Curator

## Installing the Chart

To install the chart, use the following:

```console
$ helm install stable/elasticsearch-curator
```

## Configuration

The following table lists the configurable parameters of the docker-registry chart and
their default values.

|          Parameter                   |                         Description                         |                   Default                    |
| :----------------------------------- | :---------------------------------------------------------- | :------------------------------------------- |
| `image.pullPolicy`                   | Container pull policy                                       | `IfNotPresent`                               |
| `image.repository`                   | Container image to use                                      | `quay.io/pires/docker-elasticsearch-curator` |
| `image.tag`                          | Container image tag to deploy                               | `5.5.4`                                      |
| `hooks`                              | Whether to run job on selected hooks                        | `{ "install": false, "upgrade": false }`     |
| `cronjob.schedule`                   | Schedule for the CronJob                                    | `0 1 * * *`                                  |
| `cronjob.annotations`                | Annotations to add to the cronjob                           | {}                                           |
| `cronjob.concurrencyPolicy`          | `Allow|Forbid|Replace` concurrent jobs                      | `nil`                                        |
| `cronjob.failedJobsHistoryLimit`     | Specify the number of failed Jobs to keep                   | `nil`                                        |
| `cronjob.successfulJobsHistoryLimit` | Specify the number of completed Jobs to keep                | `nil`                                        |
| `pod.annotations`                    | Annotations to add to the pod                               | {}                                           |
| `dryrun`                             | Run Curator in dry-run mode                                 | `false`                                      |
| `env`                                | Environment variables to add to the cronjob container       | {}                                           |
| `envFromSecrets`                     | Environment variables from secrets to the cronjob container | {}                                           |
| `envFromSecrets.*.from.secret`       | - `secretKeyRef.name` used for environment variable         |                                              |              
| `envFromSecrets.*.from.key`          | - `secretKeyRef.key` used for environment variable          |                                              |              
| `command`                            | Command to execute                                          | ["curator"]                                  |
| `configMaps.action_file_yml`         | Contents of the Curator action_file.yml                     | See values.yaml                              |
| `configMaps.config_yml`              | Contents of the Curator config.yml (overrides config)       | See values.yaml                              |
| `resources`                          | Resource requests and limits                                | {}                                           |
| `priorityClassName`                  | priorityClassName                                           | `nil`                                        |
| `extraVolumeMounts`                  | Mount extra volume(s),                                      |                                              |
| `extraVolumes`                       | Extra volumes                                               |                                              |

Specify each parameter using the `--set key=value[,key=value]` argument to
`helm install`.
