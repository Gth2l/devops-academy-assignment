# Section 3 – Task A: Production Went Down

## Summary

This task describes my step-by-step approach to investigating a production outage.

The goal is to:
- confirm the incident,
- assess impact,
- investigate systematically,
- restore service with the lowest-risk action,
- verify recovery.

## Investigation Process

### 1. Confirm the Incident
First, I would verify that the application is actually down by checking:
- monitoring alerts,
- health checks,
- logs,
- user-facing symptoms.

### 2. Assess Scope and Impact
Next, I would determine:
- whether all users are affected,
- whether the issue is limited to production,
- whether the outage is full or partial,
- how critical the business impact is.

### 3. Check Recent Changes
I would review recent:
- deployments,
- configuration changes,
- infrastructure changes,
- secret or environment variable updates.

This is often the fastest way to identify the cause.

### 4. Investigate by Layer
I would troubleshoot systematically:

#### Application
- startup errors,
- exceptions,
- failed dependencies,
- health endpoint behavior.

#### Runtime / Container
- restarts,
- crash loops,
- resource exhaustion,
- port binding issues.

#### Infrastructure / Platform
- ingress or load balancer,
- service routing,
- DNS,
- node or VM health,
- network connectivity.

#### Dependencies
- database,
- cache,
- third-party APIs,
- authentication systems.

### 5. Form and Test Hypotheses
Based on evidence, I would form likely hypotheses such as:
- bad deployment,
- broken configuration,
- dependency outage,
- traffic routing problem,
- resource issue.

I would validate each hypothesis using logs, metrics, and recent change history.

### 6. Mitigate Safely
The priority is service restoration.

Possible low-risk actions:
- rollback the latest deployment,
- restart failed instances,
- restore missing configuration,
- scale resources temporarily,
- reroute traffic if needed.

### 7. Communicate Clearly
During the incident, I would provide short updates covering:
- current impact,
- known findings,
- mitigation in progress,
- next checkpoint.

### 8. Verify Recovery
After mitigation, I would verify:
- health checks are passing,
- the application is reachable,
- error rates are normal,
- logs show stable behavior,
- users can access the service again.

## Follow-Up

After recovery, I would document:
- root cause,
- timeline,
- fix applied,
- lessons learned,
- preventive improvements.

## Conclusion

My approach is to stay structured, confirm the problem quickly, investigate layer by layer, restore service with the safest action, and verify stability before closing the incident.
