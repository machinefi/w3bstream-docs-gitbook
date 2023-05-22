# Event Routing Strategies

An Event Routing strategy is a rule that assigns a handler to a specific W3bstream event, and it is used to determine the appropriate action to take when a particular event is emitted in W3bstream. Multiple event strategies can be defined for each W3bstream project, and they must include the name of the event to be handled, and the name of an event handler defined in the Project's applet.

### Default Routing

A special "Default Routing" can be defined with "DEFAULT" as the event type. This route will match any IoT message sent to the project that doesn't specify an event type, as well as those with "DEFAULT" as the event type. For convenience, such a default routing is automatically added when creating a new project.
