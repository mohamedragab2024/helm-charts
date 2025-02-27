
# Victoria Metrics Helm Chart for vmanomaly

![Version: 1.4.5](https://img.shields.io/badge/Version-1.4.5-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-anomaly)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)
[![GitHub license](https://img.shields.io/github/license/VictoriaMetrics/VictoriaMetrics.svg)](https://github.com/VictoriaMetrics/helm-charts/blob/master/LICENSE)
![Twitter Follow](https://img.shields.io/twitter/follow/VictoriaMetrics?style=social)
![Subreddit subscribers](https://img.shields.io/reddit/subreddit-subscribers/VictoriaMetrics?style=social)

Victoria Metrics Anomaly Detection - a service that continuously scans Victoria Metrics time series and detects unexpected changes within data patterns in real-time.

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

* PV support on underlying infrastructure

## Chart Details

This chart will do the following:

* Rollout victoria metrics anomaly

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

 - From HTTPS repository

   ```console
   helm repo add vm https://victoriametrics.github.io/helm-charts/

   helm repo update
   ```
 - From OCI repository
  
   ```console
   helm repo add vm oci://ghcr.io/victoriametrics/helm-charts/

   helm repo update
   ```

List versions of ``vm/victoria-metrics-anomaly`` chart available to installation:

```console
helm search repo vm/victoria-metrics-anomaly -l
```

Export default values of ``victoria-metrics-anomaly`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-anomaly > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmanomaly vm/victoria-metrics-anomaly -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmanomaly vm/victoria-metrics-anomaly -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'vmanomaly'
```

Get the application by running this command:

```console
helm list -f vmanomaly -n NAMESPACE
```

See the history of versions of ``vmanomaly`` application with command.

```console
helm history vmanomaly -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmanomaly -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-anomaly

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

For more `vmanomaly` config parameters see https://docs.victoriametrics.com/anomaly-detection/components

Change the values according to the need of the environment in ``victoria-metrics-anomaly/values.yaml`` file.

<table>
  <thead>
    <th>Key</th>
    <th>Type</th>
    <th>Default</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>affinity</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Affinity configurations</p>
</td>
    </tr>
    <tr>
      <td>annotations</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Annotations to be added to the deployment</p>
</td>
    </tr>
    <tr>
      <td>config</td>
      <td>object</td>
      <td><pre lang="plaintext">
models: {}
preset: ""
reader:
    class: vm
    datasource_url: ""
    queries: {}
    sampling_period: 1m
    tenant_id: ""
schedulers: {}
writer:
    class: vm
    datasource_url: ""
    tenant_id: ""
</pre>
</td>
      <td><p>Full <a href="https://docs.victoriametrics.com/anomaly-detection/components/" target="_blank">vmanomaly config section</a></p>
</td>
    </tr>
    <tr>
      <td>config.models</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p><a href="https://docs.victoriametrics.com/anomaly-detection/components/models/" target="_blank">Models section</a></p>
</td>
    </tr>
    <tr>
      <td>config.preset</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Whether to use preset configuration. If not empty, preset name should be specified.</p>
</td>
    </tr>
    <tr>
      <td>config.reader</td>
      <td>object</td>
      <td><pre lang="plaintext">
class: vm
datasource_url: ""
queries: {}
sampling_period: 1m
tenant_id: ""
</pre>
</td>
      <td><p><a href="https://docs.victoriametrics.com/anomaly-detection/components/reader/" target="_blank">Reader section</a></p>
</td>
    </tr>
    <tr>
      <td>config.reader.class</td>
      <td>string</td>
      <td><pre lang="">
vm
</pre>
</td>
      <td><p>Name of the class needed to enable reading from VictoriaMetrics or Prometheus. VmReader is the default option, if not specified.</p>
</td>
    </tr>
    <tr>
      <td>config.reader.datasource_url</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Datasource URL address. Required for example <code>http://single-victoria-metrics-single-server.default.svc.cluster.local:8428</code> or <code>http://cluster-victoria-metrics-cluster-vminsert.default.svc.cluster.local:8480</code></p>
</td>
    </tr>
    <tr>
      <td>config.reader.queries</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Required. PromQL/MetricsQL query to select data in format: QUERY_ALIAS: &ldquo;QUERY&rdquo;. As accepted by &ldquo;/query_range?query=%s&rdquo;. See <a href="https://docs.victoriametrics.com/anomaly-detection/components/reader/#per-query-parameters" target="_blank">https://docs.victoriametrics.com/anomaly-detection/components/reader/#per-query-parameters</a> for more details.</p>
</td>
    </tr>
    <tr>
      <td>config.reader.sampling_period</td>
      <td>string</td>
      <td><pre lang="">
1m
</pre>
</td>
      <td><p>Frequency of the points returned. Will be converted to <code>/query_range?step=%s</code> param (in seconds). <strong>Required</strong> since 1.9.0.</p>
</td>
    </tr>
    <tr>
      <td>config.reader.tenant_id</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>For VictoriaMetrics Cluster version only, tenants are identified by accountID or accountID:projectID. See VictoriaMetrics Cluster multitenancy docs</p>
</td>
    </tr>
    <tr>
      <td>config.schedulers</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p><a href="https://docs.victoriametrics.com/anomaly-detection/components/scheduler/" target="_blank">Scheduler section</a></p>
</td>
    </tr>
    <tr>
      <td>config.writer</td>
      <td>object</td>
      <td><pre lang="plaintext">
class: vm
datasource_url: ""
tenant_id: ""
</pre>
</td>
      <td><p><a href="https://docs.victoriametrics.com/anomaly-detection/components/writer/" target="_blank">Writer section</a></p>
</td>
    </tr>
    <tr>
      <td>config.writer.class</td>
      <td>string</td>
      <td><pre lang="">
vm
</pre>
</td>
      <td><p>Name of the class needed to enable writing to VictoriaMetrics or Prometheus. VmWriter is the default option, if not specified.</p>
</td>
    </tr>
    <tr>
      <td>config.writer.datasource_url</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Datasource URL address. Required for example <code>http://single-victoria-metrics-single-server.default.svc.cluster.local:8428</code> or <code>http://cluster-victoria-metrics-cluster-vminsert.default.svc.cluster.local:8480</code></p>
</td>
    </tr>
    <tr>
      <td>config.writer.tenant_id</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>For VictoriaMetrics Cluster version only, tenants are identified by accountID or accountID:projectID. See VictoriaMetrics Cluster multitenancy docs</p>
</td>
    </tr>
    <tr>
      <td>containerWorkingDir</td>
      <td>string</td>
      <td><pre lang="">
/vmanomaly
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>emptyDir</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>env</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td><p>Additional environment variables (ex.: secret tokens, flags)</p>
</td>
    </tr>
    <tr>
      <td>envFrom</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>extraArgs</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>extraContainers</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>extraHostPathMounts</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td><p>Additional hostPath mounts</p>
</td>
    </tr>
    <tr>
      <td>extraVolumeMounts</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td><p>Extra Volume Mounts for the container</p>
</td>
    </tr>
    <tr>
      <td>extraVolumes</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td><p>Extra Volumes for the pod</p>
</td>
    </tr>
    <tr>
      <td>fullnameOverride</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>global.compatibility.openshift.adaptSecurityContext</td>
      <td>string</td>
      <td><pre lang="">
auto
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>global.image.registry</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>global.imagePullSecrets</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>image.pullPolicy</td>
      <td>string</td>
      <td><pre lang="">
IfNotPresent
</pre>
</td>
      <td><p>Pull policy of Docker image</p>
</td>
    </tr>
    <tr>
      <td>image.registry</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Victoria Metrics anomaly Docker registry</p>
</td>
    </tr>
    <tr>
      <td>image.repository</td>
      <td>string</td>
      <td><pre lang="">
victoriametrics/vmanomaly
</pre>
</td>
      <td><p>Victoria Metrics anomaly Docker repository and image name</p>
</td>
    </tr>
    <tr>
      <td>image.tag</td>
      <td>string</td>
      <td><pre lang="">
v1.15.9
</pre>
</td>
      <td><p>Tag of Docker image</p>
</td>
    </tr>
    <tr>
      <td>imagePullSecrets</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>license</td>
      <td>object</td>
      <td><pre lang="plaintext">
key: ""
secret:
    key: ""
    name: ""
</pre>
</td>
      <td><p>License key configuration for vmanomaly. See <a href="https://docs.victoriametrics.com/vmanomaly#licensing" target="_blank">docs</a> Required starting from v1.5.0.</p>
</td>
    </tr>
    <tr>
      <td>license.key</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>License key for vmanomaly</p>
</td>
    </tr>
    <tr>
      <td>license.secret</td>
      <td>object</td>
      <td><pre lang="plaintext">
key: ""
name: ""
</pre>
</td>
      <td><p>Use existing secret with license key for vmanomaly</p>
</td>
    </tr>
    <tr>
      <td>license.secret.key</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Key in secret with license key</p>
</td>
    </tr>
    <tr>
      <td>license.secret.name</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Existing secret name</p>
</td>
    </tr>
    <tr>
      <td>nameOverride</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>nodeSelector</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>NodeSelector configurations. Details are <a href="https://kubernetes.io/docs/user-guide/node-selection/" target="_blank">here</a></p>
</td>
    </tr>
    <tr>
      <td>persistentVolume</td>
      <td>object</td>
      <td><pre lang="plaintext">
accessModes:
    - ReadWriteOnce
annotations: {}
enabled: false
existingClaim: ""
matchLabels: {}
size: 1Gi
storageClassName: ""
</pre>
</td>
      <td><p>Persistence to store models on disk. Available starting from v1.13.0</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.accessModes</td>
      <td>list</td>
      <td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
      <td><p>Array of access modes. Must match those of existing PV or dynamic provisioner. Details are <a href="http://kubernetes.io/docs/user-guide/persistent-volumes/" target="_blank">here</a></p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.annotations</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Persistant volume annotations</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.enabled</td>
      <td>bool</td>
      <td><pre lang="">
false
</pre>
</td>
      <td><p>Create/use Persistent Volume Claim for models dump.</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.existingClaim</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>Existing Claim name. If defined, PVC must be created manually before volume will be bound</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.matchLabels</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Bind Persistent Volume by labels. Must match all labels of targeted PV.</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.size</td>
      <td>string</td>
      <td><pre lang="">
1Gi
</pre>
</td>
      <td><p>Size of the volume. Should be calculated based on the metrics you send and retention policy you set.</p>
</td>
    </tr>
    <tr>
      <td>persistentVolume.storageClassName</td>
      <td>string</td>
      <td><pre lang="">
""
</pre>
</td>
      <td><p>StorageClass to use for persistent volume. Requires server.persistentVolume.enabled: true. If defined, PVC created automatically</p>
</td>
    </tr>
    <tr>
      <td>podAnnotations</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Annotations to be added to pod</p>
</td>
    </tr>
    <tr>
      <td>podDisruptionBudget</td>
      <td>object</td>
      <td><pre lang="plaintext">
enabled: false
labels: {}
minAvailable: 1
</pre>
</td>
      <td><p>See <code>kubectl explain poddisruptionbudget.spec</code> for more. Details are <a href="https://kubernetes.io/docs/tasks/run-application/configure-pdb/" target="_blank">here</a></p>
</td>
    </tr>
    <tr>
      <td>podMonitor.annotations</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>podMonitor.enabled</td>
      <td>bool</td>
      <td><pre lang="">
false
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>podMonitor.extraLabels</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>podSecurityContext.enabled</td>
      <td>bool</td>
      <td><pre lang="">
true
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>resources</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td></td>
    </tr>
    <tr>
      <td>securityContext</td>
      <td>object</td>
      <td><pre lang="plaintext">
enabled: true
runAsGroup: 1000
runAsNonRoot: true
runAsUser: 1000
</pre>
</td>
      <td><p>Ref: <a href="https://kubernetes.io/docs/tasks/configure-pod-container/security-context/" target="_blank">https://kubernetes.io/docs/tasks/configure-pod-container/security-context/</a></p>
</td>
    </tr>
    <tr>
      <td>serviceAccount.annotations</td>
      <td>object</td>
      <td><pre lang="plaintext">
{}
</pre>
</td>
      <td><p>Annotations to add to the service account</p>
</td>
    </tr>
    <tr>
      <td>serviceAccount.create</td>
      <td>bool</td>
      <td><pre lang="">
true
</pre>
</td>
      <td><p>Specifies whether a service account should be created</p>
</td>
    </tr>
    <tr>
      <td>serviceAccount.name</td>
      <td>string</td>
      <td><pre lang="">
null
</pre>
</td>
      <td><p>The name of the service account to use. If not set and create is true, a name is generated using the fullname template</p>
</td>
    </tr>
    <tr>
      <td>tolerations</td>
      <td>list</td>
      <td><pre lang="plaintext">
[]
</pre>
</td>
      <td><p>Tolerations configurations. Details are <a href="https://kubernetes.io/docs/concepts/configuration/assign-pod-node/" target="_blank">here</a></p>
</td>
    </tr>
  </tbody>
</table>

