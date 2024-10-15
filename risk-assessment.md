# Risk Assessment and Vulnerability Analysis
Identify potential vulnerabilities within the aviation site. Consider and outline a plan for how an attacker could exploit these vulnerabilities. Analyze security measures, assess various attack vectors, and use resources like Common Weakness Enumerations (CWEs) and Common Attack Pattern Enumeration and Classification (CAPECs) to inform your assessment.

![attack_graph](https://github.com/user-attachments/assets/8a5abef2-2974-48bc-b5a8-e3f946e42acd)

## 1. Attack Entry

#### Objective:
The attackers gain entry to the aviation facility by posing as maintenance employees. They deceive airport staff by using false credentials and manipulating behavior to gain trust.

#### Attack Patterns:
1. **Identity Spoofing (CAPEC-151)**: The attackers use forged documents and credentials to apply for jobs at the aviation facility.
2. **Manipulate Human Behavior (CAPEC-416)**: Through social engineering tactics, they exploit the trust of legitimate employees, convincing them to grant access to restricted areas.

## 2. Physical Access to Critical Areas: Control Tower and Airplane Maintenance
#### Objective:
Once inside, the attackers use their positions as maintenance workers to gain access to two key locations:

1. **Control Tower**: One attacker works in proximity to the communication systems, allowing access to the tower’s data and control systems.
2. **Airplane Maintenance**: The second attacker works directly on airplanes during routine maintenance, allowing physical access to the airplane’s systems.

#### Attack Patterns:
1. **Supply Chain Attack (CAPEC-437)**: Attackers may introduce compromised components or malicious software updates within the Control Tower systems to infiltrate deeper into the network.
2. **Code Injection (CAPEC-242)**: Inside the Control Tower, the attackers inject malicious code into the communication or control software, setting up further exploits for information extraction and manipulation.

## 3. System Exploitation
#### Objective:
The attacker in the **Control Tower** uses their position to exploit the system by:

1. Excavating sensitive data, such as pilot and crew Sensitive Personal Identifiable Information (SPII), flight plans, schedules, and intercepting communications between the tower and the airplane.
2. Manipulating the data structures to create backdoors for ongoing access and manipulation.
#### Attack Patterns:
1. **Excavation (CAPEC-116)**: The attacker searches for and extracts sensitive information such as airplane communication logs, flight schedules, or operational protocols.
2. **Interception (CAPEC-117)**: They intercept real-time communications between the Control Tower and the airplane, gathering valuable data that could be sold or used in further attacks.
3. **Schema Poisoning (CAPEC-271)**: The attacker corrupts the database schema, enabling unauthorized access to critical functions, allowing for ongoing control and manipulation of communications.

## 4. Accessing the Airplane: CAN Bus and Control Domain Attack
#### Objective:
On the other side, the attacker in the airplane maintenance area connects to the airplane’s CAN Bus. They link it to the Control Domain (CD) to exploit vulnerabilities and inject malicious commands into the airplane’s systems.

#### Attack Patterns:
1. **CAN Message to Airplane (CAPEC-172)**: The attacker sends altered messages to the airplane’s CAN Bus, manipulating its internal communications.
2. **Reverse Engineer Message (CAPEC-188)**: They decode and inject commands into the CAN Bus to modify airplane operations, allowing them to manipulate the system remotely.

## 5. Coordinated Attack: Sending Malicious Commands to the Airplane via Compromised Communications
#### Objective:
The attackers collaborate to send a final malicious payload to the airplane. Using the compromised communications between the Control Tower and the airplane, they inject a Buffer Overflow command that causes the airplane’s systems to reset during flight.

#### Attack Patterns:
1. **Buffer Overflow (CAPEC-100)**: The attackers overload the system by sending too much data or malformed input, causing the airplane’s control system to crash and reset, leading to a significant operational disruption.
