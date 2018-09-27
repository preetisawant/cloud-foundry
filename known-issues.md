---

copyright:
  years: 2018
lastupdated: "2018-09-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Known issues (limitations)
{: #known-issues}

## Instability due to high cpu usage by the firehose exporter

The Cloud Foundry firehose exporter that collects Cloud Foundry metrics in a CFEE instance may cause instability due to high cpu usage. You can reduce the load that drives the high cpu on the firehose exporter by filtering out http metrics.

To filter out http metrics collection:

1. Create the `config.yaml`:

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml.
   ```
   {: pre}
  
2. Edit the `config.yaml` and add the following line in ```spec.template.spec.containers.args``` array:

   ```
   - --filter.events=ContainerMetric,CounterEvent,HttpStartStop,ValueMetric          
   ```

### Example

Original `config.yam`:

```
  ...
  template:
  ...
    spec:
      containers:
      - args:
        ...
        - --doppler.metric-expiration=10m
        - --metrics.environment=IBM-Cloud-Foundry-Enterprise-Environment
        - --filter.events=ContainerMetric,CounterEvent,HttpStartStop,ValueMetric
        image: boshprometheus/firehose-exporter
```  

The following command would reconfigure and restart the worker node pod:

```
kubectl -n cf-monitoring apply -f config.yaml.

```
