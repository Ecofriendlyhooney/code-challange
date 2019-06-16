# 02 Design Question
- need to provide Google Analytic like services to our customers
- provide a high level solution design for the backend system
- free to choose any open source tools

## The system needs to:

 - [ ] handle large write volume: Billions write events per day.
     -  [https://www.infoworld.com/article/2868513/how-to-serve-billion-web-requests-per-day.html](https://www.infoworld.com/article/2868513/how-to-serve-billion-web-requests-per-day.html)
     - [https://hackernoon.com/building-a-system-to-deliver-billions-of-daily-events-c3a56be47fc2](https://hackernoon.com/building-a-system-to-deliver-billions-of-daily-events-c3a56be47fc2)
     - 1 billion write events, 86400 seconds a day, 1440 minutes a day, 24 hours a day.
     - assume paypay payment system"s time series matrix volume explicit 
        - 20% one hour in the morning time (weekdays base)
        - 50% during one hour in the lunch time (weekdays base)
        - 30% during the day (except morning and lunch time) (weekdays base)
        
     - the peak time will be lunch time (50% portion) so 
        - 1 billion write events devide 24 hour = 41,666,666.6667 (events per hour)
        - 41,666,666.6667 write events devide 3600 seconds (1 hour)= 11,574.074074 (events per second)
        - assume that system needs 11,574 event handler per second at least. 
        - according to below article, "Visa does around 1,700 transactions per second on average (based on a calculation derived from the official claim of over 150 million transactions per day)"
        - [https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)
        - according to below BenchMarking result, MongoDB (with its horizontal scaling) will be the right choice. 
        - .  
        - [http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf](http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf)
        
     
 - [ ] handle large read/query volume: Millions merchants want to get insight about their business. 
  Read/Query patterns are time-series related metrics.
       - between lucene and ElasticSearch will be final round for query performance.
       - and I am going to choose lucene because of below reason
       
           - Elasticsearch is built over Lucene and provides a JSON based REST API to refer to Lucene features.
           - instead of REST API, use GraphQL.
           - database structure of paypay is more likely to structured data which is payment information.
           
       
        
       
 - [ ] provide metrics to customers with at most one hour delay.
 
 - [ ] run with minimum downtime.
        - use KUBERNETES ENGINE 
 - [ ] have the ability to reprocess historical data in case of bugs in the processing logic
 
 ## Solution
 
 
 #reference
  - fe
     - See [reprocess historical data](http://samza.apache.org/learn/documentation/0.7.0/jobs/reprocessing.html)
  

  - 
  - 
  