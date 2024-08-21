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
*Ref 1: SOAR EDR Playbook*
2. 
