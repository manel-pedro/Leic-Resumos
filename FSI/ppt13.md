v1. Threat Context: Intruders and DoS Attacks

Before deploying defenses, it is crucial to understand the adversaries and their methods:

Intruder Classes: Attackers range from Cyber Criminals seeking financial reward to State-Sponsored Organizations (APTs) and Activists (Hacktivists).

Skill Levels: Adversaries are categorized as Apprentices ("script-kiddies"), Journeymen (can modify tools), or Masters (discover new vulnerabilities).

Denial of Service (DoS): Attacks target availability by overwhelming network bandwidth, system resources (buffers/tables), or application resources.

Advanced DoS Methods: Attackers often use Botnets (networks of "zombie" servers) to scale attacks and Reflection/Amplification techniques (e.g., DNS, Smurf, or SYN spoofing) to hide their source and multiply traffic volume.

2. First Line of Defense: Firewalls

Firewalls act as "secretaries" that filter traffic based on predefined access policies.

Packet Filters: Lightweight and fast; they operate at the network layer but lack context regarding application data or state.

Stateful Packet Filters: Track ongoing TCP/UDP connections at the transport layer to detect protocol-level misbehavior.

Application Proxies: Most intrusive; they use application logic to inspect payload content (e.g., preventing SQL injection) but require high processing power.

3. Core Focus: Intrusion Detection Systems (IDS)

While firewalls provide perimeter defense, an IDS monitors and detects complex attacks that may bypass those initial barriers.

A. Operational Requirements

A robust IDS must meet four critical criteria:

Availability: Must run continuously and degrade gracefully if overloaded.

Security: Must be fault-tolerant and resist attempts at subversion.

Performance: Must impose minimal overhead and be highly scalable.

Adaptability: Must evolve with changes in user behavior and new attack patterns.

B. IDS Classification: HIDS vs. NIDS

The effectiveness of an IDS depends on its placement and visibility:

Host-Based IDS (HIDS): Installed on individual devices to monitor internal host activity, such as buffer overflows or privilege escalation. It can see local incidents but has no view of network-wide activity.

Network-Based IDS (NIDS): Positioned at strategic network points to monitor transport and application protocols for network probes or malformed packets. It provides a broad view but lacks the internal application logic of a host system.

C. Detection Methodologies

There are two primary ways an IDS identifies threats:

Signature-Based Detection: Matches traffic against a database of known malicious patterns (signatures). It is accurate and efficient for known threats but fails against "zero-day" attacks or variations of known exploits.

Anomaly-Based Detection: Establishes a baseline of "normal" behavior and flags deviations. While it can identify brand-new categories of vulnerabilities, it is prone to high false positive rates if the baseline is not accurately defined.

D. The Base-Rate Fallacy

A major challenge for IDS is the "Base-Rate Fallacy." Even a system with 99% accuracy can be overwhelmed by false alarms if the volume of benign traffic significantly outweighs the number of actual malicious events. For instance, if only 100 out of 1,000,100 events are malicious, a 1% false positive rate results in 10,000 false alarms for every 99 true detections.