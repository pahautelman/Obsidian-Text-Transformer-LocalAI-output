# Action Function

## Key Concepts
- Custom buttons in the message toolbar
- Interactive messaging
- Permission granting before task execution
- Data visualization
- Audio snippet download
- Action function components
- Event handling and response management

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/functions/action](https://docs.openwebui.com/features/plugin/functions/action)

### Overview
Action functions enable the creation of custom buttons in the message toolbar, enhancing user interaction with messaging systems. These buttons can perform various tasks such as granting permissions before executing actions, generating visualizations from structured data, and downloading audio snippets from chats.

### Use Cases

- **Interactive Messaging:** Enhance user engagement by allowing interactions through custom buttons.
- **Permission Granting:** Ensure users approve actions before they are executed.
- **Data Visualization:** Create visual representations of structured data for better understanding.
- **Audio Downloads:** Allow users to download audio snippets from chat conversations.

### Action Function Components

#### Button Creation
Actions create buttons in the Message UI, located directly underneath individual chat messages. These buttons can trigger various functionalities based on user interactions.

#### Main Component: Action Function
The core of an action is the **action function**, which processes data and handles events. This function takes an object defining the type of action and the data being processed.

```python
async def action(
    self,
    body: dict,
    __user__=None,
    __event_emitter__=None,
    __event_call__=None,
) -> Optional[dict]:
    print(f"action:{__name__}")
    response = await __event_call__( {
        "type": "input",
        "data": {
            "title": "write a message",
            "message": "here write a message to append",
            "placeholder": "enter your message",
        },
    })
    print(response)
```

### Event Handling
The action function handles events and manages responses. It can interact with users by displaying input prompts and processing user inputs.

## Summary

Action functions in OpenWebUI allow for the creation of custom interactive buttons in the message toolbar, enhancing user engagement through features like permission granting, data visualization, and audio downloads. The core component is the action function, which processes data and handles events to provide a seamless user experience.

# Tags
#actionfunction #interactivemessaging #datavisualization #audiodownloads #eventhandling