# Field Apps Integration & Automation Demo

This is the **complete workflow** for the integration and automation demonstration prepared for the Dev Summit 2026.

## Workflow Overview

The demo showcases a seamless integration between Python scripts and Power Automate flows for contractor management and task automation:

### Execution Sequence

1. **Contractor Registration (Python Notebook)** - Polls at an interval of your choosing
   - Initializes contractor data, assign tasks and registers new contractors in the system after they submitted a Survey123 form.
   - Adds the user to the credentials table.

2. **Send Teams message when tasks is ready flow (Power Automate)** - Automatically triggered
   - Responds to the python notebook above letting the mobile worker know that they can begin their tasks for the day

3. **Create report from feature layer (Power Automate)** - Automatically triggered
   - After the mobile worker finishes the day and complete and exit Survey123 form a report is automatically generated and added to the Task Layer.

4. **Tasks Clean Up (Python Notebook)** - Polls at an interval of your choosing
   - Transfers data from your tasks layer to the archived task layer
   - Looks at the credentials table to see if that user should be deleted from the Org


## Power Automate vs Python: When to Use Each

### Power Automate
**Best for:**
- Event-driven automation triggered by system events
- Native cloud operations (approvals, notifications, document creation)
- Low-code/no-code solutions requiring minimal technical expertise
- Real-time responsiveness and orchestration

**Advantages:**
- Fully managed within Microsoft's cloud infrastructure
- Native connectors to ArcGIS and enterprise systems
- Drag-and-drop interface requiring no programming knowledge
- Built-in approval workflows and notifications
- Constrained to available pre-built connectors

### Python
**Best for:**
- Complex data processing and scripting
- Custom business logic and heavy-duty computational tasks
- Flexible, fully customizable solutions
- Ideal for data transformation, API interactions, and automation of repetitive tasks

**Advantages:**
- Maximum flexibility with complete programming control
- Can handle complex, heavy-duty administrative tasks
- Run manually or on a pre-scheduled basis
- Supports both cloud and on-premises deployment
- Requires programming knowledge and more setup time

### The Difference
Power Automate excels at **orchestrating** workflows between systems with pre-built connectors, while Python excels at **processing** data and executing complex custom logic. This demo uses both in tandem: Power Automate handles the event-driven coordination, while Python manages data processing and cleanup operations.
