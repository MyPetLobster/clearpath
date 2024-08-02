
# Misc. Notes/Considerations 

- Environmental impact of idling cars. Are 4-way stops more or less efficient than traffic lights?
- Use available highway traffic signs to notify drivers of nearby pursuit.
- Extend possible radius and alert all schools in potential area of pursuit.
- Check for any other events or activities scheduled in the area where people may be put in danger.
- Would my system give any kind of advantage to the suspect? If so, how can I mitigate that?



# AI Summary of ClearPath

Task
State the problem you are planning to solve.

ClearPath PATS (Pursuit Activated Traffic System) aims to enhance public safety by automatically converting traffic signals in the path of emergency vehicles and police pursuits into 4-way blinking red stop lights, thereby reducing the risk of accidents and ensuring safer intersections.

Requirements
Describe the problem you are trying to solve for.
The primary problem is the high risk of accidents at intersections during emergency vehicle responses and police pursuits. Current systems often rely on manual updates and lack comprehensive automation to ensure all relevant intersections are made safer in real-time.

Describe any input data you expect to use.

GPS data from emergency vehicles (e.g., police cars, ambulances).
Real-time traffic signal status from city traffic management systems.
Voice inputs from dispatchers during pursuits for AI keyword detection.
Map data to identify intersections and road layouts.
Describe what the program will do to solve the problem.

Continuously track the GPS location of emergency vehicles.
Predict the potential path of these vehicles and identify intersections within this path.
Automatically change traffic lights within the predicted path to 4-way blinking red stop lights.
Use AI to listen for critical updates from dispatchers and adjust the path prediction and traffic light control accordingly.
Extend the safety zone (expanded cone) to include schools and public gatherings based on detected keywords and situational analysis.
Describe any outputs or results the program will provide.

Real-time updates to traffic signals, converting them to 4-way blinking red stop lights in the vehicle's path.
Visual and auditory alerts at intersections for pedestrians and drivers.
Logs of all changes made and the reasons for those changes.
Notifications to schools and public venues if they fall within the expanded danger zone.
Inspiration
Why do you want to solve this particular problem?
The idea is inspired by the need to improve public safety during critical situations involving emergency vehicles. Reducing the risk of accidents at intersections can save lives and ensure that emergency responders can perform their duties more effectively.

What source(s) of data do you believe you will need? Will the user need to supply that data, or will you get it from an external file or another source?

GPS Data: Provided by the emergency vehicle systems.
Traffic Signal Data: Obtained from city traffic management systems.
Map Data: Sourced from geographic information system (GIS) providers.
Voice Input: Real-time voice data from dispatchers.
Will you need to interact with the user throughout the program? Will users continually need to enter data in and see something to continue?

Minimal direct user interaction is expected. Most data will be obtained automatically from integrated systems.
Dispatchers may need to provide voice updates, which the AI Listener will process.
What are your expected results or what will be the end product? What will you need to tell a user of your program when it is complete?

End Product: A simulation demonstrating the ClearPath PATS system's functionality, showing real-time changes to traffic signals based on the movement of emergency vehicles.
User Information: Instructions on how to use the simulation, an overview of the system's benefits, and a summary of how it enhances public safety.
Summary
The ClearPath PATS simulation will showcase how advanced technologies can be integrated to create a safer environment for emergency responses and police pursuits. This project serves as a foundational step toward a fully operational system that can be deployed in real-world scenarios, enhancing public safety and response efficiency.




# Notes from Python Sophia Course Project Planning 

    PHASE 0 (Constant, Setup)
Each instance of ClearPath has access to a local map.
There are AI agents on standby ready to be assigned to an event. These are represented by the Agent class. Each instance of which will create its own context, event ID, and emergency vehicle IDs.


Scenario 1: 911 call for a broken leg at a specific address

    PHASE I (Analyze, Calculate Cone)
Dispatch triggers the ClearPath system, providing the system with the ID numbers of all responding emergency vehicles and the address of the caller.
The system creates an object in memory for this response ‘event’.
The system creates an object in memory for each responding emergency vehicle and plots it on the local map. This is constantly updated to check for additional vehicles.
The system will use each emergency vehicles speed, direction, x & y coords, and the caller address to calculate the potential paths that the emergency vehicles will take. This result of this calculation is the ‘cone’. 
     
    PHASE II (Action, Clear the Path, Listen)
All traffic lights within the cone are converted to blinking red light 4-way stops. This is constantly updated until the emergency vehicles reach the caller’s location, or there are no more traffic lights between the vehicle and destination. 
To account for potential route variation, the cone will effect lights beyond the calculated gps routes. 
Throughout this process the AI Agent is patched in to all dispatches related to this event and actively listening for keywords that indicate whether or not the somebody at the caller’s location will need to be transported to the hospital. If so, a route to the nearest/most likely hospital based on dispatch conversations or simply using the map. Dispatch has the ability to override this and manually enter the hospital at any point by simply stating “ClearPath, they will be going to Mercy Med in Portland”. The AI will here this voice command and override any previous calculations. 
ClearPath is activated for all traffic lights between the caller’s location and hospital when the emergency vehicle leaves the caller’s location.


Scenario 2: A police officer begins to pursue a suspect

    PHASE I (Analyze, Calculate Cone)
When a pursuit begins, the initial call to dispatch will trigger the ClearPath Pursuit Activated Traffic System, or PATS. PATS operates similarly to ClearPath’s default mode, except it has a different algorithm for calculating and updating the cone of danger.
The system creates an object in memory for this pursuit ‘event’. A pursuit event will keep track of the lead pursuer, who’s GPS data will be used for main cone calculations.
The system creates an object in memory for each responding emergency vehicle and plots them on the local map. Only the lead pursuer will interact directly with the PATS system. Other emergency responders en route to aid in the chase will be handled by the default ClearPath algorithm, even once they join the pursuit (The PATS signal will override any other cones in the area, thus avoiding conflicts).
PATS will calculate the pursuit cone based on the lead pursuer’s speed, direction and x/y coords. This will have a wider area than the basic ClearPath emergency response cone.

    PHASE II (Action, Clear the Path, Listen)
All traffic lights within the cone are converted to blinking red light 4-way stops. And all crosswalk signs at these intersections will blink “Stop” and emit an audible signal to notify visually impaired pedestrians of potential danger. Each traffic light returns to normal operation when the lead pursuer is a half mile away from the light. When PATS is deactivated, if there are still pursuing vehicles near an intersection, they will trigger the ClearPath response (the lead pursuer is essentially the “caller’s location” for these cases).
Along with traffic lights in the cone being converted to 4-way stops, any available electronic road signs are ‘hijacked’ and used to display a message notifying motorists of a potential police pursuit in the immediate area.
An expanded cone area is detected and this entire area is scanned for school or any kind of event where many pedestrians may be gathering. If any of these vulnerable locations is detected, they will be notified by dispatch of possible danger. If they are part of the ClearPath program, a notification will also be sent automatically.
Throughout this process the AI Agent is patched in to all dispatches related to this event and actively listening for keywords related to the status of the pursuit and behavior of the suspect. Examples of such keywords are: “gun”, “erratic”, “dangerous”, “shots fired”, “need backup”, etc. 
If a keyword is detected, the AI will implement the necessary response, including passing this info on to vulnerable locations and making adjustments to the cone as needed.
This process continues until the pursuit is terminated, at which point ClearPath will remain in control if any other emergency response is required including firetrucks or ambulances to scene of the terminated pursuit.



# ClearPath PseudoCode for Sophia course project

Scenario 1: 911 Call for a Broken Leg at a Specific Address
Input Data:
GPS coordinates of emergency vehicles.
Address of the caller.

Steps:
Initialize System:
Dispatch triggers the ClearPath system with emergency vehicle IDs and caller’s address.
Calculate Path:
System calculates potential paths for emergency vehicles using their speed, direction, and location.
Defines the 'cone' of influence where traffic lights need to be controlled.
Control Traffic Lights:
All traffic lights within the cone are converted to blinking red 4-way stops.
System continuously updates traffic lights based on vehicle movement until vehicles reach the caller’s location.
AI Monitoring:
AI listens to dispatcher updates for keywords indicating transportation needs.
If hospital transport is needed, the system recalculates the path and updates traffic lights accordingly.

Result:
Traffic lights are controlled to ensure a safe and efficient route for emergency vehicles to the caller’s location and potentially to a hospital.

Scenario 2: Police Officer Begins to Pursue a Suspect
Input Data:
GPS coordinates of the lead pursuing vehicle.
Voice updates from the dispatcher.

Steps:
Initialize System:
Pursuit starts, triggering the ClearPath Pursuit Activated Traffic System (PATS).
PATS tracks the lead pursuing vehicle using its GPS data.
Calculate Pursuit Path:
PATS calculates the pursuit cone based on the vehicle’s speed, direction, and location.
Control Traffic Lights:
All traffic lights within the pursuit cone are converted to blinking red 4-way stops.
Crosswalk signals blink “Stop” with audible signals for visually impaired pedestrians.
Electronic road signs display alerts about the pursuit.
AI Monitoring:
AI listens for keywords indicating heightened danger (e.g., “gun”, “erratic”).
If keywords are detected, the system expands the cone and notifies vulnerable locations like schools.

Result:
Traffic lights and pedestrian signals are controlled to ensure public safety during the pursuit. Alerts are issued to notify motorists and pedestrians of the pursuit.


Summary:
By following these simplified steps, ClearPath PATS enhances safety during emergency responses and police pursuits by dynamically controlling traffic lights and issuing public alerts, ensuring a safer environment for both emergency responders and the public.


Scenario 1: 911 Call for a Broken Leg at a Specific Address
Initialize map data 
Initialize AI agents (Agent class) for event handling

# Phase 1 - Analyze and Calculate Cone
Function handle_911_call(caller_address, emergency_vehicle_ids): 
    Create event object with event ID 
    For each vehicle_id in emergency_vehicle_ids: 
        Create vehicle object with vehicle_id 
        Plot vehicle on map 

    While event is active: 
        For each vehicle in event vehicles: 
            Update vehicle's speed, direction, x, y coordinates 
            Calculate potential path to caller_address 
            Define 'cone' of influence for each path

    # Phase 2 - Action, Clear the Path, Listen
    Function update_traffic_lights(cone): 
        For each traffic light in cone: 
            Set traffic light to blinking red 4-way stop 

    Function monitor_dispatch(): 
        Listen for keywords in dispatcher updates 
        If transport needed to hospital: 
            Calculate path from caller_address to hospital 
            Extend cone to include path to hospital 
            Update traffic lights for extended cone 
            If dispatch overrides with specific hospital: 
                Recalculate path and update traffic lights 

    While event is active: 
        Update_traffic_lights(cone) 
        Monitor_dispatch() 

    End while 
End function


Scenario 2: Police Officer Begins to Pursue a Suspect
Function handle_pursuit(lead_pursuer_id, supporting_vehicle_ids):
    Create pursuit event object with event ID
    Create lead pursuer object with lead_pursuer_id
    Plot lead pursuer on map

    For each vehicle_id in supporting_vehicle_ids:
        Create vehicle object with vehicle_id
        Plot vehicle on map

    While pursuit is active:
        Update lead pursuer's speed, direction, x, y coordinates
        Calculate pursuit cone based on lead pursuer's data
        Define wider area for pursuit cone
    Function update_pursuit_traffic_lights(cone):
        For each traffic light in cone:
            Set traffic light to blinking red 4-way stop
            Set crosswalk signals to blink "Stop" and emit audible signals

    Function update_electronic_signs(cone):
        For each electronic road sign in cone:
            Display pursuit alert message

    Function monitor_pursuit_dispatch():
        Listen for keywords in dispatcher updates
        If keyword detected (e.g., "gun", "erratic"):
            Expand cone area
            Notify schools and public venues in expanded cone
            Update traffic lights for expanded cone

    While pursuit is active:
        Update_pursuit_traffic_lights(cone)
        Update_electronic_signs(cone)
        Monitor_pursuit_dispatch()

    End while
    If pursuit ends:
        If further emergency response needed:
            Handle as regular emergency event with ClearPath

End function
