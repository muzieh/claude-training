# Content: Bilingual EN/PL

### Polish-primary, hand-authored content
Polish is the primary language; English is preserved so material can be shared and reviewed. Default language is hard-coded to `"pl"`. Polish content must be authored by hand, not machine-translated — quality in Polish must be on par with English (no MT feel).

### Update `<html lang>` on language toggle
When the language toggle changes, update the `<html lang="...">` attribute to match. This is required for screen readers and for browser spell-check to work correctly in Polish content. Do not skip this on new language-switching code paths.

**Why this matters**: The primary audience is Polish-speaking municipal comms staff. Polish content quality and proper `lang` signaling determine whether the app is usable for them at all.
