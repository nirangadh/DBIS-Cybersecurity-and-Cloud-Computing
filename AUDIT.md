# DBIS-11 course site audit, 22 November 2026

Lecturer-facing record. Not published on the site (excluded in `_config.yml`).

## 1. Scope and method

The audit covered everything a student can reach from the hub: the five hub pages (home, About, Coursework, Practice, Glossary), the 14 session notes, the 51 games, and the 14 slide decks. It asked three questions in order. Is each statement correct? Does each idea build on the one before it without contradicting it later? Does the site work well for a first-year ESL student on a phone?

Method, from principle to specifics:

1. **Accuracy.** Every note was read in full. Every game's question bank was extracted and read item by item against the notes. Time-sensitive facts were checked against primary sources on 22 November 2026 (Section 6). Numbers that a game computes (password times, risk scores, the buy-or-rent totals, the SHA-256 fingerprints) were recomputed independently.
2. **Build-up and coherence.** Each defined term was traced from its first appearance through every later use (notes, games, glossary, decks, practice questions) to find places where a later day contradicts an earlier definition, or where an earlier definition is too narrow for later use.
3. **UX and accessibility.** Every hub page and game was loaded in headless Chrome at a 360 px phone width, before and after pressing Start, and checked for script errors, horizontal overflow, small tap targets, reduced-motion support, and WCAG 2.1 AA issues with axe-core. The timed games and the two reordered games were then played through automatically.

## 2. Overall verdict

The build is in good health. No game threw a script error, nothing overflowed on a phone, every game honours reduced-motion, and the legal and numeric content is accurate. The design of the build-up (CIA growing into extended CIA, the risk words growing into risk analysis, one deciding question per look-alike pair) is consistent across notes, games, decks and the glossary, which is the hardest thing to get right in a course of this size.

The findings are therefore mostly about **three places where an early definition is narrower than its later use**, a handful of small factual slips inside games, and a set of phone-first UX improvements for ESL learners. All were fixed on `dev` except where Section 5 says otherwise.

## 3. Findings and fixes, by theme

Severity: **High** means a student could learn something wrong or contradictory. **Medium** means confusing or inconsistent. **Low** means polish.

### 3.1 Coherence of the build-up

**F1. "Attacker" was defined as someone who *tries* to harm, but the careless insider is taught as an attacker. High.**
Session 11.2 defines an attacker as "a person or group who tries to harm our information", yet the attacker table, A1.4 Attacker Profiler ("Who is the attacker?" with Careless insider as an answer), the A1.9 ladder and Practice Set 2 ("Who is the attacker here?" for Kasun's mistake) all treat a careless insider as an attacker. The Check yourself answer in 11.2 sidestepped the question. The students' confusion is predictable: the definition says intent, the games reward no intent.
*Fix (your choice):* widened to "a person or group who harms our information, on purpose or by mistake" in the notes, Words to know, glossary, A1.9 ladder and deck 11.2 (slides 6 and 28). The Check yourself answer now says "Yes, a careless insider".

**F2. "Control" was defined on Day 3 as reducing a vulnerability, then used on Day 6 for detect and fix controls that do not. High.**
An alarm, a log or a backup restore does not reduce a vulnerability; it reduces the risk by noticing harm or repairing it. Day 6 teaches prevent, detect and fix without saying the word has grown, so the Day 3 definition silently contradicts the Day 6 lesson. This is exactly the kind of build-up the module already does well for CIA, so the fix follows the same pattern.
*Fix:* a "The word grows" callout in 11.11 before Prevent, detect or fix ("a control is anything that reduces a risk"); a second, Day 6 sense for Control in the glossary (the same treatment Data breach and Ransomware already get); one line on the About page; a speaker note on deck 11.11 slide 20. The Day 3 definition is unchanged, so nothing already taught is contradicted.

**F3. "No key ever travels" in the padlock way. Medium.**
The open padlock *is* the public key, and it does travel. Practice Set 3 already says it correctly ("No secret key has to travel"); the notes, A3.4 and deck 11.6 did not. A sharp student could use this to argue against the padlock model.
*Fix:* "No secret key ever travels" in 11.6 (two places), A3.4 and deck 11.6 slide 11.

**F4. Session 11.5 restated Day 1's risk as "how likely, and how bad". Low.**
That is the Day 6 framing. Day 1 taught "the chance that a threat uses a weakness and causes harm".
*Fix:* 11.5 now restates the Day 1 wording.

**F5. Backups on the same server, taught as a good idea on Day 4 and a bad one on Day 6. Medium.**
A4.4 Stack It made "Backups" one of the five virtual machines TeaLeaf needs on its single real server. Day 6 then teaches that a backup on the same server is lost in the same attack. The game was quietly modelling the mistake.
*Fix:* that virtual machine is now "Stock" (the stock app mentioned elsewhere), and the matching distractor reads "Turn off email and stock in December".

**F6. A3.1 Packet Journey cut the order into addressed packets before DNS had found the address. Medium.**
Step 2 said "each one carries the address of the shop"; the address was only found in Step 3. Step 1's feedback even said "Next we see how the phone finds it".
*Fix:* Steps 2 and 3 swapped (find the address, then cut into packets), with their animations. Played through end to end.

**F7. Security-job labels disagreed between the hub, About and the notes. Low.**
Day 3 was "Protect" on the hub but "Protect, Detect" on About and in 11.5. Day 6 omitted Govern in both places although 11.11 is Identify and Govern.
*Fix:* hub and About now match the notes: Day 3 "Protect and Detect", Day 6 "Identify, Govern, Detect, Respond, Recover".

### 3.2 Factual slips inside games and notes

| # | Where | Problem | Fix | Sev. |
|---|---|---|---|---|
| F8 | A4.2 Pizza-as-a-Service | "email for all 25 staff"; TeaLeaf has about 45 | 45 staff | Low |
| F9 | A5.2 Misconfiguration Hunt | Leaver login "kasun.old (left in March)", but Kasun is the current finance clerk | chaminda.w | Medium |
| F10 | A5.4 Rights Rumble | Fourth chip read "End" while the taught verbs are see, fix, delete, **stop** | "Stop" | Low |
| F11 | A7.4 Answer Builder | Model Apply sentence used a fact the scenario never gives ("no IT officer"), which models the habit of inventing facts | "three branches and one old server" (both in the scenario) | Medium |
| F12 | A2.6 People Words Ladder | Passphrase example "MangoRainBridgeSeven" scores only "Better, but still guessable" in A2.4's own meter | mango-rain-bridge-seven (rates Strong) | Low |
| F13 | A7.3 Revision Arena | "rain-mango-cable-7" offered as the strong passphrase: three words, below the four the notes teach | rain-mango-cable-river | Low |
| F14 | 11.5 notes | Example IP 203.94.12.7 sits in a real allocated range; A3.1 uses the documentation range | 203.0.113.25 in both | Low |
| F15 | Deck 11.4 | Speaker note read "Includes Test 2 is only about today" | "Test 2 is only about today" | Low |

### 3.3 Navigation and rendering

**F16. The note chain was broken between Day 1 and Day 2. Medium.** 11.2 had no Next link and 11.3 no Previous link; every other note links both ways. *Fixed.*

**F17. Model answers in 11.14 may render as raw Markdown. Medium, needs your eye.** The four model answers sit inside `<details>` with Markdown lists and bold. GitHub Pages' kramdown leaves Markdown inside HTML blocks unparsed unless the block carries `markdown="1"`, so students may see literal `- **Point (2 + 2):**`. I could not open the live page from here, so I added `markdown="1"` to those four blocks, which is correct whichever way kramdown is configured. The Check yourself blocks elsewhere hold plain sentences and are unaffected.

**F18. Games did not link back to their notes. Low.** The header said "Session 11.4" as plain text, so a student who opened a game from a slide QR code had no route to the notes except via the hub. *Fix:* the session label in every game header is now a link to that session's notes (two links on the ladders that span two sessions).

### 3.4 UX for ESL learners on phones

**F19. Fourteen card games forced a 20 to 45 second clock. High for this cohort.** The word ladders already offer "Relaxed: no clock" and "Challenge", but the card games (CIA Triage, Risk Word Sorter, Attacker Profiler, Malware Line-up, Extended CIA Triage, Phish or Legit, Pressure Tricks, Door or Diary, Is It Cloud?, Deployment Matchmaker, Whose Job Is It?, Rights Rumble, Prevent Detect or Fix, Revision Arena) did not. For ESL readers, "Time is up" turns a reading-speed problem into a wrong answer, which is the opposite of what a judgement game should measure.
*Fix (your choice):* the same two-mode choice as the ladders, Relaxed by default. Relaxed hides the bar and never times out; Challenge keeps the clock and is the only mode with the speed bonus. Instructions that said "before the bar runs out" were reworded. Ransomware Tabletop keeps its clock because the time pressure is the lesson. Verified in both modes on all 14 games.

**F20. Tap targets were small on the hub and game headers. Medium.** On a 360 px phone the 75 hub links were 22 px tall with 4 px between them, the games' "Course site" link was 20 px, and the ladders' "Hear it" buttons 25 px. *Fix:* hub links get 9 px vertical padding (about 40 px rows), "Course site" is now a 40 px pill, "Hear it" is 36 px. Footer licence links were left as inline text, which WCAG allows.

**F21. Colour contrast near-misses. Low.** White on the slate option chips measured 4.42:1, tan text on cream 4.41:1, and muted grey on stone 4.49:1, all just under the 4.5:1 AA line. *Fix:* within the same palette, chip fills use the darker slate already defined (#566A6C, 5.7:1), `--tanText` is #6E5236 and `--muted` is #4E5349. Two scrollable regions (the About tables and the A2.5 log) were made keyboard-focusable, and one unlabelled SVG in A3.4 was given a label. A re-run of axe-core reports no remaining contrast or ARIA violations; only "heading order" notices remain (moderate, cosmetic).

**F22. Cast drift. Low.** Nimal (accounts) and Ruwan (stores) appear in games but not in the About page's cast. *Fix:* one row added to the cast table.

## 4. What changed, file by file

- Notes: 11-02, 11-03, 11-05, 11-06, 11-11, 11-14.
- Hub: index.html, about.html, glossary.html.
- Games: all 51 received the header link, tap-target and contrast changes; content fixes in A1.7 (contrast), A1.9, A2.5, A2.6, A3.1, A3.4, A4.2, A4.4, A5.2, A5.4, A7.3, A7.4; the Relaxed/Challenge mode in the 14 listed in F19.
- Decks: 11-02, 11-04, 11-06, 11-11 (text edited in place; layout re-rendered and checked for overflow).
- `_config.yml`: excludes this file from the site.

## 5. Considered and deliberately not changed

- **Game numbers do not follow play order** (Day 1 morning runs A1.1, A1.3, A1.2, A1.7, A1.6). Renumbering would break URLs, slide QR codes and references students have already used on Days 1 and 2. The hub already lists games in play order, which is what students follow.
- **The password meter is generous.** It models about 12.9 bits per word plus a little for separators, so four words show "11 years" and five show "hundreds of thousands of years" at 10 billion guesses a second. A stricter model would show days for four Diceware words. The teaching message (length beats tricks; more random words is far stronger) is right and the notes, meter and practice questions agree with each other, so I left the numbers alone. If you want them conservative, the change is one constant in A2.4 plus the 11.4 table.
- **"45 hours delivery" against a 42-hour timetable.** 45 is the programme's SLQF contact-hour figure for 3 credits, and the About page shows the 7-day timetable separately. Left as is.
- **Model answer (d) lists MFA as a second action after a clicked link.** MFA mainly stops stolen passwords rather than malware from a link, but it is a fair accepted answer and the deck already accepts updates and an incident plan as alternatives.
- **"Best 5 of 6 tests count"** on the Coursework page: confirmed by you, kept.

## 6. Facts verified on 22 November 2026

- **PDPA status (11.10).** The notes are correct. The Act is No. 9 of 2022, amended by Act No. 22 of 2025 (certified 30 October 2025). Extraordinary Gazette No. 2498/16 (22 July 2026) brings sections 2 and 3, Part I (processing) and Part III (controllers and processors, including DPOs and breach notification) into operation on 1 January 2027. Part II (data subject rights) and Part VII (penalties) still await a date. The DPA has operated under Part V since July 2023. The DPA's draft breach rules propose notification within 72 hours.
- **Sri Lanka CERT hotline 101 (11.12)** is correct and current.
- **SHA-256 fingerprints in 11.6** recomputed and correct.
- **A4.5 Server or Cloud totals** (LKR 2.76m against 2.88m flat; 3.96m against 3.36m with a threefold December) reproduce exactly from the game's constants and match 11.8.
- **Risk matrix bands** (1 to 4, 5 to 9, 10 to 16, 20 to 25) cover every possible product of two 1 to 5 scores; every score in the notes, register and games sits in the right band.
- **99.9% uptime** allows 8.76 hours a year, so "about 9 hours" is right.

## 7. For you to check

1. After merging `dev`, open notes 11.14 and expand a model answer: it should show a bulleted list with bold labels (F17).
2. Re-download decks 11.2, 11.4, 11.6 and 11.11 if you keep local copies; the changed text is listed in F1, F2, F3 and F15.
3. Days 1 and 2 are already delivered. F1 widens the attacker definition students learned; a one-line mention on Day 3 ("an attacker can harm on purpose or by mistake, like the careless insider") would close the loop for them.
