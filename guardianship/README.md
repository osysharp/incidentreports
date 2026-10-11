# Osysharp.IncidentReports.Guardianship

The people who look after somebody are the ones told when they are named in an incident. In an app using
[Osysharp.IncidentReports](https://github.com/osysharp) and [Osysharp.Guardianship](https://github.com/osysharp), a
child's guardians — acting for them or kept informed, not one whose link has ended — are offered on the review desk
("Tell Maya Ortiz"), told in one call (`InformContacts`), read what they were told and acknowledge it.

## Use it

Nothing to write. It arrives by itself when an app uses both kits (`osy lock` includes it and says so); to keep it out,
`without Osysharp.IncidentReports.Guardianship;` in `app.osy`. The guardians are read as the reviewer, so let whoever
reviews incidents see who looks after whom:

```osy
policy SeesFamilies => IsOffice || ReviewsIncidents;
```

An answer of the app's own (`IIncidentContacts` — next of kin, a carer) can stand beside it: everybody either names is
offered.

## Source

[github.com/osysharp/incidentreports/guardianship](https://github.com/osysharp/incidentreports/tree/main/guardianship); its tests are a youth
football club's.
