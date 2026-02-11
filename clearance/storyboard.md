### Communication flow

1. PAS-X >> HB - request for line clearance
2. HB >> Tulip - kick off workflow
	1. Tulip poll table for new work
3. HB << Tulip - poll for results/completion
4. HB >> PAS-X - POST completion results

### Panel 1: Batch Completion Trigger
PAS-X MES detects prior batch end (e.g., via ERP signal or recipe completion). It generates a "Line Clearance Required" electronic work order with details like batch ID, line number, product specs, and predefined checklist (e.g., remove labels/tools). Status updates to "Hold" in PAS-X dashboard; notification pushes to Tulip via API/MQTT/OPC UA integration.

### Panel 2: Operator App Activation
Operator scans QR code or badge at line station on Tulip tablet. Custom "Line Clearance App" loads, displaying prior batch info, visual progress bar (0%), and first task: "Clear all remnants." Multimedia instructions appear (e.g., icons for waste removal).


### Panel 3: Clearing Phase
Operator performs physical removal of materials, waste, labels, and documents. Tulip prompts barcode scans for verification (e.g., confirm empty bins). Progress bar advances; timer logs duration. If incomplete, app blocks progression with alert.

### Panel 4: Cleaning & Inspection
App guides to cleaning: "Sanitize surfaces/equipment" with checklists (e.g., wipe-down photos via Tulip Vision/AI camera check for residues). Dropdowns for notes (e.g., "No foreign objects"). Auto-flags issues like conveyor jams; progress to 70%.


### Panel 5: Verification & E-Signoff
Final checks: QA/operator reviews via split-screen checklist (e.g., "Labels correct? Equipment calibrated?"). E-signatures required; Tulip logic validates all steps. If approved, progress bar hits 100%; digital audit trail generates.

### Panel 6: Sync & Release
Tulip posts completion data (timestamps, photos, signatures) back to PAS-X. MES updates line status to "Cleared," unlocks next batch recipe, and archives for batch record (21 CFR Part 11 compliant). Supervisor dashboard shows green KPI for line readiness.
