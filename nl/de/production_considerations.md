---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Best Practices für die Ausführung von Apps in Produktionsumgebungen
{: #production}

Cloud Foundry ist eine ausgezeichnete Plattform für die Ausführung von cloudgeeigneten Anwendungen in einer Produktionsumgebung. Die hier vorgestellten Best Practices unterstützen Sie bei der Ausführung von Cloud Foundry-Apps in Produktionsumgebungen mit {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Mehrere Instanzen
{: #multiple_instances}

Für die Cloud geeignete Apps sind horizontal skalierbar und somit in der Lage, Anwendungsinstanzen dynamisch hinzuzufügen oder zu entfernen. Führen Sie von jeder Anwendung mindestens drei Instanzen aus, um bei punktuellen Störungen oder bei der Plattformwartung unerwartete Ausfallzeiten zu vermeiden.

## Überwachungsoptionen
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} vereinfacht die Überwachung Ihrer Anwendungen durch Services wie [Monitoring and Analytics](/docs/services/monana/index.html) und [New Relic ![Symbol für externen Link](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}. Weitere Informationen zu diesem Thema finden Sie unter [Integrierte Protokollierungsfunktionen](../monitor_log/logging.html#logging_for_bluemix_apps).

## Unterstützungsoptionen
{: #support}

Die gebührenpflichtigen {{site.data.keyword.Bluemix_notm}}-Preisstrukturpläne bieten eine Reihe unterschiedlicher Kontotypen mit *optionalem* gebührenpflichtigen Support.  Eine Registrierung dieser Option sollten Sie ungeachtet Ihres Kontotyps auf jeden Fall in Erwägung ziehen, wenn Sie Ihre Anwendung in einer {{site.data.keyword.Bluemix_notm}}-Produktionsumgebung nutzen wollen.

Im Abschnitt [Support erhalten](../get-support/howtogetsupport.html) ist beschrieben, wie Sie - ob mit oder ohne gebührenpflichtigem Support - Unterstützung anfordern können. Die Nutzung des gebührenpflichtigen Supports stellt sicher, dass Ihre Support-Tickets mit entsprechender Aufmerksamkeit behandelt werden.
