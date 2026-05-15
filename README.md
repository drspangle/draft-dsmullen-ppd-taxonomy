<!-- regenerate: on (set to off if you edit this file) -->

# Privacy Preference Declaration Taxonomy

This is the working area for the individual Internet-Draft, "Privacy Preference Declaration Taxonomy".

* [Editor's Copy](https://drspangle.github.io/draft-dsmullen-ppd-taxonomy/#go.draft-dsmullen-ppd-taxonomy.html)
* [Datatracker Page](https://datatracker.ietf.org/doc/draft-dsmullen-ppd-taxonomy)
* [Individual Draft](https://datatracker.ietf.org/doc/html/draft-dsmullen-ppd-taxonomy)
* [Compare Editor's Copy to Individual Draft](https://drspangle.github.io/draft-dsmullen-ppd-taxonomy/#go.draft-dsmullen-ppd-taxonomy.diff)

Use this repository for the draft source and local render workflow for this
draft only.

## Workstation Bootstrap

This repository owns its own draft-render setup. Bootstrap it with:

```sh
python3 scripts/setup_draft_workstation.py bootstrap
```

There is intentionally no shared workspace bootstrap. This bootstrap configures
only this repository.

Validation steps for this repository are in [WORKSTATION-VALIDATION.md](WORKSTATION-VALIDATION.md).

## Related Drafts

- architecture draft source: [draft-dsmullen-ppd-architecture](https://github.com/drspangle/draft-dsmullen-ppd-architecture)
- architecture draft Datatracker page: [draft-dsmullen-ppd-architecture](https://datatracker.ietf.org/doc/draft-dsmullen-ppd-architecture)
- protocol draft source: [draft-dsmullen-ppd-protocol](https://github.com/drspangle/draft-dsmullen-ppd-protocol)
- protocol draft Datatracker page: [draft-dsmullen-ppd-protocol](https://datatracker.ietf.org/doc/draft-dsmullen-ppd-protocol/)

## Start Here

1. Bootstrap the local render workflow with `python3 scripts/setup_draft_workstation.py bootstrap`.
2. Validate the local setup with [WORKSTATION-VALIDATION.md](WORKSTATION-VALIDATION.md).
3. Build the draft with `make`.

On Windows, prefer native POSIX tooling when available. Use WSL only as an
explicit fallback:

```powershell
py -3 scripts\setup_draft_workstation.py bootstrap --use-wsl --install-wsl-deps
```

## Contributing

See the
[guidelines for contributions](https://github.com/drspangle/draft-dsmullen-ppd-taxonomy/blob/main/CONTRIBUTING.md).

Contributions can be made by creating pull requests.
The GitHub interface supports creating pull requests using the Edit (✏) button.


## Command Line Usage

Formatted text and HTML versions of the draft can be built using `make`.

```sh
$ make
```

Command line usage requires that you have the necessary software installed.  See
[the instructions](https://github.com/martinthomson/i-d-template/blob/main/doc/SETUP.md).
