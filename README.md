<img width="2796" height="1406" alt="image" src="https://github.com/user-attachments/assets/c8b466b4-7a08-43a9-a92b-b6600fe8e87a" /># Groupwork-DeCorso-Donze-Gottier-346
## A)
<img width="2070" height="378" alt="image" src="https://github.com/user-attachments/assets/329c8cfd-6371-44b1-bd6e-79f06415490a" />
<img width="2058" height="442" alt="image" src="https://github.com/user-attachments/assets/54f193f9-02ee-4db0-a7c0-a8e0d6f5a11a" />

Für den Datenbankserver wurde ein separater EC2-Service hinzugefügt, da im Rehosting-Modell Web- und Datenbankserver getrennt betrieben werden, analog zur bestehenden On-Premise-Architektur.
<img width="1880" height="444" alt="image" src="https://github.com/user-attachments/assets/e518a82e-9b55-4d8c-a7f9-43a57237cae8" />

In AWS werden Backups nicht als eigener Server betrieben, sondern über EBS Snapshots realisiert. Diese sind inkrementell, hochverfügbar und ersetzen ein klassisches Backup-System aus der On-Premise-Welt.
AWS bietet keine Linux-Instanz mit exakt 1 Core & 2 GB RAM – deshalb habe ich eine t3.small gewählt (2 vCPU, 2 GB).
Für die DB ebenfalls t3.medium, da es 2 vCPU & 4 GB RAM entspricht.
EBS GP3 SSD für Block-Storage, weil es performant und kosteneffizient ist.
Backups über EBS Snapshots: tägliche, wöchentliche und monatliche Aufbewahrung berücksichtigt (Speicherkosten geschätzt).

<img width="2443" height="1595" alt="image" src="https://github.com/user-attachments/assets/468cf48f-b20e-4b87-80b7-ef983fe1bb14" />
<img width="2263" height="1029" alt="image" src="https://github.com/user-attachments/assets/917f5b5e-c96a-43fa-9ed8-d5d373945dff" />
<img width="2308" height="1484" alt="image" src="https://github.com/user-attachments/assets/7bd86597-c971-4440-b021-e9cc7dfaf30e" />
<img width="2376" height="1172" alt="image" src="https://github.com/user-attachments/assets/5957769e-3158-4ffd-9295-f3b52fa5ac01" />
<img width="2428" height="1209" alt="image" src="https://github.com/user-attachments/assets/5b3e2d71-dfcd-4d66-a78a-3fd2f3b04fa2" />
<img width="2339" height="1293" alt="image" src="https://github.com/user-attachments/assets/a982c8f4-b54f-4922-bf1a-fd941d24ea89" />
[ExportedEstimate.xlsx](https://github.com/user-attachments/files/24583059/ExportedEstimate.xlsx)

Azure bietet sehr kleine B-VMs → nahe an On-Premise

Speichergrößen nur in Stufen → leichte Abweichung

Azure Backup deckt Retention-Anforderungen ab

## B)
## Heroku Kostenrechnung (PAAS / Replatforming) – CRM (30 Benutzer)

| Komponente           | Plan        | CPU                         | RAM  | Disk                                                     | Anzahl | Preis / Monat (USD) | Kosten / Monat (USD) |
|---------------------|-------------|-----------------------------|------|----------------------------------------------------------|--------|---------------------|----------------------|
| Heroku Dyno (Web)   | Standard-2X | CPU Share 2x (Compute 2x–8x) | 1 GB | Ephemeral FS (nicht persistent), Slug ≤ 500 MB (komprimiert) | 1      | 50                  | 50                   |
| Heroku Postgres (DB)| Premium-2   | 2 vCPU                      | 8 GB | 256 GB                                                   | 1      | 350                 | 350                  |

**Total:** $400 / Monat
## Backup-Anforderungen / Abdeckung (Heroku PGBackups)

| Backup Policy (PGBackups, Scheduled) | Retention              |
|--------------------------------------|------------------------|
| Daily                                | 7 Tage                 |
| Weekly                               | 8 Wochen (Premium)     |
| Monthly                              | 12 Monate (Premium)    |

Wir wählen **1× Standard-2X Dyno** für den Web-Teil, weil die App bei Heroku ohne OS-/Server-Overhead läuft und sich bei Bedarf sehr schnell vertikal (größerer Dyno) oder horizontal (mehr Dynos) skalieren lässt. Für die Datenbank nehmen wir **Heroku Postgres Premium-2**, weil nur der **Premium-Tier** die geforderten **monatlichen Backups** (Retention) abdeckt und gleichzeitig genug Performance-Reserven bietet. Die Abweichung zur On-Prem-Disk ist bewusst: Heroku-Dynos haben **kein persistentes Filesystem**, daher gehören Daten/Uploads in **Postgres bzw. externen Storage**, was Betrieb und Backup-Handling vereinfacht.

## C) 

<img width="1459" height="733" alt="image" src="https://github.com/user-attachments/assets/614ef276-3891-4e01-9bbf-a770ffea820f" />
Für Zoho CRM wurde der Enterprise-Plan (40 € pro Benutzer und Monat) betrachtet, da dieser alle für ein KMU relevanten CRM-Funktionen bietet und für 30 Benutzer geeignet ist.
<img width="1440" height="658" alt="image" src="https://github.com/user-attachments/assets/29f3aba4-d27f-42b1-9df4-797556561c14" />
Für Salesforce Sales Cloud wurde der Pro-Suite-Plan gewählt, da dieser die notwendigen CRM-Funktionen für den täglichen Betrieb bereitstellt, während höhere Pläne für die Anforderungen der Firma nicht erforderlich sind.

| Anbieter | Plan       | Preis / User | Benutzer | Monatliche Kosten |
| -------- | ---------- | ------------ | -------- | ----------------- |
| Zoho CRM | Enterprise | 40 €         | 30       | ca. 1'200 €       |
| Salesforce| Pro Suite | 100 € | 30 | ca. 3'000 € |

Wir haben Zoho CRM ausgewählt, da es für die Anforderungen der Firma funktional ausreichend ist und im Vergleich zu Salesforce deutlich geringere Kosten verursacht.

Beim Repurchasing wird die bestehende, selbst entwickelte CRM-Applikation vollständig durch eine Standard-SaaS-Lösung ersetzt. Die Firma betreibt keine eigene Software mehr und lagert Betrieb, Wartung, Updates und Backups vollständig an den SaaS-Anbieter aus.

