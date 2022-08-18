# Databrydge Entry Exercise
### Intro
Databrydge is a company which facilitates connections through the clever use of API's, Proprietary models, serialization engine and much more. This exercise will test you on some of these features.

-----

### Practical Guidelines 
- You have an infinite amount of time to finish this exercise
- You can follow the build instructions to the letter but you are also allowed to deviate from the process, as long as the result is the same
- Build what you can build, skip what you can't, any % of completion is better than 0.
- Build the exercise in Git and share the repository with us when done
- Any comments or things we should know, can be shared with us in the readme of your repository
- Use of composer packages is allowed! Why re-invent the wheel right?


### Technical Requirements
- [ ] Fork this git repository
- [ ] Create a docker container, running the following services:
	- PHP Server with Symfony (`PHP 8.1` & `Symfony 6.1`)
	- MongoDB (`MongoDB 6.0`)
- [ ] Make sure the `export.csv` file from this repository is in your symfony project folder
- [ ] Create a homepage with a button -> `Read Data`
- [ ] When the button is clicked, the symfony application should do the following:
	- [ ] Read out the `.csv` data and group the lines by journal_id (see table for explanation below)
	- [ ] Create with the result data set the following **model** (`journalBooking`) : 
		- journalId (from `Journal_id`)
		- journalTransactionDate (from `Booked_at` convert to MongoDB Date object)
		- journalLines: (array holding following items)
			- code (from `Account_code`)
			- transactionFee (from `Debit` or `Credit`)
			- transactionType (if transactionFee -> `Debit` then transactionType = `Debit` otherwise transactionType = `Credit`)
	- [ ] Save the `.csv` data through use of the mentioned **model** to the MongoDB
- [ ] Make a simple table element on the homepage where you list the database entries
- [ ] Make the journalId clickable and make it navigate to a detailed page of the single database entry
- [ ] On this details page, list the object in it's entirety in a `<pre>` block in `json` format
- [ ] Making use of the `symfony/serializer` component grants bonus points! :wink:

### CSV Data


|Id|Journal_id|Account_code|Debit|Credit|Booked_at|
|--|----------|------------|-----|------|---------|
|20000|1110|XOQ97XWG4RB|$39.90|0|946637999|
|20001|1110|USF81BTC6TI|0|$39.90|946637999|
|20002|1111|XOQ97XWG4RB|$47.50|0|1591669200|
|20003|1112|XXA44JDI0OQ|0|$47.50|1591669200|
|20004|1112|XXA44JDI0OQ|$84.36|0|673308000|
|20005|1112|USF81BTC6TI|0|$0.666|673308000|
|20006|1112|XXA44JDI0OQ|$23.84|0|773486580|
|20007|1113|USF81BTC6TI|0|$23.84|773486580|
|20008|1113|FAKEACCOUNT|$60.70|0|773486580|


**Model Example**:
```json
{
	"journalId": 1110,
	"journalTransactionDate": "1999-12-31T23:59:59.000+00:00",
	"journalLines": [
		{
			"code":"XOQ97XWG4RB",
			"transactionFee": "$39.9",
			"transactionType": "Debit",
		},
		{
			"code":"USF81BTC6TI",
			"transactionFee": "$39.9",
			"transactionType": "Credit",
		}		
	]
}
```


That's all folks!
Good luck! If you finish this entire exercise you've definitely earned yourself a :cookie: or two :wink: