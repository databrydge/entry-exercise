# Databrydge Applicant's Exercise
### Intro
Databrydge is a company which facilitates connections through the clever use of API's, Proprietary models, serialization engine and much more. This exercise will test you on some of these features.

-----

### Practical Guidelines 
- You have an infinite amount of time to finish this exercise,
- You can follow the build instructions to the letter but you are also allowed to deviate from the process, as long as the result is the same,
- Build what you can build, skip what you can't, any % of completion is better than 0,
- Build the exercise in Git and share the repository with us when done,
- Any comments or things we should know, can be shared with us in the readme of your repository,
- Use of composer packages is allowed! Why re-invent the wheel right?,


### Technical Requirements
- [ ] Fork this git repository,
- [ ] Create a docker container, running the following services:
	- PHP Server with Symfony (PHP `8.1` & Symfony `6.1`)
	- MongoDB (MongoDB `6.0`)
- [ ] Make sure the `transactionBatch.csv` file from this repository is in your symfony project folder
- [ ] Create a homepage with a button -> "Read data"
- [ ] When the button is clicked, the symfony application should do the following:
	- [ ] Read out the csv data and group the lines by Transaction_id (see table for explanation below)
	- [ ] Create with the result data set the following **model** (`salesTransaction`) : 
		- transactionId (from `Transaction_id`)
		- customerId (from `Customer_id`)
		- transactionLines: (array holding following items)
			- generalLedgerAccountId (from `General_ledger_account_id`)
			- amount (from `Debit` or `Credit`)
			- type (if amount -> `Debit` then transactionType = `Debit` otherwise transactionType = `Credit`)
			- date (from `Transaction_date` convert to MongoDB Date object)
	- [ ] Save the csv data through use of the mentioned **model** to the MongoDB
- [ ] Make a simple table element on the homepage where you list the database salesTransactions
- [ ] Make the transactionId clickable and make it navigate to a detailed page of the single database entry
- [ ] On this details page, list the object in it's entirety in a `<pre>` block in `json` format
- [ ] Making use of the `symfony/serializer` component grants bonus points! :wink:

### CSV Data


|Batch_id|Transaction_id|Customer_id|General_ledger_account_id|Debit|Credit|Transaction_date|
|--|--|----------|------------|-----|------|---------|
|1|2270001|C1000|1300|$39.90|0|946637999|
|1|2270001|C1000|8000|0|$39.90|946637999|
|1|2270002|C1001|1300|$47.50|0|1591669200|
|1|2270002|C1001|8001|0|$45.50|1591669200|
|1|2270002|C1001|8002|$2.00|0|1591669200|
|1|2270003|C1002|1300|0|$51.00|673308000|
|1|2270003|C1002|8001|$51.00|0|673308000|
|1|2270004|C1000|1300|$23.84|0|773486580|
|1|2270004|C1000|8000|0|$23.84|773486580|



**Model Example**:
```json
{
	"transactionId": 2270001,
	"customerId":"C1000",
	"transactionLines": [
		{
			"generalLedgerAccountId":"1300",
			"amount": "$39.90",
			"type": "Debit",
			"date": "1999-12-31T23:59:59.000+00:00"
		},
		{
			"generalLedgerAccountId":"8000",
			"lineAmount": "$39.90",
			"lineType": "Credit",
			"date": "1999-12-31T23:59:59.000+00:00"
		}		
	]
}
```


That's all folks!
Good luck! If you finish this entire exercise you've definitely earned yourself a :cookie: or two :wink:



------





..... Too easy for you? 😠 Would you like a challenge?
- [ ] Add an upload functionality so any csv with the same formatting can be uploaded to your symfony server
- [ ] Add in a crud system for the entries, using symfony's API-Platform component, make an entry into an ApiResource
- [ ] Remove MongoDB, instead use relational MySQL tables each with their own models
- [ ] Add FK, Dependancies and let them be reflected in the Models
- [ ] Use Symfony Messenger component to read out tasks from a newly added RabbitMQ Queue in your docker
- [ ] Add files that were uploaded into a new queue called "tooEasy" and process them
- [ ] Add a duplicate check for files and the data within, gone with those pesky duplicated rows!
- [ ] Make the API Platform of symfony reachable with an OAuth flow in your symfony environment
- [ ] Add in a logging system, whenever anything goes wrong or something goes right, log it to a SQL table and allow for a page to list, detail & remove the logs!
