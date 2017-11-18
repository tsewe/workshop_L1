Budget Tool with React Bootstrap

Prerequisites
1. Install nodejs : https://nodejs.org/en/download/ . Nodejs is a server for our case study.
2. (Recommended) Install Visual Studio Code (VSC): https://code.visualstudio.com/download.
You can develop in any favourite editor or IDE, but also learn about VSC, which has some fancy features
making development in Javascript attractive.
3. (Recommended) Download Chrome web browser. Enable debugging in VSC with the support of
Chrome web browser : https://code.visualstudio.com/docs/editor/debugging
4. Run in the root folder of the project : npm install (In VSC you can do it from an integrated terminal : View->Integrated Terminal).
This will download all needed dependencies for the project.
5. Run in the root folder of the project : npm start
This will start the application and open it in your default web browser

Workshop tasks
1. Validation is not perfect in the app. Improve it. When introducing new validations, just save the source code and see how nodejs
refreshes the application status in the browser automatically. Try adding new participants when working on validations. Testing this
will be helpful for solving problem number 2.
	a) Currently, a phone number can be any text. By using a proper function from 'libphonenumber-js' library add validation
	inside "handleAddParticipant" function of CreateSplitView.js. Take care of validation message everywhere in the code where necessary.
	See examples of existing validations in CreateSplitView.js.
	hints : 
		to add a dependency to the project -> npm install <library_name> --save
		to import a library -> see existing imports in CreateSplitView.js
		libphonenumber-js code snippets : 
			https://www.npmjs.com/package/libphonenumber-js#usage
			https://www.npmjs.com/package/libphonenumber-js#isvalidnumberparsed_number
	b) Participant contribution can be any text. Add validation, so that only positive number or 0 will be allowed 
	hints : 
		look for javascript built-in functions helping with checking if something is a number.
	c) "this.state.amount" and "this.state.myContribution" also need validation improvements. They should be only of positive value.
	"this.state.amount" can't be 0, while "this.state.myContribution" can.
	hints : 
		The logic responsible for validations of these two fields should be inside "handleCalculate" function in CreateSplitView.js

2.	Probably you noticed (if not, this is ok too) when testing addition of participants and changing validations, that when the source code is saved and the app
refreshed in the browser, the previously added participants disappear from the list at the bottom of the page. This happens, because
during mounting the CreateSplitView component, that extends Component object from React library, does not load the saved data. This is
a bug! Fix it, so that this data will be loaded before the function "render" is called in the lifecycle of the component.
How to reproduce the bug : 
	1. Add new participants
	2. When adding second participant, provide wrong value in validated fields
	3. Try to add this second participant and tigger a validation message
	4. Add anywhere in the source code of CreateSplitView.js a comment : /* some comment */
	5. Save CreateSplitView.js and see how the page after refresh looses participants from the list
	6. Adding new participant without validation errors shows all participants again
	hints : 
		to find a proper method to place the fix in -> https://reactjs.org/docs/react-component.html
		"this.state.allParticipants" needs to be set after loading the data from "localStorage". Look for the way data is retrieved
		from localStorage and allParticipants are set. Examples already exist in CreateSplitView.js. To set a value in state object
		you can use this.setState({ <key> : <object> }); , where values in "<...>" brackets should be replaced by you properly (together
		with these brackets).
				
3.	After successful providing of the contribution data of all participants we press "Calculate" button and get to the page with the
summary of costs and information on who owes whom the money. The way this data presentation is programmed (strings concatenation)
is not flexible and to make development easier and friendly to other devs who might work with this code in future you should change
it to a tabelaric way of presentation. Change the contribution data and costs data to be displayed as tables.
	hints :
		https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects
		Add a new function to ExpensesView.js, which will accept four parameters in input : 
			sourceUser (user who either owes someone money or gets money from the pool),
			action (text describing the activity happening. Either owning or getting money),
			destinationUser (either user who receives money from other user or hardcoded value "the pool"),
			amount (the amount necessary to be transfered).
		This function should construct an object with four properties storing parameter values from the input and return this object.
		Modify "result.push(...)" calls to use your newly added function instead of a concatenation of strings.
		See "Participants overview" table source in CreateSplitView.js for an example on how to construct the data for the table body.
	
	