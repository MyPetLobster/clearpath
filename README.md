# ClearPath Traffic Safety
The goal of Clearpath is to save lives by making police pursuits safer without the need to add or modify any existing physical infrastructure.

## Mission Statement

ClearPath's PATS is a traffic safety system that uses a combination of predictive analytics, machine learning, and real-time data to detect and respond to police pursuits and emergency vehicle responses. PATS will calculate a predicted path of the pursuit and a cone of danger around the predicted path. Using the predicted path, PATS will enact a number of safety measures to protect pedestrians, drivers, and the police officers involved in the pursuit. 

These safety measures include:
- Converting all intersections in the cone to a 4-way stop until the pursuit has passed
- Converting all pedestrian crosswalks in the cone to a flashing "Do Not Cross" signal
- Audibly notify visually impaired pedestrians of the danger
- Sending a notification to all vehicles with the ClearPath app installed within the cone
- Sending a notification to all cell phones pinging of cell towers near an expanded cone of danger
- Sending a notification to all schools, hospitals, and other high traffic areas near an expanded cone of danger
- Hijacking available highway signs to display a message to drivers that a pursuit is in progress and to be cautious


## Pursuit Activated Traffic System (PATS)
    - Detect when a police pursuit is initiated or emergency vehicle is responding to a call.
        - Emergency vehicle responding will be easier to calculate a path and cone of danger for.
        - Identifying pursuits - listening to dispatch for each patrol officer. Listen for the officer's call sign and the word "pursuit" or other words that indicate a pursuit is in progress.
            - If police integrate ClearPath into their dispatch system, this could be automated.
    - Calculate a predicted path of the pursuit
    - Calculate a cone of danger around the predicted path
        - Using a measure for 'unpredictable' behavior. Higher values will widen the cone.
    - Broadcast the cone of danger to all vehicles with the ClearPath app installed within the cone
    - Using a connection to each town's traffic light system, convert all intersections in the cone to a 4-way stop until the pursuit has passed.
    - Using a system similar to the Amber Alert system, send a notification to all cell phones pinging of cell towers near an expanded cone of danger. Only activate this at a certain threshold of danger (Very high speeds, erratic driving, gunshots, etc.)
    - Using a secondary expanded cone algorithm, determine the likelihood that the pursuit may enter any sensitive areas such as schools, hospitals, or other high traffic areas. If the likelihood is high, send a notification to the affected area to alert pedestrians and drivers to danger.
        - Perhaps schools could opt-in to a system that would alert them, especially during the times when children are arriving or leaving school. This way bus drivers and parents could be alerted to the danger and take appropriate action.
    - Hijack available highway signs to display a message to drivers that a pursuit is in progress and to be cautious.


# TO DO LIST

## Research, planning, and data collection
- [ ] Create a list of all possible data sources
- [ ] Research statistics on police pursuits
- [ ] Research how traffic lights systems work and how I would approach integrating with them
- [ ] Research how to hijack highway signs
- [ ] Research how to send notifications to cell phones
- [ ] Research police protocols for pursuits and codes for different situations

## Create a prototype
- [ ] Create a small scale traffic simulation that can simulate a police pursuit with random speeds and decisions.
    - [ ] Cars should follow the rules of the road and seem random.
        - [ ] Research reaction times and decision making for drivers to make the simulation more realistic.
    - [ ] Create a system of traffic light controls based on real-world traffic light systems.
        - [ ] Enable a switch for all intersections to a simple 4-way stop system.
    - [ ] Create a randomized pursuit system that will follow a path and make random decisions.
        - [ ] Create the suspect car simulation
        - [ ] Create the police car simulation
        - [ ] Create a system for the police car to follow the suspect car
        - [ ] Create a system for the suspect car to evade the police car
        - [ ] Create a pseudo dispatch system
    - [ ] Create a pseudo-cell phone for each car (object)
    - [ ] Add some highway signs to the simulation
    - [ ] Create a system for the simulation to send notifications to the cell phones and highway signs
    - [ ] Add a school and/or hospital to the simulation
    - [ ] Create a system for the simulation to send notifications to the schools and hospitals
    - [ ] Add crosswalks and pedestrians to the simulation
    - [ ] Add crosswalk signs to the simulation
    - [ ] Add a system for the simulation to send notifications to the crosswalk signs
        - [ ] Crosswalk signs will flash "Do Not Cross" when a pursuit is in progress, requiring no additional graphics.
        - [ ] Integrate with sound system for the visually impaired
    - [ ] Create art assets for all of the above


    ## Testing/Data Collection
    - [ ] Run the simulation for a while without ClearPath enabled to collect baseline simulation data
    - [ ] Run the simulation with ClearPath enabled to collect data -- try different combinations of settings enabled and disabled
    - [ ] Analyze the data to determine if ClearPath is effective
    - [ ] Analyze the data to determine if ClearPath is safe
    - [ ] Analyze the data to determine if ClearPath is efficient
    - [ ] Analyze the data to determine if ClearPath is cost-effective
    - [ ] Analyze the data to determine if ClearPath is scalable

    ## Creating a Proposal/Presentation
    - [ ] Create a detailed proposal and presentation
    - [ ] Research who to present the proposal to
    - [ ] Present the proposal to the appropriate parties





### Background
