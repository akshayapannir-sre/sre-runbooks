# Pod CrashLoopBackOff — Runbook

**Severity:** P1
**Service:** Kubernetes
**On-call Team:** SRE

---

## Symptoms
- Pod status shows `CrashLoopBackOff`
- `kubectl get pods` shows increasing RESTARTS count
- Application alerts firing in Grafana / PagerDuty

---

## Immediate Actions (First 5 mins)

```bash
# 1. Check pod status
kubectl get pods -n <namespace>

# 2. Check logs from crashed container
kubectl logs <pod-name> -n <namespace> --previous

# 3. Describe pod for events
kubectl describe pod <pod-name> -n <namespace>

# 4. Check resource limits
kubectl top pod <pod-name> -n <namespace>
```

---

## Common Causes & Fixes

### 1. Application error on startup
```bash
# Check logs for error message
kubectl logs <pod-name> --previous | tail -50

# Fix: rollback to last stable image
kubectl rollout undo deployment/<deployment-name> -n <namespace>
```

### 2. OOMKilled (Out of Memory)
```bash
# Check if OOMKilled
kubectl describe pod <pod-name> | grep -i oom

# Fix: increase memory limits in deployment
kubectl edit deployment <deployment-name> -n <namespace>
# Update: resources.limits.memory
```

### 3. ConfigMap or Secret missing
```bash
# Check events
kubectl get events -n <namespace> --sort-by='.lastTimestamp'

# Fix: create missing secret
kubectl create secret generic <secret-name> \
  --from-literal=key=value -n <namespace>
```

### 4. Liveness probe failing
```bash
# Check probe config
kubectl describe pod <pod-name> | grep -A5 "Liveness"

# Temporary: disable probe to debug
kubectl edit deployment <deployment-name>
# Comment out livenessProbe temporarily
```

---

## Escalation

| Time | Action |
|---|---|
| 0-5 min | Check logs, describe pod |
| 5-15 min | Rollback if recent deploy |
| 15+ min | Escalate to dev team |

---

## Post-Incident

- [ ] Root cause identified
- [ ] Fix applied and verified
- [ ] Postmortem filed if P1
- [ ] Alert tuned if false positive
