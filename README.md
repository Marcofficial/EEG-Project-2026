# EEG-Project-2026
# Hair Cutting Robot Project

## Project Overview

The Hair Cutting Robot is a human-centred, interdisciplinary research project exploring how electroencephalography (EEG), real-time control, network communication, and robotics could support safe and precise remote barbering services.

The project does not aim to replace barbers. Instead, it uses technology to extend a professional's ability to work remotely. The barber remains responsible for hairstyle design, customer communication, professional judgement, and command confirmation. The robot executes only actions that have passed defined safety checks and constraints.

## Motivation

Traditional barbering often requires prolonged standing, mobility, and precise hand movements. These physical requirements may create employment barriers for some people with disabilities.

This project explores an alternative model in which people with disabilities could receive professional training and work as remote barbers through an accessible robotic interface. Remote operation may reduce barriers related to transport, workplace access, and physical mobility while preserving the creativity, communication, and professional value of the service.

The concept is inspired by avatar-robot services and inclusive employment initiatives. In this model, technology is not the autonomous decision-maker. It is a tool for carrying a person's skills, judgement, and personality into a remote workplace.

## System Concept

The proposed operating flow is:

```text
Remote barber
    ↓
Accessible control and confirmation interface
    ↓
Safety checks and motion constraints
    ↓
Haircutting robot
    ↓
System status, visual information, and operational feedback
```

When the operator proposes or selects a constrained action, the safety interface checks the operator's intent, confirmation state, system status, and predefined limits. Only an approved command may be transmitted to the robot.

## Main Technical Areas

### 1. EEG and Intention Decoding

The project investigates whether scalp EEG can identify a limited motor state, motor-imagery class, or operator intention.

EEG cannot normally reconstruct a complete three-dimensional movement trajectory in the way that cameras or inertial sensors can. Therefore, this project does not treat EEG as unrestricted motion capture. A decoding result is mapped to a small set of discrete, rejectable, and confirmable command proposals.

A conceptual processing pipeline is:

```text
EEG acquisition
  → Signal-quality monitoring
  → Preprocessing and artefact handling
  → Feature extraction
  → Intention classification
  → Confidence and rejection decision
  → Proposed command
```

### 2. MQTT Communication

MQTT may provide event transport between independent system components. Possible messages include:

- EEG signal-quality states
- Intention-classification results
- Proposed and confirmed commands
- Safety-system decisions
- Robot status and operational feedback
- Heartbeat, fault, and emergency-stop events

Messages should include timestamps, sequence numbers, expiry times, model versions, and confidence values. These fields help prevent duplicate, stale, or unauditable commands from being executed.

### 3. Hotaru Integration

Hotaru may be used to build asynchronous, multi-protocol services connecting HTTP, MQTT, the operator interface, safety logic, logging systems, and simulators.

In the proposed architecture, Hotaru does not assume that every classifier output is a valid command. It coordinates confirmation, safety review, state management, and feedback.

### 4. Robotics and Real-Time Control

The robotic system must support precise motion, workspace restrictions, collision prevention, speed limits, and real-time feedback. Every action involving the customer's head or a barbering tool must remain within explicit physical and software safety constraints.

## Safety Principles

Because barbering tools operate close to a customer's head, safety must be a core system property rather than a feature added later.

The project should follow these principles:

- Reject incomplete, stale, or uncertain commands by default.
- Separate EEG predictions from executable robot actions.
- Require explicit human confirmation for important actions.
- Limit robot speed, force, position, and available movements.
- Provide an emergency-stop path independent of the main software.
- Record commands, confirmations, safety decisions, and system states.
- Prioritise offline data and simulator-based testing.
- Complete risk analysis, ethics review, and informed consent before human testing.

## Accessibility and Inclusive Design

The remote-control interface should be co-designed with its intended users. It must not assume that every operator has the same visual, auditory, physical, or cognitive abilities.

Potential accessibility features include:

- Adjustable input methods and operating procedures
- Voice, switch, eye-tracking, or other assistive inputs
- Clear visual, auditory, and tactile feedback
- Customisable text size, contrast, and interface layout
- Extended confirmation times and accidental-input prevention
- Remote training, technical support, and workflow guidance

## Current Project Stage

The project is currently an early-stage research and proof-of-concept direction. Its immediate focus is establishing the theoretical basis, system architecture, message contracts, safety requirements, and simulation methods.

The following capabilities should not currently be presented as completed or validated:

- Reconstructing unrestricted body movement from EEG
- Directly controlling barbering tools with EEG
- Completing a haircut autonomously
- A production-grade EEG decoder
- A completed MQTT, Hotaru, and robot integration
- A commercial system that can operate safely without human supervision

## Expected Outputs

Potential project outputs include:

1. A theoretical and experimental EEG intention-decoding pipeline
2. A constrained set of operator states and commands
3. MQTT topics, message schemas, and lifecycle policies
4. A Hotaru component and interface architecture
5. A simulator and safety-service prototype
6. Risk, privacy, informed-consent, and data-governance requirements
7. An accessible workflow for operators with disabilities
8. A plan for later hardware integration and controlled testing

## Project Vision

The long-term vision is to develop a safe, reliable, and auditable human-robot collaboration system that extends professional capability and creates new training and employment possibilities for people with disabilities.

Success depends on more than whether the robot can move. The system must preserve human control, protect the customer, respect the privacy of neural data, and address the real accessibility needs of its operators.

## Contact

- **Institution:** PolyU
- **Technical collaboration:** FDS-PMINE / Hotaru
- **Contact:** aquilmirza.mohammed@polyu.edu.hk
