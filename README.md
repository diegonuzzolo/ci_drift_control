# Infrastructure Drift Control

**Infrastructure Drift Control** è un tool per il controllo e la riconciliazione del drift infrastrutturale tramite OpenTofu.

Il programma viene distribuito come **binario eseguibile per ambiente Linux** attraverso le GitHub Releases.

## Integrazione GitLab CI/CD

Il tool può essere integrato in una pipeline GitLab CI/CD attraverso uno stage dedicato alla riconciliazione dell'infrastruttura.

### Prerequisiti

Prima dell'esecuzione di `drift_control`, è necessario generare il piano OpenTofu e convertirlo in formato JSON:

```bash
tofu plan -out=tfplan
tofu show -json tfplan > plan.json
```

La **directory di lavoro corrente** deve contenere obbligatoriamente:

- `plan.json` – Piano OpenTofu convertito in formato JSON.
- `terraform.tfstate` – File di stato dell'infrastruttura, con nome esattamente `terraform.tfstate`.
- **Un solo file `.tfvars`** – File contenente le variabili di configurazione dell'infrastruttura.

> **Importante:** la directory di lavoro deve contenere esclusivamente un file con estensione `.tfvars`. Il nome del file può variare.

Se viene utilizzato un backend remoto, lo stato può essere esportato tramite:

```bash
tofu state pull > terraform.tfstate
```
