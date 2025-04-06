
# Chatbot Customization Guide

This document outlines how to customize various aspects of the Payroll Chat Assistant.

## General Settings

### Changing the Assistant Name and Robot Name

1. Open `src/components/ChatHeader.tsx`
2. Locate the following code:
   ```jsx
   <div>
     <div className="font-semibold text-lg">PAYROLL CHAT ASSISTANT</div>
     <div className="text-xs text-muted-foreground">JI Assistant</div>
   </div>
   ```
3. Change "PAYROLL CHAT ASSISTANT" to your preferred assistant name
4. Change "JI Assistant" to your preferred robot name

### Changing the Welcome Message

1. Open `src/components/RobotAnimation.tsx`
2. Locate the `RobotAnimation` component and change the `welcomeMessage` prop default value
3. Also update the welcome message in `src/components/ChatMessages.tsx` if needed

## Webhook Configuration

### Changing the Webhook URL

1. Open `src/components/ChatInput.tsx`
2. Locate the following line:
   ```javascript
   const WEBHOOK_URL = "https://thirunerechelvanraja.app.n8n.cloud/webhook-test/a704f04a-3297-4845-a1cd-af94b743d17a";
   ```
3. Replace with your new webhook URL

### Customizing Data Sent to Webhook

The current implementation sends:
- The message text (as "message" parameter)
- Any attached file (if present)

To modify what data is sent:

1. Open `src/components/ChatInput.tsx`
2. Locate the `sendToWebhook` function
3. Modify the FormData creation to include additional parameters:
   ```javascript
   const formData = new FormData();
   formData.append("message", messageText);
   formData.append("userId", user.id); // Example of adding user ID
   
   if (file) {
     formData.append("file", file);
   }
   ```

## Visual Customization

### Changing the Robot Avatar

1. Replace the file at `public/robot-avatar.png` with your preferred robot image
2. Ensure the new image has similar dimensions for optimal display

### Customizing Chat Bubble Styles

1. Open `src/components/MessageBubble.tsx`
2. Look for CSS classes controlling the appearance and modify as needed

## Advanced Customization

For more advanced customizations like modifying the authentication flow, adding new features, or changing the overall layout, refer to the component structure:

- `src/App.tsx` - Main application entry point
- `src/contexts/ChatContext.tsx` - Chat state management
- `src/contexts/AuthContext.tsx` - Authentication logic
- `src/components/` - All UI components

## Troubleshooting

If webhook sending fails, check:
1. The webhook URL is correct and accessible
2. Network connectivity is working
3. The webhook endpoint accepts the format of data you're sending
4. CORS policies aren't blocking the request

For persistent issues, inspect browser console logs for detailed error information.
