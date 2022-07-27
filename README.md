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


</details>


<details>
  <summary>diagram source</summary>
  This details block is collapsed by default when viewed in GitHub. This hides the mermaid graph definition, while the rendered image
  linked above is shown. The details tag has to follow the image tag. (newlines allowed)

```mermaid
graph LR
    A[README.md]
    B{Find mermaid graphs<br>and image paths}
    C[[docker mermaid-cli]]
    D[[docker mermaid-cli]]
    E(Graph 1 png image)
    F(Graph 2 svg image)

    A -->|passed to| B
    subgraph render-md-mermaid.sh
      B --> |path/to/image1.png<br>+mermaid source| C
      B --> |path/to/image2.svg<br>+mermaid source| D
    end
    C --> E
    D --> F
```
</details>

 