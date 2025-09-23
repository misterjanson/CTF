---
title: Capture The Flag
menuTitle: Capture The Flag
weight: 40
---
The subsequent labs will have you using FortiEDR and FortiAnalyzer, along with your knowledge of MITRE ATT&CK, to find “flags” and answer questions that test your knowledge. This will be accomplished by performing investigation steps that align to tactics, techniques, detection, and mitigation. 

Each lab will increase your knowledge of how the tools at your disposal function and can be utilized. At the end of each lab, you’ll be presented with questions to test your understanding and ability to locate “flags” within the lab environment. 

We have included icons throughout to help you identify the content that is being presented and steps that you need to take. Please refer to the explanation for this as follows:

## Investigation Steps

During the following labs we'll dig deeper into understanding the attack scenario presented by the instructor to understand how it maps to MITRE ATT&CK and how it can be prevented and detected by Fortinet tools. Each step of the killchain that we'll investigate will provide MITRE information (and links) on **TACTICS** :gear:, **TECHNIQUES** :bulb: (and sub-techniques :bulb:), **MITIGATION** :stop_sign: suggestions, and **DETECTION** :mag: methods. 

You'll then be guided to take steps using **FortiEDR and FortiAnalyzer** to **prevent** :police_officer: and **detect** :detective: these threats.

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

### Fortinet Detection :detective:

This section of the lab will primarily have you utilizing the threat hunting capabilites of FortiEDR and FortiAnalyzer to learn how to analyze telemetry collected by FortiEDR.

{{% notice note %}} Whenever you see the :police_officer: or :detective: icons that is your cue to use Fortinet tools.{{% /notice %}}

### Capture The Flag :checkered_flag:

Each lab will have instructions on gathering flags and answering questions.

## Objectives

- Understand how to operationalize the MITRE ATT&CK framework
- Understand how FortiEDR provides comprehensive prevention capabilities
- Observe how FortiEDR and FortiAnalyzer maps to the MITRE ATT&CK framework
- Learn to use the FortiEDR Central Manager and FortiAnalyzer console to perform investigations

## Time to Complete

Estimated: 120 Minutes
