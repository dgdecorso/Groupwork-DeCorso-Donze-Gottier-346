# Groupwork-DeCorso-Donze-Gottier-346
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
<img width="1799" height="731" alt="image" src="https://github.com/user-attachments/assets/4a08bbb1-dff0-4d00-8603-0e48986ea9ce" />


