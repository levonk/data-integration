# Project Workflow within Data Services

Traditionally development was the primary users of the project management system.  Given the complexity of dealing with so many different groups, different POs, different PMs, small projects, it quickly became evident we needed a cross cutting state representation to keep noise out of developers view and allow for workflow to represent PO story creation and PO work delivery.

## States
  * Misc States for getting stories out of the way with proper tracking
	  * Legacy - Get stories out of the way to allow for new process
	  * N/A - Impl Detail - Developer generated story to complete larger effort
	  * N/A - Handoff - Gave to another team
	  * N/A - Won't Do - An effort that could be solved another way
	  * N/A - Can't Do - Not possible / Permanent Block
	  * N/A - No Longer Needed - Legacy Story
	  * N/A - Labels - "decoration story" to help demarcate stories for Visable seperatation
	  * N/A - Other - Not important to surface for one of the stories
	  * Archive - Delivered, Accepted, Hypercare done, Work that no longer needs to be tracked on any board
	  * DEKanbanHistory - Should be mapped to Archive
	  * SPlit_Closed - a story was split and the previous story is moved out of the way
	  * Admin_OOO - Administrative overhead story
  * Work Definition States
	  * None - Default ingest state, POs need to review
		* Entrance Criteria - None
		* Exit Criteria - PO is prepared to work on it for denition
		* Purpose: Hold stories to be defined
	  * Flesh Out - PO is in the process of adding details
		* Entrance Criteria - PO is working on defining story
		* Exit Criteria - PO has completed initial definition of story
		* Purpose: To hold work in progress for POs
	  * For Grooming - PO is done authoring story, waiting to share with the tech lead
		* Entrance Criteria - PO has added all initial data for story
		* Exit Criteria - The story has been understood and estimated by engineering or submitted for tech design by a senior engineer
		* Purpose: To hold work to be presented to engineering
	  * Tech Design - Tech Lead needs to provide additional detail for individual contributor for go forward
		* Entrance Criteria - During grooming it was determined that senior engineers need to create a design
		* Exit Criteria - A design suitable for use by the tasked engineer is created and the story is estimated
		* Purpose: In case the story is at too high a level, then a tech design can be created & reviewed.  Infrequently used state as we prefer SPIKE stories.
	  * Sprint Ready - Ready to prioritize
		* Entrance Criteria - The story is pointed and the team understands the purpose and work associated with it
		* Exit Criteria - The PO has an idea about the priority associated with the story
		* Purpose: In case the story is at too high a level, then a tech design can be created & reviewed.  Infrequently used state as we prefer SPIKE stories.
	  * Prioritized - In order represetnation of backlog may span multiple sprints
  * Development States
	  * Scheduled - Waiting for develoepr to pick up, intended to span 1 sprint
	  * Development - Developer is actively working on the item
	  * Code Review - Waiting for code review to complete
  * Deployment and Delivery States
	  * Deploy UAT - code review is past, waiting for UAT deployment
	  * Deliver UAT - PO needs to communicate to Business
	  * Deploy to Prod - PO has gotten UAT approval, needs it on prod
	  * Deliver to Prod - Item has been put into production, PO needs to communicate delivery
	  * Accepted - PO needs to get okay from business about production deployment
	  * Accept Timeout - PO has attempted to get acceptance for three weeks, with multiple requests, assumed accepted

## Views
  * *DS Product Planning
    * Purpose
      * Allow product owners to see new requests
      * Help POs coordinate new work
    * States
      * None - Intake for PO
      * Flesh Out - WIP for PO
      * For Grooming - PO to deliver to development leads
      * Sprint Ready - Grooming complete, PO to prioritize
      * Piroritized - PO prioritizing space
      * Scheduled - PO into sprint
  * *BI Dev Stories
    * Purpose
      * Inform work in progress
    * States
      * Scheduled - Waiting for dev
      * Development - WIP for Dev
      * Code Review - Blocking on Code review
      * Deploy UAT - Pending to deploy to UAT
      * Accepted - Work complete for development projects
  * *BI Dev Delivery
    * Purpose
      * Track items that are going live, potentially not useful once full CI/CD pipeline in place
    * States
      * Scheduled - Send back to WIP for Dev due to delivery problem
      * Deploy UAT - pending to be deployed for UAT
      * Deliver UAT - Pending to be communicated for UAT
      * Deploy to Prod - Pending to be deployed for production on Tue, Wed, or Thu
      * Deliver to Prod - Pending to be commincated for Prod
  * *BI Prod Delivery
    * Purpose
      * Support business communication on delivery
    * States
      * Scheduled - Send back to Dev by PO
      * Deliver UAT - Communicate to business for UAT ready
      * Deliver to Prod - Communicate to business for Prod ready
      * Accepted - Business has approved delivery
      * Accept Timeout - Business has ignored repeat reqests from Prod to accept

