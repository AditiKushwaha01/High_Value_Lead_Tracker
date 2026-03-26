#**High Value Lead Tracker** 
*Overview*

This n8n workflow identifies high-value GitHub users from a repository’s stargazers, generates a personalized single line outreach pitch using OpenAI’s GPT-4O-MINI model, and sends the message to a Discord channel.

*Workflow Steps:*

Manual Trigger – Start the workflow manually.
Stargazer Node – Fetch the first 5 stargazers of the n8n-io/n8n repository using the GitHub API.
GitHub Node – Retrieve detailed user info (followers and public repos) for each stargazer.
If Node – Filter users who meet high-value criteria:
Followers > 100 OR Public Repos > 50.
Message a Model Node (OpenAI) – Generate a personalized outreach pitch for the selected users.
Set Node – Extract name, bio, and text from AI output for structured data.
Discord Node – Post the high-value lead info and pitch to a Discord channel.

***Setup Instructions***

*GitHub Authentication*
Create a GitHub personal access token.
Add it to n8n as a HTTP Bearer Auth credential named Bearer Auth account.

*OpenAI Authentication*
Use your n8n OpenAI API credentials (n8n free OpenAI API credits).

*Discord Webhook*
Create a webhook in your Discord channel (eg: my channel name test_channel).
Steps: channel -> settings -> integration -> new webhook -> generate 
Paste the URL in the Discord node.

*Workflow Import*
Import GitHub-Discord-Outreach-Workflow.json into n8n.
Connect all credentials and test the workflow manually.

***Logic Notes***

*Handling GitHub API Rate Limits:*

Limit the number of stargazers fetched with per_page=5 to reduce requests.
Requests are authenticated with a GitHub token for higher rate limits.
For larger batches, implement delays or check the X-RateLimit-Remaining and X-RateLimit-Reset headers.

*AI Output Handling:*

OpenAI node outputs a JSON object nested under output[0].content[0].text.
The Set node maps these fields (name, bio, text) correctly without surrounding quotes, ensuring Discord receives evaluated data instead of templates.

***WorkFlow Image***
<img width="1132" height="571" alt="image" src="https://github.com/user-attachments/assets/3c99946c-8e15-4c9d-91b5-6ef9775199dc" />

***Discord OutPut***
High Value Lead!
Name: Monalisa Octocat
Bio: "Design and build all the things. Interested in Open Source and AI
Pitch: Hi Monalisa, I admire your work in open source and would love to collaborate on a project that aligns with your interests!

