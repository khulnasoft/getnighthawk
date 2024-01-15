---
layout: docs
title: Running Performance Tests
section: "Performance Benchmarking"
---

[Meshery](https://meshplay.io/) uses Nighthawk as one of its load generators to run performance benchmarking. Meshery is the canonical implementation of [Service Mesh Performance](https://smp-spec.io/), CNCF's service mesh performance benchmarking specification.
<br/>

## Performance Benchmarking Using meshplayctl

`meshplayctl` is the command line interface of Meshery. `meshplayctl` along with other load generators,  `meshplayctl` can use Nighthawk to run performance benchmarks.
<br/>

## Install meshplayctl

Check this [quick start guide](https://meshplay.io/#getting-started) on how to install meshplayctl.

```
meshplayctl -h
```

```
Meshery is the service mesh management plane, providing lifecycle, performance, and configuration management of service meshes and their workloads.

Usage:
  meshplayctl [command]

Available Commands:
  app         Service Mesh Apps Management
  completion  generate the autocompletion script for the specified shell
  exp         Experimental commands for meshplayctl
  help        Help about any command
  mesh        Service Mesh Lifecycle Management
  pattern     Service Mesh Patterns Management
  perf        Performance Management
  system      Meshery Lifecycle Management
  version     Version of meshplayctl

Flags:
      --config string   path to config file (default "/Users/navendu/.meshplay/config.yaml")
  -h, --help            help for meshplayctl
  -v, --verbose         verbose output

Use "meshplayctl [command] --help" for more information about a command.
```
<br/>

## Run a performance test

See [this guide](https://docs.meshplay.io/reference/meshplayctl#service-mesh-performance-management) for reference to meshplayctl commands.

The command below runs a performance benchmark test with Nighthawk with the test configuration provided through flags.

```
meshplayctl perf apply --profile istio-soak-test --concurrent-requests 1 --duration 15s --load-generator nighthawk --mesh istio --url http://localhost:2323
```

<br/>
You can also run performance tests with SMP compatible test configuration files like the one shown below.

```yaml
smp_version: v0.0.1
id: d3ac6bf7-e35e-40c0-8669-5e13c9657286
name: istio-soak-test
labels: {}
clients:
- internal: false
  load_generator: nighthawk
  protocol: 1
  connections: 2
  rps: 10
  headers: {}
  cookies: {}
  body: ""
  content_type: ""
  endpoint_urls:
  - http://localhost:2323
duration: "15s"
```

You can then use `meshplayctl` to run the test using this configuration file as shown below.

```
meshplayctl perf apply -f perf-test.yaml
```

Check the [Meshery usage guides](https://docs.meshplay.io/guides) for more information on running performance benchmarks.
