# Webhooks

--8<-- "ux-reference/manager-role-only.md"

!!!note
    The Runtime Reachability Assessment feature is under limited availablity. Please contact us to gain access to this feature.

From version 1.36, Lightrun supports webhooks. A webhook is an automated notification system that sends event details to a specified URL when triggered by predefined events. The payload comprises of three key elements: the event trigger, the payload containing event information, and the URL to receive the event.

Webhooks are configured within the Lightrun Management Portal to facilitate [notifications when packages are loaded during runtime](/runtime_reachability_assessment/view-loaded-not-loaded-packages/#notifications). By leveraging webhooks, you can seamlessly integrate Lightrun processes with third-party applications, such as Slack. For instance, if a package containing a potential (CVE) is detected within your runtime application, you'll promptly receive a notification.

## How does it work?

Lightrun supports custom webhooks, allowing you to customize the HTTP request headers and payload. This customization enables seamless integration with various target services, including Datadog, Slack, and email. 

## Webhook payloads and built-in variables {#variables}

As part of setting up your webhook in Lightrun, you can set up a webhook payload. It refers to the data that is sent from Lightrun, the webhook provider, to the specified URL when a webhook event is triggered. This payload contains information relevant to the event that occurred, such as details about the event itself or any associated data. In the context of Lightrun, the webhook payload might include information about a loaded package event, CVE information or other relevant data related to the Lightrun feature being used.

When you add a webhook, you can customize the default payload template using variables or you can use the default payload template that we provide in JSON format. The following example shows the default template as a text file that will be sent.

```json
{
   "id": "${ID}",
   "date": "${DATE}",
   "type": "${TYPE}",
   "title": "${TITLE}",
   "event_msg": "${EVENT_MSG}"
}
```

For the [Lightrun Reachability](/runtime_reachability_assessment/overview/) feature, we provide this dedicated payload example that you can customize for your needs directly in the UI.

## Example: Setting a Slack payload for a webhook

For the Runtime Reachability feature, we provide this dedicated payload example that is set for a Slack webhook. The provided JSON payload illustrates how to format data for various parameters such as ID, date, type, title, and event message.

```json
{
"text": "{\n \"id\": \"${ID}\",\n \"date\": \"${DATE}\",\n \"type\": \"${TYPE}\",
\n \"title\": \"${TITLE}\",\n \"event_msg\": \"${EVENT_MSG}\"\n}"
}
```
 
## Create a webhook

1. Log in to your Lightrun account.
2. Click **Settings** on the top right hand side of your screen to navigate to the Settings dashboard.
3. Under the **Runtime Reachability** section, select **Webhooks**.
   
   The Webhooks page opens.

   ![Webhooks](/assets/images/webhooks-page.png)

4. Click the **Create new webhook** button.
   
   The **Create a webhook** page opens.

   ![Create a webhook ---half](/assets/images/webhooks-create-a-webhook.png)

5. Enter a unique **Name** for your webhook.
6. Enter the **Webhook URL** where you would like to receive payloads.
   Lightrun sends an HTTP Post to this URL.
   The HTTP header is preset to `content-type-application/json`, specifying the way the payloads will be delivered via HTTP requests is in JSON format. 
7. Click the **Payload Properties** tab.
   In the text input area, you have the variables to set for the payloads. The payloads variables are delivered in a JSON format (`application/json`). 

   To learn more about setting the Payload properties, see [Webhooks payloads and variables](#variables).

   To use your webhook, insert the following code snippet into the text of the alert you wish to trigger along with your customized description: `"event_msg": "$[EVENT_MSG]"`. 
   When this alert is triggered, it will initiate a POST request to the designated URL with the provided content in JSON format. 

8. Click **Create** to save the webhook.

## Delete a webhook

!!! important
    Deleting a webhook will also remove all the notifications that are associated with it.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right hand side of your screen to navigate to the Settings dashboard.
3. Under the **Runtime Reachability** section, select **Webhooks**.
4. In the Webhooks list, click on the webhook.

   The webhooks details dialog opens.

   ![Delete a webhook ---half](/assets/images/webhooks-delete-webhook.png)

5. Click **Delete Webhook** and **Done**.
   
   The webhook will be removed from the list.


## Next steps

[Set up notifications for loaded packages](/runtime_reachability_assessment/view-loaded-not-loaded-packages/#notifications).