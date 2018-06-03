# The three ways explained

* **The first way** is about left to right flow work from Development to IT Operations to the customer.

	The necessary practices include continuous building, integration, deployment, creating environments on demand.

* **The second way** is about the constant flow of fast feedback from right to left at all stages of the value stream.

	The necessary practices include "stopping the production line" when builds and tests fail in the deployment pipeline, improving daily work over daily work, creating fast automated test suites, creating pervasive production telemetry so that everyone can see whether code and environments are operating as designed.

* **The third way** is about creating a culture that fosters continual experimentation and understanding that *repetition and practice is the prerequisite of mastery*.

	"The practice of kata is the act of practicing a pattern so that it becomes second nature".

# The four types of work

Because work can be assigned to people in more ways than ever (emails, phone calls, hallway conversations, text messages, meetings,...) we want to make visible our existing commitments.

* **Business Project**
These are business initiatives, of which most of development projects encompass

* **Internal IT Projects**
These include the infrastructure or IT Operations that business projects may create, as well as internally generated improvement projects (create new environment, automate deployment). Often these are not centrally tracked anywhere, instead residing with the budget owners (e.g database manager, storage manager, etc.)

	This creates a problem when IT Operations is a bottleneck, because there is no easy way to find out how much of capacity is already committed to internal projects.

* **Changes**
These are often generated from the previous two types of work and are typically tracked in a ticketing system (e.g. Jira, Remedy for IT Operations, etc.).

* **Unplanned work**
These include operational incidents and problems, often caused by the previous types of work.

### Visualize IT Work and control Work In Progress

The wait time of a resource is a function `y = busy/(1-busy)` where busy is a value in `[0,1]`.

If a resource is 50% busy, thus 50% idle, the wait time would be 1 unit of time, let's call it an hour. So on average a task would wait in the queue an hour before it gets worked.

# DevOps Myths

**DevOps means NoOps**

DevOps will often put more responsibility on Development to do code deployments and maintain service levels.
DevOps requires many IT Operations tasks become self-service. On other words, instead of Development opening up a ticket and waiting for IT Operations to complete the work, many of these activities will be automated so that developers can do them themselves.

**DevOps is just Automation**

DevOps also requires shared goals and shared pain througout the IT value stream.