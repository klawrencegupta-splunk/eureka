<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <h2>ReadMe - Eureka 1.2</h2>
    <h3>Disclaimer:</h3>
    <p><u>This app is provided as part of a POC between Splunk our customers and
        is not an officially supported Splunk app</u>. All requests for support
      should be submitted to <a href="mailto:klawrencegupta@splunk.com">klawrencegupta@splunk.com</a>
      or to the GitHub repository.</p>
    <h3>Requirements</h3>
    <ul>
      <li>Splunk 7.3.x</li>
      <li>This app should run on the Monitoring Console as it will need access
        to all Splunk nodes in the deployment.</li>
    </ul>
    <h2>Dashboards</h2>
    <h3>Capacity Estimates</h3>
    <p><strong>Count of Hosts Selected </strong>- keeps a running total of the
      host count (selected in input) - <em>this can be used for sampling*</em></p>
    <p><strong>Ingest Potential Rate</strong> - Blended Across all Hosts ((core
      data based on Function + Time Resolution )</p>
    inputs along with Time Range picker to calculate a range of Indexer Ingest
    Rates using a Standard Deviation Percentile distribution of 50/60/70/80/90
    percentiles.
    <p>Functions Available:</p>
    <ul>
      <li>Average (default)</li>
      <li>Max</li>
      <li>Median</li>
      <li>Mode</li>
      <li>First</li>
      <li>Last</li>
    </ul>
    Time Resolution:
    <ul>
      <li>1h (default)</li>
      <li>30m</li>
      <li>15m</li>
      <li>5m</li>
      <li>1m</li>
    </ul>
    <h4>Example:</h4>
    Select the past 24 hours using the Time Range picker + Time Resolution of 1
    hour + Function is avg (average)
    <p>= the <strong>hourly</strong> <strong>average</strong> of the ingest
      rate over the <strong>past 24 hours</strong></p>
    <p><strong>Ingest Potential Rate: Per Host </strong>Standard Deviation
      Percentile distribution (core data based on Function + Time Resolution) by
      host</p>
    <p>= Same breakdown as the above example except by host </p>
    <strong>Ingest Pattern - Reads/Writes per-second</strong>
    <ul>
      <li>Reads/Writes per-second-rate over time based on the Time Range picker
        + Time Resolution + Function</li>
      <li>Overlay is the "Workload" or data.cpu_pct (_introspection)</li>
    </ul>
    <h3>Infrastructure Detailed Review</h3>
    <ul>
      <li><strong>Total vCPU Count</strong></li>
      <li>
        <meta charset="utf-8">
        <strong>Total vCPU found on host &amp; roles</strong><br>
        <meta charset="utf-8">
      </li>
      <li>CPU - Idle over Time Resolution</li>
      <li> Memory Utilization % over Time Resolution</li>
      <li> IOwait in ms by _time, type, mount_point - Trellis</li>
      <li>IO utilization in KB/s over time vs data.cpu_pct utilization | samples
        as time resolution rate using last(value) Trellis</li>
    </ul>
    <h3>Infrastructure Overview</h3>
    <ul>
      <li>CPU Utilization -- Minimum/Maximum/Average</li>
      <li>vCPU Info (Trellis by Host)</li>
      <li>CPU Health Summary (data.cpu_idle_pct)</li>
      <ul>
        <li>Using the drop downs available KPI ranges can be set for measuring
          CPU Activity in terms of low/moderate/critical (exhaustion) detected.
          Default values are:</li>
        <ul>
          <li>low&gt;85% idle</li>
          <li>moderate 15%&gt;&lt;85%</li>
          <li>critical &lt;15%</li>
        </ul>
      </ul>
      <li>Memory Health Status (<strong>data.mem_perc_util=round(('data.mem_used'/'data.mem')*100,2)</strong>)</li>
      <ul>
        <li>healthy&lt;90% </li>
        <li>critical&gt;90% - Memory Exhaustion</li>
      </ul>
      <li>Storage Health Status - <strong>(data.avg_total_ms by mount point)</strong></li>
      <ul>
        <li>Measures ranges of IOwait found in _introspection to provide a
          summary overview of storage latency distribution</li>
      </ul>
    </ul>
    <h3>Splunk Application Errors </h3>
    <ul>
      <li>Blocked Queues (Trellis)</li>
      <li> All Splunkd Errors/Warnings (sorted by highest count)</li>
      <li>CM Errors by Component</li>
      <li>LDAP Authentication Errors</li>
      <li>SHC Errors</li>
    </ul>
    <h3>Splunk Search Review</h3>
    <ul>
      <li>Search Concurrency Metrics </li>
      <li>Search Run Time statistics</li>
      <li>Timechart stack searches by type based on overall CPU utilization</li>
      <li>Top Searches Consuming CPU </li>
    </ul>
  </body>
</html>
