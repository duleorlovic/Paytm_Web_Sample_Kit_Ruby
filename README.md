# How to install the sample kit on a web server:
1. Copy the 'samplekit' folder in document root of your server (like /var/www/html)
2. The 'samplekit' folder is having the following files:
 - TxnTest.html - Testing transaction through Paytm gateway.
 - generate_checksum.rb - This file has the logic of checksum generation and passing all required parameters to Paytm PG.
 - verify_checksum.rb - This file has the logic for processing PG response after the transaction processing.
 - paytm/encryption_new_pg.rb - This is the library file.
3. Open generate_checksum.rb file from the folder and update the below values (these can be downloaded from the Paytm portal. One time downloadable).
 - PAYTM_MERCHANT_KEY = ""
 - WEBSITE = ""
 - MID = ""
 - INDUSTRY_TYPE_ID = ""
 - CHANNEL_ID = ""
4. Provide the required values by running the TxnTest.html file and click on the 'submit' button to process a test transaction.

# To generate checksum in Ruby :
1. Create an associative array with key value pair of following paytm parameters 
(MID, ORDER_ID, CUST_ID, INDUSTRY_TYPE_ID, CHANNEL_ID, TXN_AMOUNT, EMAIL, WEBSITE)
2. To generate checksum, call the following method. This function returns the checksum as a string.
new_pg_checksum(paytmparams, merchant key).gsub("\n",'') where,
 - 'paytmparams' is an associative array containing Paytm parameters.
 - 'merchant key' is the Paytm Merchant Key provided by Paytm.

# To verify checksum in Ruby:
1. Get all the parameters received from Paytm and put them in an associative array (“key => value” pair).
2. Get the CHECKSUMHASH parameter value received from Paytm store in a variable and remove the parameter from the array 
3. To verify checksum call the following function. This function returns a Boolean (true/false)
new_pg_verify_checksum(paytmparams, check_sum, merchant_key) where,
- 'paytmparams': is a parameter array which was created in step 1 of this section (NOTE: Do not include the CHECKSUMHASH parameter)
- 'check_sum' : Is the CHECKSUMHASH parameter as received in step 2.
- 'merchant_key': Is the merchant key received from Paytm

# To generate refund checksum in Ruby :
1. Create an associative array with key value pair of following paytm parameters 
(MID, ORDERID, TXNTYPE, REFUNDAMOUNT, TXNID, REFID)
2. To generate checksum, call the following method. This function returns the checksum as a string.
new_pg_refund_checksum(paytmparams, merchant key).gsub("\n",'') where,
 - 'paytmparams' is an associative array containing Paytm parameters.
 - 'merchant key' is the Paytm Merchant Key provided by Paytm.
