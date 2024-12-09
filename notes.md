# Notes

<!-- TOC -->
* [Aanbod](#aanbod)
  * [Class](#class)
  * [Properties](#properties)
    * [beleidsdomein](#beleidsdomein)
    * [beschrijving](#beschrijving)
    * [categorie](#categorie)
    * [doelgroep](#doelgroep)
    * [infrastructuur](#infrastructuur)
    * [intake](#intake)
    * [gerealiseerdDoor](#gerealiseerddoor)
    * [maxAantalDeelnemers](#maxaantaldeelnemers)
    * [medium](#medium)
    * [subcategorie](#subcategorie)
    * [taal](#taal)
* [IndividueelAanbod](#individueelaanbod)
  * [Class](#class-1)
  * [Properties](#properties-1)
* [GroepsAanbod](#groepsaanbod)
  * [Class](#class-2)
  * [Properties](#properties-2)
    * [minAantalDeelnemers](#minaantaldeelnemers)
* [Activiteit](#activiteit)
  * [Class](#class-3)
  * [Properties](#properties-3)
    * [aanbod](#aanbod-1)
    * [aantal aanmeldingen](#aantal-aanmeldingen)
    * [aantal inschrijvingen](#aantal-inschrijvingen)
    * [annulatie reden](#annulatie-reden)
    * [infrastructuur](#infrastructuur-1)
    * [naam](#naam)
    * [status](#status)
    * [subactiviteit](#subactiviteit)
    * [superactiviteit](#superactiviteit)
    * [tijdschema](#tijdschema)
    * [vervangen door](#vervangen-door)
    * [vervangt](#vervangt)
* [Sessie (subclass of Activiteit)](#sessie-subclass-of-activiteit)
  * [Class](#class-4)
  * [Properties](#properties-4)
* [Sessiereeks (subclass of Activiteit)](#sessiereeks-subclass-of-activiteit)
  * [Class](#class-5)
  * [Properties](#properties-5)
* [Doelgroep](#doelgroep-1)
  * [Class](#class-6)
  * [Properties](#properties-6)
    * [kenmerk](#kenmerk)
* [DoelgroepKenmerk](#doelgroepkenmerk)
  * [Class](#class-7)
  * [Properties](#properties-7)
    * [deel van](#deel-van)
    * [kenmerktype](#kenmerktype)
    * [waarde](#waarde)
* [GebruikteVTE](#gebruiktevte)
  * [Class](#class-8)
  * [Properties](#properties-8)
    * [aantal](#aantal)
    * [vteType](#vtetype)
* [Financiering](#financiering)
  * [Class](#class-9)
  * [Properties](#properties-9)
    * [bedrag](#bedrag)
    * [financieringstype](#financieringstype)
    * [gefinancierd door](#gefinancierd-door)
    * [karakter](#karakter)
    * [uitbetalingsmoment start](#uitbetalingsmoment-start)
    * [uitbetalingsmomet einde](#uitbetalingsmomet-einde)
* [Financieringsbron](#financieringsbron)
  * [Class](#class-10)
  * [Properties](#properties-10)
    * [beleidsdomein](#beleidsdomein-1)
    * [financiert](#financiert)
    * [niveau](#niveau)
<!-- TOC -->

## Aanbod

### Class

Considered classes:

- http://purl.org/vocab/cpsv#PublicService
  - Definition: This class represents the service itself. A public service is the capacity to carry out a procedure and 
    exists whether it is used or not. 
    It is a set of deeds and acts performed by or on behalf of a public agency for the benefit of 
    a citizen, a business or another public agency.
  - This can only be used when "Aanbod" is considered public service.
  - The definition does not include non-citizens, while prisons might have non-citizens.
  - If we use it, I think that we should subclass it instead of saying that "Aanbod" is of the class PublicService.
- https://schema.org/Service
  - Definition: A service provided by an organization, e.g. delivery service, print services, etc.
  - ❌ The definition refers to the class that it describes.
  - Reusable properties:
    - schema:audience for "Doelgroep"
- https://schema.org/Offer
  - Definition: An offer to transfer some rights to an item or to provide a service — 
    for example, an offer to sell tickets to an event, to rent the DVD of a movie, to stream a TV show over the internet, 
    to repair a motorcycle, or to loan a book.
  - ❌ The definition refers to the class that it describes.
  - There is a relationship between schema:Service and schema:Offer via schema:offerCatalog.
- https://www.wikidata.org/wiki/Q161837
  - Definition: service provided by a government to people living within its jurisdiction
  - Can we consider an "Aanbod" to be provided by the government?

Decision: new class.

### Properties

#### aantalAanmeldingen

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### activiteit

We see Aanbod as a subclass of CIDOC-CRM:Activity so we consider instances of Activiteit as subactivities of Aanbod.

Decision: use https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.subactiviteit

#### beleidsdomein

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### beschrijving
- dcterms:description
  - This one is used for all descriptions in OSLO I've seen so far.

Decision: use dcterms:description

#### beïnvloedDoor

Realisatie is a subclass of prov:Activity, so we use http://www.w3.org/ns/prov#wasInfluencedBy.

Decision: http://www.w3.org/ns/prov#wasInfluencedBy

#### categorie
- http://data.europa.eu/snb/model/elm/category
  - Definition: A category to which this specification belongs. 
    This property can be used instead of dc:type, if the category cannot provided via a controlled vocabulary.
  - ❌ Different scope.
- https://data.vlaanderen.be/ns/statistiek#categorie
  - Definition: De categorie waarvoor de probaliteit bepaald is.
  - ❌ Different scope.
- https://schema.org/category
  - Definition: A category for the item. Greater signs or slashes can be used to informally indicate a category hierarchy.
  - ❌ The definition refers to the class that it describes.
  - schema:Service is in the domain.
  - skos:Concept is in the range because the range is schema:Thing.
- https://www.bbc.co.uk/ontologies/creativework/category
  - ❌ 404
- http://www.agls.gov.au/agls/terms/category
  - ❌ 404

Decision: new property.

#### doelgroep

- https://schema.org/audience
  - Definition: An intended audience, i.e. a group for whom something was created.
  - Domain incl. Event and Service.
- https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.doelgroep
  - ❌ Domain: http://www.cidoc-crm.org/cidoc-crm/E7_Activity

Decision: schema:audience

#### gerealiseerdDoor
- http://cidoc-crm.org/cidoc-crm/P14_carried_out_by
  - Definition: This property describes the active participation of an instance of E39 Actor in an instance of E7 Activity.
  - Domain: Activity
  - Range: Actor
  - From OSLO Cultuurparticipatie.
- https://schema.org/provider
  - Definition: The service provider, service operator, or service performer; the goods producer.
    Another party (a seller) may offer those services or goods on behalf of the provider.
    A provider may also serve as the seller. Supersedes carrier.
  - ❌ The definition is too vague.
  - Domain: Service
  - Makes sense if we use schema:Service as class for "Aanbod".

Decision: http://cidoc-crm.org/cidoc-crm/P14_carried_out_by

#### infrastructuur

- https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.infrastructuur
  - ❌ "Aanbod" is not in the domain, only "Activiteit".
- https://schema.org/location
  - Definition: The location of, for example, where an event is happening, where an organization is located, or where an action takes place.
  - ❌ Domain: Action, Event, Organisation, InteractionCounter.
- https://www.w3.org/ns/prov#atLocation
  - Definition: A location can be an identifiable geographic place (ISO 19112), 
    but it can also be a non-geographic place such as a directory, row, or column. 
    As such, there are numerous ways in which location can be expressed, 
    such as by a coordinate, address, landmark, and so forth.
  - Domain: prov:Activity or prov:Agent or prov:Entity or prov:InstantaneousEvent
    - ❓ Is the domain ok here?
  - Range: prov:Location
    - ❓ Is the range ok here?

Decision: prov:atLocation

#### intake
- Nothing in schema.org 
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### maxAantalDeelnemers
- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### medium
- https://schema.org/eventAttendanceMode
  - Definition: The eventAttendanceMode of an event indicates whether it occurs online, offline, or a mix.
  - ❌ Domain is only schema:Event and not schema:Service.
- Nothing in LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### minAantalDeelnemers

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### naam

Decision: http://purl.org/dc/terms/title because it's used a lot in other OSLO APs.

#### participatiegraad

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### taal
- https://schema.org/inLanguage
  - Definition: The language of the content or performance or used in an action.
  - ❌ Domain: Event, but not Service.
  - From OSLO Cultuurparticipatie
- http://purl.org/dc/terms/language
  - Definition: A language of the resource.

Decision: dcterms:language

## IndividueelAanbod

### Class
No existing classes found.

Decision: create new class.

### Properties

Doesn't have own properties.

## Groepsaanbod

### Class
No existing classes found.

Decision: create new class.

### Properties

Doesn't have own properties.

## Activiteit

### Class

Note that we can subclass from multiple classes.

Considered classes:

- https://www.w3.org/ns/prov#Activity
  - Definition: An activity is something that occurs over a period of time and acts upon or with entities; 
    it may include consuming, processing, transforming, modifying, relocating, using, or generating entities.
  - This class is more for when an activity generates a result: she becomes a doctor (result) after graduation (activity).
- https://schema.org/Event
  - Definition: An event happening at a certain time and location, such as a concert, lecture, or festival. 
    Ticketing information may be added via the offers property. 
    Repeated events may be structured as separate Event objects.
  - ❌ Definitions refers to the term itself.
  - ❌ "Event" is not the same as Activity. Activity is done with a specific purpose (which is what we need in our context).
  - Reusable properties:
    - schema:subEvent
    - schema:superEvent
    - schema:eventSchedule
    - schema:eventStatus
    - schema:inLanguage
    - schema:previousStartDate for an event that is rescheduled. The problem is that it's just a date and not dateTime.
- http://www.w3.org/ns/sosa/Actuation
  - Definition: An Actuation carries out an (Actuation) Procedure to change the state of the world using an Actuator.
  - ❌ Actuator is a device, so I think that it doesn't work for organisations and people.
- http://www.cidoc-crm.org/cidoc-crm/E7_Activity
  - Definition: This class comprises actions intentionally carried out by instances of E39 Actor that result in changes of state in the cultural, social, or physical systems documented.
    This notion includes complex, composite, and long-lasting actions such as the building of a settlement or a war, as well as simple, short-lived actions such as the opening of a door.
  - This class is a subclass of [E5 Event](https://cidoc-crm.org/html/cidoc_crm_v7.1.3.html#E5).
  - The definition reads like it aligns with the definition of prov:Activity.

Decision: http://www.cidoc-crm.org/cidoc-crm/E7_Activity aligns best with Activity in our case.

### Properties

#### aanbod

This is the inverse of Aanbod.activiteit.

Decision: use https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.superactiviteit

#### aantalDeelnames

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### aantal inschrijvingen

- Nothing in schema.org
- Nothing via LOV

Decision: new property.

#### beschrijving
- dcterms:description
  - This one is used for all descriptions in OSLO I've seen so far.

Decision: use dcterms:description

#### infrastructuur

- https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.infrastructuur
  - Definition: Informatie rond de infrastructuur waarrond of waarin de Activiteit doorgaat.
  - Domain: http://www.cidoc-crm.org/cidoc-crm/E7_Activity
- https://schema.org/location
  - Definition: The location of, for example, where an event is happening, where an organization is located, or where an action takes place.
  - Domain: Action, Event, Organisation, InteractionCounter.
  - Range: Place, PostalAddress, Text, VirtualLocation
- https://www.w3.org/ns/prov#atLocation
  - Definition: A location can be an identifiable geographic place (ISO 19112),
    but it can also be a non-geographic place such as a directory, row, or column.
    As such, there are numerous ways in which location can be expressed,
    such as by a coordinate, address, landmark, and so forth.
  - Domain: prov:Activity or prov:Agent or prov:Entity or prov:InstantaneousEvent
    - ❓ Is the domain ok here?
  - Range: prov:Location
    - ❓ Is the range ok here?
    - Very generic. More generic than schema:location.

Decision: prov:atLocation

#### maxAantalDeelnemers
- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### minAantalDeelnemers
- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### naam

- http://purl.org/dc/terms/title
  - Definition: A name given to the resource.
  - Also used by OSLO Cultuurparticipatie
- https://schema.org/name

Decision: dcterms:title

#### status

![img.png](search-results-status.png)

- The search results above show that a custom property is sometimes created/used in other APs, next to adms:status.
- http://www.w3.org/ns/adms#status
  - Definition: Links to the status of the Asset or Asset Distribution in the context of a particular workflow process.

Decision: adms:status because of the definition and because it's also used in other APs.

#### subactiviteit

- https://schema.org/subEvent
  - Definition: An Event that is part of this event. 
    For example, a conference event includes many presentations, each of which is a subEvent of the conference.
  - ❌ We don't use schema:Event because of its definition. See above.
- https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.subactiviteit

Decision: use https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.subactiviteit.

#### superactiviteit

- https://schema.org/superEvent
  - Definition: An event that this event is a part of. 
    For example, a collection of individual music performances might each have a music festival as their superEvent.
  - ❌ We don't use schema:Event because of its definition. See above.
- https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.superactiviteit

Decision: use https://data.vlaanderen.be/ns/cultuurparticipatie#Activiteit.superactiviteit.

#### tijdschema

- https://schema.org/eventSchedule
  - This is the object https://data.vlaanderen.be/doc/applicatieprofiel/generiek-basis/#Tijdschema 
    which is schema:Schedule
  
Decision: schema:eventSchedule

#### vervangenDoor

- http://purl.org/dc/terms/isReplacedBy
  - Definition: A related resource that supplants, displaces, or supersedes the described resource.
  - No domain or range.
  - Inverse of dcterms:replaces.

Decision: Definition fits and dcterms is stable.

#### vervangt

- http://purl.org/dc/terms/replaces
  - Definition: A related resource that is supplanted, displaced, or superseded by the described resource.
  - No domain or range.
  - Inverse of dcterms:isReplacedBy

Decision: Definition fits and dcterms is stable.

## Binnenruimte

We reuse it completely from OSLO Cultuurparticipatie.

## DetentiehuisVestiging

This is distinct from a GevangenisVestiging.
Therefore, we create a separate class.

## Doelgroep

### Class

Considered classes:

- https://schema.org/Audience
  - Definition: Intended audience for an item, i.e. the group for whom the item was created.
  - The problem is that the properties of this group are stored as text.
  - We can work around this problem by adding our own properties and ignoring the existing property.
  - This class doesn't work if "Doelgroep" can also be used to limit who participates in an "Aanbod".
  - It directly connects with schema:Serivce.
- http://data.europa.eu/snb/model/elm/targetGroup
  - Definition: A specific target group or category for which this specification is designed.
  - ❌ Different scope.
- https://data.vlaanderen.be/ns/mobiliteit/#doelgroep
  - Definition: Groep of categorie die belang hebben bij de mobiliteitsmaatregel.
  - ❌ Different scope.

Decision: schema:Audience

### Properties

#### kenmerk

- Nothing in schema.org
- Nothing via LOV
- http://purl.org/dc/terms/hasPart
  - A related resource that is included either physically or logically in the described resource.
  - This property is an inverse property of dcterms:isPartOf.
  - ❌ Too generic.

Decision: create own property.

## Faciliteit

We reuse this completely from OSLO Cultuur en Jeugd.

## Financiering

### Class

Considered classes:

- https://schema.org/Grant
  - Definition: A grant, typically financial or otherwise quantifiable, of resources.
    Typically a funder sponsors some MonetaryAmount to an Organization or Person,
    sometimes not necessarily via a dedicated or long-lived Project, resulting in one or more outputs, or fundedItems.
    For financial sponsorship, indicate the funder of a MonetaryGrant.
    For non-financial support, indicate sponsor of Grants of resources (e.g. office space).
  - Reusable properties:
    - schema:funder
    - schema:sponsor
    - schema:fundedItem --> Organisation, Person, Product, and so on.
  - If we use schema:Event and schema:Service then schema:Grant makes more sense.
- https://schema.org/MonetaryGrant
  - Definition: A monetary grant.
  - Subclass of schema:Grant.
- http://purl.org/cerif/frapo/Funding
  - Definition: An amount of money available to finance some project or activity.
  - FRAPO ontology: "It can also be used to describe other types of projects, for example building projects and educational projects."
  - Reusable properties:
    - http://purl.org/cerif/frapo/supports
      - Definition: An object property linking an agent to something that the agent supports by financial or other means.
    - http://purl.org/cerif/frapo/funds (subproperty of frapo:supports)
      - Definition: An object property that links a grant to something that it funds (i.e. that it finances or pays for), or that links an agent providing funding to something that it funds.
- http://vivoweb.org/ontology/core#Grant
  - Doesn't look maintained.
- https://eurocris.org/ontologies/cerif/1.3#Funding
  - ❌ Page not found.
- https://rains-uoa.github.io/RAInS-Ontology/v2.0/index-en.html#Funding
  - Definition: A sao:InformationElement which records a specific piece of information detailing a funding source.
  - The ontology has a different scope: The RAInS ontology is an ex-tension of the System Accountability Ontology (SAO)
    for the AI systems' domain by defining a set of concepts required to document the design and
    implementation stage of such systems.
- http://www.w3.org/ns/prov#Activity
  - Financing can be seen as an activity.
  - ❗️Implicitly via property prov:startedAtTime

Decision: schema:MonetaryGrant (and prov:Activity)

### Properties

#### bedrag

- http://qudt.org/schema/qudt/hasQuantity
  - Too generic?
- https://schema.org/amount
  - Definition: The amount of money.
  - Domain: MonetaryGrant
  - Range: MonetaryAmount, Number
    - ❌ So qudt:Quantity is not in range.
- http://data.europa.eu/snb/model/elm/amount
  - Definition: The full (sticker) price of the learning opportunity.
    - ❌ Limited to learning opportunity.

Decision: qudt:hasQuantity

#### financieringstype

- http://purl.org/dc/terms/type
  - This is used in other APs as well to denote a type.

Decision: dcterms:type

#### financiert

- https://schema.org/fundedItem

Decision: schema:fundedItem

#### gefinancierdDoor

- https://schema.org/funder
  - Definition: A person or organization that supports (sponsors) something through some kind of financial contribution.
  - Domain: MonetaryGrant
  - Range: Organization, Person
- https://purl.org/cerif/frapo/isFundedBy
  - Definition: An object property linking something to the funding that funds it (i.e. that finances or pays for it),
    or to the funding agency providing that funding.
  - No domain or range.

Decision: schema:funder because we use schema:MonetaryGrant.

#### karakter

- Nothing in schema.org
- Nothing via LOV

Decision: new property.

#### uitbetalingEinde

- http://www.w3.org/ns/prov#endedAtTime
  - Definition: End is when an activity is deemed to have been ended by an entity, known as trigger

Decision: prov:endedAtTime

#### uitbetalingStart

- http://www.w3.org/ns/prov#startedAtTime
  - Definition: Start is when an activity is deemed to have been started by an entity, known as trigger.

Decision: prov:startedAtTime

## Financieringsbron

### Class

Considered classes:

- http://purl.org/dc/terms/Agent
  - The properties we want to add can be relevant for other organisations as well regardless of the fact that
    they are involved in funding.

Decision: dcterms:Agent

### Properties

#### beleidsdomein

See Aanbod > beleidsdomein

Decision: new property.

#### beleidsniveau

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### financiert

- http://purl.org/cerif/frapo/funds
  - Definition: An object property that links a grant to something that it funds (i.e. that it finances or pays for),
    or that links an agent providing funding to something that it funds.
  - No domain or range.
- Nothing in schema.org
  - schema:funder doesn't have an inverse property.

Decision: frapo:funds

## GevangenisVestiging

We needed a custom subclass of Vestiging for a prison.

## Groepsaanbod

This subclass only exists to show that an Aanbod is offered to a group of prisoners.

## IndividueelAanbod

This subclass only exists to show that an Aabod is offered to one prisoner.

## Infrastructuur

We reuse it from OSLO Jeugd en Cultuur.
We add one property.

### Properties

#### effectievePopulatie

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

## Kenmerk

### Class

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new class.

### Properties

#### type

Decision: use dcterms:type. This is used in other OSLO APs as well.

#### waarde

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new class.

## Organisatie

Decision: we reuse it from 
[OSLO Organisatie Basis](https://data.vlaanderen.be/doc/applicatieprofiel/organisatie-basis/#Organisatie) 
but only keep the link with Vestiging.

## Organisator

Decision: we reuse it from OSLO Cultuurparticipatie.

## Populatie

### Class

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new class.

### Properties

#### infrastructuur

Decision: use prov:atLocation like we did for the other classes.

#### kenmerk

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

## Realisatie

We see a Realisatie also as a prov:Activity.

### Class

Decision: we reuse the class from OSLO Cultuurparticipatie.

### Properties

#### beïnvloedt

Decision: http://www.w3.org/ns/prov#influenced because a Realisatie is also a prov:Activity.

#### gebruikteVTE

Decision: http://www.w3.org/ns/prov#qualifiedUsage because Realisatie is also a prov:Activity.

#### geplandeVTE

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### gerealiseerdDoor

Decision: http://www.w3.org/ns/prov#wasAssociatedWith because Realisatie is also a prov:Activity.

#### locatie

Decision: http://www.w3.org/ns/prov#atLocation because Realisatie is also a prov:Activity.

#### type

- http://purl.org/dc/terms/type
  - This is used in other APs as well to denote a type.

Decision: dcterms:type

## Realisator

We reuse it from OSLO Cultuurparticipatie.

### Class

Decision: https://data.vlaanderen.be/ns/cultuurparticipatie/#Realisator because we took it from OSLO Cultuurparticipatie.

### Properties

#### beleidsdomein

See Aanbod > beleidsdomein

Decision: new property.

#### gefinancieerdDoor

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### naam

Decision: reuse https://data.vlaanderen.be/ns/cultuurparticipatie#Realisator.naam.

#### realisatie

Decision: http://www.w3.org/ns/prov#wasAssociateFor because Realisatie is a prov:Activity.

#### realiseert

Decision reuse https://data.vlaanderen.be/ns/cultuurparticipatie#Realisator.realiseert.

## Sessie (subclass of Activiteit)

### Class

Considered classes:

- https://schema.org/Event

Decision: model Sessie as new subclass of [Activiteit](#Activiteit).

### Properties

No own properties.

## Sessiereeks (subclass of Activiteit)

### Class

Considered classes:

- https://schema.org/Event

Decision: model Sessiereeks as new subclass of [Activiteit](#Activiteit).

### Properties

No own properties.

## Uitvoerder

Decision: we reuse it from OSLO Cultuurparticipatie.

## Vestiging

Decision: we reuse it from 
[OSLO Organisatie Basis](https://data.vlaanderen.be/doc/applicatieprofiel/organisatie-basis/#Vestiging).

## VTEGebruik

### Class

No existing classes found.

Decision: create new class and make it subclass of prov:Usage.

### Properties

#### aantalPersonen

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### aantalVTEs

- http://data.europa.eu/snb/model/elm/count
  - ❌ Domain: Result Category
- Nothing in schema.org
- Nothing via LOV

Decision: new property.

#### realisatie

Decision: use http://www.w3.org/ns/prov#qualifiedUsingActivity because VTEGebruik is a subclass of prov:Activity.

#### type

- http://purl.org/dc/terms/type
  - This is used in other APs as well to denote a type.

Decision: dcterms:type

## Activiteitsstatus

We want to combine the status of an activity and the reason of that status.
We do this in this complex datatype.
OSLO Cultuurparticipatie only considered the status but not the reason.

### Class

Decision: create new class.

### Properties

#### reden

- Nothing in schema.org
- Nothing via LOV
- Nothing in another OSLO AP/VOC

Decision: new property.

#### type

- http://purl.org/dc/terms/type
  - This is used in other APs as well to denote a type.

Decision: dcterms:type

## EnkeleWaarde

### Class

- Nothing in schema.org
- Nothing via LOV
- We checked https://data.vlaanderen.be/doc/applicatieprofiel/bodem-en-ondergrond/ because there was something relevant
  for Fractiewaarde (see below).
  We didn't find anything though.

Decision: new class.

### Properties

#### kenmerkwaarde

- https://qudt.org/schema/qudt/quantityValue
  - ❌ The range is too restrictive. We want to be able to put any Resource there.

Decision: new property.

#### waarde

- https://qudt.org/schema/qudt/quantityValue
  - ❌ The range is too restrictive. We want to be able to put any Resource there.

Decision: new property.

## Fractiewaarde

### Class
This is based on https://data.vlaanderen.be/ns/bodem-en-ondergrond/#Fractiemetingwaarde.
We didn't reuse this though because this is for a measurement while in our case they don't measure this value.
It's something they know exactly.

Decision: create new class with a broader purpose/definition.

### Properties

#### bovengrens

- https://qudt.org/schema/qudt/upperBound
  - ❌ The range is xsd:anySimpleType.

Decision: new property.

#### ondergrens

- https://qudt.org/schema/qudt/lowerBound
  - There is no range set.
  - ❌ It doesn't make much sense to use this property but not use qudt:upperBound for bovengrens. 
- http://wikiba.se/ontology#quantityUpperBound
  - ❌ The range is limited to a decimal.

Decision: new property.

#### waarde

- https://qudt.org/schema/qudt/quantityValue
  - ❌ The range is too restrictive. We want to be able to put any Resource there.

Decision: new property.

## TaalString

Decision: use http://www.w3.org/1999/02/22-rdf-syntax-ns#langString.

## Tijdschema

Decision: use schema:Schedule because we follow 
[OSLO Cultuurparticipatie](https://data.vlaanderen.be/doc/applicatieprofiel/cultuurparticipatie/#Schema).
