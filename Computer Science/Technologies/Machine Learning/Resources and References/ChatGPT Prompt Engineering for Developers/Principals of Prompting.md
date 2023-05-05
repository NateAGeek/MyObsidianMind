## Principal 1: Write Clean Instructions
Provide clear instructions for the prompt to best follow.

#### Clear and Specific Instructions
Writing as many details for the AI to use is important. Short is not always clean, and giving as much data for the model to interpret and understand helps allow the model to generate full fledge details. 

#### Specifications
Clear with domains of focus. Giving the model some structure of data with delimiter, like \`\`\` or """ can help give context of what to focus on and use.

These also can prevent prompt injects. By properly creating fixed delimiters you can prevent prompt injections that could lead the user entering more details and instructions outside of the context of your instructions. Thus preventing possible exploits. 

#### Requesting Formats are Useful
You can request different formats of data, such as json or html. 

#### Check if conditions are met is a useful technique
Giving a model a condition that it must follow, with a fallback option if it can not attempt it. Is useful as it will prevent the model from trying too hard, and possibly not giving accurate results, and just fallback to a defined parameter. 

#### Few Shot Prompting
Giving examples of doing successful attempts before prompting it for further details. Kinda like giving it some mini training before asking for a full result can be useful.

## Principal 2: Time to Think
Make the model the ability to longterm plan and execute tasks. This gives the simulation of thinking of actions to follow and then come up with a conclusion.

#### Specify the steps required to complete a task
```
Perform the following actions: 
1 - Summarize the following text delimited by triple \
backticks with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
keys: french_summary, num_names.
```
Example of pushing model to describe the steps and then lead to a conclusive answer

```
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in Italian summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
```
This is an example that has more stable template. 
#### Instruct the model to work out its own solution before rushing to a conclusion
Asking the model to give more clear step by step solutions to push the model to explain its reasoning before giving the final solution can lead to a more accurate answer. This can actually prompt the next series of words to be more correct.

### Hallucinations 
It is important to make sure you pay attention to the data being outputted by the model. It can sometimes come up some fake companies, ideas, or names. You can kinda get around this by requesting the model determines its own source for the information and tracing that to validate the model is correct. 

