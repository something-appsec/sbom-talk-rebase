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

A [verdreht Augen]: Guten Morgen, Chef. Ich kann ja nur für mich sprechen, aber wir haben gerade monsterviel Stress mit...

C: Mir geht es grandios, danke der Nachfrage!

A [seufzt]: Was kann ich denn für Sie tun?

- Slide: State of Supply Chain Attacks

C: Haben Sie schon von den ganzen Supply Chain Angriffen gehört? Die sind gerade überall! Wir müssen uns hier wirklich _schnellstmöglich_ dagegen schützen!

A: Naja, also...

C: Aber ich habe auch schon die Lösung dafür: S-B-O-M-S

- Slide: Spongebob SBOMs

A: Bitte was?

C: S-B-O-M-S

A: Was?

C: Software... Billy...

A: Software Bill of Materials? SBOMs?

C: Ja genau, hab ich ja gesagt! Die müssen jetzt alle erstellen, um ihre Security Posture zu verbessern!

A: Waren sie mal wieder auf einem Compliance Kongress?

- Slide: Distracted by SBOMs

C: Woher... [sammelt sich kurz] Die Anzahl an Supply Chain Attacks wie log4j hat in den letzten Jahren so stark zugenommen und wir müssen uns dagegen schützen. Hier gibt es mit SBOMs wirklich eine tolle Lösung!

A: Ähm... SBOMs als Lösung für Supply Chain Attacks? Wissen sie denn, was eine SBOM ist?

C: Ja klar, eine SBOM ist wie so eine Zutatenliste, die mir sagt was in einem Lebensmittel enthalten ist, nur halt für Software. Also 30 Zeilen HTML, 50 Zeilen Java, sowas halt.

- Slide: Blackduck Scans

A: Gar nicht mal sooo schlecht. Aber fangen wir mal etwas kleiner an: In der modernen Softwareentwicklung schreiben die Entwickler:innen nicht jede Zeile Code selbst, sondern greifen auf vorgefertigte Teile zurück. Nehmen wir die Datumsauswahlfunktion in einer x-beliebigen Anwendung: das ist einerseits recht komplex, andererseits wird sie immer wieder benötigt. Somit ist es effizienter, solchen Code in Form von Bibliotheken oder Frameworks aus dem Internet zu laden, statt jedes Mal das Rad neu zu erfinden.

C: Die Entwickler:innen nehmen schon fertigen Code aus dem Internet? Wofür geben wir denn dann Unmengen an Geld für die Entwicklungsteams aus?

A: Wollen Sie das Geld ausgeben, damit jedes Team sein Datumsauswahltool selbst schreibt, oder sollen sie lieber Business Value generieren? :D

C: Ja, Business Value...

A: Das wäre ohne den Einsatz solcher externen Komponenten heutzutage kaum mehr möglich. Unterschiedliche Analysen kommen zu dem Schluss, dass durchschnittlich 70-90% aller halbwegs moderner Software aus externen Komponenten besteht.

C: So viel?! Aber so viele Datumsfelder haben wir doch gar nicht in unserer Software?!

A: Es geht ja nicht nur um Datumsfelder, sondern um ganz unterschiedliche, grundlegende Funktionalitäten, die in Form von Bibliotheken oder Frameworks aus unterschiedlichen Fremdquellen geladen werden und ihrerseits wiederum von anderen Komponenten abhängen, den sogenannten 'Transitiven Abhängigkeiten' - wie beispielsweise von log4j

C: log4j, ja, genau! Da wusste ja auch niemand, wo das alles drinhängt.

A: Richtig. Und diese Komponenten haben wiederum ihre eigenen Abhängigkeiten, auf die sie zurückgreifen.

C: ...und die wiederum haben auch wieder Abhängigkeiten, die ihrerseits wieder...

- Slide: Direct/Transitive Dependencies

A: Genau! So können also auch schon wenige _direkte_ Komponenten einen Rattenschwanz an weiteren Abhängigkeiten nachladen.

C: Das wird ja dann immer komplexer! Wie behalten Sie denn da den Überblick?

A [grinst] ...und genau da kommen SBOMs ins Spiel!

C: Ja klar, die Zutatenliste, wusste ich doch!

- #12 SBOM contents

A: Sehr gut! SBOMs sind folglich standardisierte Strukturen, in denen die wichtigsten Datenpunkte zu all diesen Abhängigkeiten aufgeführt werden. Was ist das für eine Komponente, wo kommt sie her, welche Version hat sie, welche Lizenz,... Wollen Sie mal eine solche SBOM sehen?

C: Oh, ja, gerne!

- Slide: SPDX JSON

C: Oh, das kann ja kein Mensch lesen!!

A: Korrekt, SBOMs sind auch eigentlich in erster Linie für Maschinen gedacht.

C: [schleimig] ...und für solche Top-Talente wie Sie! Haben sie das geschrieben?

A: Nein, das wäre unmöglich. Diese SBOM haben wir von einem unserer Software-Lieferanten erhalten.

C: Ach, das stammt gar nicht von unserer Software?

A: Nein, diese nicht. Die listet die Komponenten auf, die in seiner Software genutzt werden. Aber für unsere eigene Software können wir auch SBOMs erstellen, die wiederum unsere Abhängigkeiten auflisten.

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

C: ...dann sind wir ja bald fertig damit! Prima!

A: Nicht so schnell! Damit wir die SBOMs für unsere Produkte finalisieren können, brauchen wir die SBOMs von Komponenten, die von unseren Lieferanten kommen.

C: Das geht doch schnell, wir schreiben es in die Verträge und zwingen alle dazu. Jeder macht heutzutage SBOMs, da müssen wir auch mithalten!

- #15 cumulative SBOMs

A: Naja... es stimmt schon, dass immer mehr SBOMs erstellt werden, aber wir sind noch lange nicht da, wo wir sein sollten. Fast 7M veröffentlichte Komponenten in 2024 und nur 61k SBOMs. 

- #17 cumulative vs. packages

C: Nur so wenige???

A: Die großen Hersteller sind nicht so problematisch, die kleinen Lieferanten, in bestimmten Nichen die nicht auf Software-Entwicklung spezialisiert sind haben es schon schwieriger.

C: SBOMs sollten dann trotzdem bei den nächsten Verlängerungen in die Verträge mit aufgenommen werden...

A: Wie vorhin kurz angedeutet, beinhalten unsere Anwendungen nicht nur Komponenten von unseren Lieferanten, sondern auch...

C: Open Source Teile?

A: Genau, und diese Projekte müssen nicht unbedingt eine SBOM liefern. Verträge haben wir in diesen Fällen auch nicht.

C: Na, das lässt sich ja auch einfach lösen. Wir verbieten unseren Entwickler:innen einfach, Open Source zu verwenden. 

A: Sie haben keine wirkliche Ahnung, wie viel Open Source bei uns im Unternehmen verwendet wird, oder? 

C: Das kann doch nicht so viel sein...

// TODO
A: 97% der Anwendungen die ein Hersteller gescannt hat, haben Open Source Komponenten im Einsatz.

C: Dann nutzen wir halt einfach kein Linux mehr... 

A: Es geht hierbei nicht um Betriebssysteme, sondern um Bibliotheken, die Entwickler:innen verwenden um die Arbeit zu beschleunigen, Datenbanktechnologien, CI/CD-Tools, Programmiersprachen und Containertechnologin.

C: Dann sollten wir an die Quelle gehen und die Open Source Projekte irgendwie bringen, SBOMs zur Verfügung zu stellen. Das erhöht ja schlussendlich auch deren Marktanteil

- Slide: Open Source Maintainer

A: Marktanteile spielen im Open Source Kontext nicht wirklich eine Rolle. Hinzu kommt, dass die meisten Open Source Projekte von einzelnen oder wenigen Menschen gewartet werden. Diese haben wenig Zeit, wenig Support und sind sehr unter Druck und kommen nicht wirklich dazu. Da könnten wir als Unternehmen sowohl mit finanzieller als auch mit fachlicher Unterstützung supporten!

- Slide: Sponsor Open Source Projects!

C: Ach nein, das wurde in diesem Geschäftsjahr nicht budgetiert und die Finanzplanung ist bereits abgeschlossen. Vielleicht nächstes Jahr.

A: Mal abgesehen von diesen Herausforderungen hängt die Komplexität für die Erstellung einer SBOM stark von der Programmiersprache und den verwendeten Frameworks ab.

C: Hä, warum denn das? Code ist doch Code, egal in welcher Sprache!

A: Die Sprachen und wie sie funktionieren unterscheiden sich recht stark. In der modernen Web-Welt erhält man häufig schon automatisch die direkten Abhängigkeiten einer Applikation. Bei den nächsten Ebenen, den Transitiven Abhängigkeiten, kann es aber schon schwieriger werden.

C: Wir haben aber nicht nur Web-Applikationen bei uns...

A: Genau! Bei Server-Applikationen oder Hardware-naher Entwicklung werden Drittanbieter-Bibliotheken oftmals anders eingebunden und es gibt keine schöne Liste wie in der Web-Welt. Da müssen die Entwicklungsteams daran arbeiten, die Abhängigkeiten klar zu dokumentieren. Je älter die Technologie, desto schwieriger wird es, eine SBOM dafür zu erstellen.
  
C: Naja, da wird es wohl schon irgendeine technische Lösung geben, um diese SBOMs ganz einfach zu erstellen. Das kann doch nicht so schwer sein.
  
A: Leider doch schon. Die Erstellung von SBOMs ist nicht standardisiert. 

C: Es gibt doch Richtlinien und Standards!

A: Ja, die Richtlinien und Standards beziehen sich auf die Struktur.

C: Das ist ja, was wir brauchen!

A: Das ist wichtig, aber nicht genug. Granularität, Tiefe, oder die Beziehung zwischen den Komponenten sind nicht definiert und jeder macht das ein bisschen anders. 

C: Stellt das ein echtes Problem dar?

A: So ist es sehr schwer herauszufinden, ob eine gelieferte SBOM korrekt und vollständig ist.

C: Das sollte man aber technisch lösen können, es gibt ja bereits verschiedenste Tools auf dem Markt! Ich habe sogar bereits den Prozess initiiert, um ein kostenloses Tool für uns auszuwählen und das alles zu beschleunigen.

A: Wie vorhin bereits angedeutet: einige unserer Teams erstellen bereits SBOMs als Teil der automatisierten Build Pipelines. Würden wir aber jetzt zwei Tools zur automatischen Erstellung von SBOMs über die Anwendungen laufen lassen, würden diese mit hoher Wahrscheinlichkeit verschiedene Ergebnisse liefern.

C: Na, da muss doch dann eins falsch sein!

A: Womöglich ist keine SBOM falsch, sondern beide unvollständig.

C: Dann sollten wir diese ganzen SBOMs einfach harmonisieren. Das geht bestimmt mit irgendeiner KI.
  
A: *schappatmung* Ich will ja keine Spielverderberin sein, aber da kommt schon das nächste Problem...

C: Was kann denn jetzt noch fehlen?

A: Die Übermittlung von SBOMs ist auch nicht standardisiert. Manche Hersteller stellen diese auf ihrer Website zum Download zur Verfügung, andere als Metadaten des Produkts, andere wiederum stellen sie via e-Mail auf Anfrage zur Verfügung.

C: Das ist doch super aufwendig. Mit Sharepoint ginge das bestimmt einfacher.

A: [Verdreht die Augen] Aktuell fragen wir die SBOMs meistens per e-Mail an und auf demselben Weg erhalten wir diese dann auch. Aber so richtig können wir dabei auch die Integrität und Authentizität der SBOMs nicht überprüfen; wir können also nichtmal automatisiert sicherstellen, dass die aus der richtigen Quelle kommen und auf dem Weg zu uns nicht manipuliert wurden.

C: Dafür gibt es doch bewährte Methoden, wie z.B. Signaturen oder Checksums, die man ja auch an anderer Stelle benutzt.

A: Ok, dann bekommen wir eine signierte SBOM, aber woher wissen wir, dass es sich um eine legitime Signatur handelt und nicht von jemandem, der uns etwas unterschieben möchte?

C: [schleimig] Sie haben wohl wirklich Zero Trust, hm?

A: [seufzt]

C: Nun ja, dann nehmen wir erstmal das, was wir bekommen können. Das ist dann mein Inventar in dem ich nach log4j und anderen Supply Chain Attacken suchen kann.

A: Erstmal haben Sie nur eine Menge einzelner Dokumente, die händisch durchsucht werden müssten. Und vergessen Sie nicht, dass die SBOMs in erster Linie maschinenlesbar sind - oder wollen SIE noch einmal einen Blick reinwerfen? [grinst]

C: Nein, nein, auf keinen Fall!

A: Das bedeutet also, wir brauchen ein Tool, das die SBOMs verwalten kann, um diese durchsuchbar zu machen.

C: Ja, dann haben wir das ja zusammen. Noch ein weiteres Tool einkaufen kriegen wir auch noch hin! Dann wissen wir endlich, welche Schwachstellen die ganzen Produkte besitzen und können die Supply Chain Angriffe beheben. Großartig!

A: Hier sollten wir kurz einige Missverständnisse rund um Supply Chain Angriffe und Vulnerabilities aus dem Weg räumen.

C: Wie das? 

A: Fangen wir mit den Supply Chain Angriffen an: Bei einem Supply Chain Angriff wird ein Opfer über seine Supply Chain angegriffen, anstatt direkt seine Systeme zu penetrieren. Zum Beispiel über einen Softwarelieferanten mit schlechteren Sicherheitsmaßnahmen. Andere Beispiele wären, Schadcode in einem legitimen Code-Repository zu injizieren oder die Entwickler:innen zu täuschen, dass sie schadhafte Abhängigkeiten installieren.

C: War das bei log4j nicht der Fall?

A: Nein, log4j war eine kritische Zero-Day Schwachstelle.

C: Aber Supply Chain Angriffe nehmen doch zu...

A: Ja, das stimmt. Ein sehr bekanntes Beispiel für eine Supply Chain Attacke war, als der Software-Hersteller Solarwinds in 2020 gehackt wurde: dabei haben die Angreifer das Build System kompromittiert und es ihnen so ermöglicht, Schadcode in das entwickelte Produkt einzubauen. Die Kunden haben dann die Software installiert, weil diese von ihrem Lieferanten kam. Dadurch haben sich die Angreifer dann Zugriff auf die Zielsysteme verschafft.

C: Ja, aber das würden wir ja anhand der SBOM verstehen, dass da was drin ist, was nicht da sein sollte.

A: Aber woher erhalten wir die SBOM?

C: Ja... vom Anbieter!

A: ...der von einem Angreifer kompromittiert wurde, welcher dann wahrscheinlich auch die SBOM entsprechend anpasst, um seine Absichten zu verschleiern. ...und selbst wenn es eine Änderung an der SBOM geben sollte, haben wir als Konsumenten kaum Anhaltspunkte, um eine bösartige Änderung der Software von einer regulären Weiterentwicklung zu unterscheiden.

C: Verstanden... also helfen SBOMs gar nicht gegen Supply Chain Attacken?

A: Nein.

C: ...und was ist denn dann mit log4j?

A: Ja, da wären SBOMs schon eher hilfreich, weil es eine Dependency mit einer kritischen Schwachstelle war.

C: Das war ein Alptraum herauszufinden wo das im Einsatz war! Aber mit den SBOMs hätten wir ja jetzt die Schwachstellen alle in der SBOM gelistet.

A: Mooooooment, machen wir einen kurzen Schritt zurück. Durch dieses Inventar bekommt ein Entwicklungsteam in erster Linie einen Überblick über die Abhängigkeiten ihrer Software. Durch die Informationen wie Hersteller, Name und Version der Komponenten werden diese zunächst einmal eindeutig identifiziert.

C: Und woher kriegen wir dann die Schwachstellen zu diesen Abhängigkeiten?

A: Indem wir öffentliche Schwachstellen-Datenbanken nach Informationen dazu durchsuchen.

C: Öffentliche Schwachstellen-Datenbanken? Kann man sich da einfach anschauen, in welcher Software Sicherheitslücken enthalten sind?

A: Ja, genau. In diesen Datenbanken werden alle möglichen Sicherheitslücken dokumentiert, die von Unternehmen und Sicherheitsforscher:innen veröffentlicht werden. Die größte Datenbank an Schwachstellen wird nebenbei vom US-amerikanischen MITRE betrieben. Das Programm ist ein Eckpfeiler der globalen Sicherheit, da es weltweit von Unternehmen genutzt wird, um Schwachstellen zu veröffentlichen und von Security-Tool-Herstellern, um ihre Services damit zu füttern.

C: Welch ein Glück, dass wir uns in Punkto Sicherheit mal wieder auf die USA verlassen können!

A: Genau da liegt das nächste Problem: Durch die monetäre Abhängigkeit von der US-amerikanischen Regierung können sich politische Entscheidungen, z.B. von freidrehenden Präsidenten, recht schnell auf die Verfügbarkeit solcher zentralen Services auswirken.

C: Oh, ja, das könnte problematisch sein... Vielleicht sollten wir auch an dieser Stelle in Europa ein bisschen suveräner werden und unsere eigene Datenbank bauen.

A: Ja, die ENISA arbeitet bereits daran und hat gerade die Beta-Version ihrer Platform im Einsatz. Damit bewegen wir uns weg von der aktuellen "single source of truth", welche die Datenbank von MITRE war, hin zu mehreren Datenbanken und das Ganze wird fragmentiert.

C: Na gut, dann haben wir halt mehrere Quellen die mir sagen wo ich angreifbar bin. Doppelt gemoppelt hält ja besser!

A: Naja, wir haben dann eine sehr lange, eventuell inkonsistente Liste an Schwachstellen. Aber nur weil eine verwendete Bibliothek eine Schwachstelle enthält, bedeutet es nicht zwangsläufig, dass diese ausgenutzt werden kann.

C: Wie geht das denn?

A: Wenn die Entwickler:innen den verwundbaren Teil nicht benutzen der von der Schwachstelle betroffen ist, dann haben Angreifende häufig auch nicht die Möglichkeit, diese zu missbrauchen. Das ist das Konzept der sogenannten "Exploitability".

C: Aber woher wissen wir denn dann, ob wir angreifbar sind oder nicht?

A: Das müssen wir entsprechend testen und das damit verbundene Risiko bewerten.

C: Das klingt nach ganz schön viel Aufwand... Hah, warum lassen wir das nicht die Anbieter selber testen und die Ergebnisse mit uns teilen?

A: Ja, das gibt es auch schon. Das ist das sogenannte "Vulnerability Exploitability eXchange", kurz "VEX"

C: Lassen Sie mich raten: Wieder ein nur maschinell lesbares Dokument?

A: Ja, damit kann der Anbieter die SBOM erweitern, um die Ausnutzbarkeit von Schwachstellen in den aufgelisteten Komponenten zu klären.

C: Das klingt doch vielversprechend!

A: Naja, nicht wirklich. Die VEX ist ein statisches Dokument, Schwachstellen sind aber leider ein bisschen dynamischer. Der VEX gibt mir nur einen Snapshot zu einem gewissen Zeitpunkt. Wenn neue Schwachstellen entdeckt werden, muss der Hersteller diese neu für jede noch aktiv genutzte Version seiner Software bewerten und neue VEX-Dateien für diese Produkte schicken.

C: Ohje, dann ertrinken wir ja diesen Unterlagen!

A: Nicht nur das: Hersteller haben natürlich einen impliziten Anreiz zu zeigen, dass sie von möglichst wenigen Schwachstellen betroffen sind. Und wir können auch nicht bewerten, ob und wie der Hersteller die Anwendbarkeit getestet hat. 

C: ...weil es auch hier an einheitlichen Ansätzen fehlt?

A: Ja, sowohl bei SBOMs als auch VEX-Dokumente müssen wir darauf vertrauen, dass die Verfasser:innen ordentlich arbeiten und wissen was sie tun...

## Akt 3

// TODO
C: Na jetzt haben sie es aber geschafft mir die SBOMs komplett kaputt zu machen! Das ist ja nur noch sinnloser Aufwand der gar keinen Mehrwert bringt!

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

A: Das kann hilfreich sein um die Awareness der Entwickler:innen zu erhöhen so wenig Abhängigkeiten wie möglich einzubinden. Aber ihnen auch helfen Kriterien zu definieren für Komponenten die nicht in produktive Software eingebaut werden sollten.

C: Komponenten mit zu vielen Schwachstellen zum Beispiel?

A: Das ist ein Parameter der bei der Entscheidung helfen kann, aber nicht nur...wichtig ist auch ob die Library weiterhin maintained wird oder wie häufig diese verwendet wird. Hier gibt es z.B. die openssf scorecard zur Bewertung von open source projekten direkt in den Pipelines.

C: Sollten das Entwickler:innen nicht schon alles kennen?

A: Nicht unbedingt, das Thema gewinnt immer mehr an wichtigkeit und sollte auch so weitergeben werden. Wie sie schon sagten..."Doppelt gemoppelt hält ja besser!"

C: Also sind die Entwickler:innen die Verantwortlichen rund um die SBOMs

A: So weit würde ich nicht gehen, die Entwicklungsteams müssen sicherstellen, dass sie nur die nötigen und "guten" Abhängigkeiten einbauen und diese regelmäßig aktualisieren während der Entwicklung. Ein netter side-effect ist, dass man durch die transitiven Abhängigkeiten einen besseren Einblick in die Lizenzen der open source bibliotheken hat... //wollen wir das Fass aufmachen??

C: Wer soll da noch was tun?

A: Es Bedarf auch einer ordentlichen Governance und Monitoring rund um Produkte die auf dem Markt sind und den ganzen Hersteller SBOMs.

C: Es reicht nicht aus einfach die SBOMs irgendwo liegen zu haben.

A: Nein, die müssen zentral gemonitort werden um neue kritische Schwachstellen zu identifizieren, bewerten und in die Kommunikation mit Entwicklungsteams und Lieferanten zu treten. 

C: *nachdenklich*

A: Wenn man dann die Hausaufgaben gemacht hat, kann man auch anfangen, produktiv mit SBOMs zu Arbeiten. Beispielsweise indem man die Informationen der SBOM sowie die dazugehörigen Vulnerabilities in automatisierte Tests einpflegt um z.B. die Exploitability zu überprüfen und das Produkt zu verbessen.

C: Also sind SBOMs nicht nur Schwachsinn

A: Nein...

C: Großartig! Toll dass Sie da auch meiner Meinung sind!

[C schaut auf's Handy]

C: Oh, entschuldigen Sie bitte, da muss ich rangehen. Arbeiten Sie mir dann bitte mal ein Konzept aus, wie wir die besprochenen Sachen alle im nächsten Quartal umsetzen können. Schaffen Sie das bis nächste Woche?

[C nimmt Handy ans Ohr und läuft von der Bühne]

C: Ja Tachchen Hermann! Du, wir machen jetzt auch SBOMs... ja, richtig, die Supply Chain Attacken sind damit abgewehrt

[A schlägt die Hände vor's Gesicht]

# Q&A [5min]

// Streichkandidaten: Integrität, ENISA, VEX
