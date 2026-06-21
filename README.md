# BillMaster — Monorepo (Git Submodules)

Το **BillMaster** είναι μια cloud-native εφαρμογή διαχείρισης λογαριασμών και παραστατικών, αναπτυγμένη σε Kubernetes (MicroK8s) με GitOps deployment, external secret management μέσω HashiCorp Vault, και πειραματική αξιολόγηση απόδοσης (SLA) με k6.

Αυτό το repository λειτουργεί ως **monorepo** μέσω git submodules: περιέχει pointers προς τα τρία επιμέρους repositories, σε συγκεκριμένο commit το καθένα. Κλωνοποιώντας αυτό το repo, παίρνεις αυτόματα όλο τον κώδικα.

## Δομή

```
BillMaster-Monorepo/
├── kustomize/           → Charos01/Kustomize (main)
├── billmaster/          → Charos01/BillMaster (dev) — frontend, IaC, Jenkinsfile, SLA
└── billmaster-backend/  → Charos01/BillMaster_Backend (dev)
```

## Repositories

| Submodule path | Repository | Περιεχόμενο | Branch |
| --- | --- | --- | --- |
| `kustomize/` | [Kustomize](https://github.com/Charos01/Kustomize.git) | Kubernetes manifests (base + overlays), GitOps repository | `main` |
| `billmaster/` | [BillMaster](https://github.com/Charos01/BillMaster.git) | Frontend, OpenTofu/Ansible, Jenkinsfile, SLA tests (k6) | `dev` |
| `billmaster-backend/` | [BillMaster_Backend](https://github.com/Charos01/BillMaster_Backend.git) | Backend (REST API, business logic) | `dev` |

## Κλωνοποίηση

```bash
git clone --recurse-submodules https://github.com/Charos01/BillMaster-Monorepo.git
```

Αν έχεις κάνει ήδη clone χωρίς `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Ενημέρωση των submodules σε νεότερο commit

```bash
cd billmaster
git checkout dev
git pull
cd ..
git add billmaster
git commit -m "Update billmaster submodule to latest dev commit"
```

## Authors

- Παναγιώτης Χάρος — ais25133
- Ιωάννης Μαυροδήμος — ais25126
