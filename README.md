# InsiderTrading

While Insider Trading cases are very complex and can be indicated to some extent by different metrics, a basic assumption I have made for the purpose of this project is that huge, anomalous trades that coincide with a large percentage change in share price may be indicative of insider trading.

## Data

I considered the 2021 data for two companies – Yes Bank and Infosys 
For each company I obtained raw data from the NSE website, that contained many columns such as Low Price, High Price, Total Turnover, Total Deliverable Quantity, etc. but I considered four relevant attributes – Date, Open Price, Close Price, and Total Traded Quantity. 

## Calculations

i) In order to identify huge anomalous trade, I used an attribute (TTQ dev from mean) that measures the deviation of a particular day’s trade, from the average daily trade (TTQ_avg) for the year.  

I calculated these as: 

TTQ_avg = mean (Total Traded Quantity)  
TTQ Dev from Mean % = ((Total Traded Quantity – TTQ_avg) / TTQ_avg) * 100  

ii) In order to identify large change in share price, I calculated the percentage difference in Close Price and Open Price:  
Change in Share Price % = ((Close Price – Open Price) / Open Price) * 100  

iii) I then used a metric (Correlation) that indicates how suspect the case is. I calculated this as multiplication of the above two attributes.  
Correlation = (TTQ Dev from Mean % * Change in Share Price %)  / 10^4  

I considered a Correlation greater than 0.15 as a suspect case.   
I transferred the suspect cases to a new DataFrame and sorted the cases in decreasing order of Correlation.  

