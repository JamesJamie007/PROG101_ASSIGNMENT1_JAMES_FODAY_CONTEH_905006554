# PROG101_ASSIGNMENT1_JAMES_FODAY_CONTEH_905006554
This is assignment 1 for Programming Logic and Design. About FloodWatch SL Community Flood Risk Early Warning System


## Overview

FWSL is a classroom logic prototype for a community flood early warning workflow in Freetown, Sierra Leone. It reads four environmental indicators for each community, validates them, calculates a weighted risk score, classifies it into one of four alert levels, applies a Boolean escalation rule, and repeats until the user enters STOP. It is designed to demonstrate sequence, selection, repetition, functions, Boolean logic, and modularity. No source code is included, by design.

## Problem solve

The FloodWatch SL early warning system (FWSL) solves the problem of late and inconsistent flood warnings in Freetown communities by providing a structured, repeatable, low-cost decision process. Key aspects of the problem and its solution include:

- The Problem: Seasonal flooding in Freetown causes deaths, displacement and cholera outbreaks. Communities learn a flood is coming only when water enters their homes, and decisions about when to warn are made informally and inconsistently.
- The Solution: A structured algorithm that turns rainfall, river level, drainage blockage and households at risk into a score from 0 to 135, an alert level (LOW, MODERATE, HIGH or SEVERE), a colour and a recommended action. If blockage is 70% or more AND river level is 75% or more, the alert is raised one level.
- Impact: Gives communities time to move belongings and evacuate, gives NDMA and the City Council an objective basis for allocating response resources, and supports a shift from reactive to anticipatory disaster response aligned with Sustainable Development Goals (SDG 11, SDG 13 and SDG 3).

## SDG alignment

- SDG 11 — Sustainable Cities and Communities: Target 11.5 reduces deaths and losses from water-related disasters.
- SDG 13 — Climate Action: Target 13.1 strengthens resilience and adaptive capacity to climate-related hazards.
- SDG 3 — Good Health and Well-being: Target 3.9 reduces illness from water contamination, since flooding triggers cholera outbreaks.

## Modules

- Main — controls the community loop and the summary counters.
- ReadValue — prompts for a number and repeats until it is inside the permitted range.
- CalculateRiskScore — applies the four scoring bands and returns the score (0–135).
- DetermineAlertLevel — maps the score to LOW, MODERATE, HIGH or SEVERE.
- ApplyEscalation — raises the alert one level when blockage is 70% or more AND river level is 75% or more.
- GetAlertColour — returns GREEN, YELLOW, ORANGE or RED.
- GetActionAdvice — returns the recommended action for the alert level.
- DisplayCommunityReport — prints the assessment for one community.
- DisplaySummary — prints totals, households under SEVERE alert and the highest-risk community.

## Pseudocode

```
MODULE FloodWatchSL

    SET communityCount ← 0, severeCount ← 0, highCount ← 0
    SET moderateCount ← 0, lowCount ← 0, severeHouseholds ← 0
    SET highestScore ← -1, highestCommunity ← ""

    DISPLAY "Enter community name (or STOP to finish): "
    READ communityName

    WHILE communityName <> "STOP" DO

        SET rainfall   ← CALL ReadValue("Rainfall 24h (mm, 0-1000): ", 0, 1000)
        SET riverLevel ← CALL ReadValue("River level (%, 0-100): ", 0, 100)
        SET blockage   ← CALL ReadValue("Drainage blockage (%, 0-100): ", 0, 100)
        SET households ← CALL ReadValue("Households at risk (0-50000): ", 0, 50000)

        SET score      ← CALL CalculateRiskScore(rainfall, riverLevel, blockage, households)
        SET alertLevel ← CALL DetermineAlertLevel(score)
        SET alertLevel ← CALL ApplyEscalation(alertLevel, blockage, riverLevel)
        SET colour     ← CALL GetAlertColour(alertLevel)
        SET advice     ← CALL GetActionAdvice(alertLevel)

        CALL DisplayCommunityReport(communityName, rainfall, riverLevel,
                                    blockage, households, score,
                                    alertLevel, colour, advice)

        SET communityCount ← communityCount + 1

        IF alertLevel = "SEVERE" THEN
            SET severeCount ← severeCount + 1
            SET severeHouseholds ← severeHouseholds + households
        ELSE IF alertLevel = "HIGH" THEN
            SET highCount ← highCount + 1
        ELSE IF alertLevel = "MODERATE" THEN
            SET moderateCount ← moderateCount + 1
        ELSE
            SET lowCount ← lowCount + 1
        END IF

        IF score > highestScore THEN
            SET highestScore ← score
            SET highestCommunity ← communityName
        END IF

        DISPLAY "Enter community name (or STOP to finish): "
        READ communityName

    END WHILE

    CALL DisplaySummary(communityCount, severeCount, highCount, moderateCount,
                        lowCount, severeHouseholds, highestCommunity, highestScore)

END MODULE
```

The pseudocode for the other modules is in the Pseudocode folder.

## Flowcharts

**Figure 1: Main algorithm**



![Figure 1](Flowcharts/figure1-main-flowchart.png)



**Figure 2: ReadValue validation module**



![Figure 2](Flowcharts/figure2-readvalue-flowchart.png)



**Figure 3: CalculateRiskScore module**



![Figure 3](Flowcharts/figure3-riskscore-flowchart.png)



**Figure 4: ApplyEscalation module**



![Figure 4](Flowcharts/figure4-escalation-flowchart.png)



## Author

James Foday Conteh  
Student ID: 905006554  
Limkokwing University of Creative Technology, Sierra Leone