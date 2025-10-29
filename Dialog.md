Dauer: 35 min

Rollen:
- CISO: begeistert ohne zu verstehen worum es eigentlich geht, naiv
- Architektin: Kritisch zu SBOMs, versucht, alles anschaulich zu erklären

# Dialog [30min]

## Setting the Stage

Slides:
- Disclaimer
- No CISOs were harmed
- 1. Akt

Architektin sitzt mit Laptop am Tisch und arbeitet  
CISO kommt herein, kommt zu Architektin, setzt sich 'legere' auf die Tischkante

## Akt 1 [5min]

C: Einen wunderschönen guten Morgen, Frau Mair! Wie geht's uns denn heute?

A [verdreht Augen]: Guten Morgen. Ich kann ja nur für mich sprechen, aber wir haben gerade monsterviel Stress mit...

C: Mir geht es grandios, danke der Nachfrage!

A [seufzt]: Was kann ich denn für Sie tun?

C: Haben Sie schon von den ganzen Supply Chain Angriffen gehört? Die sind gerade überall! Wir müssen uns hier wirklich _schnellstmöglich_ dagegen schützen! Aber ich habe auch schon die Lösung dafür: S-B-O-M-S

A: Bitte was?

C: S-B-O-M-S

A: Was?

C: Software... Billy...

A: Software Bills of Materials? SBOMs?

C: Ja genau, hab ich ja gesagt! Die müssen jetzt alle erstellen, um ihre Security Posture zu verbessern!.

A: Waren sie wieder auf einem Compliance Kongress? **-> compliance meme**

C: Woher... [sammelt sich kurz] Die Anzahl an Supply Chain Attacks wie log4j hat in den letzten Jahren so stark zugenommen und wir müssen uns dagegen schützen. Hier gibt es mit SBOMs wirklich eine tolle Lösung!

A: SBOMs als Lösung für Supply Chain Attacks? Wissen sie denn, was eine SBOMs ist?

C: Ja klar, eine SBOM ist wie so eine Zutatenliste, die mir sagt was in einem Lebensmittel enthalten ist, nur halt für Software. Also 30 Zeilen HTML, 50 Zeilen Java, sowas halt.

A: Gar nicht mal soooo schlecht. Aber fangen wir mal etwas kleiner an: In der modernen Softwareentwicklung schreiben die Entwickler:innen nicht jede Zeile Code selbst, sondern greifen auf vorgefertigte Teile zurück. Nehmen wir die Datumsauswahlfunktion in einer x-beliebigen Anwendung: das ist einerseit recht komplex, andererseits wird es immer wieder benötigt. Somit ist es effizienter, solchen Code in Form von Bibliotheken oder Frameworks aus dem Internet zu laden, statt jedes Mal das Rad neu zu erfinden.

C: Die Entwickler:innen nehmen schon fertigen Code aus dem Internet? Wofür geben wir denn dann Unmengen an Geld für die Entwicklungsteams aus?

A: Wollen Sie das Geld ausgeben, damit jedes Team sein Datumsauswahltool selbst schreibt, oder sollen sie lieber Business Value generieren? :D

C: Ja, Business Value...

A: Das wäre ohne den Einsatz solcher externen Komponenten heutzutage kaum mehr möglich. Unterschiedliche Analysen kommen zu dem Schluss, dass durchschnittlich 70-90% aller halbwegs moderner Software aus externen Komponenten besteht.

C: So viel?! Aber so viele Datumsfelder haben wir doch gar nicht in unserer Software?!

A: Es geht ja nicht nur um Datumsfelder, sondern um ganz unterschiedliche, grundlegende Funktionalitäten, die in Form von Bibliotheken oder Frameworks aus unterschiedlichen Fremdquellen geladen werden und ihrerseits wiederum von anderen Komponenten abhängen, den sogenannten 'Transitiven Abhängigkeiten' - wie beispielsweise von log4j

C: log4j, ja, genau! Da wusste ja auch niemand, wo das alles drinhängt.

A: Richtig. Und diese Komponenten haben wiederum ihre eigenen Abhängigkeiten, auf die sie zurückgreifen.

C: ...und die wiederum...

A: So können also auch schon wenige _direkte_ Komponenten einen Rattenschwanz an weiteren Abhängigkeiten nachladen.

C: Das wird ja dann immer komplexer! Wie behalten Sie denn da den Überblick?

A [grinst] ...und genau da kommen SBOMs ins Spiel!

C: Ja klar, die Zutatenliste, wusste ich doch!

A: Sehr gut! SBOMs sind folglich standardisierte Strukturen, in denen die wichtigsten Datenpunkte zu all diesen Abhängigkeiten aufgeführt werden. Was ist das für eine Komponente, wo kommt sie her, welche Version hat sie, welche Lizenz,... Wollen Sie mal eine solche SBOM sehen?

C: Oh, ja, gerne!

[SPDX Slide]

C: Oh, das kann ja kein Mensch lesen!!

A: Korrekt, SBOMs sind auch eigentlich in erster Linie für Maschinen gedacht.

C: ...und für solche Top-Talente wie Sie! Haben sie das geschrieben??   

A: Nein, das wäre unmöglich. Diese SBOM haben wir von einem unserer Software-Lieferanten erhalten.

C: Ach, das stammt gar nicht von unserer Software?  

A: Nein, diese nicht. Die listet die Komponenten auf, die in seiner Software genutzt werden. Aber für unsere eigene Software können wir auch SBOMs erstellen, die wiederum unsere Abhängigkeiten auflistet.

C: ...und die geben wir dann wiederum an unsere Kunden?

A: Ja, genau!

C: Aber dann wissen die ja, wie unsere Software gebaut wurde! Können die das dann nicht einfach nachbauen?

A: Nein, in der SBOM steht ja nur drin, welche externen Komponenten genutzt werden. Die Geschäftslogik und wie die diese Komponenten nutzt, ist ja nicht aufgeführt.

C: Okay... aber wenn wir so viele Komponenten in unserer Software nutzen, müsste die SBOM ja jedes Mal neu erstellt werden, wenn sich daran etwas ändert...

A: Richtig.

C: Ist das nicht ein Riesenaufwand? Ist das der Grund, warum die Entwickler:innen immer so stark ausgelastet sind?

A: In moderner Software-Entwicklung glücklicherweise nicht, weil sich die Erstellung im Build Process automatisieren lässt; die SBOM wird also jedes Mal automatisch generiert, wenn wir aus dem Quellcode das entsprechende Programm kompilieren.

C: Ach, das ist ja praktisch!


## Akt 2 [15min]

C: Wow, also haben wir mit diesen ganzen SBOMs die Zutatenliste von jeder Software die wir einsetzen?  

A: Teilweise. Für unsere moderneren Applikationen, dessen build und deployment Prozess durchautomatisiert ist, ist die Erstellung einer SBOM trivial. Viele Legacy Anwendungen, speziell die auf compilierte Sprachen basieren, stehen vor großen Herausforderungen. Und dabei haben wir noch nicht unsere Zulieferer betrachtet.

C: Das geht doch schnell, wir schreiben es in die Verträge und zwingen alle dazu uns die SBOMs zu geben! Jeder macht das ja und alle tun das

A: Es geht aber nicht nur um die Lieferanten, die komplette Software Industrie hinkt noch sehr stark bei der Erstellung von SBOMs hinterher. Fast 7M veröffentlichte Komponenten und nur 61k SBOMs. So ähnlich sieht es auch bei unseren Lieferanten aus, die großen sind nicht so problematisch, kleine Nichen-Hersteller die nicht auf Software Entwicklung spezialisiert sind stehen hier vor großen Herausforderungen. Außerdem, ist Open Source aus den aktuellen Regularien wie den Cyber Resilience Act oder die Executive Direktive, und FDA in den USA, die SBOMs vorschreiben, großteils ausgenommen. **-> review OSS sentence**

C: Na das lässt sich ja auch einfach lösen. Wir verbieten unseren Entwickler:innen Open Source zu verwenden. 

A: Sie haben keine wirkliche Ahnung wie viel Open Source bei uns im Unternehmen verwendet wird, oder? Je nach 97% der Anwendungen die Sie gescannt haben, open source Komponenten im Einsatz haben. Es geht nicht nur um Bibliotheken, die Entwickler:innen verwenden um die Arbeit zu beschleunigen, sondern auch bei Datenbanktechnologien, CI/CD tools, Programmiersprachen und Containertechnologie.

C: Dann sollten wir an die Quelle gehen und die Open Source Projekte irgendwie bringen SBOMs zur Verfügung zu stellen um den Marktanteil zu erhöhen.

A: Kritisch ;) Die meisten open source Projekte sind tatsächlich von einzelnen Maintainern abhängig...overload, wenig zeit, kein support. Wir als Unternehmen könnten da sowohl mit finanzieller als auch mit fachlicher Unterstützung supporten!

C: Ach nein, das wurde in diesem fiscal year nicht budgetiert und die Finanzplanung ist bereits abgeschlossen. Vielleicht nächstes Jahr.

A: Mal abgesehen von den Open Source Projekten gibt es noch weitere Challenges, ich habe es vorhin kurz angedeutet. SBOMs sind im Kontext neuer Projekte und aktueller Technologien kein Hexenwerk. Bei interpretierten Programmiersprachen wie JavaScript oder Python sind die externen Abhängigkeiten in manifests wie package.json gelistet und können weiterverarbeitet werden. Da erhält man direkt den direkten Bibliotheken die eingesetzt werden. Bei kompilierten Sprachen, werden Abhängigkeiten und Libraries in Binaries verpackt und erfordern deutlich mehr Maintenance und Arbeit von den Entwicklungsteams. Und wir reden gar nicht über Legacy code, bei dem keiner so genau weiß was da reingepackt wurde. Dann sind wir schon beim Endgegner: Compilierte 20 Jahre alte legacy anwendung, die nicht mehr gewartet wird aber trotzdem weiter im Einsatz bleibt. **weniger technisch**
  
C: Naja da wird es wohl eine technische Lösung geben, um diese SBOMs ganz einfach zu erstellen. Das kann ja nicht so schwer sein.
  
A: Leider doch schon. Die Erstellung von SBOMs ist nicht standardisiert. Es gibt Richtlinien und Standards bezüglich der Struktur, alles andere wie Granularität, Tiefe, Beziehung zwischen den Komponenten sind nicht definiert und jeder macht das ein bisschen anders. Da kann man sehr schnell den Überblick verlieren, außerdem ist noch gar nicht definiert ob die gelieferte SBOM korrekt und vollständig ist.

C: Tools gibt es ja bereits, ich habe bereits den Prozess initiiert um ein kostenloses Tool für uns auszuwählen um das alles zu beschleunigen.

A: Einige unserer Teams haben bereits SBOMs, die aus den automatisierten Pipelines herauspurzeln. Bei den anderen Teams, wo es um Kompilate geht hängt die Qualität der Tools von den Frameworks und Programmiersprachen ab und worauf sich ein Tool für die automatische SBOM Generierung fokussiert. Die heterogene Landschaft in diesem Kontext bringt weitere Herausforderungen. Man nehme eine Applikation und lässt 2 Tools zur Erstellung von SBOMs drüber laufen: die Ergebnisse werden unterschiedlich sein, und womöglich keine komplett falsch, sondern eher unvollständig. Letztendlich haben wir irgendwann einen Haufen SBOMs, in verschiedenen Tiefen mit denen man wenig anfangen kann.

**compiled vs anderes weg lassen**

C: Dann sollten wir diese ganzen SBOMs ja einfach harmonisieren, das geht bestimmt mit irgendeiner KI.
  
A: *schappatmung* Ich will ja keine Spielverderberin sein, aber da kommt schon das nächste Problem: die Übermittlung von SBOMs ist auch nicht standardisiert. Manche Hersteller stellen diese auf ihrer Website zum Download zur Verfügung, andere als Metadaten des Produkts, andere wieder stellen sie via Email auf Anfrage zur Verfügung.

C: Können wir nicht allen einfach einen link zu unserem Sharepoint geben?  

A: *verdrehte augen* Aktuell kommen die SBOMs auf verschiedene Wege zu uns, den größten Teil müssen wir aber bei den Suppliern anfragen und je nach Unternehmensgröße ist die Reaktion darauf. Abgesehen davon müsste man sich auch überlegen wie man die Integrität dieser Dokumente sicherstellt. 

C: Wenn wir die SBOMs von allen Applikationen, in jeder Version bei uns dann haben...ist das ein vollständiges Inventar in dem ich nach log4j und anderen Supply Chain Attacken suchen kann.

A: Vergessen Sie nicht, dass die SBOMs nur maschienenlesbar sind - oder wollen SIE noch einmal einen blick reinwerfen? Bedeutet wir brauchen ein Tool, das die SBOMs verwalten kann um diese durchsuchbar zu machen und in einem zweitern Schritt Schwachstellen anzeigen kann.

C: Ja, dann haben wir das ja zusammen. Noch ein Tool einkaufen kriegen wir auch noch hin. Dann wissen wir direkt welche Schwachstellen die ganzen Produkte besitzen und die Supply Chain Angriffe beheben. Großartig!

A: Hier sollten wir kurz einige Missverständnisse rund um Supply Chain Angriffe und Vulnerabilities aus dem Weg Räumen.
Fangen wir mit den Supply Chain Angriffen an: Ein Supply Chain Angriff ist ein Cyberangriff, bei dem ein Angreifer Schwachstellen in der Lieferkette von Software und/oder Dienstleistungen ausnutzt, um indirekt das eigentliche Zielsystem zu kompromittieren. Das Ziel davon kann somit eine opensource-Bibliothek, ein CI/CD tool oder eine Drittanbieter-Software sein. Z.B. Beim SolarWinds Angriff in 2020 wurde Schadcode in ein Tool eingeschleust, dass dan bei Kunden weltweit installiert wurde, da die Software legitim ist. Es wir auch regelmäßig versucht z.B. in python pakete schadcode einzuführen. Log4j war eine kritische 0-day Schwachstelle, keine supply chain attacke.

**angriff auf die supply chain um das eigentliche Opfer anzugreifen**

C: Verstanden, aber ich möchte dann trotzdem alle Schwachstellen in meinen Produkten kennen.

A: Das ist ein berechtigter Wunsch, leider wird das zunehmend komplexer. Um Schwachstellen zu identifizieren und aufzuzeigen sind diese werden diese zentral angemeldet bei MITRE mit einer eindeutigen CVE-ID. Das ist die größte (?) Datenbank mit allen Schwachstellen und diese sind öffentlich zugänglich. Alle Schwachstellen-scanner tools binden diese Datenbank ein um auf neue Probleme hinzuweise. MITRE war letztens auch in der Presse, da eine große Abhängigkeit von funding von z.B. der USAen Regierung abhängig ist um weiterhin die Leistung zu erbringen. Politische Einflüsse können eine große Auswirkung darauf haben.
Grundsätzlich ist es schon schwierig an sich diese Datenbasis zu handhaben, da die Qualität der Daten stark con der Community abhängt. Man kann auch klar sehen wie die Anzahl an gemeldeten Schwachstellen von Jahr zu Jahr steigt. *diagram evolution CVEs*

**zusammenhang zwischen SBOM und vulnerabilities**

C: Ich habe doch letztens von einer neuen Datenbank in Europa gelesen, das sollte damit ja abgedeckt sein.

A: Ja, die ENISA hat gerade die Beta-Version ihrer Platform im Einsatz. Damit bewegen wir uns weg von einer fas "signle source of truth", das die MITRE DB war, zu mehreren Datenbanken und das ganze wird fragmentiert. Es wird somit verschiedene IDs geben, ob eine 1:1 Mapping immer gewährlistet wird, ist dann auch fragwürdig und wird sich noch herausstellen. Außerdem müssen die verschiedenen Tools, die nach Schwachstellen schauen diese Datenbanken alle unterstützen.

C: hm, schwierig... ha! dann sollten doch einfach die anbieter am besten selber testen und die ergebnisse in die SBOM mit einfügen!  

A: Ja, das gibt es auch schon. Das ist das sogenannte VEX "Vulnerability Exploitability eXchange", wieder ein machine-readable Dokument, das die SBOM erweitern kann um die Ausnutzbarkeit von Schwachstellen zu klären. Hier ist ein Punkt ganz besonders wichtig, die entdeckung neuer Schwachstellen ist nicht statisch, das Vex Dokument aber schon. Oder ein Hersteller müsste bei jeder neuen Schwachstelle in Componenten in ihrer Software eine neue Vex für ein Produkt zur Verfügung stellen. Denn 99% der Zeit kann nur das Entwicklungsteam eine aussage treffen ob eine bestimmte Schwachstelle ausnutzbar ist. Aktuell gibt es keine besonderen Anreize für die Supplier um Schwachstellen zu veröffentlichen.

C: Das klingt irgendwie alles nicht besonders vielversprechend!

A: Um nochmal zurück auf das Thema Supply chain Angriffe zurückzukommen. Wenn ein Drittanbieter von dem wir Software beziehen, dann kann diese auch potentiell kompormittiert werden. Es gibt kein standardisiertes Verfahren, dass die SBOMs auf Integrität und Authentizität prüft.

C: Na jetzt haben sie es aber geschafft mir die SBOMs komplett kaputt zu machen! Das ist ja nur noch sinnloser Aufwand der gar keinen Mehrwert bringt!

## Akt 3

A: Ich kann die Frustration gut nachvollziehen. SBOMs können aber auch einen sinnvollen Einsatz haben. Nur sind sie nicht die silver bullet die man sich oft erhofft. SBOMs werden in vielen Regularien genannt und bilden die Grundlage für sichere Produkte wie z.B. der CRA. Da wir das somit eh machen müssen, sollten wir auch was sinnvolles damit anstellen und nicht nur wie eine Checkbox betrachten.

C: Wie soll dass jetzt funktionieren? All meine Ideen haben sie zerrissen...

A: In der Software Entwicklung ist ein thema von vitaler Wichtigkeit: Dependencies tracken. Entwicklungsteams müssen ihre Abhängigkeiten managen, updaten, patchen und warten. Wenn Componenten z.B. End-of-life gehen müssen diese ausgetauscht werden und man muss nicht nur den selbst-geschriebenen Code absichern, sondern vielmehr die Abhängigkeiten.

C: Das klingt aber nach nichts neuem...

A: Ist es auch nicht, durch die Einführung von SBOMs ist dieses Thema wieder in den Vordergrund getreten. Die Notwendigkeit einer ordentlichen Inventarisierung von Software gibt es schon seit einiger Zeit.

C: Aber was soll das dann konkret bringen?

A: Naja, eine sinnvolle Inventarisierung gekoppelt mit entsprechender Governance rund um das Monitoring, Schwachstellen Management wie es schon auf Infrastruktur erfolgt auf die Software anwenden -> dies gibt einem Unternehmen eine sehr gute visibility in die Software und kann dann auch darauf besser reagieren. Und ja, mit einem ordentlichen Inventar, kann man sich bei einer kritischen zero-day lücke wie log4j das Leben leichter machen und schneller identifizieren wo diese zu finden ist, allerdings nur unter der Annahme dass die SBOMs gepflegt, richtig, zentral durchsuchbar und up to date sind.

C: *nachdenklich*

A: Wenn man dann die Hausaufgaben gemacht hat, kann man auch anfangen mit SBOMs zu Arbeiten. Z.B. indem man die Infromationen der SBOM wie vulnerabilities mit in ein DAST tool fließen lässt um z.B. die Exploitability zu überprüfen und das Produkt zu verbessen.

C: 

Q&A

5 Minuten