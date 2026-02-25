# ShinnyHunters-KQL-Hunt
These KQL queries can be used to hunt for ShinnyHunters tatics 
Entra ID Threat Hunting Library (KQL)
This repository contains high-fidelity Kusto Query Language (KQL) hunting queries for Microsoft Sentinel. These hunts focus on detecting modern identity-based attacks, specifically those used by sophisticated threat actors like ShinyHunters and Scattered Spider.

🔍 1. MFA Modification Anomaly (T1556.006)
Goal: Detect unauthorized MFA persistence by flagging "stranger" IP addresses.

The Problem
Threat actors often use Vishing to obtain a one-time MFA code. Once inside, their first move is to "change the locks" by registering their own device or phone number. Standard logs only show that MFA was changed; they don't tell you if the person changing it is a stranger.

The Solution
This query builds a 90-day behavioral baseline for every user. It compares the IP address used for a security change against every IP that user has successfully used to work in the last 3 months. If the change comes from a "Stranger IP," it surfaces for investigation.

🛡️ 2. High-Risk OAuth Consent Detection (T1136)
Goal: Detect "App-Based Phishing" where users grant dangerous permissions to third-party apps.

The Problem
Attackers are moving away from stealing passwords and toward stealing Tokens. By tricking a user into consenting to a "helper app," the attacker gains permanent access to the user's inbox or files without needing to bypass MFA again.

The Solution
This query monitors the ConsentToApplication operation and filters for High-Risk Scopes (permissions). It specifically looks for apps requesting the ability to read all mail or access CRM data.

🛠️ How to Use This Library
Copy the KQL code into your Microsoft Sentinel Logs blade.

Tune the "Noise Suppression" section of the MFA hunt by adding your company's VPN/Office IP ranges.

Automate these by saving them as Scheduled Analytics Rules to generate incidents in real-time.
