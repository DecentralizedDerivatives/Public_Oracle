# Public Oracle

This repository creates a public Oracle for price feeds from an API using Oraclize.  The value is set as the daily value measured by the first call of the day.  


The contract can be tested easily using the Oraclize Remix IDE.  

http://dapps.oraclize.it/browser-solidity


## DAPP Oracle

The DRCT contracts live on the DApp at http://drct.decentralizedderivatives.org uses this public oracle contract referencing the GDAX BTC/USD API at https://api.gdax.com/products/BTC-USD/ticker

DDA will perform daily Oracle calls on contract start/end dates however in the event DDA is unable to make the calls, it is the responsibility of the parties to make the Oracle on the contract end date.

### How it works

Any party can call query the API and store the data by calling the PushData function:

        Oracle.PushData();
        
 
The contract stores the first Oracle call of each day using the daily GMT Unix timestamp (e.g. 1/23/2018 00:00:00 GMT stores as 1516665600), calculated in solidity as:

        key = now - now % 86400;
        
Any further calls in the day will fail.  

To query the data, users can call the retrieve data function with the corresponding datestamp (key)

        RetrieveData(key);
