# mermaind-playground


<details>
    <summary>Download Report</summary>
    
    
    
``` mermaid
    graph TB
    User((User)) -- Publish --> Downloader_Queue
    Downloader_Queue{{Downloader_Queue}} -- Trigger --> downloadTransaction\nReport
    
    subgraph BPI_Controller[" "]
        direction TB
        downloadTransaction\nReport --> |crawl| BPI_WEBSITE
        BPI_WEBSITE --> crawling{isSuccess?}
        
        crawling -- Yes --> formatToZipAndUploadToS3
        crawling -- No --> Catch_Error
        
        formatToZipAndUploadToS3 --> uploaded{isSuccess?}
        uploaded -- Yes --> publishReportResult
        
        uploaded -- No --> Catch_Error
        Catch_Error -- Trigger --> publishReportResult
        Catch_Error -- Publish --> publishToSentry
    end
    
    publishReportResult -- Publish --> Report_Queue{{Report_Queue}}
    publishToSentry -- Publish --> Sentry{{Sentry}}
```   