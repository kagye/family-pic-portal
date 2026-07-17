# Family Pic Portal

A private, invite-only web portal for our family's photo archive. Family members sign in to upload photos, tag the people and places in them, and browse the collection by person, place, or timeline. There is no public access and no self-service signup — accounts are provisioned by the owner.

## Tech stack

- **.NET 10 / Blazor Web App** using Interactive Server render mode — a single server deploy with no WebAssembly payload, which fits a private, always-authenticated app
- **Azure** for hosting, blob storage (photo originals and derivatives), and CI/CD (built out in later milestones)
- **Central Package Management** — all NuGet versions live in `Directory.Packages.props`

## Solution layout

```
FamilyPicPortal.slnx
Directory.Build.props        shared MSBuild settings
Directory.Packages.props     central NuGet package versions
src/
  FamilyPicPortal.Web/       Blazor Web App (UI, pages, components)
  FamilyPicPortal.Core/      domain model and application logic
```

## Getting started

Requires the [.NET 10 SDK](https://dotnet.microsoft.com/download).

```
dotnet build
dotnet run --project src/FamilyPicPortal.Web
```

Then open the URL printed in the console (e.g. `https://localhost:5001`).

## Development notes

- Secrets are never committed — local configuration uses [user secrets](https://learn.microsoft.com/aspnet/core/security/app-secrets) (`dotnet user-secrets`).
- Work is organized as one branch per ticket (e.g. `df-13-upload-page`), reviewed against the ticket's acceptance criteria before merging.

## Roadmap

The build is organized into seven epics, each roughly shippable before the next begins:

1. **Foundation** — solution skeleton, domain model, Azure provisioning, CI/CD, domain + TLS, config
2. **Authentication & accounts** — owner-provisioned login, roles, one-time setup links, sessions
3. **Photo ingest** — upload, blob originals, derivatives, photo records
4. **People, places & tagging** — person/place registries, photo metadata, tagging UI
5. **Browse & discover** — home carousel, indexes, timeline, filters, person pages
6. **Admin** — account management, trash, merges, activity log
7. **Ops** — storage durability, nightly backups, export, restore drills, monitoring
