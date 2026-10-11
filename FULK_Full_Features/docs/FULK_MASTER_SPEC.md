# FULK — Master Project Specification

**Status:** Master reference for implementation. Locked decisions must not be changed without the user's explicit approval.

## Project identity
- App name: **FULK**
- Android application ID: `id.fulk.app`
- Initial development environment: GitHub Codespaces through browser
- Proposed stack: native Android, Kotlin, Jetpack Compose
- Connectivity strategy: most functions and learning materials require internet
- Official logo: `app/src/main/res/drawable-nodpi/fulk_logo_original.jpg`
- Logo must not be redrawn, recolored, distorted, cropped, or redesigned. Preserve original asset; any additional platform-size exports must retain the same artwork.

## Visual design decisions
- Modern, minimalist, warm and welcoming; not overtly religious in the home screen.
- Home screen: blue gradient header with subtle abstract waves; two summary cards side-by-side; six feature cards in a 3-column × 2-row grid; no extra activity-feed section below the grid.
- Official logo stays unchanged and adapts to neither theme nor layout by being recolored.
- Theme options: Follow Android system / Light / Dark. Persist user's selection. All screens, cards, dialogs and navigation should respond to theme. Keep logo blue/white on a background with sufficient contrast.
- FULK Reflect specifically uses a boat/ark visual whose visible portion increases as water recedes; this visual belongs to Reflect, not necessarily the home screen.
- UI mockups are visual references, not evidence that functionality is implemented.

## Qur'anic introductory screen for every feature
Whenever a user opens any feature, first show a Qur'anic basis screen containing the feature name, verified Arabic verse, verified translation, surah/verse reference, a concise explanation of relevance, and a Continue button. Continue opens the actual feature screen. Do not claim modern digital threats are directly discussed by a verse if the relation is contextual. Verify Arabic and translation before release.

### Agreed verse mapping
- **FULK Time:** QS al-'Asr [103]: 1–3 — awareness and use of time.
- **FULK Shield:** QS al-Baqarah [2]: 188 — avoiding wrongful acquisition of wealth; contextual relevance to digital fraud/phishing and online gambling promotions, not a direct reference to modern technology.
- **FULK Check:** QS al-Hujurat [49]: 6 — tabayyun / checking information before acting.
- **Suara FULK:** QS al-Ma'idah [5]: 2 — ta'awun / mutual help in goodness.
- **FULK Reflect:** QS al-Hashr [59]: 18 — reflection on what one prepares for tomorrow.
- **FULK Learn:** QS al-Mu'minun [23]: 27 — conceptual grounding connected to the user's prior Barthes reconstruction of Prophet Nuh's ark story. Do not expand this into a new tafsir claim; explain the digital-literacy connection as contextual analogy.

## Six feature specifications

### 1. FULK Time
- Digital time management based on QS al-'Asr [103]: 1–3.
- User sets application/social-media usage limits, views usage history, and receives reminders before reaching the limit.
- Example locked design: for a 2-hour limit, reminder at minute 110.
- Smart Pause appears as a pop-up over the social-media app being used. Initial implementation is duration-triggered; do not claim pattern-based scrolling detection unless actually implemented.
- If user chooses a 1-minute break, simulate/implement the break and its post-break path.
- If user chooses to continue, route to FULK Learn module **Mengenali Ancaman dan Manipulasi**, with no skip button. After learning and its exercise, continue to the action-selection stage.
- Android overlay, usage access, notification, and background limitations must be handled explicitly with user permission and real-device tests.

### 2. FULK Shield
- Protects users from phishing, online scams, online-gambling promotions, and harmful digital content.
- Ethical basis QS al-Baqarah [2]: 188; contextual connection to protection of wealth (hifz al-mal).
- Warn when a user is asked to provide bank details through an unknown link; explain risk and provide a choice to return or continue after understanding the risk.
- Includes guidance to block one specific site on Redmi/HyperOS. Do not claim the site is blocked until verified on device. DNS limitations must be explained; app cannot promise system-wide blocking without a supported mechanism.
- Coverage includes digital security and warnings for sources/content that appear misleading, but don't present an unverified suspicion as a confirmed fact.

### 3. FULK Check
- Automatic checks should prioritize available verification sources/services rather than pretending an AI chatbot alone proves truth.
- Show sources, what was checked, result/status, and limitations. Clearly handle no result, service unavailable, and uncertain verdicts.
- Based on QS al-Hujurat [49]: 6 (tabayyun).
- Distinguish source-supported verification from model inference; do not invent fact-checking results.

### 4. Suara FULK
- Public participation and transparency reporting feature, distinct from individual FULK Check.
- Users can report problematic information or activity and see report status, verification source, and update time.
- A reported scam link that has been checked can show its verified status to other users.
- Based on QS al-Ma'idah [5]: 2 (ta'awun).
- Reports must not be labelled verified until actual review/source checks have occurred. A backend/service is required for shared reports across users.

### 5. FULK Reflect — version 1.0 LOCKED
- Digital muhasabah based on QS al-Hashr [59]: 18.
- Visual: ark/boat becomes more visible as the water level recedes. Water is symbolic, not a scientific measure of epistemic flooding or a moral judgement.
- After **2 consecutive days without meaningful activity**, water starts rising by **10 percentage points per day**. Maximum water level: **100%**.
- Every activity point reduces water by **5 percentage points**.
- Activity weights: FULK Learn completion = 3; FULK Check claim check completion = 3; Smart Pause / exposure management = 2; FULK Reflect completed reflection = 2; self-reported reduction in social-media use = 1.
- Merely opening FULK does not count as meaningful activity. Activities must be completed; prevent duplicate point farming. Self-reported activity must be labelled as user-reported, not device-verified.
- Daily mission indicator resets each new day, but long-term progress, history and achievements are not deleted due to inactivity.
- Notifications: one main reminder at user-chosen time when no meaningful activity has occurred; at most one optional follow-up. Maximum total: **2 FULK Reflect notifications/day**. User can disable reminders and set quiet times. Notifications themselves do not count as activity.
- Weekly summaries only show data actually recorded; distinguish device-measured, app-recorded, user-reported, and verified outcomes. Do not fabricate time reductions or threats avoided.

### 6. FULK Learn
- Reuse the previously agreed Safina Learn learning concept, with evaluations; do not redesign feature scope without user approval.
- Includes learning materials and assessment, with varied correct answer positions for multiple-choice questions (not always B), and enough questions to make evaluation meaningful rather than only three questions.
- Includes module **Mengenali Ancaman dan Manipulasi**: recognize threats in detail and prepare a response before impact. This is the mandatory Smart Pause continuation path when user chooses to continue media use.
- Educational videos prioritize Indonesian; English with subtitles is acceptable if Indonesian is unavailable. User accepts larger install size for offline video storage, although the overall strategy is mostly online.
- Qur'anic introductory screen uses QS al-Mu'minun [23]: 27 as contextual/conceptual grounding, not as a direct verse about modern digital literacy.

## Cross-feature constraints
- Preserve the agreed six features and their names. Do not add, remove, merge, or redefine features without explicit user approval.
- Build real functionality, not decorative buttons or simulated success. Label unfinished integrations honestly.
- Test persistence across app restarts, errors/offline behavior, permissions, notifications, and device behavior.
- Android platform limitations (cross-app overlays, usage tracking, site blocking, online verification, shared public reports) require appropriate APIs, permissions, services, and tests; never claim they work before verified.
- FULK's Qur'anic framing is contextual and careful; the app does not replace tafsir or assert that verses directly discuss modern technology.
