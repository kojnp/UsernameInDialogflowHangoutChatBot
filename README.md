# UsernameInDialogflowHangoutChatBot
Shows how to get the user name in a Hangouts Chat bot using Dialogflow

Adding this since the documentation is not that clear, may help other people.

[Hangouts Chat message format](https://developers.google.com/hangouts/chat/reference/message-formats/events#event_types)

```
exports.dialogflowFirebaseFulfillment = functions.https.onRequest((request, response) => {
  const agent = new WebhookClient({ request, response });
  console.log('Dialogflow Request headers: ' + JSON.stringify(request.headers));
  console.log('Dialogflow Request body: ' + JSON.stringify(request.body));
  var name=request.body.originalDetectIntentRequest.payload.event.user.displayName;
  console.log('user name: ' + name);
  const parameters = { // Custom parameters to pass with context
      name: name,
    };
  agent.setContext({name:'welcome-context', lifespan:5, parameters:parameters});
  
  function welcome(agent) {
    agent.add(`Welcome to my agentx!`);
	agent.add('Your name is ' + agent.getContext('welcome-context').parameters.name);
  }
  ```
  ![alt](https://storage.googleapis.com/other-public/screenshot.png)
  ![alt](https://storage.googleapis.com/other-public/code.png)

  
reading [source](https://github.com/dialogflow/dialogflow-fulfillment-nodejs/blob/master/src/dialogflow-fulfillment.js#L348) seems context is deprecated . Will figure out an alternative when time permits.
