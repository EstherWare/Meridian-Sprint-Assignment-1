

# Solstice Events Co. - Check-in Kiosk

## Overview
This repository contains the frontend kiosk interface for Solstice Events Co., developed during the Meridian Sprint simulation. 

This project successfully executed a strict mid-sprint architectural pivot. It transitioned from a deprecated synchronous polling model to a modern, asynchronous event-driven architecture utilizing a message queue and a serverless webhook callback system.

## Tech Stack
* **Frontend:** HTML, CSS, Vanilla JavaScript (Hosted via GitHub Pages)
* **Backend:** Microsoft Azure Service Bus, Azure Functions (Node.js)
* **Security:** Configured Cross-Origin Resource Sharing (CORS)

## Core Features
* **Asynchronous UI State:** The kiosk enforces a strict "Pending" lock state upon scan, waiting for the asynchronous cloud webhook callback before confirming check-in.
* **Duplicate-Scan Protection:** Implements local state validation to instantly block duplicate attendees from re-printing badges under an out-of-order execution model.

## How to Test
Visit the live GitHub Pages link and utilize the provided test cases:
1. **Scan Attendee 1 (Fresh):** Expected result is a successful green check-in.
2. **Scan Attendee 2 (Fresh):** Expected result is a successful green check-in.
3. **Scan Attendee 1 (Duplicate Test):** Expected result is a blocked red error, verifying the security validation.
   
## Sprint Documentation

* **Assignment 1:** [Learning & Blocker Journal](<The Learning & Blocker Journal.pdf>)
* **Assignment 2:** [Scope Delta Analysis](<Scope Delta Analysis.pdf>)

