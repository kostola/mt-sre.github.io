---
title:  Plug and Play Addon
linkTitle: Plug and Play Addon
---

## Package

For each addon that has `packageOperator` defined in its `spec`, a
ClusterObjectTemplate[https://package-operator.run/docs/getting_started/api-reference/#clusterobjecttemplate].
The average user does not need to interact with the `ClusterObjectTemplate`; they will interact with the resultant
ClusterPackage[https://package-operator.run/docs/getting_started/api-reference/#clusterpackage] that is created.

The `ClusterPackage` manifest will look like this:

```shell
apiVersion: package-operator.run/v1alpha1
kind: ClusterPackage
metadata:
  name: <addon_name>
spec:
  image: <addon.spec.packageOperator>
   config:
    addonsv1:
      clusterID: a440b136-b2d6-406b-a884-fca2d62cd170
      deadMansSnitchUrl: https://example.com/test-snitch-url
      ocmClusterID: abc123
      ocmClusterName: asdf
      pagerDutyKey: 1234567890ABCDEF
      parameters:
        foo1: bar
        foo2: baz
      targetNamespace: pko-test-ns-00-req-apy-dsy-pdy
```

The `deadMansSnitchUrl` and the `pagerDutyKey` come from the `configMap`s with the default names in the default
locations
documented in
the [addons deadMansSnitch](https://mt-sre.github.io/docs/creating-addons/monitoring/deadmanssnitch_integration/)
and
the [addons pagerDuty documentation](https://mt-sre.github.io/docs/creating-addons/monitoring/pagerduty_integration/)
respectively. *To have these values inject you must maintain the default naming scheme and location of these configMaps*
.

All the values in `.spec.config.addonsv1` can be injected into the objects contained in your packageImage. See the
[package operator documentation](https://package-operator.run/docs/guides/packaging-an-application/#go-templates) to see
how to do this.
