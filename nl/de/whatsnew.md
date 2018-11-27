---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Neuerungen in IBM Cloud Foundry Enterprise Environment

In diesem Dokument wird beschrieben, was in jeder Version neu ist, die bis zu diesem Datum des {{site.data.keyword.cfee_full_notm}}-Service freigegeben wurde.

## Version 1.1.0
{: #v101}

_Freigabedatum:_ 16. 11. 2018

Die folgenden Änderungen wurden in Version 1.1.0 des {{site.data.keyword.cfee_full_notm}}-Service freigegeben:

* Neue Funktionen:
   * [Aktualisierung](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) einer CFEE-Instanz auf eine neue Version. 
   * [Skalierung](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) der Kapazität einer CFEE-Instanz durch Hinzufügen oder Löschen von Cloud Foundry-Zellen.
   * [Audit](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) für Cloud Foundry-Aktivitäten durch Integration einer automatisch konfigurierten IBM Cloud Activity Tracker-Serviceinstanz.
   * Persistente Cloud Foundry-[Protokollierungsereignisse](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) mithilfe einer automatisch konfigurierten IBM Cloud Log Analysis-Serviceinstanz.
   * Neue `ibmcloud cfee`-[Befehle](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) zum Abfragen und Festlegen von Berechtigungen zum Erstellen von CFEE-Instanzen. Durch die Befehle wird die Einstellung der Berechtigungen für den CFEE-Service und für die erforderlichen unterstützenden Services zusammengefasst und vereinfacht.
   * Neuer Befehl `ibmcloud catalog blacklist` zum Vereinfachen der [Sichtbarkeitssteuerung](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) für die IBM Cloud-Services für Benutzer in einem IBM Cloud-Konto.

* Behobene Probleme:
   *  Behobenes Problem: Sporadisch auftretender Fehler beim Zugriff auf Zellenmetriken
   
Eine Demonstration der Neuerungen in CFEE Version 1.1.0 sehen Sie in diesem [Kurzvideo](https://ibm.biz/CFEE-V110){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

Weitere Videos zu unterschiedlichen CFEE-Themen finden Sie in der [CFEE-Videowiedergabeliste](https://ibm.biz/CFEE-Playlist){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
