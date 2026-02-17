# Prompt Guide for Scenario: PAP Transaction Stuck + Shift Change Failure
This guide helps automation testers add the following scenario into the existing **Behave Python framework** using the VS Code AI Agent.

> **Test Case:**  
  Scenario: PAP transaction stuck during fueling prevents shift change
    Given Initializing GPI Interfaces
    When I select pump "1"
    And Card Swiped on pump with ";37144983511002=191210196051234500000?"
    And I Set the flow rate on pump to 50
    And the nozzle is lifted on pump
    And the grade is selected on pump
    Then fueling is started on pump
    When I restart the fuel from FCC in the middle of fueling
    Then the transaction should be in a stuck state
    When EOD is requested from FCC
    Then the shift change should fail
    And I should see the message "Dispensing"
    And I hang up the nozzle
    And the shift ID remains unchanged
    And the socket connection is closed successfully

## Context Setup (Tester Instructions)
When asking the AI Agent in VS Code to generatecode for this code, make sure you provide the right **context**:

1. **Feature Files**  
  - Open `C:\automation\Retalix\bdd\features` to view existing feature files.
  - Create the new feature file under: ```features\PerformEOD.feature``` 

2. **C++ Dev APIs**  
  - Open `C:\automation\C++` to view GPI, Ctrl, GCI FCC APIs.
  - Note: 
    - FCC APIs are wrapped in Python via **fuel_proxy.py**.  
    - Simpumps APIs are wrapped in Python via **simpump_proxy.py**.

3.**Proxy Python APIs**
  - **Rule:** Always create raw API wrappers in `fuel_proxy,py` before using them in Behave steps.
  - Behave steps should call **only proxy APIs**, never raw c++.

4. **Logs**  
  - To check the logs of autoamtion run, open `C:\automation\Retalix\bdd\fuel-bdd.log`

## Promts to Use with the Agent

### Step1: Generate a behave feature scenario for the given test case