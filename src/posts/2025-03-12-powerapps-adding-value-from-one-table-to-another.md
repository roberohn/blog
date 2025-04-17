---
title: Creating Dynamic Field Updates in Microsoft Dataverse
description: Here I'll show you how to add a value from a field to another entity in a PowerApps MDA.
date: '2025-03-12'
categories:
  - automation
  - powerapps
published: true
---

### The Challenge I Tackled

I recently developed a Model-Driven App (MDA) to streamline weekly finance processing for our team. A specific challenge emerged: when users select a value from a lookup field that references data in another entity, I needed to automatically populate a second field with related information from that same source entity. What made this tricky? Standard Business Rules couldn't help since they're limited to working within the primary entity of your form, not across related entities.

### Exploring Solutions

Initially, I experimented with several JavaScript approaches, but encountered implementation challenges. While JavaScript remains a viable option I plan to revisit, I discovered a more straightforward solution using the classic **Workflow** functionality.

### The Workflow Solution: Step-by-Step Implementation

<img src="./powerapps-adding-value-from-one-table-to-another/pa-00001.png" alt="Here we're showing the steps to navigate to the workflow option in the PowerApps solution">

#### Setting Up Your Workflow
1. **Create the Workflow**: Provide a descriptive name and select the target table. Uncheck "Run workflow in the background" for immediate processing, then click "Create".

2. **Configure Workflow Settings**: After creation, click the three dots and select "Edit" to access the classic PowerApps interface.

#### Adding Dynamic Logic
1. **Define Trigger Conditions**: I configured mine to trigger when a record is created AND when my lookup field changes - perfect for capturing both scenarios.

2. **Add Processing Steps**: Click "Add Step" and select "Update Record" from the dropdown.
   *Note: If the page experiences issues, a simple refresh usually resolves it.*

<img src="./powerapps-adding-value-from-one-table-to-another/pa-00002.png" alt="Here we're showing the selections I've used to update a value on a field based on the selection of a lookup field">

#### Configure the Update Action
  - Enter a clear description of what this step accomplishes
  - Select the entity you want to update
  - Click "Set Properties" to access the form layout
  - **Set Value Mappings**: In the properties window, select the target field and configure the operator settings to specify exactly which related value should be pulled when the lookup changes.

<img src="./powerapps-adding-value-from-one-table-to-another/pa-00003.png" alt="In the form we're showing the operation that needs to be performed on the selected field">

### Activating Your Solution
1. Click "Save and Close" to return to the workflow main screen
2. Click "Activate" in the top menu, confirm activation, then close
3. In your Solution's "Processes" page, select your workflow and "Turn on" to enable it

### Real-World Behavior

Since this isn't configured as a background process, the workflow executes immediately after record creation and saving. Once the record is saved, your target field will automatically populate with the related value.

### Looking Forward

For more complex scenarios requiring background processing, Microsoft now recommends Power Automate flows over classical workflows. This modern approach offers enhanced capabilities I'm eager to explore in future implementations.

This workflow solution provides an elegant way to enhance form usability without complex coding, creating a more intuitive experience for team members.
