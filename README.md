# SOAR-EDR

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned
[Bullet Points - Remove this afterwards]

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps
1. Using <a href="draw.io">Draw.io</a> create a playbook workflow. Where an alert is propagated and sent over to <a href="https://limacharlie.io/">LimaCharlie</a>. Then sent to <a href="https://www.tines.com/">Tines</a>. Tines then sends a message with specified details to <a href="https://slack.com/">Slack</a>, am email to a registered email address, and prompts the user to isolate the machine or not. If the user says yes then LimaCharlie goes ahead and isolates/quarantines the affected machine and delivers a message to Slack with a status of the isolated machine including a message of isolation. If no, then a message is sent to Slack notifying the machine has not been isolated/quarantined and an investigation should be performed.<br>
    ![SOAR EDR Playbook](https://github.com/user-attachments/assets/a68917fd-6f2a-4d90-94cd-fde2fbb6a3cf)<br>
*Ref 1: SOAR EDR Playbook*<br>
2. Setup an account with LimaCharlie. Navigate over to Installation keys to create an installation key.<br>
    ![1  Limacharlie installation keys screen](https://github.com/user-attachments/assets/070ec4b4-6eb9-4587-b1f8-4232545c9dc7)<br>
*Ref 2: Installation keys screen*<br>
3. Under the Sensor Downloads section right-click the Windows 64-bit one and copy link address.<br>
    ![2  New installation key](https://github.com/user-attachments/assets/4eec227b-3fca-4d14-a7c0-16cfc9aaca20)<br>
4. Spin up a VM (or use a cloud option) with Windows 10 and paste the link into the browser on that VM. Go back to the Installation Keys screen and copy the Sensor key. Open a PowerShell with admin. privilieges on your Windows machine and navigate it to your downloads directory. <br>
    ![3 Navigate to download directory in PS](https://github.com/user-attachments/assets/e87c34af-a25d-44f5-98f9-8fe643b1ae9e)<br>
*Ref 3: PS download directory*<br>
*Ref 4: PS navigate to downloads*<br>
5. Type in hcp and hit <tab> -i <Sensor key> and hit enter to install the sensor.<br>
    ![4  successful agent installled](https://github.com/user-attachments/assets/a24482c4-37a5-4148-a0c8-51785a292276)<br>
*Ref 5: LC Agent Install*<br>
6. Go back to the LimaCHarlie dashboard and click sensor list, find the newly installed sensor name, and click it.<br>
    ![5  LC VM Sensor](https://github.com/user-attachments/assets/003897c8-9174-4bee-bb7e-8a1955197e9c)<br>
*Ref 6: LS VM Sensor*<br>
7. Next download <a href="https://github.com/AlessandroZ/LaZagne">LaZagne</a> and open a PowerShell on your Windows VM to check. We can also check for activity in LimaCHarlie dashboard under Sensors and can see a timeline of activity.<br>
    ![6  LC Sensor lazagne](https://github.com/user-attachments/assets/af617828-cf8e-4d5a-847c-7035f7971e4f)<br>
*Ref 7: LC Sensor LaZagne*<br>
8. Open LimaCharlie in a new tab, and click your orginization, next select automation then Detection and Response rules. Having a rule that detects any occurence of LaZagne with operators that check for certain criteria in the file path, command line, and hash executions. After we define detection criteria, define the response actions and save the rule.<br>
    ![7  EDR Rules](https://github.com/user-attachments/assets/97a683b7-d88b-4a6e-9163-bef12a23904e)<br>
*Ref 8: EDR Rules*<br>
    ![8  Event Collection](https://github.com/user-attachments/assets/799065ae-2e09-4b90-a87d-b736965807de)<br>
*Ref 9: Event Collection section for reference*<br>
    ![9  Events for detection](https://github.com/user-attachments/assets/147203ef-71dc-4df2-a668-7ac929c75940)<br>
*Ref 10: Events for detection*<br>
    ![10  Events for response](https://github.com/user-attachments/assets/6d12188a-6cef-4a85-aa64-d96b67e22405)<br>
*Ref 11: Events for response*<br>
9. To test your rule, copy and paste an event in the Event box under Target Event.<br>
    ![11  Target even for testing](https://github.com/user-attachments/assets/c90a299f-1e71-42e6-871b-772d5b090465)<br>
*Ref 12: Target event for testing*<br>
    ![12  Testing results](https://github.com/user-attachments/assets/219c1451-189f-45b9-83dc-eba9a4671225)<br>
*Ref 13: Testing results*<br>
    ![13  Lazagne detections from new rule](https://github.com/user-attachments/assets/f05ac6af-5670-48d4-a65d-b3409cc02f48)<br>
*Ref 14: LaZagne detections from new rule*<br>
10. Go to orginization from the home page of LimaCharlie dashboard and select detection. Clear all of them and head back to your Windows 10 VM/server to run LaZagne. Go back to find detections after LaZagne is ran. We can now use the available fields in the event detection in our playbook.
11. Get Slack, create a new channel for alerts so that Tines can send alert messages to teh alert channel.<br>
    ![14  Alerts channel](https://github.com/user-attachments/assets/e8709c6a-9e01-4d3c-9e49-4c9bb07c0cd2)<br>
*Ref 15: Alerts channel*<br>
12. Get Tines and establish a new link between LimaCharlie and Tines. <br>
    ![15  Start Tines playbook](https://github.com/user-attachments/assets/8ca0896f-2023-4eb5-96f3-8fd03facb62b)<br>
*Ref 16: Star Tines Playbook*<br>
13. Drag in a webhook and name it "Retrieve Detections", a description of "Retrieves LimaCharlie dections" and copy the webhook URI.
14. Go to LimaCharlie, select your orginization then go to outputs, add output, pick Tines, and paste in the webhook URI.<br>
    ![16  LC to Tines output](https://github.com/user-attachments/assets/52b439f4-5f74-4db7-9d8f-af7b87849496)<br>
*Ref 17: LC to Tines output*<br>
    ![17  LC output event](https://github.com/user-attachments/assets/d9469055-84c0-42c8-81df-c77e53fe9a03)<br>
*Ref 18: LC output event*<br>
15. Back at Tines, select events under retrieve detections webhook and select the most recent detection<br>
    ![18  Tines event detected LaZagne](https://github.com/user-attachments/assets/d729d927-ad78-4873-a600-57409e1592c4)<br>
*Ref 19: Tines event detected LaZagne*<br>
    ![19  Tines recent detection](https://github.com/user-attachments/assets/6fb9b87c-0db8-464b-8472-5d64a3d4e1b2)<br>
*Ref 20: Tines recent detection*
16. Go over to Slack and click more and then automations. Search for Tines under Apps. In Tines go to your teams, then credentials to add a new credential, pick Slack. Use Tines app for Slack.<br>
    ![20  Slack for Tines](https://github.com/user-attachments/assets/0ffc2fe8-a286-4573-92d1-ed1895a13281)<br>
*Ref 21: Slack for Tines*<br>
17. Head over to your story, select templates and drag over Slack. Search for message on the right, select send a message.<br>
    ![21  Tines Send a message](https://github.com/user-attachments/assets/5362c3a5-20f9-4f9e-b2e2-9ea52fc98dd5)<br>
*Ref 22: Tines send a message*<br>
18. In Slack right click alertd channel and select view channel details.<br>
    ![22  View channel details](https://github.com/user-attachments/assets/af40927a-9dff-428a-a32c-8e8579c079ab)<br>
*Ref 23: View channel details*<br>
19. Copy the channel ID. Paste it into the Slack channel ID field over in Tines, click connect to Slack(close the popup).<br>
    ![23  Channel ID field tines](https://github.com/user-attachments/assets/365ff708-61a6-46ae-916d-2a25695c2c7f)<br>
*Ref 24: Channel ID field Tines*
20. Click out of the Slack app and click connect on the right beside slack (if no connections refresh, if not reconnect and click Tines slack app). Connect the webhook to Slack app, click run, then click status. Check the log to see sending to channel, head over to Slack channel to see the maessage<br>
    ![24  Connect webhook to slack](https://github.com/user-attachments/assets/3c581356-6aaf-409b-9f90-426267c6f1fb)<br>
*Ref 25: Connect webhook to Slack*<br>
    ![25  Slack status](https://github.com/user-attachments/assets/ffea54f3-5278-4937-92b0-eed53543b95c)<br>
*Ref 26: Slack status*<br>
    ![26  Logs sending](https://github.com/user-attachments/assets/120866df-e6d1-4d3d-8e97-9f63b846782e)<br>
*Ref 27: Logs sending message*<br>
    ![27  Tines alert message](https://github.com/user-attachments/assets/18b50492-81f0-4e10-bace-7ee7dcfb00d7)<br>
*Ref 28: Tines alert in Slack*<br>
21. Back at Tines, drag in a send email, connect retrieve detections to it.<br>
    ![28  Connect wh to send email](https://github.com/user-attachments/assets/d92816ce-4c67-4fbf-8214-124f5e225bf1)<br>
*Ref 29: Connect webhook to send email*<br>
22. Click build tab in send email, fill in the description, for the email <a href="https://sqrx.com/">SquareX</a> disposable email was used.<br>
    ![29  Build tab in send email](https://github.com/user-attachments/assets/5292c0a6-3af3-461a-a179-b759653dc7b7)<br>
*Ref 30: Build tab in send email*<br>
23. Click on send email then test, select the retrieve detections webhook and test. Check for Tines email.<br>
    ![30  Tines alert email](https://github.com/user-attachments/assets/a04685f7-2241-4c9f-9fc6-675cd4ed89f5)<br>
*Ref 31: Tines alert email*<br>
24. In Tines click under tools on left, drag in a page, name it user prompt, put in a desctiption of what it does, and link the webhook to it.<br>
    ![31  User Prompt](https://github.com/user-attachments/assets/ff6ad892-0dbd-4931-bed5-ee54084ac3b1)<br>
*Ref 32: User Prompt*<br>
    ![32  webhook linked to user prompt](https://github.com/user-attachments/assets/10892023-b0b9-4524-a90c-8188e81fc881)<br>
*Ref 33: Webhook link to user prompt*<br>
25. Click on edit page and fill out the header and body of the user prompt, drag in a boolean and change it's name.<br>
    ![33  user prompt page](https://github.com/user-attachments/assets/b27bb0ff-f27d-4059-a0a2-97d08aabcc54)<br>
*Ref 34: User prompt page*<br>
26. Select the webhiook on the story page, click events, expand body and copy relevant fields.<br>
    ![34  Event fields](https://github.com/user-attachments/assets/0b8c0887-fe38-4840-b3cc-be120c7f84de)<br>
*Ref 35: Event fields*<br>
27. Im Tines click on Slack, under message click the +. Click Value and look for data. Click on retrieve detections(x2), click body(x2), find each field and click out of it to save. Pasting in the value from your notes also works<br>
    ![35  Slack Message fields](https://github.com/user-attachments/assets/4aaf1899-f5b5-45a6-a126-97532bcfaa0a)<br>
*Ref 36: Slack message fields*<br>
28. Click on test under Slack app. Should see an alert on slack itself. For readability add labels to fields. And clicking on the detection link will display the details in LimaCharlie.<br>
    ![36  Alerts on Slack](https://github.com/user-attachments/assets/59ca6565-0477-4d47-bc33-45ca11e23326)<br>
*Ref 37: Alert on Slack*<br>
    ![37  Readability fields](https://github.com/user-attachments/assets/e370aa44-f16b-485d-a4db-365201e7021b)<br>
*Ref 38: Readability Fields*<br>
    ![38  Slack readability fields](https://github.com/user-attachments/assets/297a1d1c-d6ec-4a8b-86c3-9e889a4447e7)<br>
*Ref 39: Readability in Slack*<br>
    ![39  Alert details from detection link](https://github.com/user-attachments/assets/e4665f88-b052-4cb7-8204-09bfc5f6ca0b)<br>
*Ref 40: Alert details from detection link*<br>
29. Click on send email and paste those readability fields into the body to make it look better(or keep them like the original). Click on open HTML editor and insert breaks, again for readability.<br>
    ![40  Readability fields in send email](https://github.com/user-attachments/assets/f06c054c-22a9-45df-9f03-cc29ad83bc20)<br>
*Ref 41: Readability fields in send email*<br>
    ![41  Email line break readability](https://github.com/user-attachments/assets/4350e943-06bf-4650-81d9-9a3236f02c9e)<br>
*Ref 42: Email line break readability*<br>
    ![42  Tines alert email](https://github.com/user-attachments/assets/f3a36f53-99b0-4d15-8a66-de195b6d02b8)<br>
*Ref 43: Tines alert email*<br>
30. Click on User Prompt then on edit page, paste in alert fields and go back to test, click on visit page.<br>
    ![43  User prompt alert fields](https://github.com/user-attachments/assets/a8701b68-80b2-433f-b4d4-fd962e7877c2)<br>
*Ref 44: User Prompt alert fields*<br>
31. Back on the story screen drag in a trigger form the left. Name it "No" and connect the User Prompt element to it.<br>
    ![44  Tines trigger](https://github.com/user-attachments/assets/e03c3a6c-3f4b-4088-b881-01d031402e86)<br>
*Ref 45: Tines trigger*<br>
    ![45   Tines no trigger](https://github.com/user-attachments/assets/02c6ea1d-5683-4c2b-aa07-4a3f182989e1)<br>
*Ref 46:  Tines "No" trigger*<br>
32. For rules click on +, value, user prompt(x2), body(x2), isolate then click out of it to save. On the right change foo to false in the trigger build tab.<br>
    ![46  foo to false](https://github.com/user-attachments/assets/7d6fb291-bef1-4280-bca2-61dd37bc21e2)<br>
*Ref 47: Foof to false*<br>
33. Copy the Slack message and paste it into the story, change the message and connect it to the "No" trigger and test it from the trigger element.<br>
    ![47  Slack message for no trigger](https://github.com/user-attachments/assets/8394cfd5-dcaa-42a4-b2d6-da2812318c89)<br>
*Ref 48: Slack message from no trigger*<br>
    ![48  Slack alert from trigger test](https://github.com/user-attachments/assets/71f99d55-e1db-4d95-9876-7d67de4255e9)<br>
*Ref 49: Slack alert from trigger test*<br>
34. 
