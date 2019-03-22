---

copyright:
  years: 2018
lastupdated: "2019-01-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Ressourcennutzung

Administratoren und Entwickler können anzeigen, wie die Ressourcenkapazität (Hauptspeicher und CPU) einer CFEE-Umgebung von Anwendungen und Zellen verwendet wird. Gehen Sie wie folgt vor, um die Ressourcennutzung in einer CFEE-Instanz zu überwachen:

1. Wechseln Sie zum [{{site.data.keyword.Bluemix_notm}} Foundry-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) und öffnen Sie die {{site.data.keyword.cfee_full_notm}}-Instanz, in der Sie die Ressourcennutzung verwalten möchten.
2. Wechseln Sie in der {{site.data.keyword.cfee_full_notm}}-Benutzerschnittstelle im linken Navigationsbereich zum Eintrag **Ressourcennutzung**, um die Seite _Ressourcennutzung_ zu öffnen. Auf der Seite _Ressourcennutzung_ können Sie entweder zum Untereintrag _Anwendungen_ oder zum Untereintrag _Zellen_ wechseln, um die entsprechenden Seiten zu öffnen.  Die Informationen, die auf den Seiten _Anwendungen_ und _Zellen_ angezeigt werden, können als zwei Methoden zum Gliedern der Ressourcennutzung betrachtet werden:
   * Auf der Seite **Anwendungen** wird die Ressourcennutzung durch Anwendungen analysiert (zusammengefasst für all Instanzen).
   * Auf der Seite **Zellen** wird die Ressourcennutzung der Anwendungsinstanzen angezeigt, die auf bestimmten Zellen ausgeführt werden. Das Muster der Ressourcennutzung in den Zellen kann Aufschluss über die Kapazität und die Lastverteilung geben.  Dies kann zum Beispiel das Ermitteln von Problemen im Zusammenhang mit der Lastverteilung der Anwendungen (beispielsweise große Unterschiede bei den Ressourcen, die von einer Anwendung in Zellen verwendet werden) oder einer Ressourcennutzung, die allmählich die gesamte Kapazität in Anspruch nimmt (also große Prozentsätze an Ressourcennutzung in allen Zellen) erleichtern.

**Hinweis:** Die Ressourcennutzungsdaten stellen die Nutzung der Ressourcen während des Erfassungszyklus in den letzten fünf Minuten dar. Die Ressourcennutzungsdaten können durch Klicken auf **Daten aktualisieren** ganz oben auf der Seite aktualisiert werden.

## Anwendungen
{: #usage_apps}

Die Seite für die Anwendungen besteht aus zwei Abschnitten:
1. Horizontale Balkendiagramme, die die physische und reservierte Speicherbelegung anzeigen.
   * Reservierter und physischer Speicher, der von den **ausgewählten Apps** in der nachstehenden Tabelle verwendet wird.
   * Reservierter und physischer Speicher, der von **allen Apps** in der CFEE-Instanz verwendet wird.
   * Physischer Speicher, der vom **System** verwendet wird, einschließlich Speicher, der von der Cloud Foundry-Steuerebene verwendet wird, und Anwendungsspeicher, der von der Cloud Foundry-Steuerebene im Cache zwischengespeichert wird.
   * **Insgesamt verfügbarer** reservierter und physischer Speicher in der CFEE-Instanz.
   
   **Hinweis:** Wenn Anwendungen mehr Speicher reservieren, als physisch verfügbar ist, wird im Balkendiagramm für reservierten Speicher eine gestrichelte rote Linie angezeigt, um die Speicherkapazität darzustellen, die von der/den ausgewählten Anwendung(en) zu viel reserviert wird.

   Wenn Sie den Wert für den Prozentsatz an Hauptspeicher anzeigen möchten, der von allen Anwendungen oder den in der Tabelle ausgewählten Anwendungen verwendet wird, bewegen Sie den Mauszeiger über den entsprechenden Teil des Diagramms. Wenn Sie den Mauszeiger über den Teil *Alle Apps* des Diagramms bewegen, wird der Prozentsatz des Hauptspeichers, der von allen Anwendungen in der CFEE verwendet wird, im Verhältnis zur verfügbaren Gesamtmenge angezeigt. Wenn Sie den Mauszeiger über den Teil *Ausgewählte Apps* des Diagramms bewegen, wird der Prozentsatz des Hauptspeichers, der von den in der Tabelle ausgewählten Anwendungen verwendet wird, im Verhältnis zur verfügbaren Gesamtmenge des Hauptspeichers angezeigt. 

2. Eine Tabelle, in der alle Anwendungen aufgelistet werden.  In jeder Zeile der Tabelle werden Ressourceninformationen für diese Anwendung angezeigt.  Wenn eine Zeile erweitert wird, werden Ressourcennutzungsinformationen für die unterschiedlichen Instanzen dieser Anwendung angezeigt.

  Die erste Spalte in der Tabelle ist ein Kontrollkästchen, mit dem festlegt wird, ob die entsprechende Anwendung in die Gruppe *Ausgewählte Apps* aufgenommen werden und somit in das Diagramm oben auf der Seite eingeschlossen werden soll. Falls Sie eine Anwendung in die Gruppe 'Ausgewählte Apps' einschließen (oder ausschließen) möchten, klicken Sie auf das entsprechende Kontrollkästchen.  Wenn eine Anwendung zur Aufnahme in die Gruppe ausgewählt oder ihre Auswahl rückgängig gemacht wird, wird das Diagramm aktualisiert.  In der Legende _Ausgewählte Apps_ rechts vom Balkendiagramm wird die Anzahl der Anwendungen (in Klammern) angegeben, die derzeit für die Aufnahme in das Diagramm ausgewählt sind.

  In der Anwendungstabelle werden folgenden Informationen als Spalten angezeigt:
   * **Anwendungsname:** Der Name der Anwendung oder Anwendungsinstanz. Wenn der Benutzer nicht über die Berechtigung für den Zugriff auf die Anwendung verfügt, wird stattdessen die Anwendungs-GUID angezeigt.
   * **Instanzen:** Für eine Anwendung gibt sie die Anzahl der aktiven Instanzen an.  Für eine Anwendungsinstanz (die unter dem Anwendungsnamen angezeigt wird, wenn die Anwendungszeile erweitert wird) steht sie für den Namen der Zelle, in der die Anwendungsinstanz ausgeführt wird.
   * **Gesamter physischer Hauptspeicher:** Megabyte (MB) an physischem Hauptspeicher, der von allen Instanzen einer Anwendung verwendet wird.  Der von einer Anwendung verwendete physische Hauptspeicher entspricht der Summe des physischen Hauptspeichers, der von allen Instanzen der Anwendung verwendet wird.
   * **Gesamter reservierter Hauptspeicher:** Megabyte (MB) an Hauptspeicher, der für alle Instanzen einer Anwendung reserviert ist.  Der für eine Anwendung reservierte physische Hauptspeicher entspricht der Summe des Hauptspeichers, der für alle Instanzen einer Anwendung reserviert ist.
   * **Durchschnittliche CPU-Auslastung (% der Zelle):** Für Anwendungsinstanzen stellt die Metrik die durchschnittliche CPU-Auslastung **in der Zelle der jeweiligen Ausführung dar**.  Für eine Anwendung stellt diese Metrik den Durchschnitt der CPU-Auslastung dar, der sich aus den Instanzdurchschnittswerten ergibt.
   * **Maximale CPU-Auslastung (% der Zelle):** Für Anwendungsinstanzen stellt die Metrik die maximale von dieser Instanz verwendete CPU-Auslastung **in der Zelle der jeweiligen Ausführung dar**.  Für eine Anwendung stellt diese Metrik die höchste der maximalen CPU-Auslastungen ihrer Instanzen dar.
   * **CPU-Auslastung (% des Systems):** Der Prozentsatz der gesamten in der CFEE-Umgebung verfügbaren CPU-Kapazität, die von einer Anwendung und ihren Instanzen verwendet wird.  Der von einer Anwendung verwendete CPU-Prozentsatz entspricht der Summe der CPU-Prozentsätze aller Instanzen der Anwendung.
   * **Anforderungen:** Die Anzahl der Anforderungen an eine Anwendung während des letzten Datenerfassungszyklus (fünf Minuten).
   * **Organisation:** Die Organisation, in der die Anwendung bereitgestellt wird. Wenn der Benutzer kein Mitglied der Organisation ist, wird stattdessen die Organisations-GUID angezeigt.

Erweitern Sie eine Anwendungszeile in der Tabelle, um die Liste der Anwendungsinstanzen und die zugehörigen Ressourcennutzungsmetriken anzuzeigen.

### Anwendungen filtern
Sie können den Inhalt der Tabelle mithilfe der Dropdown-Listen **Anwendungen** und **Organisationen** ganz oben in der Tabelle filtern.

Darüber hinaus können Sie das Filtereingabefeld oberhalb der Tabelle verwenden, um nur Anwendungen anzuzeigen, die mit der Zeichenfolge übereinstimmen, die Sie in das Filterfeld eingeben.  Der Filter findet sowohl in der Tabelle als auch in dem Diagramm darüber seinen Niederschlag.

**Hinweis:** Die Filter arbeiten unabhängig von den Tabellenzeilen, die (über das Kontrollkästchen in der Tabellenspalte) zum Aufnehmen der Anwendung in die Gruppe _Ausgewählte Apps_ ausgewählt werden und auch in das obige Diagramm eingeschlossen werden. Falls zum Beispiel insgesamt zehn Anwendungen in der CFEE-Umgebung vorhanden sind, fünf davon für die Aufnahme in das Diagramm ausgewählt sind und Sie die Anwendungen so filtern, dass nur eine Anwendungsinstanz den Filterregeln entspricht, wird in der Tabelle nur diese Anwendungsinstanz angezeigt.  Darüber hinaus enthält die Gruppe _Ausgewählte Apps_ jetzt nur die übereinstimmende Anwendung und das Diagramm wird entsprechend aktualisiert.  Wenn Sie den Filter entfernen, werden in der Tabelle wieder alle zehn Anwendungen angezeigt und die Gruppe _Ausgewählte Apps_ wird zurückgesetzt, sodass alle Anwendungen enthalten sind.


## Zellen
{: #usage_cells}

Die Seite für die Zellen besteht aus zwei Abschnitten:
1. Vertikale Balkendiagramme, in denen Folgendes angezeigt wird:
   * *Insgesamt verfügbare* Hauptspeicherkapazität und CPU-Kapazität, die in der CFEE-Instanz zur Verfügung steht.
   * Hauptspeicherkapazität und CPU-Kapazität, die von **ausgewählten App-Instanzen** in der CFEE-Instanz verwendet werden.
   * Hauptspeicherkapazität und CPU-Kapazität, die von **allen App-Instanzen** in der CFEE-Instanz verwendet werden.
   * Hauptspeicherkapazität und CPU-Kapazität, die vom **System** in der nachfolgenden Tabelle verwendet werden.  Die Systemnutzung stellt die Ressource dar, die von den CFEE-Servicekomponenten und dem Anwendungscache verwendet wird.
   * Gesamtspeicher und Gesamt-CPU, die in der Zelle verfügbar sind. Die **Gesamtzelle** entspricht dem Gesamtspeicher oder der Gesamt-CPU, der/die im Kubernetes-Workerknoten (in dem die Zelle bereitgestellt ist) verfügbar ist, abzüglich des Speichers, der vom System verwendet wird.

   Wenn Sie den Prozentsatz an Hauptspeicher oder CPU anzeigen möchten, der von allen App-Instanzen oder den in der Tabelle ausgewählten App-Instanzen verwendet wird, bewegen Sie den Mauszeiger über den entsprechenden Teil des Diagramms.  Wenn Sie den Mauszeiger über das Balkendiagramm oben bewegen, werden der absolut verfügbare Hauptspeicher oder die gesamte verfügbare CPU-Kapazität, die von allen Apps verwendete Hauptspeicherkapazität oder CPU-Kapazität und die von System und Cache verwendete Hauptspeicherkapazität und CPU-Kapazität angezeigt.  Außerdem wird der Prozentsatz der Hauptspeicherkapazität oder CPU-Kapazität, der von allen Apps und von System und Cache verwendet wird, im Vergleich zur insgesamt verfügbaren Kapazität angezeigt.

2. Eine Tabelle, in der alle Zellen und Anwendungsinstanzen aufgeführt sind, die in ihnen ausgeführt werden.  In jeder Zeile der Tabelle werden Ressourceninformationen für diese Zelle und Anwendungsinstanz angezeigt.

  Die erste Spalte in der Tabelle ist ein Kontrollkästchen, mit dem festlegt wird, ob die entsprechende Anwendungsinstanz in die Gruppe *Ausgewählte App-Instanzen* aufgenommen und somit in das Diagramm oben auf der Seite eingeschlossen werden soll. Falls Sie eine Anwendungsinstanz in die Gruppe 'Ausgewählte Apps' einschließen (oder ausschließen) möchten, klicken Sie auf das entsprechende Kontrollkästchen.  Wenn eine Anwendungsinstanz zur Aufnahme in die Gruppe ausgewählt oder ihre Auswahl rückgängig gemacht wird, wird das Diagramm entsprechend aktualisiert.

  In der Tabelle werden folgenden Informationen als Spalten angezeigt:
   * **Zellenname:** Der Name der Zelle.
   * **Anwendungsname:** Der Name der Anwendung, die in der Zelle ausgeführt wird. Wenn der Benutzer nicht über die Berechtigung für den Zugriff auf die Anwendung verfügt, wird stattdessen die Anwendungs-GUID angezeigt.
   * **Instanzen:** Die Anzahl der Anwendungsinstanzen, die in der Zelle ausgeführt werden.
   * **Physischer Hauptspeicher:** Megabyte (MB) an physischem Hauptspeicher, der von der Anwendungsinstanz verwendet wird, die in der Zelle ausgeführt wird.
   * **Reservierter Hauptspeicher:** Megabyte (MB) an reserviertem Hauptspeicher, der für die Anwendungsinstanz reserviert ist, die in der Zelle ausgeführt wird.
   * **CPU (% der Zelle):** Der Prozentsatz der gesamten in der CFEE-Umgebung verfügbaren CPU-Kapazität, die von der Anwendungsinstanz verwendet wird, die in der Zelle ausgeführt wird.

### Zellen und App-Instanzen filtern
Sie können den Inhalt der Tabelle mithilfe der Dropdown-Liste **Zellen** oberhalb der Tabelle filtern und die Zellen auswählen, die in der Tabelle angezeigt werden sollen.

Darüber hinaus können Sie das Filtereingabefeld oberhalb der Tabelle verwenden, um nur Anwendungsinstanzen anzuzeigen, die mit der Zeichenfolge übereinstimmen, die Sie in das Filterfeld eingeben.  Der Filter findet sowohl in der Tabelle als auch in dem Diagramm darüber seinen Niederschlag.

**Hinweis:** Die Filter arbeiten unabhängig von den Tabellenzeilen, die (über das Kontrollkästchen in der Tabellenspalte) für die Aufnahme einer Anwendungsinstanz in die Gruppe _Ausgewählte App-Instanzen_ ausgewählt und in das obige Diagramm eingeschlossen werden. Falls zum Beispiel insgesamt zehn Anwendungsinstanzen in der CFEE-Umgebung vorhanden sind, fünf davon für die Aufnahme in das Diagramm ausgewählt sind und Sie die Anwendungen so filtern, dass nur eine Anwendungsinstanz den Filterregeln entspricht, wird in der Tabelle nur diese Anwendungsinstanz angezeigt.  Darüber hinaus enthält die Gruppe _Ausgewählte App-Instanzen_ jetzt nur diese App-Instanz und das Diagramm wird entsprechend aktualisiert.  Wenn Sie den Filter entfernen, werden in der Tabelle wieder alle zehn Anwendungsinstanzen angezeigt und die Gruppe _Ausgewählte App-Instanzen_ wird zurückgesetzt, sodass alle App-Instanzen enthalten sind.

## Speichermetriken
{: #memory_metrics}

In CFEE stehen verschiedene Speichermetriktypen zur Verfügung. Diese unterschiedlichen Speichermetriken stammen aus den verschiedenen Perspektiven, über die die Speichernutzung analysiert werden kann. Die Speichernutzung kann relativ zu der für die Cloud Foundry-Zelle(n) verfügbaren Kapazität gemessen werden oder relativ zur gesamten physischen Kapazität des Kubernetes-Workerknotens, in dem Zellen bereitgestellt werden (diese kann auch andere Speichernutzungen umfassen, die nicht mit Cloud Foundry in Verbindung stehen). Die Speicherkapazität kann auch aus der Perspektive des Speichers betrachtet werden, der von Anwendungen reserviert (zugeordnet) wird, oder aus der Perspektive des tatsächlich von diesen Anwendungen genutzten Speichers.   

Im Folgenden sind die Speichermetriken aufgeführt, die Benutzern einer CFEE-Instanz zur Verfügung stehen: 

* Gesamter Speicher, der von den Kubernetes-Workerknoten genutzt wird, die die Cloud Foundry-Zellen unterstützen, relativ zur Gesamtspeicherkapazität dieser Knoten. Hierbei wird nicht nur der von Cloud Foundry-Zellen genutzte Workerknotenspeicher, sondern auch der für System- oder Cacheaufwand genutzte Workerknotenspeicher, der nicht mit Cloud Foundry in Verbindung steht, dargestellt. Dies wird als Messanzeige **Gesamtnutzung** auf der Seite **Übersicht** angezeigt. 
* Der Speicher, der Anwendungen zugeordnet ist, relativ zum verfügbaren Zellenspeicher, unabhängig davon, ob der Speicher tatsächlich genutzt wird. Dies wird als Messanzeige **Zugeordnet** auf der Seite **Übersicht** angezeigt. 
* Speicher, der von Anwendungen physisch genutzt wird, relativ zum verfügbaren Zellenspeicher. Der gesamte genutzte Anwendungsspeicher wird in der Messanzeige **App-Nutzung** auf der Seite **Übersicht** angezeigt. Der Speicher, der von bestimmten Anwendungen genutzt wird, wird auf der Seite **Ressourcennutzung - Anwendungen** angezeigt. 
* Von Cloud Foundry-Zellen genutzter Speicher relativ zur Speicherkapazität des Workerknotens. Dies wird auf der Seite **Ressourcennutzung - Zellen** angezeigt. 
* Gesamter, von Workerknoten genutzter Speicher (in Verbindung mit Cloud Foundry oder unabhängig davon). Dies wird auf der Seite **Aktualisierungen und Skalierung** sowohl für Knoten, die die CFEE-Zellen unterstützen, als auch für Knoten, die die CFEE-Steuerebene unterstützen, angezeigt. 
* Zusätzliche Speichermesswerte werden in Grafana-Dashboards angezeigt, die über die Seite **Überwachung** gestartet werden können. Diese Metriken zeigen die detaillierte Speicherkapazität und -nutzung für Cloud Foundry-Zellen, Kubernetes-Cluster und Workerknoten an. 
