# Platform Documentation Outline

## Platform sections
1. Dashboard
2. Conversations
3. Agents
4. Agent Settings
5. Account
6. Integrations
7. Tasks
8. Content

## Dashboard

### My Metrics

Section includes simple graphs of each KPI offered. Graphs can be expanded to full screen, however it does not appear that offers any more details. 

### My KPIs

By default, the following KPIs are shown:
* **Total Calls** - No. of calls
* **Average Call Duration (sec)** - Average call duration in seconds
* **Human Intervention** - Number of calls transferred
* **Qualified Calls** - No. of calls with a qualified event
* **Disqualified Calls** - Disqualified calls

**TODO** - Outstanding questions below
* Are these metrics able to be modified? 
* How do we enable users to update with their own metrics
* What metrics are missing?

## Conversations

### Calls

List of inbound and outbound calls involving the selected agent. Immediate list shows phone number, call direction (inbound/outbound), start time, duration, transferred boolean, and voicemail boolean.
Can search based on phone number
Filter menu option exists, however is not functional at this time
Selecting a call's check box allows you to export or archive from this screen

**TODO** - Not immedately apparant what "archive" means or if a call is recoverable once archived. FIND OUT

#### Call details

Clicking on a phone number allows you to view a transcript of the call. Additionally, there is a summary pane which has a gen AI generated summary of what happened during the call. 
You can also archive the call from this view.

### SMS

List of SMS outbound and inbound messaging grouped by phone number. List shows Phone Number, Last Message Time, and Agent Enabled. No clear definition of "Agent Enabled" meaning.

#### SMS details
Shows a transcript of all incoming and outgoing messages based on the phone number. Similar to the call details, provides a transcript as well as an AI generated summary describing the content of the transcript.

### Emails

Similar functionality and design as the SMS section. Unclear if this is actually in use by anyone.

### Web Chats

Assuming a list of conversations through the web interface grouped by IP Address. No content to view on test agent, however the list has fields for IP Address and Conversation Start time.

## Agents

List of all created agents for an account. Unsure of how agents are being listed, does not appear to be alphabetical.
Clicking directly on an agent name allows you to change the name of the agent.

Three button options to the right of each agent listed:
1. **Set Active** - Sets the selected agent as active, making its settings and history viewable throughout the platform
2. **Delete** - Deletes the agent, cannot delete the "primary" agent, nor any "active" agent
3. **Make Primary** - Sets the selected agent as primary, meaning it cannot be deleted and is the default agent that appears on login

The only difference is that whichever agent is listed as Primary will only have the "Set Active" button option.
Deleted agents appear to not be recoverable. There is a confirmation alert to prevent mistaken deletions

## Agent Settings

### Voiceprint

#### Select a Voice sample

Allows a user to select the voice used with the selected agent. List of elevenlabs voices are selectable from a dropdown. Once selected, a user can play a sample of the voice or activate the voice to assign it to the agent.

#### Upload a voice sample

Allows a user to select a file off of their computer to then upload to be used by the agent. Once a file is selected, clicking the upload button should put it on the system.
Unsure of restrictions of file types or how well the process works.
**TODO** - Test out this functionality, learn about file type restrictions

#### Generate Snippets

Provides a link that goes to a *Create Voice Snippet* page. This screen allows you to free form enter text that you would like to hear your agent speak. Once text is entered and the submit button pressed, a *Your Voice Snippet* section appears at the bottom. This section allows you to play back the snippet in the agent's voice from this page. This also provides you with a shareable link containing an MP3 that can be distributed for others to listen to in MP3 format.

### Voice Prompts

There are several situations that an agent will generate scripted speach as opposed to having the gen AI model generate the content. The voice prompt section is where these scripts are created and updated. Modifyable scripts are available for the following processes:

#### Welcome Phrase

The greeting your agent uses when it answers a call.
**TODO** - See if it's possible to have multiple welcome messages that are randomly selected. If so, I'm assuming this is done by just adding new lines.

#### Processing Phrases

What the agent says when it's processing something the caller has said. It will choose one at random from the list. These phrases effectively work as a "buffer" to fill the silence while the AI is processing the spoken text. 

Each line item can be prepended with an `S:` or `Q:` to signify if that particular processing phrase should follow a statement (S) or a question (Q)

#### Next Action Phrase

After an agent completes a request, the agent will say this to prompt the caller to speak again. Essentially a follow up to any statement made by the agent


#### Voicemail Phrase

The agent will say this after the caller has asked to leave a voicemail.
**TODO** - Gather more information on voicemail capabilities

#### Extended Silence Phrase

The agent will say this after 15 seconds of silence.

### Agent Prompts

This section contains a large text field for the *Agent Content Prompt*. This is where we build out the prompt that will be sent with every request to the agent. For brand new agents, this can be built out directly within this text field. However, there is an option to use template libraries to create reusable components across many different agents. This method utilyzes Jinja python templates. 

**TODO** - This will likely be the most advanced section of any guide. Gather more information on how much we expect users to interact with these options and to see how deep we will need to go. 

In addition to the template library, we now have a *History* option which will allow users to revert back to previous versions of their agent prompt. 

### Voice Settings

Here is where the voice generation settings are modified. 

#### model

Offers 3 options:
1. Multilingual V2
2. Turbo V2 (English Only)
3. Turbo V2.5 (Multilingual)

*Tooltip* - V2 supports more languages and is preferred for built in voices. Newer is not necessarily better and should be experimented with your voice print.

**TODO** - Gain a better understanding of the differences between each model

#### Stability

Provides a slider that ranges from *More variable* to *More stable*

*More variable tooltip* - Increasing variability can make speech more expressive with output varying between re-generations. It can also lead to instabilities.

*More stable tooltip* - Increasing stability will make the voice more consistent between re-generations, but it can also make it sound a bit monotone. On longer text fragments, we recommend lowering this value.

#### Clarity and Similarity Enhancement

Provides a slider that ranges from *low* to *high*

*Low tooltip* - Low values are recommended if background artifacts are present in generated speech

*High tooltip* - High enhancement boosts overall voice clarify and target speaker similarity. Very high values can cause artifacts, so adjusting this setting to find the optimal value is encouraged.

#### Style Exaggeration

Provides a slider that ranges from *None (Fastest)* to *Exaggerated*

*Exaggerated tooltip* - High values are recommended if the style of the speech should be exaggerated compared to the uploaded audio. Higher values can lead to more instability in the generated speech. Setting this to 0.0 will greatly increase generation speed and is the default setting.

#### Speaker Boost

Checkbox that when filled, enables Speaker Boost. 

*Speaker Boost tooltip* - Boost the similarity of the synthesized speech and the voice at the cost of some generation speed.

This page also provides buttons to reset all values to their default, play a test sample, or save the updated setting to the agent.

### Additional Settings

**TODO** - Need to gain a better understanding of what each of these actually means. Some are fairly self explanitory, but there are a lot here that it isn't 100% clear.

* Agent Locale - dropdown
    * English
    * Arabic
    * Bengali
    * Czech
    * Dutch
    * French
    * German
    * Hindi
    * Polish
    * Russian
    * Spanish
    * Swedish
* Agent Location (street address of city & state) - text field
* Agent Timezone (automatically set by Agent Location) - dropdown
* Email to send post call summary - text field
* Webhook URL for post call summary - text field
* Additional webhook headers - large text field
* Pronunciation dictionaries - text field (may have different options to select from)
* Initial Trigger (Instead of waiting for first response, use this. Good to launch a task) - text field
* Generate next action phrase automatically where possible - checkbox
* Disable voicemail request detection - checkbox
* Do not expose a method for the agent to send SMS - checkbox
* Allow the agent to be interrupted while it's speaking - checkbox
* Let DTMF flow to Agent (BETA) - checkbox
* Let Agent send DTMF Tones - checkbox
* Use RAG query as tool - checkbox
* Send opening text by default if message is populated. Otherwise this is triggered by 'openingsms:true' in API metadata (BETA) - checkbox
* Text message to send when call is answered (BETA) - large text field
* Enable elevenlabs request stitching (BETA) - checkbox
* Speech to Text Provider (LABS) - dropdown
    * Azure
    * Deepgram
* Enable SMS Channel during calls (LABS) - checkbox
* Enable outbound answering machine detection (LABS) - checkbox
* Enable Agent to remember details between conversations (BETA) - checkbox
* Send webhook when there is no response to the Agent - checkbox
* Enable template library - checkbox
* Only put links in summary emails, no details - checkbox
* LLM filter to apply to email - text field

## Account

This section contains details about the management of your account as a whole, as well as integration details for testing the currently selected agent. It is made up of two sections:

1. Your Account
2. Agent Integration

### Your Account

This section contains a reference to the email address of the primary user, as well as options to create a new password or log into our *Legacy Portal*

* Email Address - the email address for the logged in user
* Password - provides a link to change the password
* Legacy Portal - provides a button to login to the legacy system

**TODO** - Learn to what extend users will have access to the legacy portal and whether we need further documentation for that system.

### Agent Integration

This section contains several bits of information related to the usage and connection of the agent to other systems.

* **Chatbot URL** - This provides a sharable link providing a webpage with the current agent wired into a text chat system. Currently on prod, clicking the [link](https://agent.revmo.ai/g/chatdemo/?key=OGMwOWY4ODgtYTA3YS0xMWVmLThlNDEtMGE1OGE5ZmVhYzAy) takes the user to a page where it appears documentation should exist to help a user connect to a chat platform. Copy/pasting the provided [text link](https://app.revmo.ai/chatjs/OGMwOWY4ODgtYTA3YS0xMWVmLThlNDEtMGE1OGE5ZmVhYzAy/) only shows some javascript code in the web browser and is not a functioning interface for the chat platform.

    **TODO** Need to see what is supposed to be showing here and how to ensure that the chat application works properly

* **Agent ID** - Provides an Agent ID string to be used in outbound and potentially other communications. There is also a [*Learn More*](https://docs.revmo.ai/docs/outgoing) link that directs the user to our documentation on *Outgoing Calls*

    **TODO** - Need to find other places this Agent ID will need to be used

* **API Key** - An API key. There is also a link to re-generate the API key. Clicking the link does generate/regenerate the API key, however it does appear to direct to a new page as well with no confirmation of the API key being updated.

* **Direct Phone Numbers** - Provides a phone number that a user can test out their new voice agent on. On this line are also two dropdowns related to deployment environments:

    * First dropdown
        * Production
        * Staging
        * Labs

    * SMS Responder dropdown
        * Disabled
        * Production
        * Staging
        * Labs

    **TODO** - Learn more about the intended usage for each environment, including how a user is intended to promote from one to the next.

* **Support ID** - ID that we can use to help with supporting in our back end systems.

    **TODO** - Learn any other uses for this ID

* **Third Party Connections** - Link to the *Integrations* panel to handle standard connections we've enabled. 

    **TODO** - need to determine if this link will still exist once staging is pushed up

Outside of the two main sections, there is also a button along the bottom for the user to log out of their profile.

## Integrations

This section contains links to enable connecting to various CMS systems as well as connected/not connected status for each one.

External Integrations listed:

* Leadconnector(GHL)
* Hubspot
* Google
* Microsoft - Delegated
* Microsoft - Admin
* Salesforce
* SmartSheets

The salesforce object also contains a [link](https://docs.revmo.ai/docs/integrations/salesforce) to our documentation on how to integrate with services.

For Leadconnector, there are two links available. 
* Connect
* Connect - Whitelabel 

**TODO** - Learn when to use "Leadconnector" option and when to use the standard link vs the "white glove" link.

**TODO** - Work on adding documentation for the connectors other than Salesforce. [There is very little](https://docs.revmo.ai/docs/integrations/googlecalendar) on some of the other connectors, and some with no information whatsoever.

## Tasks

Provides a task management interface for the creation and activation of tasks that have been built. 

### Creating a new task

By clicking on the *Add Task* button in the upper right, you gain access to a dropdown of the various task types available for your account to create. The tasks available are:

* Responder
* Conversation To email
* Conversation to transfer
* Conversation to webhook
* EmailValidator
* External Responder
* HUBSPOT: Createcontact
* MICROSOFT: Calendar
* REVMO: Ms And Hubspot Calendar V2
* Task Chain
* TRIPLESEAT: Submit Lead
* Voicemail
* Schedule Meeting - Google

**TODO** - Need to gain more information about all of these. Responder is one I've used before, but will need to determine when it makes sense to use any of the other options.

**TODO** - Find out if all of these are available to a "standard" user or if there is a subsection that is available.

### Managing Tasks

Created tasks will show in a list in the middle of the page. Each task will contain a name, a trigger (lighting bolt), a task type (wrench icon), a status, last modification date, and icons to configure, activate, or delete the task.

**TODO** - confirm my understanding of the various icons

## Content

Provides a section to manage and create content models and templates. Similar to tasks, provides an interface to add a new model as well as manage the existing ones showing in a list. 

### Creating a new model

When selecting the "Add New Model" button from the upper right, the user is prompted to give the model a name for it to be created. Once created, clicking the red gear icon will all you to configure the model.

On the modle content screen, there are several options to populate the model with information. A user can select one of several options to have the model created from:

* Add Web Site
* Add Single URL
* Add File

**TODO** - confirm if web site will crawl the entire web site or not. Confirm is there is a way to see the output of adding a model in order to troubleshoot.

Above this section, you have triggers to enable "Use as Template" and "Enable Auto Refresh", both of which can be saved by selecting the "Save Settings" button. 

* *Use as Template* - provides fields for the user to name the template as well as provide additional processing instructions to the LLM.
* *Enable Auto Refresh* lets the user select a number of days they would like to update the model from the content provided. Timeframe is restricted to number of days.

**TODO** - test this out and see how well it works. See what data you get back.

Finally, in the upper left there are two button options for publishing the content (V1 & V2)

**TODO** - Find out the differences and why both are an option

### Additional Content Models

Below your content models will have the templates to your account listed. Each listing will contain a name, a last updated date, a published/unpublished status, markers for being active or being a template, and additional actions to configure the model, run the model, activate the model, and delete it.

**TODO** - play around with these to better understand their functions. 

**TODO** - Where is this information retrieved from by the agent? Is it included in the prompt or is there some kind of RAG element to this equation?