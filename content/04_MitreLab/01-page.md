---
title: Lab Instructions
menuTitle: Lab Instructions
weight: 5
---

## Investigation Steps

During the following labs we'll dig deeper into understanding the attack scenario presented by the instructor to understand how it maps to MITRE ATT&CK and how it can be prevented and detected by FortiEDR. Each step of the killchain that we'll investigate will provide MITRE information (and links) on **TACTICS** :gear:, **TECHNIQUES** :bulb: (and sub-techniques :bulb:), **MITIGATION** :stop_sign: suggestions, and **DETECTION** :mag: methods. 

You'll then be guided to take steps using **FortiEDR** to **prevent** :police_officer: and **detect** :detective: these threats.

### Tactic :gear:

Tactics represent the "why" of an ATT&CK technique or sub-technique. It is the adversary's tactical goal: the reason for performing an action. In this section we'll understand a specific tactic that was used during the attack scenario. This section of each lab will provide information on a specific tactic as defined by MITRE.

### Technique and Sub-Technique :bulb:

Techniques represent 'how' an adversary achieves a tactical goal by performing an action. In this section we'll understand a specific technique, or sub-technique, of the ATT&CK Matrix that was used during the attack scenario.

### Mitigation :stop_sign:

Mitigations represent security concepts and classes of technologies that can be used to prevent a technique or sub-technique from being successfully executed. In this section we'll review a mitigation recommended by MITRE.

### FortiEDR Prevention :police_officer:

This section of each lab is where you'll start getting hands on and learning the various methods FortiEDR uses to implement prevention mechanisms. This is effectively where we start putting the recommendations from MITRE into action.

### Detection :mag:

Many behaviors observed through various tactics and techniques may not always be specific to an attack and will not warrant explicit mitigation. However, security analysts will commonly threat hunt across an environment in search of early warning signs of attacker activity in a network. ATT&CK can help cyber defenders develop analytics that detect the techniques used by an adversary. In this section we'll review a detection recommended by MITRE.

### FortiEDR Detection :detective:

This section of the lab will primarily have you utilizing the threat hunting capabilites of FortiEDR to learn how to analyze telemetry collected by FortiEDR.

{{% notice note %}} Whenever you see the :police_officer: or :detective: icons that is your cue to use the FortiEDR Central Manager.{{% /notice %}}

## Objectives

- Understand how to operationalize the MITRE ATT&CK framework
- Understand how FortiEDR provides comprehensive prevention capabilities
- Observe how FortiEDR natively maps to the MITRE ATT&CK framework
- Learn to use the FortiEDR Central Manager to perform investigations

## Time to Complete

Estimated: 120 Minutes