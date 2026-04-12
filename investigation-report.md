# SOC Investigation Report

## Objective
Investigate authentication logs using Splunk SIEM to detect suspicious login attempts.

## Tools Used
- Splunk SIEM
- Log Analysis

## Investigation Steps
1. Imported authentication logs into Splunk
2. Searched for failed login attempts
3. Identified IP addresses with repeated login failures
4. Investigated suspicious login activity

## Findings
Multiple failed login attempts were observed from a single IP address, indicating a potential brute-force attack.

## Conclusion
Log analysis helped identify abnormal authentication behavior and possible unauthorized access attempts.
