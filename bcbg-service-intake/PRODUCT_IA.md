# Bucks County Bike Garage — Service Intake Product IA

**Purpose:** A designer-facing map of the service workflow. This describes the product and the mechanic/customer journey, not the technical architecture.

The primary object is a **customer-owned bicycle moving through an agreement about what work should be done, the work itself, and a safe handoff back to the customer.**

## Primary lifecycle

```mermaid
flowchart LR
    A["1. Intake<br/>Customer identity<br/>Bike details<br/>Requested service<br/>Intake photos<br/>Initial authorization"]
    B["2. Inspection<br/>Mechanic evaluates bike<br/>Findings documented<br/>Existing service reviewed<br/>Additional work proposed"]
    C{"3. Customer Decision<br/>Finding communicated<br/>Proposal snapshot<br/>Approve or decline"}
    D["4. Authorized Work<br/>Authorized-at-intake work<br/>Approved additional work<br/>Service lines = work commitment<br/>Mechanic completes work"]
    E["5. Final QC<br/>Final once-over<br/>Test ride / Not required<br/>Finished-bike photo"]
    F["6. Ready for Customer<br/>Open customer handoff<br/>Completed-work summary<br/>Customer communication"]
    G["7. Waiting for Pickup<br/>Customer notified<br/>Bike remains in shop custody<br/>Pickup / delivery obligation"]
    H["8. Payment → Closed<br/>Payment recorded<br/>Bike handed back<br/>Repair history retained"]

    A --> B --> C
    C -->|Approved| D
    C -->|Declined additional work| D
    D --> E --> F --> G --> H
```

The decision stage does not imply that all work waits for customer approval. Work already authorized at intake can remain authorized; the decision applies to additional work proposed after inspection.

## Persistent product model

These are not sequential screens. They are information that should remain associated with the repair as the bicycle moves through the lifecycle.

```mermaid
flowchart TB
    JOB["SERVICE JOB / BICYCLE LIFECYCLE"]

    CUSTOMER["Customer<br/>Identity<br/>Contact information<br/>Communication & approvals"]
    BIKE["Bicycle<br/>Make / model / color<br/>Description<br/>Condition"]
    SERVICE["Service Commitment<br/>Service lines<br/>Scope & price<br/>Authorization origin"]
    FINDINGS["Findings & Decisions<br/>Mechanic diagnosis<br/>Proposal snapshot<br/>Approved / declined"]
    EVIDENCE["Evidence<br/>Intake / finished photos<br/>QC state<br/>Test ride"]
    STATUS["Status & Obligation<br/>Where is the bike?<br/>Who acts next?<br/>What must happen next?"]

    JOB --- CUSTOMER
    JOB --- BIKE
    JOB --- SERVICE
    JOB --- FINDINGS
    JOB --- EVIDENCE
    JOB --- STATUS
```

## Information that persists across the journey

### Customer
- Name and contact information
- Communication history
- Approval/decision history

### Bicycle
- Make / model / color / description
- Intake condition
- Finished condition

### Service commitment
- Service lines
- Scope and price
- Authorization origin: authorized at intake or approved after intake

### Findings and decisions
- Mechanic diagnosis/finding
- Immutable proposed-service communication snapshot
- Customer approved / declined outcome

### Evidence
- Intake and finished photos
- Final QC state
- Test ride result
- Work/handoff record

### Status and obligation
At any point the system should make three things understandable:

1. **Where is the bicycle in the lifecycle?**
2. **Who owes the next action?**
3. **What must happen before the job advances?**

## Questions for design critique

- Does this lifecycle match the mechanic's mental model, or does it expose too much process?
- What information should remain continuously visible while moving through stages?
- Are **Finding**, **Customer Decision**, and **Service Line** understandable product concepts, or are implementation concepts leaking into the UI?
- Should the interface primarily orient around the physical bike, the customer, or the service job?
- Which transitions deserve explicit confirmation and which should feel almost invisible?
- When a mechanic reopens a bike after several days, what should be immediately obvious?
- Where can the workflow reduce cognitive load without hiding important authorization or safety information?

## Design intent

This map is intentionally not a proposed screen layout. The existing application already implements the workflow; this artifact is meant to make the product model easy to critique before over-investing in visual implementation.

The working application and implementation repository remain private. This public artifact contains no customer data or private operational configuration.
