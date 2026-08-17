Meridian Sprint Assignment 1: Solo Recon

Overview
This repository contains the working mini-prototype for Assignment 1 of the Meridian Pivot sprint. The goal was to build a functional Exponential Retry/Backoff script and execute it successfully in a mobile browser environment.

The Architecture
The code utilizes a unified single-file architecture (`index.html`) containing both the UI elements and the inline JavaScript backoff logic. This structure was necessary to bypass mobile simulator restrictions.



Learning & Blocker Journal
This journal documents the autonomous troubleshooting process required to deploy this prototype.

Blocker Entry 1: The Scope Error

  Date: August 17, 2026
  The Goal: Trigger the `fetchInventory` exponential backoff function via an HTML button click.
  The Error / Blocker: Console threw `Uncaught ReferenceError: fetchInventory is not defined`. The HTML button could not locate the JavaScript function because of how the code editor isolates HTML and JS into separate scopes.
  Resources Consulted: Researched MDN Web Docs regarding "ReferenceError: not defined" and standard event binding practices.
  The Resolution: I removed the inline `onclick` attribute from the HTML. Instead, I used `document.getElementById('inventoryBtn').addEventListener('click', fetchInventory)` within the JavaScript file to securely bind the click event without relying on the global scope.

Blocker Entry 2: The DOM Race Condition
   Date: August 17, 2026
   The Goal: Connect the newly written JavaScript event listener to the HTML button.
   The Error / Blocker: A "Silent Failure." The button became completely unresponsive, and no errors appeared in the console. The JavaScript was executing fractions of a second before the HTML button had finished rendering, meaning the script was trying to attach an event to a button that did not technically exist yet.
   Resources Consulted: Investigated JavaScript DOM loading lifecycles and "race conditions" in mobile browser environments.
   The Resolution: I attempted to fix the load order by wrapping the event listener inside a `window.onload` function. This forces the JavaScript execution to pause until the entire HTML document is fully loaded and drawn on the screen.

### Blocker Entry 3: Environment Sandbox Limitations
   Date: August 17, 2026
   The Goal: Execute the fully connected exponential backoff logic on a mobile browser simulator.
   The Error / Blocker: The platform's mobile split-pane iframes continued to aggressively block the `window.onload` command and isolated the JavaScript from the HTML, causing repeated ReferenceErrors despite the code being structurally perfect. 
   Resources Consulted: Explored standalone single-file web application architecture and inline `<script>` execution.
   The Resolution: I completely abandoned the editor's split-pane sandbox setup. I injected the entire JavaScript logic directly into the HTML file using a `<script>` tag. This bypassed the platform's artificial environment restrictions entirely, mimicking a raw, deployment-ready file structure and resulting in a 100% functional prototype.
