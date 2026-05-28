# SRE Runbooks & Incident Playbooks

> Production-grade incident response runbooks, postmortem templates,
> and on-call playbooks based on real-world SRE experience.

---

## 📁 Structure

```
sre-runbooks/
├── incidents/
│   ├── high-cpu-ec2.md
│   ├── pod-crashloopbackoff.md
│   ├── disk-pressure-node.md
│   └── jenkins-pipeline-failure.md
├── postmortems/
│   └── postmortem-template.md
├── kubernetes/
│   ├── node-not-ready.md
│   ├── pvc-stuck-terminating.md
│   └── cluster-upgrade-checklist.md
├── aws/
│   ├── ec2-instance-recovery.md
│   └── rds-failover-playbook.md
└── templates/
    └── on-call-handoff.md
```

---

## 🚨 Incident Runbooks

| Runbook | Severity | Service |
|---|---|---|
| [High CPU on EC2](incidents/high-cpu-ec2.md) | P2 | EC2 |
| [Pod CrashLoopBackOff](incidents/pod-crashloopbackoff.md) | P1 | Kubernetes |
| [Disk Pressure on Node](incidents/disk-pressure-node.md) | P2 | Kubernetes |
| [Jenkins Pipeline Failure](incidents/jenkins-pipeline-failure.md) | P3 | CI/CD |
| [Node Not Ready](kubernetes/node-not-ready.md) | P1 | Kubernetes |
| [PVC Stuck Terminating](kubernetes/pvc-stuck-terminating.md) | P2 | Kubernetes |

---

## 📋 Postmortem Template

Every incident gets a postmortem. See [postmortem-template.md](postmortems/postmortem-template.md)

---

## 🔧 Based On Real Experience

- Self-managed Kubernetes cluster operations (v1.32 → v1.34)
- AWS infrastructure (EC2, EKS, RDS, VPC)
- Jenkins CI/CD pipeline management
- GCP → AWS migration incident handling
- SOC 2 compliance operations

---

## 📖 References

- [Google SRE Book](https://sre.google/sre-book/table-of-contents/)
- [PagerDuty Incident Response](https://response.pagerduty.com/)
