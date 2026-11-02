# [G7]team Dashboard

Node monitoring dashboard for Prometheus and node_exporter, migrated from Grafana
8 to the Grafana dashboard JSON schema 42. Validated on Grafana 13.3.0.

## Import

1. In Grafana, open **Dashboards → New → Import** and upload `dashboard.json`.
2. Open the imported dashboard and select your Prometheus source in **Data source**.
3. Select a **Node** and the desired time range.

The source can have any name or UID. It must be a working Prometheus data source
that scrapes node_exporter. For file provisioning, provision the Prometheus source
separately and point a dashboard provider at this JSON file. The same source
selector works with both UI import and file provisioning.

The existing queries expect the labels `origin_prometheus` and `label`, in
addition to the usual `job` and `instance`. `label` identifies the node displayed
in the Node selector. Configure these in Prometheus target labels/relabeling if
they are not already present. Disk panels select ext/xfs filesystems; overlay
filesystems do not appear in those panels.

## Migration

The dashboard preserves the 20-panel layout, all 71 PromQL expressions, units,
thresholds, and existing dashboard UID. It uses built-in Table, Time series, Stat,
and Bar gauge panels; external or Angular panel plugins are not required.

Updated configuration includes typed data source references at panel and query
level, current table `cellOptions` (including gradient backgrounds), explicit
legend visibility, Prometheus query modes, and string-valued refresh settings.
Obsolete export metadata and cached selections of the original servers have
been removed. The dashboard ID is unset so it can be imported into another
Grafana instance.
