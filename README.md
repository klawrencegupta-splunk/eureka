<html>
  <body>
    <h1>Read Me - Eureka 1.2.5 - a Monitoring Console Companion application with Focus on Infrastructure Health & Splunk capacity</h1>
    <p>This app is provided by Kate Lawrence-Gupta and is not support by Splunk.
      Please report all issues to https://github.com/klawrencegupta-splunk/sdrt/issues</p>
  <h1> List of Dashboards available</h1>
    <h2>Capacity Estimates (experimental)</h2>
    <ul>
      <li>Ingest Pattern by Function - Reads/Writes
        MB/per-second + overall Workload</li>
      <li>Reads/Writes MB/per-second and Workload (CPU Storage
          Utilization) </li>
      <ul>
        <li>Reads/Writes MB/per-second-rate over time based on the Time
          Range picker + Time Resolution + Function | Overlay is the "Workload"
          or data.cpu_pct (_introspection)</li>
      </ul>
      <li> Ingest Potential Rate - Blended  Across
          ALL Indexers </li>
      <ul>
        <li>-- (core data based on Function + _time )</li>
        <li>This represents a per-Indexer "score" or in other words:
          prediction of the 24-hour processing capacity of an indexer(s) given
          the current ingest pattern utilization and extrapolated over time. The
          basic idea here is to set a target ingestion rate for the environment
          using on CPU/Memory/Store as KPIs for an initial capacity measurement.</li>
      </ul>
      <li>Ingest Potential RateIndividual Hosts </li>
      <ul>
        <li>-- (core data based on Function + _time )</li>
        <li>Extrapolated GB/day indexer score using a STDEV (50/60/70/80/90)
          percentiles grouped by GB/day rating</li>
      </ul>
    </ul>
    <p> </p>
    <h2>Infrastructure Detailed Review</h2>
    <ul>
      <li>Total vCPU Count</li>
      <li>Total vCPU count by host</li>
      <li>CPU Utilization -- Minimum/Maximum/Median</li>
      <li>CPU - Idle% over Time Resolution</li>
      <li>Memory Utilization % over Time Resolution</li>
      <li>IO utilization in KB/s over time vs data.cpu_pct utilization </li>
      <ul>
        <li>samples as time resolution rate using last(value) data.cpu_pct is
          the amount of time the server spent processing storage requests: </li>
        <li>As the workload approaches 100% fewer resources are available to
          process storage requests (ingest/search) at the host.</li>
      </ul>
      <li>IOwait in ms by _time, type, mount_point</li>
      <ul>
        <li>Charts provide the Average/Median/Perc95 and Max IOwait using the
          time resolution selected over the total time available in the diag
          file. </li>
        <li>Values exceeding <b>5-10ms</b> are a key performance indicator
          (KPI) that storage contention has been found on the host.</li>
      </ul>
    </ul>
        <h2>SmartStore Analysis - (beta)</h2>
    <ul>
      <li>SmartStore Activity in KB/Elapsed_ms into MB/elapsed time in seconds by action -- overall blended time scale</li>
      <li>SmartStore Activity by Time Elapsed by Action in MS</li>
      <li>MBps by SmartStore operations (relative to job/event activity)</li>
      <li>Remote Downloads in GB by Index **  Note: index for regular expression may not match your deployment ** </li>
      <li>Remote Bucket GB Downloads by Index ** Note: index for regular expression may not match your deployment ** </li>
      <li>Local Evictions by Index in total seconds spent</li>
      <li>Sums by S2-Index, action, files (activity)
      </ul>
    <h2>Splunk Application Errors</h2>
    <ul>
      <li>Queue Status By Host - % of fill for each queue by host</li>
      <li>Counts of ERROR/ WARN/ INFO by Component</li>
      <li>DrillDown and Filter into All Splunkd ERROR/ WARN/ INFO by Component
      </li>
      <ul>
        <li>gives the event_message and is sorted by highest count</li>
      </ul>
    </ul>
    <h2> Splunk Application Errors</h2>
    <ul>
      <li> Search Concurrency Metrics *multiple selection is touchy*</li>
      <ul>
        <li>Search Concurrency is defined as the total # of vCPUs + 6 base
          searches. </li>
        <li>If you are running in a SHC it will be each of those nodes vCPUs + 6
          base searches to equal your overall base search capacity. </li>
        <li>Your search concurrency is the # of searches you are running at that
          time (ad-hoc/scheduled/etc). If your search concurrency exceeds your
          available search capacity then you will see searches start to queue
          or be skipped.</li>
      </ul>
      <li>Search Run Time Distribution by SH and peers (experimental)</li>
      <ul>
        <li>Sample Set is measured in hours/days + peer count (metrics.log) -
          average runtime is extrapolated into cumulative run hours per Indexer
          (theoretical)</li>
      </ul>
      <li>Timechart stack searches by search type based on overall CPU
        utilization</li>
      <ul>
        <li>This chart tracks a stacked amount of CPU utilization by search
          types - this indicates the where the search activity is being directed</li>
      </ul>
      <li>Top 10 Saved Searches Consuming CPU sorted by highest CPU Utilization</li>
      <ul>
        <li>Split-By available for app, label, proveance, user and type of
          search</li>
        <li>Sort-By available for CPU Utilization, Writes (MB), Reads (MB)</li>
      </ul>
    </ul>
  </body>
</html>
