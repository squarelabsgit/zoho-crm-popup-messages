# Create Pop-Up Messages in Zoho CRM

Blog Post: https://www.squarelabs.com.au/post/create-pop-up-messages-in-zoho-crm

YouTube Video: https://youtu.be/GXkvTFrnml8

Navigating a CRM often requires leaving crucial notes or ensuring vital information reaches others accessing specific records. However, relying on static notes can be risky – they might easily be overlooked if not actively sought out. So, how can we guarantee these important messages are seen, the moment the record is opened?

Enter pop-up Messages – These dynamic alerts appear precisely when a record is accessed, offering a direct and immediate way to communicate. Whether you need a subtle reminder or a mandatory acknowledgement, pop-ups ensure critical information doesn't get missed.

To create pop-up messages in Zoho CRM, this we will be using a client script. To get started, we'll navigate to Settings > Developer Hub > Client Scripts. Here, you'll find a button to create a New Script, which will present you with the Create Script form.

This tutorial will guide you through creating a pop-up that appears when you access a record. To achieve this, we'll be selecting Detail Page as the context and setting the trigger to on load of that page. This ensures the message appears immediately when someone opens the record.

![Screenshot of the Client Script Configuration Form](https://static.wixstatic.com/media/c8c3af_484a67d875da4a709b8430d6ccaa236b~mv2.png/v1/fill/w_736,h_504,al_c,q_90,usm_0.66_1.00_0.01,enc_auto/c8c3af_484a67d875da4a709b8430d6ccaa236b~mv2.png)

When you click next you will be directed to the code editor where we can configure our pop-up message.

```js
const popupNoteFieldObj = ZDK.Page.getField('FIELD_API_NAME');
const popupNoteValue = popupNoteFieldObj.getValue();
if (popupNoteValue)
{
    ZDK.Client.showMessage(popupNoteValue, { type: 'success' });
    ZDK.Client.showAlert(popupNoteValue);
}
```
To make this code work for your specific needs, the first crucial step is to replace 'FIELD_API_NAME' with the actual API Name of the field in your Zoho CRM where you will store the note you want to display in the pop-up. You can easily find a field's API Name by navigating to Settings > Developer Hub > APIs and SDK's > API Names. Locate the relevant module and find the API Name of your chosen field.

Next, you have a choice in how you want the pop-up to behave. The sample code provides two options:

1. ZDK.Client.showMessage(pop-upNoteValue, { type: 'success' }); This line will display a discrete message that appears for approximately 5 seconds with a success theme. You can customise the theme to 'info', 'warning', or 'error' to match the tone of your message.
2. ZDK.Client.showAlert(pop-upNoteValue); This line will display an alert box that requires the user to click an "Okay" button to acknowledge the message and continue accessing the record. The content of the alert will be the value stored in the field you specified using its API Name.

Decide which type of pop-up best suits you. If you prefer a subtle notification, keep the showMessage line. If you need to ensure the user actively acknowledges the note, keep the showAlert line. Simply remove the line of code corresponding to the type of pop-up you do not wish to use.

For those looking to take their pop-up messages a step further, the ZDK.Client.showMessage() and ZDK.Client.showAlert() functions offer even more customisation options. The links above will direct you to the official Zoho Developer documentation for each of these functions. There, you'll discover how to enhance your pop-ups by:
- Adding Titles: Provide clear context for your messages.
- Including Links: Direct users to relevant records, external resources, or internal documentation.
- Formatting Text: Use bold or other styling to highlight key information within the message.

We encourage you to explore these documentation pages to tailor your pop-up messages precisely to your needs and create an even more effective communication tool within your Zoho CRM.

With your function saved, open a record and populate your note field – that message will now be seen by anyone who accesses the record.

![Example of the pop-up message successfully working](https://static.wixstatic.com/media/c8c3af_50319b8f9b254243879603d36dbc4749~mv2.png/v1/fill/w_736,h_385,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/c8c3af_50319b8f9b254243879603d36dbc4749~mv2.png)

I hope this article has empowered you to configure effective messages within your CRM. Remember, client scripts offer a wide range of possibilities, allowing you to target your messages to specific roles, users, or even implement location-based logic. If you require assistance in implementing these more advanced customisations, reach out to us and we can help you!

Need Help? [Contact us!](https://www.squarelabs.com.au/contact-us)

<a href="http://www.youtube.com/watch?feature=player_embedded&v=GXkvTFrnml8" target="_blank"><img src="http://img.youtube.com/vi/GXkvTFrnml8/0.jpg" 
alt="YouTube Video" width="240" height="180" border="10" /></a>

## Resources

https://www.zoho.com/crm/developer/docs/client-script/overview.html

https://www.zohocrm.dev/explore/client-script/clientapi/Page
