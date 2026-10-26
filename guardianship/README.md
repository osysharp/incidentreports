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

## Examples

Taken from this package's own tests, which compile and run on every release.

```osy
using Osysharp.Identity;
using Osysharp.UserAccounts;
using Osysharp.Guardianship;
using Osysharp.IncidentReports;

[Test(Training)]
[runas(Wendy)]
void a_players_guardians_acting_or_kept_informed_are_who_is_told() {
  Assert.Equal(["Maya Ortiz", "Tom Ortiz"], ContactsToInform(Sam()).Select(p => p.DisplayName).ToList());
  var sent = InformContacts(Sam(), "He was able to walk to the car.");
  Assert.Equal(2, sent.Count);
  Assert.Equal(0, InformContacts(Sam()).Count);
}
```

From [`tests/told.test.osy`](tests/told.test.osy).

```osy
using Osysharp.Identity;
using Osysharp.UserAccounts;
using Osysharp.Guardianship;
using Osysharp.IncidentReports;

[Test(Training)]
[runas(Maya)]
void a_guardian_reads_what_she_was_told_and_acknowledges_it_and_never_reads_the_report() {
  runas(Wendy) { InformContacts(Sam()); }
  var mine = MyIncidentNotices();
  Assert.Equal(1, mine.Count);
  Assert.Contains("Injury: Sprained right ankle", mine[0].Summary);
  Assert.Equal(0, IncidentReport.Count());
  AcknowledgeIncidentNotice(mine[0], "Thanks — we are seeing the doctor tomorrow.");
  Assert.NotNull(MyIncidentNotices()[0].AcknowledgedAt);
}
```

From [`tests/told.test.osy`](tests/told.test.osy).

## Learn more

- [The Osysharp.IncidentReports.Guardianship reference](https://osysharp.com/reference/ui/incident-reports-kit/)
- [Osysharp.IncidentReports.Guardianship in the package catalogue](https://osysharp.com/packages/#osysharp-incidentreports-guardianship)
- [The Osy# reference](https://osysharp.com/reference/) — the language, the runtime and every kit
- [`llms-full.txt`](https://osysharp.com/llms-full.txt) — the whole reference and specification as one Markdown file, for a coding agent

## Licence

MIT — see [`LICENSE`](LICENSE).
