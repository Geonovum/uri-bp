# URI-strategie assets stedelijk water

Versie: 20200925

## In het kort
<span style="color:gray;font-size:0.8em;">*Beschrijving van de best practice in iets langere bewoordingen*</span>

Een **best practice** voor het identificeren van individuen in linked-data vorm binnen de discipline stedelijk
water.

Gebaseerd op het **Gegevenswoordenboek Stedelijk Water (GWSW)** zie [data.gwsw.nl](https://data.gwsw.nl)

*en*

Gebaseerd op de [NTA 8035](https://www.nen.nl/NEN-Shop/Norm/NTA-80352020-nl.htm), zie hoofdstuk 7.7.1 .
Daarin worden de volgende bronnen aangehaald:
* [CEDR Interlink URI
Strategie](https://www.roadotl.eu/static/media/INTERLINK_D4._Defining_the_Principles_9Okqubw.PDF),
vanaf p. 84
* [Towards a NL URI Strategy](https://www.geonovum.nl/uploads/documents/D1-2013-09-19_Towards_a_NL_URI_Strategy.pdf)
* Best Practices for Publishing Linked Data [[ld-bp]]
* Cool URIs for the Semantic Web [[cooluris]]

Zie ter informatie ook de werkversie [NEN 3610 - Linked Data](https://geonovum.github.io/NEN3610-Linkeddata/#nen3610id)

## Waarom
<span style="color:gray;font-size:0.8em;">*Beschrijft de reden waarom dit goed is om te doen*</span>

Het Gegevenswoordenboek Stedelijk Water (GWSW) wordt breed toegepast voor stedelijk water beheer in Nederland. Het
GWSW is een ontologie, een speciale datastructuur die systemen en processen op het gebied van stedelijk water
beschrijft.
Het is een open datastandaard volgens het linked data principe die door Stichting RIONED namens de sector is ontwikkeld.
Het is onderdeel van het Semantisch Web en is gemodelleerd in RDF/RDFS/OWL-2.

Meer dan 80 gemeenten hebben al datasets opgebouwd conform het GWSW en gepubliceerd op de GWSW Server. Die datasets
bevatten de assets en activiteiten op het gebied van stedelijk water. Die assets bestaan veelal uit putten en
leidingen, ze worden in het algemeen "individuen" genoemd. Het verwijzen naar individuen met URI’s is essentieel binnen
het linked-data principe, zeker nu er meer linked-data platforms verschijnen en de GWSW datasets steeds breder worden
toegepast.

Een URI-strategie voor individuen in de "bebouwde omgeving" zoals beschreven in dit document is daarvoor noodzaak. 

## Beoogd resultaat
<span style="color:gray;font-size:0.8em;">*Beschrijft het beoogde resultaat*</span>

We willen komen tot een uniforme URI-strategie voor linked-data-individuen in de bebouwde omgeving, om te beginnen met
stedelijk water. 
Elk te onderscheiden individu wordt met de URI uniek geïdentificeerd zodat de implementatie en toepassing van linked data over de hele sector voorspelbaarder en gelijkvormiger wordt.

## Implementatie

<span style="color:gray;font-size:0.8em;">*Het "hoe": de implementatierichtingen, voorbeelden, concrete aanwijzingen
  etc. Het was de bedoeling bij de SDW-BP dat het 'waarom' en het 'beoogde resultaat' algemeen genoeg zijn om
  voorlopig overeind te blijven, terwijl wat beschreven staat onder 'mogelijke aanpak' veel concreter is, maar daardoor
  ook veranderlijker kan zijn en misschien ook vaker geactualiseerd moet worden.*</span>

### URI-strategie voor concepten in het GWSW Datamodel versie 2.0
De vigerende versie van het GWSW (versie 1.5.1) wordt al veel in de praktijk gebruikt, de daarbij gehanteerde URI's zijn nog niet genormaliseerd. 
GWSW versie 2.0 is in ontwikkeling, die wordt afgestemd op de NTA 8035 en mogelijk in combinatie met de linked-data versie van IMBOR uitgebracht. 
Zie de documentatie op https://stichtingrioned.github.io/GWSW_2.0 . Vanaf GWSW 2.0 verwijzen we naar GWSW-concepten met:

**https://{domain}/{type}/[version]/{reference}** *(http wordt omgeleid naar https)*

* {domain} is het web-domein: voor de GWSW-Ontologie is dit {locatie}.gwsw.nl. Het subdomein {locatie} voor de ontologie is "data".
* {type} is het soort resource: voor het datamodel (concepten) is dat type "def".
* [version] is de versie van het data-model. De versie is optioneel, als die ontbreekt geldt de vigerende versie van de GWSW ontologie (vanaf "2.0").
* {reference} is de verwijzing naar het specifieke concept. Het hanteren van begrijpbare namen voor concepten is een gangbare RDF praktijk en ook voor het GWSW heel bruikbaar.
We gaan uit van camelCase en CamelCase notatie van de namen voor respectievelijk de properties (starten met lowercase)
en de klassen (starten met uppercase).

Een externe overstortput is een GWSW concept (klasse) en heeft in GWSW versie 2.0 de URI

https://data.gwsw.nl/def/2.0/ExterneOverstortput

De onderdelen van een externe overstortput worden beschreven met de relatie (predicate)

https://data.gwsw.nl/def/hasPart   *(vigerende versie = "2.0")*

<div class="note" title="Domeinnaam versus modelnaam">
  Er zijn ook URI-voorbeelden waarbij de modelnaam als submap is opgenomen, bijvoorbeeld in de vorm van: https://imbor.crow.nl/gwsw/def/2.0/ExterneOverstortput .
  Op de lange termijn is dit een optie, vooralsnog is de domeinnaam data.gwsw.nl voldoende specifiek.
</div>

### URI's van individuen binnen de discipline stedelijk water

De URI is een samenstelling van discipline (domain), soort (type) en bronhouder (source holder) van de gegevens (gemeente, waterschap, provincie).
De algemene opbouw van de URI - bruikbaar voor zowel de bestaande GWSW versies als voor GWSW 2.0 - is:

**https://{domain}/{type}/{source holder}#{reference}** *(http wordt omgeleid naar https)*

* {domain}: Identiek aan het GWSW-model (data.gwsw.nl, zie requirements)
* {type}: Het betreft een individu, dus is het type een identifier "id".
<div class="note" title="Documentatie en metadata">
  Om te verwijzen naar aanvullende documentatie (bijvoorbeeld revisietekeningen) kan het type "doc" worden gebruikt (zie de voorbeelden).
</div>
* {source holder}: De initiator, in de meeste gevallen de bronhouder, die het individu heeft geregistreerd. Voor identificatie van de bronhouder wordt conform de URI-strategie van het Digitaal Stelsel Omgevingswet de CBS-systematiek gehanteerd. Dit is de code van de overheidslaag (01 rijk, 02 uitvoeringsorgaan, 03 provincie, 04 waterschap, 05 gemeenschappelijke
regeling, 06 gemeente) gevolgd door de viercijferige CBS-code van de overheidsinstelling. Voor bijvoorbeeld de gemeente Roosendaal betekent dit de code "061674".
<div class="note" title="Andere bronhouder">
  Eigenaars van de stedelijk water voorzieningen zijn niet altijd in de overheidslaag onder te brengen, denk aan
  terreinriolering. Daarvoor zal een extra code nodig zijn, Stichting RIONED zal de uitgifte daarvan coördineren.
</div>
* {reference}: Als URL-fragment: de, binnen de scoop van de bronhouder, unieke identificatie van het object (bijvoorbeeld een GUID). De reference van het individu wordt als fragment genoteerd, een paragraaf binnen het "bronhouder-document". Een apart document per individu is niet nodig, de individuen worden immmers volledig beschreven in de GWSW-dataset (en zijn daar al gedocumenteerd).

**Wijziging van bronhouder**

De individu-identicatie {source holder}#{reference} blijft ongewijzigd gedurende de levensduur van het object, ongeacht of de eigenaar van het individu wijzigt, bijvoorbeeld bij een gemeentelijke herindeling. De bronhouder kan dus ook gezien worden als initiator, de instantie die het individu in eerste instantie heeft geregistreerd.

<div class="note" title="Waarom bronhouder als deel van de URI">
Er zijn goede argumenten om de individu-identificatie landelijk te faciliteren zodat de bronhouder-aanduiding overbodig wordt. Er zou dan een centraal locatie ingericht moeten worden om de uitgifte van ID's te faciliteren.
Vooralsnog is dat praktisch gezien niet haalbaar. Een lokale uitgifte van identificaties (door de bronhouder) is snel en eenvoudig in te richten, daar is nu behoefte aan.
In de gekozen opzet faciliteert Stichting RIONED alleen de uitgifte van de bronhouder-ID.
</div>

**Levenscyclus individu**

De individu-identificatie kan gedurende de gehele levenscyclus - van fabricage tot verwijderen - van een object worden gebruikt. In de stedelijk water praktijk zal de identificatie vanaf aanleg worden geïntroduceerd. Aanpassingen en onderhoud hebben geen invloed op de individu-identificatie. Bij vervanging wordt echter een nieuw individu met een eigen - nieuwe - identificatie geïntroduceerd. Natuurlijk is hier sprake van een "grijs gebied", een aanpassing van een object kan zodanig zijn dat er sprake is van een nieuwe individu. De keuze is dan aan de bronhouder.

<div class="note" title="Individu-naam versus individu-identificatie">
Voor het gebruik van de individu-naam heeft de bronhouder meer vrijheid, de beheerder kan er bijvoorbeeld voor kiezen om dezelfde objectnaam te blijven gebruiken na vervanging van een individu.
</div>

**Te onderscheiden individuen**
Herkenbare individuen in het datamodel stedelijk water zijn bouwwerken, putten en leidingen, daarvoor ligt een individu-identificatie voor de hand. Maar ook voor bijvoorbeeld apparatuur kan een individu-identificatie nuttig zijn, denk bijvoorbeeld aan een pomp, geïnstalleerd in een gemaal (bouwwerk). Die pomp moet worden onderhouden, wordt mogelijk verplaatst naar een ander object en wordt op enig moment vervangen. Een individu-identificatie is nuttig voor alles wat op zichzelf kan bestaan, geen vast deel uitmaakt van de constructie en een onafhankelijke levenscyclus heeft. 

### Uitgewerkt in enkele voorbeelden (in turtle formaat)

Gemeente Roosendaal met bronhouder-code 061674 bezit (en beheert) stedelijk water voorzieningen. Onderdeel daarvan is een externe overstortput met de naam "P123". 
Deze putnaam is de identificatie voor "menselijk gebruik" en wordt bijvoorbeeld toegepast in rapportages en overzichtstekeningen. 
Daarnaast is elke put binnen de gemeente voor identificatie door computersystemen voorzien van een GUID. 

<div class="example">
  <div class="example-title marker">De URI van het individu in gemeente Roosendaal:</div>
  <code>https://data.gwsw.nl/id/061674#b2ad189a-8c46-49f2-557ba07c49a2</code>
</div>

<div class="example">
  <div class="example-title marker">Prefixes in een dataset</div>
  <code>
    @prefix gwsw: &lt;https://data.gwsw.nl/def/2.0/&gt; .
    <br/>@prefix indiv: &lt;https://data.gwsw.nl/id/061674#&gt; . 
  </code>
</div>

De assets van elke bronhouder (gemeente, waterschap) staan in een aparte dataset (repository, SPARQL-endpoint). De
prefix indiv: is dan bruikbaar voor alle in de dataset opgenomen individuen.

<div class="example">
  <div class="example-title marker">De naam van het individu (putnaam), GWSW 2.0 hanteert skos:prefLabel</div>
  <code>indiv:b2ad189a-8c46-49f2-557ba07c49a2 skos:prefLabel “P123” .</code>
</div>

<div class="example">
  <div class="example-title marker">Een synoniem kan, GWSW 2.0 hanteert skos:altLabel</div>
  <code>indiv:b2ad189a-8c46-49f2-557ba07c49a2 skos:altLabel “bv te gebruiken voor oude code INSP24442”.</code>
</div>

<div class="example">
  <div class="example-title marker">Idem, in een andere taal-context</div>
  <code>indiv:b2ad189a-8c46-49f2-557ba07c49a2 skos:altLabel “gebrauch alter kode INSP24442”@de .</code>
</div>

<div class="example">
  <div class="example-title marker">Typering van het individu</div>
  <code>indiv:b2ad189a-8c46-49f2-557ba07c49a2 rdf:type gwsw:ExterneOverstortput .</code>
</div>

De externe overstortput P123 bevat een debietmeter, dit apparaat heeft een eigen individu-identificatie zodat het effectief beheerd kan worden. De debietmeter heeft een beperkte levensduur en vraagt regelmatig onderhoud.

<div class="example">
  <div class="example-title marker">De externe overstort bevat een debietmeter</div>
  <code>indiv:b2ad189a-8c46-49f2-557ba07c49a2 gwsw:hasPart indiv:c2ad189a-8c46-49f2-557ba07c49a2 
  <br/>[ rdf:type gwsw:Debietmeter; ] .
  </code>
</div>

<div class="example">
  <div class="example-title marker">Metagegevens, documenten over de debietmeter</div>
  Om te verwijzen naar aanvullende documentatie, gebruik de URI:
  <code>https://data.gwsw.nl/doc/061674#c2ad189a-8c46-49f2-557ba07c49a2</code>
</div>

### Terzijde: Alternatieve notaties

  #### BGT-ID
  Zie de [Basisregistratie Grootschalige Topografie](https://docs.geostandaarden.nl/imgeo/catalogus/bgt/). De
  BGT-objectidentificatie (object-ID) hanteert de richtlijnen van NEN3610:2011. Aan elk object wordt een uniek
  identificatienummer toegekend, dat uit twee delen bestaat: een namespace en een identificatiecode. Zolang het
  object bestaat, mag dit ID niet ver­an­deren. Vanwege de samenhang tussen de BGT en IMGeo wordt één notatiewijze voor het
  object-ID voorgeschreven.

  Een BGT-ID bestaat uit de namespace **NL.IMGeo** (Landcode + Sectormodel) gevolgd door een code voor de
  **Bronhouder** (5 posities) en een **UUID** (32 cijfers).
  De notatiewijze voor het put-voorbeeld wordt dan:
  <div class="example">
    <div class="example-title marker">De BGT-ID van de voorbeeld-put</div>
    <code>NL.IMGeo:G1674.b2ad189a-8c46-49f2-557ba07c49a2</code>
  </div>
  Voor de discipline stedelijk water (zeker voor riolering) zijn de BGT-ID's niet over te nemen. Ondergrondse
  leidingen ontbreken in de BGT en van de putten zijn alleen de deksels in de BGT vastgelegd.

  **Een redelijk alternarief?**

  Het BGT-ID is geen URI, het is afgestemd op XML-notaties. Het identificatiedeel kan wel toegepast worden.

  <div class="example">
    <div class="example-title marker">Gebruik de BGT-notatie in de URI</div>
    <code>https://data.gwsw.nl/id/G1674.b2ad189a-8c46-49f2-557ba07c49a2</code>
  </div>
  Of, als HTML-fragment:
  <div class="example">
    <div class="example-title marker">De BGT-notatie als HTML-fragment</div>
    <code>https://data.gwsw.nl/id#G1674.b2ad189a-8c46-49f2-557ba07c49a2</code>
  </div>

  De bronhouder-code is onderdeel van het identificatiedeel, is er geen URI-scheiding (pad/fragment). 
  Volgens de BGT principes blijft deze identificatie voor altijd bij het individu, ook als de bronhouder wijzigt.

<div class="note" title="BGT in Linked Data vorm">
De BGT wordt naar verwachting in het vierde kwartaal van 2020 gepubliceerd als Linked Data, met naar alle waarschijnlijkheid URI's die beginnen met bgt.basisregistraties.overheid.nl.
Die ontwikkeling is in deze opzet nog niet meegenomen maar wordt uiteraard op de voet gevolgd.
</div>

## Testen
<span style="color:gray;font-size:0.8em;">*Beschrijft hoe je kan toetsen of de best practice inderdaad
  geïmplementeerd is in een specifieke omgeving.*</span>
<p>De gekozen URI-strategie is een beproefde notatievorm. 
    Een extra PoC is niet nodig, de eerste praktische toepassing volgt snel na acceptatie van deze "best practice".</p>

## Relevante requirements
<span style="color:gray;font-size:0.8em;">*In het SDW-BP document staan geen use cases en requirements; deze waren al
  in
  een apart document opgenomen [[SDW-UCR]]. Onder dit kopje 'relevante requirements' wordt verwezen naar de voor
  deze
  best practice relevante requirements.*</span>

### Datasets opbouwen conform GWSW-OroX definitie
Zie het document [GWSW-OroX Bestandsopbouw](https://apps.gwsw.nl/doc/GWSW.orox%20Beschrijving.pdf)

### Dataset via website op de GWSW Server publiceren
Zie de website met [GWSW Applicaties](https://apps.gwsw.nl)

### Dataset via GWSW API op de GWSW Server publiceren
Zie de [API Specificatie](https://apps.gwsw.nl/item_redoc)

## Baten
<span style="color:gray;font-size:0.8em;">Het Data on the Web Best Practices [[dwbp]] document bevat een
  [bijlage](https://www.w3.org/TR/dwbp/#BP_Benefits) waarin een aantal baten worden beschreven die kunnen worden
  bereikt door het volgen van de best practices. Onder dit kopje 'baten' wordt dan verwezen naar de specifieke baten die
  worden gerealiseerd door deze specifieke best practice te volgen.*
</span>

De eerste toepassingen die gebruik maken van de GWSW Datasets op landelijk niveau zijn al in ontwikkeling, daarvoor is
een uniforme URI-strategie noodzaak.
De baten vinden we in geavanceerde nieuwe toepassingen die analyses doen met landelijke gegevens van stedelijk water
voorzieningen. Een mooi voorbeeld is het onderzoek naar trends bij voorgekomen rioolinstortingen.
