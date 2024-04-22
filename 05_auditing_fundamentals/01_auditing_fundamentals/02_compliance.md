# Compliance

1. Business Needs

Sometimes companies want to accept their risks, however, they are not always allowed to do that. There are a set of regulations that some types of business should comply with. These regulations are put out by some companies and some others by governments. They are a must depending on your business type, otherwise you could be fined and lose the ability to operate in certain regions.

- PCI DSS: Personal information protection when handling payment data
- HIPAA: Healthcare information
- GDPR: Data Protection in EU and EEA
- CPPA: Data Protection in California US 
- SOX: Properly financial record keeping and reporting for corporations

NIST:

NIST frameworks
Nist es un programa opcional alternativo a ISO que permite a las empresas NO obligadas, a implementar un programa de seguridad, NIST se apoya en CISA y SANS en conjunto con otras entidades para proveer trainings costosos pero se pueden hacer gratis.

Alternativas y diferencias con ISO y CIS
+ NOTA: todo programa de seguridad trabaja: Personas, Procesos y Tecnologia. 

ISO es conocido por empezar por el eslabon mas debil, empieza por las PERSONAS, sus ROLES y RESPONSABILIDADES.
Alternativamente, CIS y NIST (COBIT tambien aplica aqui), trabajan el la tecnologia y los procesos, para limitar la cantidad de trabajo en PERSONAS, aunque NIST ha mejorado con su ultimo framework 2.0 donde aplica mucha gobernabilidad.

Descripcion de NIST y sus Special Publications SP
Relacionado a Cybersecurity Framework (CSF):
dependiendo de la madurez de cada empresa, siempre lo ideal es empezar con implementar Controles de Seguridad (tomando un eje del paradigma de Personas, procesos o tecnologia), es decir: 800-53 revision 5, para madurez baja o principiantes en seguridad.

En cambio, para madurez media: Si es una empresa con un esquema mas amplio de Gobernabilidad, es decir, CIO, CISO, IT team, Mesa de Ayuda, SOC o alguna combinacion de estas, ya vamos a NIST CSF (que no tiene numero porque es el framework en si) y autocontiene los SP de manera naturalizada y delega responsabilidades a distintos equipos.

Para madurez alta, a veces ya se habrá pasado por las otras dos, se recomienda un RMF o Risk Management Framwork, que requiere un profile muy definido y conducir un programa de este calibre debe ser justificado muy bien, mas que todo por budget  y se empieza por NIST SP 800 30 rev 1.
[9:50 AM]
Referencias:
NIST CSF Small business overview
Small Business Quick-Start Guide

Cybersecurity Framework (CSF) Related:
SP 800-53: Security and Privacy Controls for Federal Information Systems and Organizations.
SP 800-171: Protecting Controlled Unclassified Information in Nonfederal Systems and Organizations.
SP 800-30: Guide for Conducting Risk Assessments.
SP 800-37: Risk Management Framework for Information Systems and Organizations.
SP 800-161: Cyber Supply Chain Risk Management Practices for Systems and Organizations.
 (edited)
[9:50 AM]
Referencias avanzadas
Compliance and Assurance Related:
SP 800-53A: Assessing Security and Privacy Controls in Federal Information Systems and Organizations.
SP 800-37: Risk Management Framework for Information Systems and Organizations.
SP 800-66: An Introductory Resource Guide for Implementing the Health Insurance Portability and Accountability Act (HIPAA) Security Rule.
SP 800-171B: Protecting Controlled Unclassified Information in Nonfederal Systems and Organizations: Enhanced Security Requirements for Critical Programs and High Value Assets.
SP 800-53B: Control Baselines for Information Systems and Organizations.

Software Development and Management Related:
SP 800-160: Systems Security Engineering: Considerations for a Multidisciplinary Approach in the Engineering of Trustworthy Secure Systems.
SP 800-64: Security Considerations in the System Development Life Cycle.
SP 800-193: Platform Firmware Resilience Guidelines.
SP 800-160: Systems Security Engineering: Cyber Resiliency Considerations for the Engineering of Trustworthy Secure Systems.
SP 800-160: Systems Security Engineering: Security Capabilities Assessment for Engineering of Trustworthy Secure Systems.

## Nota relacionada con CIS

ahora si viene lo sabroso, CIS Controls o CSC, este equipo endereza el paradigma de PEOPLE, PROCESS, TECHNOLOGY y coloca la tecnologia primero, aumenta el presupuesto y tiene la mala reputacion de NO aplicar politicas a los usuarios (pero no es correcto). Pero es mas facil y digerible, y tiene sus variantes como Benchmarks y suites (pagas)