# mermaind-playground


<details>
    <summary>Download Report</summary>
    
```mermaid
    flowchart TB
    User -- Publish --> Downloader_Queue
    Downloader_Queue -- Trigger --> downloadTransaction\nReport
  
    
    publishReportResult -- Publish --> Report_Queue
    publishToSentry -- Publish --> Sentry

```

</details>


