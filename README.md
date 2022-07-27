# mermaind-playground


<details>
    <summary>Download Report</summary>
    
    
    
``` mermaid
    graph TB
    User((User)) -- Publish --> Downloader_Queue
    Downloader_Queue{{Downloader_Queue}} -- Trigger --> downloadTransactionReport
    
    subgraph BPI_Controller[" "]
        direction TB
        downloadTransactionReport --> |crawl| BPI_WEBSITE{{BPI_WEBSITE}}
        BPI_WEBSITE --> crawling{isSuccess?}
        
        crawling -- Yes --> formatToZipAndUploadToS3
        crawling -- No --> Catch_Error
        
        formatToZipAndUploadToS3 --> uploaded{isSuccess?}
        uploaded -- Yes --> publishReportResult
        
        uploaded -- No --> Catch_Error
        Catch_Error -- Trigger --> publishReportResult
        Catch_Error -- Trigger --> publishToSentry
    end
    
    publishReportResult -- Publish --> Exchange_Route{{Exchange_Route}}
    publishToSentry -- Publish --> Sentry{{Sentry}}
```   