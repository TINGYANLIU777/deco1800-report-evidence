# Evidence scope and provenance

Collection date: 29 October 2026, Australia/Brisbane.

## Application versions

- Earlier estimator: V13 `app.js`, lines 76–87, from the retained V13 source package.
- Weighted estimator and captured interface: `out-about-brisbane-final-release.zip`, whose SHA-256 is `26DCAF160E35035A316246D08C428E92D5E3557A57219B56987C89A50C90743A`.
- Later repository source inspected: `3064766203-arch/deco1800-jetz`, main at `eab476f393123480baed57cbe402c3fcd042b066`. This application repository was private when inspected. This public evidence page is readable without access to that repository.
- The source excerpts include their original line numbers and file hashes. They are selected technical excerpts, not the complete application.

## Reproduced cases and tests

The two synthetic Zumba cases hold the activity title and structured category constant and vary the description. The earlier estimator was extracted from its source and evaluated on those cases; the weighted estimator was executed from `social-model.js`.

The supplied release's `tests/social-model.test.cjs` and `tests/social-validation.test.cjs` were rerun using Node's test runner. The accompanying log reports 15 tests passing and zero failing. Agreement-statistics tests use synthetic numbers; they are not completed human ratings.

## Screenshot capture

- Application code was unchanged.
- Browser: local Chrome, 1600 × 1050 viewport, Brisbane timezone.
- Test clock: 29 October 2026, 12:00 Brisbane time.
- Snapshot: 14 October 2026, 2,151 listings, sourced from Council Events and Events—Library.
- The local file preview supplied event/weather snapshot fetch responses from the original packaged JSON files. Other fetches received a simulated 503 response and external network requests were blocked.
- Images were cropped at capture time to the social-level meter and expanded explanation. No annotations or visual alterations were added.
- Figure 1: Zumba Gold®, listing start `2026-10-29T01:30:00+00:00`, L3 with fair evidence. Complete records may have conflicting fields, unlike the isolated synthetic regression fixtures.
- Figure 2: Bellbowrie mobile library, provisional L2 with guess/unknown evidence.

## Changes in the later GitHub version

Current-main inspection established that unknown facts are excluded from the internal preference-score denominator (`discovery.js`, lines 111–119), while provisional L2 still participates in the maximum social-level filter. A later commit also removed the match-percentage display. The supplied-release screenshots should therefore be cited as version-specific evidence of the social explanation, not as a comprehensive screenshot of current main.

Historical audit percentages refer to earlier snapshots and are not used here to claim an accuracy improvement. Commit history and implementation tests establish technical changes, not improved real-world participation or social outcomes.
