# Description

This role configures [`smartctl_exporter`](https://github.com/prometheus-community/smartctl_exporter) tool to export [SMART metrics](https://en.wikipedia.org/wiki/Self-Monitoring,_Analysis_and_Reporting_Technology) for hard drives on the host.

# Configuration

The defaults are sane, but a basic config could include:
```yaml
smart_metrics_log_level: 'debug'
smart_metrics_log_format: 'logfmt'
smart_metrics_refresh_interval: '60s'
smart_metrics_listen_port: 9633
smart_metrics_listen_address: 0.0.0.0
smart_metrics_telemetry_path: '/metrics'
```
Optionally you can specify list of devices to monitor:
```yaml
smart_metrics_smartctl_devices: ['/dev/sda']
```
Or include and exclude rules:
```yaml
smart_metrics_smartctl_devices_exclude: 'vd.*'
smart_metrics_smartctl_devices_include: 'sd.*'
```

# Usage

You can just query the `/metrics` endpoint:
```
 > curl -s localhost:9633/metrics | grep smartctl_device_media_errors
# HELP smartctl_device_media_errors Contains the number of occurrences where the controller detected an unrecovered data integrity error. Errors such as uncorrectable ECC, CRC checksum failure, or LBA tag mismatch are included in this field
# TYPE smartctl_device_media_errors counter
smartctl_device_media_errors{device="sda"} 0
```
