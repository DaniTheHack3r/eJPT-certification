# Frameworks and Maturity

1. How do we implement those regulations in order to comply?

There are an important amount of frameworks that we can use to properly implement and comply.

  - ISO/IEC 27000
  - COBIT
  - NIST
  - CIS
  - CMMC
  - ASD

2. ISO/IEC 27000

Known as the Internal Organization for Standarization (ISO) and the International Electrotechnical Commission (IEC).

  - Deliberately broad in scope
  - Covering more than just privacy, confidentiality and IT/technical/cybersecurity issues.
  - Applicable to organizations of all shapes and sizes

It is broken down into many different publications but the ISO 27001 it's the guidelines. And the 27002 it's a code practice on how to implement all those guidelines.

3. COBIT

Known as Control Objectives for Information and Related Technologies.

  - Created by ISACA for information technology (IT) management and IT governance
  - Business focused and defines a set of generic processes for the management of IT

4. NIST

Known as the National Institute of Standards and Technology

  - Catalog of security and privacy controls for all U.S. federal information systems except those related to national security
  - Agencies are expected to be compliant with NIST security standards and guidelines
  - NIST Special Publication 800-53B provides a set of baseline security controls and privacy controls for information systems and organizations

**Note**: SP 800-53B it is useful to look at to know if the organization we are working with already have some security controls in place.

5. CIS

Known as Center for Internet Security

  - Set of 18 prioritized safeguards to mitigate the most prevalent cyber-attacks
  - A defense-in-depth model to help prevent and detect malware
  - Offers a free, hosted software product called the CIS Controls Self Assessment Tool (CIS-CSAT)

**Note**: CIS is fairly straightforward and it has free products.

6. CMMC

Known as Cybersecurity Maturity Model Certification.

  - A training, certification, and third party assessment program of cybersecurity in the United States government Defense Industrial Base
  - Requires a third party assessor to verify the cybersecurity maturation level
  - 5 levels

**Note**: Applies only to defense businesses or anyone working with the Department of Defense.

There are 17 capability Domains (CMMC v1.0):

  - Access Control (AC)
  - Incident Response (IR)
  - Risk Management (RM)
  - Asset Management (AM)
  - Maintenance (MA)
  - Security Assessment (CA)
  - Awareness and Training (AT)
  - Media Protection (MP)
  - Situational Awareness (SA)
  - Audit and Accountability (AU)
  - Personal Security (PS)
  - System and Communications Protection (SC)
  - Configuration Management (CM)
  - Physical Protection (PE)
  - System and Information Integrity (SI)
  - Identification and Authentication (IA)
  - Recovery (RE)

And the 5 levels are:

  - level 1 => Processes: Performed, Practices: Basic Cyber Hygiene
  - level 2 => Processes: Documented, Practices: Intermediate Cyber Hygiene
  - level 3 => Processes: Managed, Practices: Good Cyber Hygiene
  - level 4 => Processes: Reviewed, Practices: Proactive
  - level 5 => Processes: Optimizing, Practices: Advanced/Progressive

7. ASD Essential 8

Known as Australian Signals Directorate, from Australian Cyber Security Centre, Essential Eight Maturity Model.

  - Help organisations protect themselves against various cyber threats
  - Designed to protect Microsoft Windows-based internet-connected networks
  - 4 maturity levels

The essential 8 security controls are:

  - Prevents attacks: Application Control, Patch Applications, Configure Microsoft Office Macros, User Application Hardening.
  - Limits extent of attacks: Restrict Admin Privileges, Patch Operating System, Multi-Factor Authentication
  - Recovers data & system availability: Daily Backups

8. Why does any of this matter as a pentester?

Because we as pentester need to add value to the companies and they need to get something useful that they can then decide to implement, to mix into their risk management, to understand how they can implement them. And it is better if you match their tier or maturity level.