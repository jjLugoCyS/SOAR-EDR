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
*Ref 3: PS navigate to downloads*<br>
5. Type in hcp and hit <tab> -i <Sensor key> and hit enter to install the sensor.<br>
    ![4  successful agent installled](https://github.com/user-attachments/assets/a24482c4-37a5-4148-a0c8-51785a292276)<br>
*Ref 4: LC Agent Install*<br>
6. Go back to the LimaCHarlie dashboard and click sensor list, find the newly installed sensor name, and click it.<br>
    ![5  LC VM Sensor](https://github.com/user-attachments/assets/003897c8-9174-4bee-bb7e-8a1955197e9c)<br>
*Ref 5: LS VM Sensor*<br>
