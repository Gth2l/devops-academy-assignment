# Section 2 – Troubleshooting

Táto sekcia obsahuje troubleshooting úlohy zamerané na hľadanie a opravu problémov v konfigurácii, infraštruktúre a runtime správaní aplikácií.

## Tasks in this section

### Task A – 502 Bad Gateway (Nginx + Node.js)
Cieľom je nájsť príčinu chyby 502, opraviť konfiguráciu a vysvetliť, ako podobnému problému predísť v produkcii.

### Task B – Terraform Error: Error locking state
Cieľom je vysvetliť locking error v Terraforme, navrhnúť short-term a long-term fix a popísať bezpečný workflow pre tím.

### Task C – Docker Build Fails (no space left on device)
Cieľom je diagnostikovať problém s nedostatkom miesta počas CI buildu, navrhnúť dočasné aj trvalé riešenie a doplniť monitoring.

### Task D – Pod in CrashLoopBackOff
Cieľom je zistiť, prečo sa Kubernetes pod opakovane reštartuje, ako odhaliť root cause cez logy a probes a aké zlepšenia odporučiť.

### Task E – Secret Not Mounted as ENV
Cieľom je zistiť, prečo premenná z Kubernetes Secret nie je dostupná za behu aplikácie, a opraviť mismatch v namespace alebo chýbajúci resource.

## Folder structure

Každý task má vlastný priečinok s vlastným `README.md`, kde bude:
- popis problému,
- root cause analysis,
- návrh riešenia,
- prípadne obrázky, výstupy alebo poznámky.

## Current status

Completed:
- Task B – Terraform Error: Error locking state

In progress / pending:
- Task A
- Task C
- Task D
- Task E
