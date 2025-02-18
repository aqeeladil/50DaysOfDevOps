## Project Requirements: IVR System Using Asterisk with 3 Extensions and CDR Logging

1. Asterisk IVR Setup:
o Create an Interactive Voice Response (IVR) system in Asterisk.
o The IVR will provide 3 options:
```
1. Press 1 for Sales (Extension: 1001)
2. Press 2 for Support (Extension: 1002)
3. Press 3 for Billing (Extension: 1003)
```
o Route the call to the appropriate department based on the caller's input.

2. Extension Configuration:
o Create 3 extensions in Asterisk:
```
▪ 1001 (Sales): Route to the sales department or agent.
▪ 1002 (Support): Route to the support department or agent.
▪ 1003 (Billing): Route to the billing department or agent.
```
o Each extension should have a unique destination and ring on a different phone or 
softphone.

3. Call Detail Record (CDR) Logging:
o Configure CDR logging in Asterisk to store call information (such as caller's 
number, extension reached, call duration, and call status) in a MySQL database.
o Set up a CDR MySQL database with appropriate tables to log call details for 
analysis.

4. Pre-recorded IVR Message:
o Record and play a custom IVR menu message:
"Press 1 for Sales, Press 2 for Support, Press 3 for Billing."
o Use Asterisk’s Playback() or Background() functions to play the message.

5. Call Routing Logic:
o Implement logic to handle the user’s input (1, 2, or 3) and route the call to the 
correct extension.
o Handle cases where the caller doesn’t enter a valid option.

6. Testing:
o Test the IVR system to ensure the correct routing and functionality.
o Verify that call details are properly logged in the MySQL database.
