# Notes

## Aanbod

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
  - Reusable properties:
    - schema:audience for "Doelgroep"
- https://schema.org/Offer
  - Definition: An offer to transfer some rights to an item or to provide a service — 
    for example, an offer to sell tickets to an event, to rent the DVD of a movie, to stream a TV show over the internet, 
    to repair a motorcycle, or to loan a book.
- https://www.wikidata.org/wiki/Q161837
  - Definition: service provided by a government to people living within its jurisdiction
  - Can we consider an "Aanbod" to be provided by the government?

Decision: TODO

## IndividueelAanbod

No existing classes found.

Decision: create new class.

## GroepsAanbod

No existing classes found.

Decision: create new class.

## Activiteit

Considered classes:

- https://www.w3.org/ns/prov#Activity
  - Definition: An activity is something that occurs over a period of time and acts upon or with entities; 
    it may include consuming, processing, transforming, modifying, relocating, using, or generating entities.
- https://schema.org/Event
  - Definition: An event happening at a certain time and location, such as a concert, lecture, or festival. 
    Ticketing information may be added via the offers property. 
    Repeated events may be structured as separate Event objects.
  - Reusable properties:
    - schema:subEvent
    - schema:superEvent
    - schema:eventSchedule
    - schema:eventStatus
    - schema:inLanguage
    - schema:previousStartDate for an event that is rescheduled. The problem is that it's just a date and not dateTime.
- http://www.w3.org/ns/sosa/Actuation
  - Definition: An Actuation carries out an (Actuation) Procedure to change the state of the world using an Actuator.
- http://www.cidoc-crm.org/cidoc-crm/E7_Activity
  - Definition: This class comprises actions intentionally carried out by instances of E39 Actor that result in changes of state in the cultural, social, or physical systems documented.
    This notion includes complex, composite, and long-lasting actions such as the building of a settlement or a war, as well as simple, short-lived actions such as the opening of a door.
  - This class is a subclass of [E5 Event](https://cidoc-crm.org/html/cidoc_crm_v7.1.3.html#E5).

## Sessie (subclass of Activiteit)

Considered classes:

- https://schema.org/Event

## Sessiereeks (subclass of Activiteit)

Considered classes:

- https://schema.org/Event

## Doelgroep

Considered classes:

- https://schema.org/Audience
  - Definition: Intended audience for an item, i.e. the group for whom the item was created.
  - The problem is that the properties of this group are stored as text.
- http://data.europa.eu/snb/model/elm/targetGroup
  - Definition: A specific target group or category for which this specification is designed.
  - Different scope.
- https://data.vlaanderen.be/ns/mobiliteit/#doelgroep
  - Definition: Groep of categorie die belang hebben bij de mobiliteitsmaatregel.
  - Different scope.

Decision: create new class.

## DoelgroepKenmerk

No existing classes found.

Decision: create new class.

## GebruikteVTE

No existing classes found.

Decision: create new class.

## Financiering

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

## Financieringsbron

Considered classes:

- http://purl.org/dc/terms/Agent
  - The properties we want to add can be relevant for other organisations as well regardless of the fact that
    they are involved in funding.
