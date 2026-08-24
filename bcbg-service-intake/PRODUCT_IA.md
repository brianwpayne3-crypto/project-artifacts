# Bucks County Bike Garage — Service Intake Product IA

**Purpose:** A designer-facing map of the service workflow. This describes the product and the mechanic/customer journey, not the technical architecture.

The primary object is a **customer-owned bicycle moving through an agreement about what work should be done, the work itself, and a safe handoff back to the customer.**

## Primary lifecycle

```text
INTAKE
  Customer identity
  Bike details
  Requested service
  Intake photos
  Initial authorization
      |
      v
INSPECTION
  Mechanic evaluates bike
  Findings documented
  Existing service reviewed
  Additional work proposed
      |
      v
CUSTOMER DECISION
  Finding communicated
  Proposed-service snapshot
  Approved or declined
      |
      v
AUTHORIZED WORK
  Work authorized at intake
  Approved additional work
  Service lines represent the work commitment
  Mechanic completes work
      |
      v
FINAL QC
  Final once-over
  Test ride result / Not required
  Finished-bike photo
      |
      v
READY FOR CUSTOMER
  Customer handoff
  Completed-work summary
  Customer communication
      |
      v
WAITING FOR PICKUP
  Customer has been notified
  Bike remains in shop custody
  Pickup / delivery obligation remains
      |
      v
PAYMENT -> CLOSED
  Payment recorded
  Bike handed back
  Repair history retained
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
