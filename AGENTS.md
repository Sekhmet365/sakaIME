# SakaIME

SakaIME is a customized Windows Rime Weasel fork.

## Architecture
- include/WeaselIPCData.h defines UIStyle, comparison and Boost IPC serialization.
- RimeWithWeasel/RimeWithWeasel.cpp loads global style and schema overrides.
- WeaselUI/Layout.cpp applies DPI-scaled margins; concrete layouts size candidates dynamically.
- WeaselUI/WeaselPanel.cpp owns Direct2D rendering, interactions and the 33 ms animation timer.
- UIStyle::EffectiveAnimatedSkin is the shared policy for layout, rendering and animation.

## Current goal
Support style/animated_skin: sakaban, tipsy_couple and default.
Missing global values select Sakaban; missing or invalid schema values preserve inheritance.
Sakaban retains its existing drawings and interactions. tipsy_couple currently uses ordinary
Weasel rendering and margins; PNG loading and artwork are future work.
Animated skins currently apply only to non-fullscreen horizontal candidate layouts.

## Development constraints
- Work incrementally and preserve Sakaban coordinates, appearance, expressions, tracking,
  hover interactions, particles and timing.
- Reuse Direct2D and the existing 33 ms timer; preserve DPI scaling and dynamic layout.
- Skin switches must not cancel click or auto-hide timers.
- Append IPC fields without reordering existing fields. Communicating components must
  be rebuilt and deployed together after this IPC contract change.
- Format modified C++ files with clang-format 18 and check with --dry-run --Werror.
- Run git diff --check and review the complete diff.
- Windows compilation is verified separately through GitHub Actions.
- Do not commit, push, switch branches or modify global Git configuration without approval.
- Leave .vscode/settings.json untouched.
