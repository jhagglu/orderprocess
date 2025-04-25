# Vendor_CustomOrderProcessing

## 🔧 Installation

```bash
bin/magento module:enable Vendor_CustomOrderProcessing
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento cache:flush


## REST API Endpoint

Method - POST
store_url/rest/V1/order/status/update
{
  "incrementId": "100000123",
  "status": "shipped"
}

##  Steps to Test Package

Generate admin token using below end point using magento admin username,password
 Step-1   curl -X POST "http://storeurl/rest/V1/integration/admin/token" \
	     -H "Content-Type: application/json" \
	     -d '{"username":"admin", "password":"admin123"}'

Step-2 Use token generated from step 1 in below request and use incrementId from any test order
	curl -X POST "http://storeurl/rest/V1/order/status/update" \
	-H "Content-Type: application/json" \
	-H "Authorization: Bearer <your-token-here>" \
	-d '{
	  "incrementId": "2000671687",
	  "status": "shipped"
	}'
	
	
## Architectural Decisions

Used Magento 2 latest standard to achieve this task.

Used repository pattern for updating orders.

Observer logs status changes in custom table 'vendor_order_status_log'.

Email is triggered only when status is changed to "shipped".

Uses dependency injection everywhere – no ObjectManager.

PSR-4 autoloading compliant.
