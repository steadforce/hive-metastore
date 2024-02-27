# Trino

Repository containing manifests for
[hive](https://hive.apache.org/)
installation. Never install the content of this repo on our clusters manually. This is all done by argo-cd.

## Dependencies

This chart has no dependencies yet specified in `Chart.yaml` in the `dependencies` section.
If you add dependencies, you need to then run

    $ helm dependency update

in order to have the chart downloaded to the `charts` directory
and then also commit that new version alongside with the altered
`Chart.yaml` file.

See the [Helm docs](https://helm.sh/docs/topics/charts/#chart-dependencies)
for details.


## Render helm charts locally

The following command renders the charts like argo-cd does to validate the content.

### local

```
 helm template --release-name hive-metastore -n hive-metastore --skip-tests \
  -a acid.zalan.do/v1 \
  --output-dir _render/local . 
```


You can use this command to check if the output is as you expect. The `-a` parameters are needed since we use the
helm feature `.Capabilities.APIVersions.Has` to determine if a `CR` is installable in the cluster or not. Since
helm templating is designed to work offline we have to list the supported `CR`. Using `.Capabilities.APIVersions.Has`
feature in templating prevents sync errors in argo-cd if a `CR` can't be applied since its `CRD` isn't ready.
