# 125. Amazon Quick: Hands-On

A tour of **Amazon Quick** showing the features from the previous lectures: connectors, spaces, flows, research, chat agents, apps and knowledge bases.

## Getting access

- Go to `quick.aws.com`. On first visit it prompts you to create an account, with many identity providers to choose from, including your AWS account. This is a **separate account from your AWS account**: Quick targets general business users, not just developers.
- Opening Amazon Quick **from the AWS console** takes you to **QuickSight**, the legacy analytics platform now rebranded **Quick Sight** and part of the Quick suite. That is not the agentic AI assistant for business users covered here.

## Steps

1. **Connectors**: under **more > connectors** there is a large menu of services to connect, such as Google Calendar, Google Meet, Google Drive, Google Docs, SharePoint, Slack, Zoom and Teams, many with read and write. The lab connected **Google Slides**: Quick walks you through authentication, and Google sends notification emails about the new connection. This lets Quick publish generated slides to Google Slides.
2. **Chat**: a new chat is a basic chatbot interface. Nothing is tied to enterprise data yet, so it uses general knowledge. The scope drop-down defaults to **all data and apps** (model knowledge, web, and anything you added). You can limit it to **general knowledge** or to **specific data and apps** (spaces, knowledge bases, actions). A general question such as the meaning of life gets a generic philosophical answer.
3. **Create a space**: under **spaces** (a way to organize permissions to information and capabilities for a group), create a space named `self-employment research`, whose goal is guiding people from corporate work to self-employment. Add knowledge by **file upload**: the course's book text file. Processing is quick.
4. **Ask against the space**: back in chat, **all data** now includes the space, or you can scope chat to it specifically. The question "How do I approach health insurance when I am self-employed?" was answered from the book's advice.
5. **Use an action**: asking for a 10-slide deck on moving from corporate to self-employment, published to Google Slides, first failed because Google Slides was not in the space. Quick offered to connect it on the spot, but the lab instead **edited the space to add the Google Slides action**, to show that **spaces hold capabilities as well as information**. The retry worked and the deck appeared in Google Slides.
6. **Flows**: under **more > flows** there are built-in examples, such as a **5 Whys root cause analysis**. Create a flow by describing it in natural language: "Root cause analysis for an operational failure using the 5 Whys approach". The generated flow asks for the failure description and supporting context (a text input step), summarizes it in an **AI output** step, walks through the 5 Whys and corrective actions, then produces a report. Each step can be edited, reordered and renamed, and the flow can be **shared**. More detail in the prompt gives a better flow.
7. **Research**: from home, open **Research** and prompt for a report on prospects for solopreneurs over the next five years, including the effects of AI and big-company layoffs and the competition. You can list **preferred websites** and **sites to avoid**, browse **third-party datasets** (S&P, Patents Database, PubMed and others), include **Quick assets** (such as the space with the book), keep **web search** enabled and upload files. You can **review the plan** before it runs.
8. **Chat agents**: the default **system agent** is what chat has used so far. You can create specialized agents with their own capabilities and personality, from a **blank agent** or the menu of **pre-created agents**. Example: a meeting facilitator that integrates with Outlook and Teams to manage and schedule meetings.
9. **Apps**: enter a text description of the app wanted. Examples offered include an **EV adoption trends dashboard** ("Build an interactive dashboard that visualizes EV vehicle adoption trends in the US"), a **customer feedback tracker** and a **task management (Kanban) board**. Opening the EV example shows the **chat history** that built it and an interactive web app with mouse-over, date range changes and drill-down.
10. **Knowledge bases**: import data from external applications and index it for use in Quick. Sources shown include Google Drive, SharePoint, OneDrive, Box and Atlassian.

## What it showed

- The scope drop-down controls whether chat answers from general knowledge or from specific spaces, knowledge bases and actions.
- **Spaces** bundle data and **capabilities** (actions), so an agent scoped to a space can only use what the space includes.
- The research run took about **5 to 10 minutes** and returned a report backed by **reliable citations**. It concluded that freelancers doing creative work face a weaker outlook, while corporate AI consulting looks better.
- The generated 10-slide deck was a bare-bones starting point with good structure. A more specific prompt (theme, diagrams, illustrations) would improve it.
- **Apps** build on **Quick Sight** capability and can be built from any prompt.
- Quick is a **business-user tool**: no programming or technical experience is needed. You say what you want, connect enterprise data sources, and it merges them into one agentic system that answers questions, does research, builds apps and controls other applications.

## Exam takeaways

1. Opening Quick from the AWS console leads to **Quick Sight**. Amazon Quick is the separate agentic AI assistant for business users, with its own account.
2. **Connectors** give Quick **actions** in external apps (for example publishing to Google Slides). **Knowledge bases** import and index external data.
3. **Spaces** group data and actions for a team, and a chat scoped to a space only uses those resources. A needed action must be added to the space.
4. **Flows** can be generated from a natural-language description and then edited, and shared.
5. **Research**, **chat agents** and **apps** are all built from prompts, with no code.
