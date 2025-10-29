Dauer: 35 min

Rollen:
- CISO: begeistert ohne zu verstehen worum es eigentlich geht, naiv
- Architektin: Kritisch zu SBOMs, versucht, alles anschaulich zu erklären

# Dialog [30min]

## Setting the Stage

Slides:
- #1 Disclaimer
- #2 No CISOs were harmed
- #3 1. Akt

Architektin sitzt mit Laptop am Tisch und arbeitet  
CISO kommt herein, kommt zu Architektin, setzt sich 'legere' auf die Tischkante

## Akt 1 [5min]

C: Einen wunderschönen guten Morgen, Frau Mair! Wie geht's uns denn heute?

A [verdreht Augen]: Guten Morgen. Ich kann ja nur für mich sprechen, aber wir haben gerade monsterviel Stress mit...

- #4 State of supply chain attacks

C: Mir geht es grandios, danke der Nachfrage!

A [seufzt]: Was kann ich denn für Sie tun?

C: Haben Sie schon von den ganzen Supply Chain Angriffen gehört? Die sind gerade überall! Wir müssen uns hier wirklich _schnellstmöglich_ dagegen schützen! Aber ich habe auch schon die Lösung dafür: S-B-O-M-S

A: Bitte was?

C: S-B-O-M-S

A: Was?

C: Software... Billy...

A: Software Bill of Materials? SBOMs?

C: Ja genau, hab ich ja gesagt! Die müssen jetzt alle erstellen, um ihre Security Posture zu verbessern!

- #5 Spongebob SBOMs

A: Waren sie wieder auf einem Compliance Kongress?

C: Woher... [sammelt sich kurz] Die Anzahl an Supply Chain Attacks wie log4j hat in den letzten Jahren so stark zugenommen und wir müssen uns dagegen schützen. Hier gibt es mit SBOMs wirklich eine tolle Lösung!

A: SBOMs als Lösung für Supply Chain Attacks? Wissen sie denn, was eine SBOM ist?

C: Ja klar, eine SBOM ist wie so eine Zutatenliste, die mir sagt was in einem Lebensmittel enthalten ist, nur halt für Software. Also 30 Zeilen HTML, 50 Zeilen Java, sowas halt.

- #8 blackduck scan folie

A: Gar nicht mal sooo schlecht. Aber fangen wir mal etwas kleiner an: In der modernen Softwareentwicklung schreiben die Entwickler:innen nicht jede Zeile Code selbst, sondern greifen auf vorgefertigte Teile zurück. Nehmen wir die Datumsauswahlfunktion in einer x-beliebigen Anwendung: das ist einerseits recht komplex, andererseits wird es immer wieder benötigt. Somit ist es effizienter, solchen Code in Form von Bibliotheken oder Frameworks aus dem Internet zu laden, statt jedes Mal das Rad neu zu erfinden.

C: Die Entwickler:innen nehmen schon fertigen Code aus dem Internet? Wofür geben wir denn dann Unmengen an Geld für die Entwicklungsteams aus?

A: Wollen Sie das Geld ausgeben, damit jedes Team sein Datumsauswahltool selbst schreibt, oder sollen sie lieber Business Value generieren? :D

C: Ja, Business Value...

A: Das wäre ohne den Einsatz solcher externen Komponenten heutzutage kaum mehr möglich. Unterschiedliche Analysen kommen zu dem Schluss, dass durchschnittlich 70-90% aller halbwegs moderner Software aus externen Komponenten besteht.

C: So viel?! Aber so viele Datumsfelder haben wir doch gar nicht in unserer Software?!

A: Es geht ja nicht nur um Datumsfelder, sondern um ganz unterschiedliche, grundlegende Funktionalitäten, die in Form von Bibliotheken oder Frameworks aus unterschiedlichen Fremdquellen geladen werden und ihrerseits wiederum von anderen Komponenten abhängen, den sogenannten 'Transitiven Abhängigkeiten' - wie beispielsweise von log4j

C: log4j, ja, genau! Da wusste ja auch niemand, wo das alles drinhängt.

A: Richtig. Und diese Komponenten haben wiederum ihre eigenen Abhängigkeiten, auf die sie zurückgreifen.

C: ...und die wiederum...

- #9 direct/transitive dependencies

A: So können also auch schon wenige _direkte_ Komponenten einen Rattenschwanz an weiteren Abhängigkeiten nachladen.

C: Das wird ja dann immer komplexer! Wie behalten Sie denn da den Überblick?

A [grinst] ...und genau da kommen SBOMs ins Spiel!

- #12 SBOM contents

C: Ja klar, die Zutatenliste, wusste ich doch!

A: Sehr gut! SBOMs sind folglich standardisierte Strukturen, in denen die wichtigsten Datenpunkte zu all diesen Abhängigkeiten aufgeführt werden. Was ist das für eine Komponente, wo kommt sie her, welche Version hat sie, welche Lizenz,... Wollen Sie mal eine solche SBOM sehen?

C: Oh, ja, gerne!

- #13 SPDX slide

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

A: In moderner Software-Entwicklung glücklicherweise nicht, weil sich die Erstellung im Build Process automatisieren lässt; die SBOM wird also jedes Mal automatisch generiert, wenn wir aus dem Quellcode das entsprechende Programm bauen.

C: Ach, das ist ja praktisch!


## Akt 2 [15min] -> slide, sip of water, weiter

C: Also haben wir mit diesen ganzen SBOMs die Zutatenliste von jeder Software die wir entwickeln und einsetzen?  

A: Ja, teilweise. Unsere Entwickler:innen arbeiten dran, SBOMs für unsere Produkte zu erstellen. 

C: ..und dann sind wir ja fertig damit! Prima!

A: Nicht so schnell! Damit wir die SBOMs für unsere Produkte finalisieren können brauchen wir die SBOMs von Komponenten die von unseren Lieferanten kommen.

C: Das geht doch schnell, wir schreiben es in die Verträge und zwingen alle dazu. Jeder macht heutzutage SBOMs, da müssen wir auch mithalten!

- #15 cumulative SBOMs

A: Naja... es stimmt schon, dass immer mehr SBOMs erstellt werden, aber wir sind noch lange nicht da wo wir sein sollten. Fast 7M veröffentlichte Komponenten in 2024 und nur 61k SBOMs. 

- #17 cumulative vs. packages

C: Nur so wenige???

A: Die großen Hersteller sind nicht so problematisch, die kleinen Lieferanten, in bestimmten Nichen die nicht auf Software-Entwicklung spezialisiert sind haben es schon schwieriger.

C: SBOMs sollten dann trotzdem in den Verträgen bei den nächsten Verlängerungen mit aufgenommen werden...

A: Wie vorhin kurz angedeutet, beinhalten unsere Anwendungen nicht nur Componenten von unseren Lieferanten, sondern auch...

C: Opensource Teile

A: Genau, und diese Projekte müssen nicht unbedingt eine SBOM liefern, Verträge haben wir in diesen Fällen auch nicht.

C: Na das lässt sich ja auch einfach lösen. Wir verbieten unseren Entwickler:innen Open Source zu verwenden. 

A: Sie haben keine wirkliche Ahnung wie viel Open Source bei uns im Unternehmen verwendet wird, oder? 

C: Das kann doch nicht so viel sein

A: 97% der Anwendungen die ein Hersteller gescannt hat, hat open source Komponenten im Einsatz.

C: Dann nutzen wir kein Linux mehr... 

A: Es geht nicht nur um Betriebssysteme sondern um Bibliotheken, die Entwickler:innen verwenden um die Arbeit zu beschleunigen, Datenbanktechnologien, CI/CD tools, Programmiersprachen und Containertechnologin.

C: Dann sollten wir an die Quelle gehen und die Open Source Projekte irgendwie bringen SBOMs zur Verfügung zu stellen. Das erhöht ja schlußendlich auch deren Marktanteil

- #18 maintainer open source

A: Marktanteile spielen im Opensource Kontext nicht wirklich eine Rolle. Hinzu kommt, dass die meisten open source Projekte werden von einzelnen oder wenigen Menschen gewartet. Diese haben wenig Zeit, wenig Support und sind sehr unter Druck und kommen nicht wirklich dazu. Da könnten wir als Unternehmen sowohl mit finanzieller als auch mit fachlicher Unterstützung supporten!

- #19 sponsor open source

C: Ach nein, das wurde in diesem Geschäftsjahr nicht budgetiert und die Finanzplanung ist bereits abgeschlossen. Vielleicht nächstes Jahr.

A: Mal abgesehen von diesen Herausforderungen, hängt die Komplexität für die Erstellung einer SBOM stark von der Programmiersprache und den verwendeten Frameworks ab.

C: Warum denn das? Code ist ja code!

A: Die Sprachen und wie sie funktionieren unterscheiden sich recht stark. In der modernen Web-Welt erhält man automatisch die direkten Abhängigkeiten einer Applikation, bei den nächsten Ebenen, den transitiven Abhängigkeiten kann es schon schwieriger werden.

C: Wir haben aber nicht nur web-applikationen bei uns...

A: Genau, bei Hardware-naher Entwicklung, werden Drittanbieter Bibliotheken anders eingebunden und es gibt keine schöne Liste wie in der Web Welt. Da müssen die Etnwicklungsteams daran arbeiten die Abhängigkeiten klar zu dokumentieren. Je älter die Applikation, je schwieriger es wird eine SBOM dafür zu erstellen.
  
C: Naja da wird es wohl eine technische Lösung geben, um diese SBOMs ganz einfach zu erstellen. Das kann ja nicht so schwer sein.
  
A: Leider doch schon. Die Erstellung von SBOMs ist nicht standardisiert. 

C: Es gibt doch Richtlinien...

A: Ja, die Richtlinien und Standards beziehen sich auf die Struktur.

C: Das ist ja was wir brauchen!

A: Das ist wichtig, aber nicht genug. Granularität, Tiefe, Beziehung zwischen den Komponenten sind nicht definiert und jeder macht das ein bisschen anders. 

C: Stellt das ein echtes Problem dar?

A: So ist es sehr schwer herauszufinden ob eine gelieferte SBOM korrekt und vollständig ist.

C: Das sollte man ja technisch lösen können, es gibt ja bereits verschiedenste Tools auf dem Markt! Ich habe bereits den Prozess initiiert um ein kostenloses Tool für uns auszuwählen um das alles zu beschleunigen.

A: Wie vorhin bereits angedeutet, einige unserer Teams erstellen SBOMs als Teil der automatisierten Build Pipelines. Würden wir jetzt zwei Tools zur automatischen Erstellung von SBOMs über die Anwendungen laufen lasseen, würden diese mit hoher Wahrscheinlichkeit verschiedene Ergebnisse liefern.

C: Na da muss dann eins falsch sein!

A: Womöglich ist keine SBOM falsch, sondern beide unvollständig.

C: Dann sollten wir diese ganzen SBOMs ja einfach harmonisieren, das geht bestimmt mit irgendeiner KI.
  
A: *schappatmung* Ich will ja keine Spielverderberin sein, aber da kommt schon das nächste Problem...

C: Was kann denn jetzt noch fehlen?

A: die Übermittlung von SBOMs ist auch nicht standardisiert. Manche Hersteller stellen diese auf ihrer Website zum Download zur Verfügung, andere als Metadaten des Produkts, andere wieder stellen sie via Email auf Anfrage zur Verfügung.

C: Das ist doch super aufwendig.

A: Genau, wir fragen die aktuell meistens per Email an und auf dem selben Weg erhalten wir diese auch. So richtig können wir dabei auch die Integrität und Authentizität der SBOMs nicht überprüfen.

C: Dafür gibt es ja bewährte Methoden, wie z.B. Signaturen oder Checksums die man auch an anderer Stelle benutzt.

A: Ok, dann bekommen wir eine signierte SBOM, woher wissen wir dass die Person diese signieren darf?

C: Sie haben wohl wirklich Zero Trust

A: -.-

C: Nun ja, dann nehmen wir mal das was wir bekommen können her. Das ist dann mein Inventar in dem ich nach log4j und anderen Supply Chain Attacken suchen kann.

A: Erstmal haben Sie nur eine Menge einzelner Dokumente die händisch durchsucht werden müssten. Und vergessen Sie nicht, dass die SBOMs nur maschienenlesbar sind - oder wollen SIE noch einmal einen blick reinwerfen? 

C: Nein, nein, auf keinen Fall!

A: Das bedeutet wir brauchen ein Tool, das die SBOMs verwalten kann um diese durchsuchbar zu machen und in einem zweitern Schritt Schwachstellen anzeigen kann.

C: Ja, dann haben wir das ja zusammen. Noch ein Tool einkaufen kriegen wir auch noch hin. Dann wissen wir direkt welche Schwachstellen die ganzen Produkte besitzen und die Supply Chain Angriffe beheben. Großartig!

A: Hier sollten wir kurz einige Missverständnisse rund um Supply Chain Angriffe und Vulnerabilities aus dem Weg räumen.

C: Wie das? 

A: Fangen wir mit den Supply Chain Angriffen an: Ein Supply Chain Angriff ist ein Cyberangriff, bei dem ein Angreifer die Software Supply Chain einer dritten Partei angreift um dadurch an das eigentliche Opfer zu gelangen.

C: War das bei log4j nicht der Fall?

A: Nein, log4j war eine kritische Zero-Day Schwachstelle. Supply Chain Angriffe sind zum Beispiel, schadcode in einem legitimen Code-Repository zu injizieren oder die Entwendung von Zertifikaten zum Signieren von Anwendungen.

C: Aber Supply Chain Angriffe nehmen doch zu...

A: Ja, das stimmt. Ein sehr bekanntes Beispiel für eine Supply Chain Attacke war Solarwinds in 2020: dabei wurde deren Build System kompromittiert und hat den Angreifern ermöglicht schadcode in das entwickelte Produkt einzubauen. Die Kunden haben dann die Software installiert, weil diese von ihrem Lieferanten kam und damit haben sich die Angreifer Zugriff auf die Zielsysteme verschafft.

C: Ja, das würden ja anhand von der SBOM verstehen, dass da was drin ist was nicht da sein sollte.

A: Aber woher erhalten wir die SBOM?

C: Ja... vom Anbieter!

A: Der kompromittiert wurde und wahrscheinlich auch die SBOM entsprechend anpasst. Außerdem wenn was neues eingebaut wird, muss die SBOMs sich nicht notwendigerweise ändern. Es ist ausgeschlossen, dass Angreifer ihre Schadsoftware in der SBOM als solche auflisten :D 

C: Verstanden, also helfen SBOMS gar nicht gegen supply chain attacken?

A: Nein...

C: Was ist denn mit log4j?

A: Ja, das schon eher, weil es Dependency mit einer kritischen Schwachstelle ist.

C: Das war ja ein Alptraum herauszufinden wo das im Einsatz war. Jetzt hätten wir ja die Schwachstellen alle in der SBOM gelistet.

A: Mooooooment, machen wir einen kurzen Schritt zurück. Durch dieses Inventar bekommt das Team in erster Linie einen Überblick über deren Abhängigkeiten. Durch die Informationen wie Hersteller, Name und Version der Komponenten diese eindeutig identifiziert.

C: Und woher kriegen wir dann die Schwachstellen zu den Abhängigkeiten?

A: Die werden gegen Datenbanken gecheckt. Und wir begeben uns in deren Abhängigkeit. Die größte Datenbank an CVEs von MITRE betrieben... 

C: Die waren letztens doch in der Presse wegen der Entscheidung des USA Präs das Programm nicht weiter zu Unterstützen.

A: Ja genau. Es wird weltweit von Unternehmen genutzt um Schwachstellen zu veröffentlichen und von Security-Tool Herstellern um ihre Tools damit zu füttern, weil Sicherheitsforscher:innen und Unternehmen dort die bekannten Schwachstellen melden. Das Programm ist ein Eckpfeiler der globalen Sicherheit, man hat aber gemerkt wie politische Einflüsse sich darauf auswirken können.

C: Ich habe doch letztens von einer neuen Datenbank in Europa gelesen, das sollte damit ja abgedeckt sein.

A: Ja, die ENISA hat gerade die Beta-Version ihrer Platform im Einsatz. Damit bewegen wir uns weg von der aktuellen "signle source of truth", das die CVE DB war, zu mehreren Datenbanken und das ganze wird fragmentiert.

C: Na gut, dann haben wir halt mehrere Quellen die mir sagen wo ich angreifbar bin. Doppelt gemoppelt hält ja besser!

A: Naja, wir haben dann eine sehr lange liste an Schwachstellen. Aber nur weil eine verwendete Bibliothek eine Schwachstelle enthält, bedeutet es nicht zwangsläufig dass diese ausgenutzt werden kann.

C: Wie geht das denn? Schwachstelle ist Schwachstelle

A: Nicht wirklich, wenn die Entwickler:innen den Teil nicht benutzen der von der Schwachstelle betroffen ist, dann haben Angreifende auch nicht die Möglichkeit diese zu misbrauchen. Das ist das Konzept der Exploitability.

C: Aber woher wissen wir ob wir angreifbar sind oder nicht?

A: Das müssten wir dann entsprechend testen und damit verbundene Risiko bewerten.

C: Das klingt nach ganz schön viel Aufwand! Hah, warum lassen wir das nicht die anbieter selber testen und die Ergebnisse mit uns teilen.

A: Ja, das gibt es auch schon. Das ist das sogenannte VEX "Vulnerability Exploitability eXchange"

C: Wieder ein nur maschinell lesbares Dokument? -.- 

A: Ja, damit kann der Anbieter die SBOM erweitern um die Ausnutzbarkeit von Schwachstellen zu klären in den aufgelisteten Komponenten.

C: Klingt doch vielversprechend?

A: Naja, nicht wirklich. Die VEX ist ein statisches Dokument, Schwachstellen sind ein bisschen dynamischer. Der VEX gibt mir nur einen Snapshot zu einem gewissen Zeitpunkt. Wenn neue Schwachstellen entdeckt werden muss der Hersteller diese neu bewerten und uns eine neue VEX Datei für das Produkt schicken.

C: Ja, dann ertrinken wir ja diesen Unterlagen!

A: Nicht nur das, Hersteller haben natürlich einen impliziten Anreiz zu zeigen, dass sie von wenigen Schwachstellen betroffen sind. Und wir können nicht bewerten ob und wie der Hersteller bestimmte die Anwendbarkeit getestet hat. 

C: Weil es auch hier an einheitlichen Ansätzen fehlt?

A: Ja, sowohl bei SBOMs als auch VEX Dokumente müssen wir darauf vertrauen, dass die Verfasser:innen ordentlich arbeiten und wissen was sie tun... ;)

C: Na jetzt haben sie es aber geschafft mir die SBOMs komplett kaputt zu machen! Das ist ja nur noch sinnloser Aufwand der gar keinen Mehrwert bringt!


## Akt 3

A: Ich kann die Frustration gut nachvollziehen. SBOMs können aber auch einen sinnvollen Einsatz haben. Nur sind sie nicht die silver bullet die man sich oft erhofft.

C: Und das wäre?

A: Auf der einen Seite, werden SBOMs in neuen Regularien genannt und bilden die Grundlage für sichere Produkte wie z.B. der CRA. Da wir das somit eh machen müssen, sollten wir auch was sinnvolles damit anstellen und nicht nur wie eine Checkbox betrachten.

C: Wie soll dass jetzt funktionieren? All meine Ideen haben sie zerrissen...

A: In der Software Entwicklung ist ein thema von vitaler Wichtigkeit: Abhängigkeiten tracken. Das macht man in Bezug auf Open Source Packages mit einer Software Composition Analyse.

C: Was bringt mir das?

A: Naja mit der SCA wird die Applikation nach OSS durchsucht und überprüft ob die Komponenten aktuell sind, schwachstellen enthalten und ob diese problematische Lizenzen beinhalten.

C: Das klingt aber nach nichts neuem...

A: Ist es auch nicht, durch die Einführung von SBOMs ist dieses Thema wieder in den Vordergrund getreten und erweitert um kommerzielle Componenten. Die Notwendigkeit einer ordentlichen Inventarisierung von Software gibt es schon seit einiger Zeit.

C: Aber was soll das dann konkret bringen?

A: Naja, eine sinnvolle Inventarisierung gekoppelt mit entsprechender Governance rund um das Monitoring, Schwachstellen Management wie es schon auf Infrastruktur erfolgt auf die Software anwenden -> dies gibt einem Unternehmen eine sehr gute visibility in die Software und kann dann auch darauf besser reagieren. Und ja, mit einem ordentlichen Inventar, kann man sich bei einer kritischen zero-day lücke wie log4j das Leben leichter machen und schneller identifizieren wo diese zu finden ist, allerdings nur unter der Annahme dass die SBOMs gepflegt, richtig, zentral durchsuchbar und up to date sind.

C: *nachdenklich*

A: Wenn man dann die Hausaufgaben gemacht hat, kann man auch anfangen mit SBOMs zu Arbeiten. Z.B. indem man die Infromationen der SBOM wie vulnerabilities mit in ein DAST tool fließen lässt um z.B. die Exploitability zu überprüfen und das Produkt zu verbessen.

C: 

Q&A

5 Minuten

**SBOMs sind per Definition auch flach abgebildet...bedeutet die Teams brauchen ein tiefes Verständnis der verwendeten Bibliotheken.**

// developer awareness -> Bewusstsein wie sie mit abhängigkeiten umgehen -> reduce, woran erkenne ich eine gute vs böse Dependency -> wo problematisch openssf checken -> kennzahlen was eine gute dependency

//governance -> nicht nur alles mögliche haben -> man braucht lifecycle mgmt

//


Streichkandidaten: Integrität, ENISA, VEX,...
