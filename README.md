# VoxGarden for LemmingsStudio

This independent repository develops the LemmingsStudio-bound VoxGarden edition.
The existing [KiwiSingh/VoxGarden](https://github.com/KiwiSingh/VoxGarden) repository
and its local modifications are not changed by this work.

## Source baseline and current status

The clean source snapshot is pinned to upstream commit
`8ab73f3a123a92655f5d340183a91f9a01848152`. It excludes upstream's uncommitted
Windows experiments. The source pin is complete; application-private device
integration, Windows build validation and neural portability are not complete.
See `LEMMINGS_INTEGRATION.json` for provenance.

`UPSTREAM_README.md` records the original product and its behavior. Its external
DAW installation instructions are historical upstream documentation, not the
installation contract of this integrated edition. The inherited build files also
still describe upstream wrappers; they must not be used as integrated release
packaging.

## Integrated product contract

- Runs inside LemmingsStudio. No external DAW or standalone installer is delivered.
- Reuses VoxGarden's native processing, original editor, parameter identifiers,
  factory sounds, score/lyrics tools and appearance. Do not replace these with
  a simplified Python effect.
- Build an application-private device target, connect it through the native
  device-worker boundary, and report actual latency to LemmingsStudio.
- Preserve per-instance processor, score, lyrics and appearance state within
  `.lemmingsproject`. Share model storage, never musical instance state.
- Transfer project context through explicit actions. Return mix/stems to the
  originating position; cancellation retains source audio and score.
- Validate Windows DSP before neural workflows. Apple-only inference needs a
  tested Windows runtime and model/voice rights verification, not a silent no-op.
- Test independent instances, original presets, host recall, latency, aligned
  rendering, cancellation, missing models, offline DSP and worker recovery.

The host's implementation gates are maintained in
[LemmingsStudio's parity record](https://github.com/KiwiSingh/LemmingsStudio/blob/rewrite/python-windows/Docs/Parity/IMPLEMENTATION.md).

## Licensing

The upstream GNU AGPLv3 license, dependency licenses and attribution remain in
place. LemmingsStudio-bound describes this edition's packaging and integration;
it does not remove any rights or obligations under those licenses. Sound/model
redistribution rights require their own review.
