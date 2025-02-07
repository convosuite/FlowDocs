# How to Use

#### 1 - Invite your teams

Invite your team and start collaboration in your workplace. By bringing everyone together, you enforce productivity and seamless communication, foster creativity, and facilitate a more connected and efficient working environment.

#### 2 -Select AI Chatflow from Marketplace

Start deploying AI application for example Custom ChatGPT for your data Just connect your data sources and get a ChatGPT-like chatbot for your data. Then add it as a widget to your website or chat with it through our integrations or API.Test your AI chatflow with the chat interface on convosuite, edit and share it, go live in a minutes.

**3- Unlock productivity**

Empower your team to focus on significant tasks and reduce busywork with Convosuite. This tool efficiently manages emails, replies, and integrates seamlessly with Teams or Slack. It's like ChatGPT Plus but with the most powerful integrated plugins, allowing for real-time task management, AI image generation, GPT-4 access, and compatibility with various file formats. With Convosuite, you can turn ideas into apps in minutes, handle various files such as audio, video, docs, CSV, PDF, and presentations, and create content with **the latest information.**

**4 - Promts Engineering Tools**

With our advanced prompts engineering templates, you can create compelling job ads, write engaging blog posts, and craft effective social media ads that drive conversions. You can even generate email marketing templates from URLs, as well as write code.

**5- Advanced AI Dashboard**

This will display user activity and growth, usage statistics, Top active users, OpenAI usage, tracking total token, consumption, file and media interactions, usage of integrated Google Search and Dall-E capabilities, estimated time savings, productivity increase, sentiment analysis, and error rates or issues.



Now after you select your chatbot template and you have tested your chatflow with the chat interface on Convosuite, you want to "export" it out to be able to use with other applications. Convosuite provides 2 ways to do that:

* API
* Embed

## API

You can use the chatflow as API and connect to frontend applications.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

You also have the flexibility to override input configuration with **overrideConfig** property.

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

An example of API call using Postman:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="161">Key</th><th>Description</th><th>Type</th><th>Required</th></tr></thead><tbody><tr><td>question</td><td>User's question</td><td>string</td><td>Yes</td></tr><tr><td>overrideConfig</td><td>Override existing flow configuration</td><td>object</td><td>No</td></tr><tr><td>history</td><td>Provide list of history messages to the flow</td><td>array</td><td>No</td></tr></tbody></table>

```json
// Example body request
{
    "question": "What's my name?",
    "history": [
        {
            "message": "Hello, how can I assist you?",
            "type": "apiMessage"
        },
        {
            "type": "userMessage",
            "message": "Hello I am Bob"
        },
        {
            "type": "apiMessage",
            "message": "Hello Bob! how can I assist you?"
        }
    ],
    "overrideConfig": {
        "returnSourceDocuments": true
    }
}
```

#### Flow with Document Loaders

If the flow contains [Document Loaders](../document-loaders.md), the API looks slightly different. Instead of passing as **JSON** body, **form-data** is being used. This allows you to upload any files to the API.

Note: It is user's responsibility to make sure the file type is compatible with the expected file type from document loader. For example, if a Text File Loader is being used, you should only upload file with `.txt` extension.

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

An example of API call with `form-data` using Postman:

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>

## Streaming

Convosuite also support streaming back to your front end application when the final node is a **Chain** or **OpenAI Function Agent.**

<figure><img src="../.gitbook/assets/screely-1687030897806.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/screely-1687030924019.png" alt=""><figcaption></figcaption></figure>

1. Install socket.io-client to your front-end application

```bash
yarn add socket.io-client
```

or using npm

```bash
npm install socket.io-client
```

Refer [official docs](https://socket.io/docs/v4/client-api/) for more installation options.

2. Import it

```javascript
import socketIOClient from 'socket.io-client'
```

3. Establish connection

```javascript
const socket = socketIOClient("http://localhost:3000") //flow url
```

4. Listen to connection

```javascript
import { useState } from 'react'

const [socketIOClientId, setSocketIOClientId] = useState('');

socket.on('connect', () => {
  setSocketIOClientId(socket.id)
});
```

4. Send query with `socketIOClientId`

```javascript
async function query(data) {
    const response = await fetch(
        "http://localhost:3000/api/v1/prediction/<chatflow-id>",
        {
            method: "POST",
            body: data
        }
    );
    const result = await response.json();
    return result;
}

query({
  "question": "Hey, how are you?",
  "socketIOClientId": socketIOClientId
}).then((response) => {
    console.log(response);
});
```

5. Listen to token stream

```javascript
socket.on('start', () => {
  console.log('start');
});

socket.on('token', (token) => {
  console.log('token:', token);
});

socket.on('sourceDocuments', (sourceDocuments) => {
  console.log('sourceDocuments:', sourceDocuments);
});

socket.on('end', () => {
  console.log('end');
});
```

6. Disconnect connection

```javascript
socket.disconnect();
```

## Embed

You can also embed a chat widget to your website.

Simply copy paste the embedded code provided to anywhere in the `<body>` tag of your html file.

![](<../.gitbook/assets/image (32).png>)



