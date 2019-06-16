## 02 Design Question
- need to provide Google Analytic like services to our customers
- provide a high level solution design for the backend system
- free to choose any open source tools

## The system needs to:
 - [ ] handle large write volume: Billions write events per day.   
 - [ ] handle large read/query volume: Millions merchants want to get insight about their business. 
  Read/Query patterns are time-series related metrics.
 - [ ] provide metrics to customers with at most one hour delay.
 - [ ] run with minimum downtime.
 - [ ] have the ability to reprocess historical data in case of bugs in the processing logic
 
  
# reference documentation
  - [http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf](http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf)
  - [http://samza.apache.org/learn/documentation/0.7.0/jobs/reprocessing.html](http://samza.apache.org/learn/documentation/0.7.0/jobs/reprocessing.html)
  -  [https://www.infoworld.com/article/2868513/how-to-serve-billion-web-requests-per-day.html](https://www.infoworld.com/article/2868513/how-to-serve-billion-web-requests-per-day.html)
  - [https://hackernoon.com/building-a-system-to-deliver-billions-of-daily-events-c3a56be47fc2](https://hackernoon.com/building-a-system-to-deliver-billions-of-daily-events-c3a56be47fc2)
  - [https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)
  - [https://www.researchgate.net/publication/220673065_Historical_Data_Analysis_through_Data_Mining_From_an_Outsourcing_Perspective_The_Three-Phases_Model](https://www.researchgate.net/publication/220673065_Historical_Data_Analysis_through_Data_Mining_From_an_Outsourcing_Perspective_The_Three-Phases_Model)
  
# Base Assumtion

     + 1 billion write events, (86400 seconds a day, 1440 minutes a day, 24 hours a day).
     + assume paypay payments time series matrix volume explicit 
        - 20% one hour in the morning time (weekdays base)
        - 50% during one hour in the lunch time (weekdays base)
        - 30% during the day (except morning and lunch time) (weekdays base)
        - do not calculate weekends as weekend's volume expected lower than weekdaya's peak.
        
     + the peak time will be lunch time (50% portion) so 
        - assume 50% of daily write events taken place during the 1 hour lunch time = 0.5 billion 
        - 500,000,000 write events divide 3600 seconds (1 hour)= 138,888.888889 (events per second)
        - assume that system needs 138,889 event handler per second at least. 
        - according to research, "Visa does around 1,700 transactions per second on average 
           - "based on a calculation derived from the official claim of over 150 million transactions per day" 
           - so new system needs much faster performance than VISA.
        
      + paypay handles structured database as it is payment information.
        
        
# solution 
 + use Mongo DB 
	- [http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf](http://www.datastax.com/wp-content/themes/datastax-2014-08/files/NoSQL_Benchmarks_EndPoint.pdf)
 + use GraphQL instead of REST API to maximize read speed for analytics
 + use Kubernetes Engine to minimize downtime.
 + use Apache lucene (instead of Elastic Search)
    - payment information is more likely to structured database. 
    -  Elasticsearch is built over Lucene and provides a JSON based REST API to refer to Lucene features.
 + use D3.js for customer visualization when it come to build front side.
 