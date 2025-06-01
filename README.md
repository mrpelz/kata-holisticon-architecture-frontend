# kata-holisticon-architecture-frontend

## Problems and Ideas for Solving them Ordered by Severity

### Manual Mock-Server Maintenance/Introduction of GraphQL
* The frontend developers manually maintaining a parallel mock-server is possibly binding development-time that could easily be freed up by using available tooling: the framework used to build the backend might easily produce interface definitions (Swagger UI/JSON-schema/Typescript- or ZOD- definitions, see next headline), which could be used to automatically generate a locally-running mock-server without much manual development needed.
* Not matter which technical approach is taken, it should be strongly emphasized that orally communicating API changes is a huge source of bugs/regressions and finding *any other formalized process* should be the topmost priority.
* Given the ongoing compatibility problems between backend and frontend, I understand the frontend-devs’ desire to introduce GraphQL. On the one hand, GraphQL provides language-agnostic ways to specify interfaces in a type-safe manner, on the other hand it would introduce a huge refactoring. This is a decision the team and stakeholders need to make. GraphQL would ensure a formalized process for a (possibly ever-changing?) API, but proper JSON-schemas (utilized like mentioned in next headline) could serve the same purpose without the need for much refactoring.

### “Hanging Application”/Error Displays
* The introduction of unit tests is a great first step (and is well paired with technically enforcing code coverage goals e.g. in a CI), but might not cover all causes for errors. Is the team using additional tooling to test component-code with unit tests as well (e.g. in React-codebases, all code that produces virtual DOMs needs additional setup to be properly tested)?
* If only the frontend is tested using unit tests, who is testing the backend? Is it enough to introduce end-to-end testing using frameworks like Cypress, does the backend need its own unit tests?
* Is there a technically enforceable “contract” between backend API and frontend consumer? Can this easily be produced by the framework used by the backend, e.g. to automatically create a Swagger UI documentation? Might it be advisable to go the other way around and agree on the endpoints and data structures beforehand and enforce adherence to them using CI-tests?
* If the basis is set to technically test for adherence to specifications, the CI could be setup to only allow deployments to main once a comprehensive test-suite passes (e.g. unit tests for backend and frontend, end-to-end-tests).  
The passing of this test-suit could form part of a “definition of done” for every user story.
* Again: this is an internal application, users might be happy to “dogfeed” new features in a separate beta-test environment, this could improve the quality of feedback regarding new features (see above) and avoid that big bugs only become apparent once deployed to the production environment.

### Codebase Complexity
* It might be advisable to think about special time allotment for maintenance/keeping the codebase tidy long-term.
* For clearing up accumulated “damage”, a temporary team-split could be discussed. This way, a portion of the team could work on necessary refactorings while the other portion keeps working towards deadlines (only feasible if the team itself is confident such a split could work or if new developers can be onboarded quickly).

### Negative Feedback from Users:
* The fact that feedback is collected in a very disjointed, separate process (isolated Jira board managed by a superior) might have historical reasons I can only speculate about and might want to investigate further.  
For external-facing applications it might well be a good idea do have an external process pre-filter feedback in this manner, but given that the software is only used internally, different assumptions can be made about the deep domain-knowledge that can be gained from more direct user feedback. After all, the customer is willing to invest into building bespoke software/expressly wants to replace ready-made software: It can be assumed that they’re looking for a closely “taylor-made” solution.
  * Getting more direct feedback from the users could be facilitated by stopping the practice of using a separate Jira-board for feedback.
    * The lowest-hanging fruit might me using Jira’s own facilities to require certain input for feedback items and using items more directly in the developers’ sprint planning.
    * A more involved process might want to bring users and the development team into direct contact to “air out” the biggest gripes in UX, share domain-specific best-practices and sync expectations. This could happen once or on a regular basis. If this becomes a regular ceremony, it might be a good idea to only send delegates to this meeting (in order to avoid taking too much development-time away from a possibly already time-crunched team).  
    Collecting feedback in a regular meetup and reserve “feedback tickets” for concrete bug reports would possibly enable the team to find commonalities between single feedback items and reduce duplications.
  * A classical user survey in which users are observed while using the software could unearth how their expectations differ from what the new custom software (and possibly even the current, ready-made software) provides, this can result in “bigger picture” insights.  
  For external-facing software, conducting such a survey in a GDPR-compliant manner might be a tricky proposition—the software’s sole internal use could be an advantage.

### Scrum-Adherence and Backend-/Frontend-Split
* I can only speculate what particular flavor of “custom Scrum-like” process the team started out with, but consistently overrunning user stories might point to a slicing problem. If user feedback is collected more directly (see above), I’d encourage the product owner to reintroduce story estimations and sprint plannings and use these ceremonies to refine stories using a previously agreed-upon “definition of ready”. Reintroducing the concept of sprints as a well-defined and successful industry-standard will enable the PO to argue for maintenance and the proper observation of technical dependencies in the planning-stage.
* The differentiation of frontend- and backend-stories could be useful or useless and I can only make assumptions about why it was introduced. It is worth discussing this split, but only with proper knowledge about how deeply integrated the frontend and backend are on a technical level.  
This can also inform technical decisions about the backend-/frontend-split, if there’s tight coupling between the backend and frontend, a monorepo could be a better fit (though the same could be achieved in separate repositories by other technical means)?
