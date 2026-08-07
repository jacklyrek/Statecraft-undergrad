# Kickoff prompt — Statecraft learning wiki

Paste everything below the line into a fresh Claude Code session running in the new,
empty repo directory. Delete this file afterward.

---

I want you to bootstrap a **self-maintaining, LLM-built study system** for political science and
history, on the same architecture as an existing repo of mine. You are the researcher, author, and
maintainer; I provide direction, spot-check sourcing, and do the practice.

## The lens — this governs everything

One question runs through every unit, every page, and every quiz item:

> **If I wanted to rule a nation — at any point in history — how would I actually do it?**

Not "what do scholars say about the state" but "what is the job, what are its constraints, what
decisions land on the desk, and what happened to the people who chose each way." Every concept
earns its place by answering a ruler's problem. If a page can't say which problem it solves for
someone actually holding power, it doesn't belong.

Three consequences you must build in, not sprinkle on:

**1. The material is organized by the ruler's problems, in the order they bite.** You take power
before you can administer; you pay the army before you build the road system; you survive the
succession before you worry about GDP in fifty years. The spine below follows that sequence, which
is *not* how political science departments sequence things. Keep it.

**2. "At any point in history" is a real constraint, not a flourish.** Most writing on statecraft is
covertly about the modern bureaucratic nation-state. A ruler in 1200 cannot run a census, cannot
move an order faster than a horse, cannot tax income because no one records it, and cannot survive
without personally binding an armed aristocracy. The job changes with what technology and scale
allow. So:
   - **Every unit chapter page and every concept page carries a required `## Across eras` section**
     — how this problem looks in a pre-state chiefdom, an agrarian empire, an early-modern composite
     monarchy, an industrial nation-state, and a contemporary state; what is **invariant** across all
     of them; and what specific technology or condition changed it (writing, coinage, standing
     armies, gunpowder, printing, double-entry records, railroads and telegraph, mass literacy, mass
     media, nuclear weapons, digital surveillance).
   - **Add a page type `wiki/era-<slug>.md`** describing a ruler's operating environment in each
     era: what he can see, what he can move, what he can collect, who can kill him, how fast news
     travels, and what a "government" physically consists of. Units link to these constantly.
   - Flag **anachronism** as a first-class error. Advice that assumes a modern tax apparatus is
     useless to a Ming emperor and vice versa. When a mechanism is era-bound, say so.

**3. The flagship item type is the decision.** See Step 2.4. The system should regularly put me in
the chair: here is your position, your year, your revenue, your coalition, your neighbors — what do
you do, and what happened to rulers who did each thing?

A framing note on honesty: this lens covers coup-proofing, purges, patronage, censorship, and
repression, because rulers used all of them and the scholarship is largely about *why* and *at what
cost*. Treat those analytically — mechanism, historical evidence, and consequences to the ruler and
the ruled — the way Machiavelli, Weber, and the selectorate literature do. Explain how power works;
don't write operational guidance for harming people. The analytical version is also the more useful
one, since the interesting finding is usually that the brutal option was expensive and often fatal.

This is grad-seminar-level self-study, not a survey course. A confidently-wrong page is worse than
no page, and a page that launders one school's interpretation as settled fact is the specific
failure mode I care most about avoiding.

## Step 1 — Read the reference implementation first

There is a working instance of this system at `/Users/jacklyrek/Documents/GitHub/psych-undergrad`.
Read these before writing anything:

- `CLAUDE.md` — the schema: directory layout, the `create chapter X` command, research rules, page
  conventions, item conventions, generate rules, `lint`, bookkeeping files.
- `counseling-syllabus.md` — the shape of a good spine (units → objectives, core concepts, anchor
  resource, why it matters, practice rep). Note how it's ordered by payoff, not by convention, and
  how it keeps one hard idea in view throughout. Mine does the same with the ruler's lens.
- `learning-science-for-self-study.md` — the generation rulebook (retrieval practice, spacing,
  interleaving, Bloom coverage, calibration, pitfalls).
- `items/unit01-*.md` and one `wiki/concept-*.md` — the actual output shape.
- `apps/` and `docs/` — the Streamlit quiz runner, the SM-2 scheduler, and the static PWA.

Everything about the architecture carries over unchanged unless I say otherwise. Do not redesign it.
What follows is only what must differ because the subject and the lens differ.

## Step 2 — The adaptations that matter

Counseling has a DSM, an ethics code, and a body of outcome research. This subject has none of
that. Its central questions — why Rome fell, whether a ruler's choices matter — are live disputes
among competent people. The system has to be built for that, not patched for it.

**1. Contested-by-default, with a page type to carry it.** Add `wiki/debate-<slug>.md`. Any causal
question with serious disagreement gets one instead of a smoothed-over concept page. Required
structure: the question stated precisely; each major position in its **strongest** form with its
leading proponents; the best empirical objection to each; what evidence would discriminate; and an
explicit "settled vs. interpretation" section. Close each debate page with **"what this means for
the person in charge"** — because a ruler has to act under exactly this uncertainty, and that is the
realistic version of the skill. Steelmanning is a hard requirement: if a position's best-known
advocate wouldn't recognize your summary as fair, it's a bug.

**2. A case library as a first-class page type.** Add `wiki/case-<slug>.md`. Cases are the raw
material and the test bed. Deliberately span eras and regions so the lens holds up: Achaemenid
Persia, Rome (republic and late empire), Han and Qing China, the Abbasid caliphate, the Mongol
succession crises, Norman England, Venice, the Ottoman and Habsburg empires, Spain's silver century,
Tokugawa and Meiji Japan, revolutionary and Napoleonic France, Britain's rise and managed decline,
the USSR from Lenin to collapse, Weimar, Argentina's reversal, Singapore, Botswana, Venezuela, the
PRC reform era. Each case page carries: the ruler's actual position and constraints, the decisions
taken, the outcome, the competing explanations that invoke it, and — critically — **what this case
is and isn't good evidence for**. Cases are cited by units, not owned by them.

**3. Source discipline for a field with schools.** Write a second rulebook,
`historical-epistemics.md`, covering: primary/secondary/tertiary sources and when each applies;
source tiers (peer-reviewed work, university presses, and replicable datasets such as V-Dem, Polity,
Correlates of War, Maddison, World Bank over think-tank and popular-press material, which is
orientation-only and must be labeled); how to name a source's school inline rather than feign a view
from nowhere; the difference between a **fact**, an **interpretation**, and a **projection**, which
every page must keep visibly distinct; how to handle popular grand-narrative authors (Diamond,
Harari, Turchin, Ferguson, Acemoglu & Robinson) — usable, often the best-known statement of a
position, each with a substantial professional critique that must appear alongside them; and the
special problem of **premodern sources**, where the surviving record was usually written by the
winners, the literate elite, or a successor dynasty with a motive to indict the last one. Also put
the working methods here rather than saving them for a final unit: comparative method, case
selection and its traps, disciplined counterfactual reasoning, causal inference in observational
settings, and forecasting. These are consulted from Unit 1 onward, not studied once at the end.

**4. Item types built for the chair, not the exam hall.** Keep the reference repo's
`cloze | recall | mcq | compare | explain` and its Bloom levels. Replace `vignette` with `case`, and
add four:
   - **`decision`** — *the flagship.* "You are the ruler of X in year Y. Your revenue is Z, your army
     is loyal to A, your neighbors are B and C, your succession is unsettled. What do you do?" Reveal
     afterward: what the actual ruler did, what rulers in structurally similar positions did, and how
     each turned out. Every unit needs several. These are the items the whole system exists for.
   - **`counterfactual`** — "Remove factor X from case Y. What does each theory predict changes, and
     how much did the outcome actually depend on it?"
   - **`attribution`** — "Here is an event. How would a realist, an institutionalist, and a
     world-systems theorist each explain it? Which does the evidence best support?"
   - **`forecast`** — state a polity's conditions at time T **without the outcome**, ask what a given
     framework predicts, then reveal what happened and why the framework did or didn't catch it.

   Add an **`era` field** to every item where the answer is era-bound, and write explicit
   cross-era transfer items: "This worked for Augustus. Why can't Louis XIV do it, and what is his
   substitute?"

**5. Anti-hindsight rules, the analog of the fluency illusion.** Append a section to the
learning-science doc covering this material's failure modes, and design items against them:
**hindsight bias** (outcomes look inevitable once known — never leak the outcome into a prediction
prompt), **narrative fallacy** (a good story is not evidence), **survivorship and selection on the
dependent variable** (studying only collapsed empires — or only famous successful rulers — tells you
nothing about what distinguished them from those who faced the same conditions and fared
differently), **great-man attribution**, **presentism**, and **anachronism** per the lens above.
Include items that ask me for the *strongest objection* to a position I just gave, and items that ask
*what evidence would change my mind*.

**6. Clusters are the interleaving unit.** Confusable theories (realism vs. liberalism vs.
constructivism; institutions vs. geography vs. culture as growth explanations), confusable
institutional designs (presidential vs. parliamentary vs. semi-presidential; PR vs. FPTP; tax
farming vs. salaried collection), confusable regime types (competitive authoritarian vs. electoral
democracy vs. closed autocracy), confusable rulers' dilemmas across eras, and confusable comparable
collapses (Rome vs. Qing vs. Ottoman vs. USSR). Compare-and-contrast items across these are
mandatory.

**7. The stance shift.** The counseling repo names one hard unlearning and keeps it in view.
Mine is this: **structure constrains far more than a ruler's choices do — and yet some decisions
genuinely swing outcomes.** Cheap analysis collapses to one pole: everything was inevitable, or
everything was the ruler's doing. The whole point of the lens is to live in the middle and learn to
tell which case is which and on what evidence. The ruler's-eye view makes this trap *worse*, not
better, because it flatters the reader's sense of agency — so generate items that repeatedly test
where in that range a case actually sits. Its corollary, and most of the answer to "how do you rule":
**the hard part is almost never knowing the right policy — it's revenue, coalition maintenance, an
army that might turn, orders that arrive distorted, and information that reaches you filtered by
people with reasons to filter it.** Keep that in view throughout. Do not frame readings or items
around my personal background or career.

## Step 3 — The spine

Draft `statecraft-syllabus.md` from the outline below, in the style of the reference repo's syllabus:
per unit, **objectives · core concepts · anchor resources · why it matters in the chair · practice
rep**. The units are sequenced by the order a ruler's problems actually bite. Improve it where you
have grounds — I want your judgment, and I especially want to know what a serious political science
or history department would say I've left out, and where the ruler's-eye framing is distorting the
scholarship rather than organizing it. **Bring me the revised spine and stop before building
content.**

**Tier 1 — Taking and keeping power** *(without this, nothing else happens)*
1. **What you are actually seizing.** What a state is: sovereignty, the monopoly on violence, state
   formation (Tilly's war-makes-states and its critics), state capacity, fragility. What "ruling" has
   physically meant across eras — chiefdom, agrarian empire, feudal monarchy, party-state, modern
   democracy — and the ruler's first question: what apparatus exists, and does it obey me?
2. **Who actually keeps you in power.** Selectorate theory and winning coalitions, elite bargains,
   patronage, the core trade between rewarding your coalition and providing public goods. Machiavelli,
   Ibn Khaldun on *asabiyyah*, Bueno de Mesquita & Smith. Why the same ruler behaves differently with
   a coalition of 50 than with one of 50 million.
3. **Legitimacy: why people obey when they don't have to.** Weber's three types; divine right,
   mandate of heaven, popular sovereignty, performance legitimacy; ritual, symbol and spectacle;
   information control from court chronicles to state media. And **succession** — the single most
   reliable way a regime dies is failing to transfer power.
4. **The means of coercion.** Who the army belongs to; coup-proofing and what it costs you in
   military effectiveness; praetorians, mercenaries, slave soldiers, conscript armies, secret
   police. The permanent dilemma: a force strong enough to defend you is strong enough to remove you.

**Tier 2 — Making the machine work** *(the part that decides whether you accomplish anything)*
5. **Money.** Taxation and fiscal capacity across eras — tribute, plunder, tax farming, customs, land
   tax, income tax — plus debt and credit, coinage and debasement, inflation, the fiscal-military
   state, the resource curse. Nearly every dynasty's terminal crisis is fiscal; this unit explains
   more failures than any other.
6. **Administration.** Bureaucracy and the principal-agent problem, corruption, legibility (Scott's
   *Seeing Like a State*), the Chinese examination system, the modern civil service. Why your order
   arrives distorted 500 miles away, and what the telegraph and the filing cabinet changed.
7. **Binding yourself.** Rule of law as credible commitment, constitutions, courts, property rights;
   why rulers who tied their own hands could borrow cheaply, and often lasted longer; and the modern
   form of the same problem — presidential vs. parliamentary systems, electoral rules, federalism.
8. **Deciding.** Allison's three models, groupthink, advisory system design, crisis decision-making,
   the autocrat's information problem, and the honest question of what a leader actually controls.
   This is the "in the chair" unit; lean hard on `decision` items.

**Tier 3 — Surviving history** *(the rise-and-fall question)*
9. **Neighbors.** The international system: anarchy and the security dilemma; realism, liberalism,
   constructivism; balance of power; alliances; deterrence and nuclear strategy; war as an instrument
   of policy; trade and interdependence; hegemony and power transition. Grand strategy as the ruler's
   problem of matching commitments to resources.
10. **Rupture from within.** Revolution (Skocpol, Goldstone), civil war onset, ethnic conflict,
    insurgency and counterinsurgency, peasant rebellion; what rulers do that invites or forestalls
    each; and democratization, the third wave, and contemporary backsliding as the modern forms.
11. **Prosperity.** Long-run growth as the resource base under everything above: the Industrial
    Revolution, the Great Divergence debate (Pomeranz, Mokyr, Allen), institutions vs. geography vs.
    culture (Acemoglu & Robinson and their critics — a `debate-` page, not a verdict). The ruler's
    version of the question: can you *cause* prosperity, or only avoid destroying it?
12. **Decline and fall — and how much of this is knowable.** Ibn Khaldun's cycle, Gibbon, Tainter on
    complexity and diminishing returns, Kennedy's imperial overstretch, Turchin's elite
    overproduction; fiscal-military exhaustion; environmental and epidemic shocks — set against the
    serious methodological case that "collapse" is often an artifact of the surviving sources. This
    unit doubles as the capstone where the methods from `historical-epistemics.md` get applied to the
    hardest cases in the curriculum, because this is exactly where hindsight, narrative fallacy, and
    selection on the dependent variable bite hardest.

Also plan the build order for `era-` and `case-` pages: roughly five era pages and eight case pages
should exist early, since Units 1–4 will already need to reach across them and Tier 3 is unusable
without them.

## Step 4 — What to produce in this bootstrap pass

Create, adapted from the reference repo and from the sections above:

- `CLAUDE.md` — the schema for this repo. Same structure as the reference, updated for: the ruler's
  lens as the governing frame, the new page types (`case-`, `debate-`, `era-`), the required
  `## Across eras` section, the new item types (`case`, `decision`, `counterfactual`, `attribution`,
  `forecast`) and the `era` field, the two-rulebook setup, the source-tier rules, and an elective
  namespace (`aux-<slug>`) for off-spine topics I ask for.
- `statecraft-syllabus.md` — the spine, per Step 3.
- `learning-science-for-self-study.md` — copied from the reference repo, plus the anti-hindsight
  section from Step 2.5 and the item-type guidance from 2.4.
- `historical-epistemics.md` — the new rulebook, per Step 2.3.
- `course-map.md` — per-unit scope, objectives, dependencies, anchor resources, clusters, and which
  eras and cases each unit will lean on.
- `index.md`, `coverage.md`, `log.md` — bookkeeping, stubbed with headers and the elective section.
  `coverage.md` additionally tracks **era coverage**: I should be able to see at a glance that I've
  been drilling the modern state and neglecting everything before 1500.
- Empty `research/`, `wiki/`, `items/`, each with a short `README.md`.

**Port, don't rewrite, the machinery.** Copy `apps/` and `docs/` from the reference repo. They are
almost entirely content-agnostic; adapt paths, the item-type vocabulary, and any hardcoded
psych-specific strings, then run `python apps/test_sm2_parity.py` and `python apps/test_web_logic.py`
and report results. Two notes: the phone app needs its **own Supabase project** (or a course column
in the schema) so the two repos don't share one review queue, and `docs/config.js` must point at it;
leave it unconfigured and local-only if I haven't set one up yet, and tell me what I need to do.

## Step 5 — Stop

Do not build Unit 1 in this pass. When the scaffolding is in place, show me: the revised spine; the
source-tier rules you settled on; one `era-` page outline and one `case-` page outline; a `debate-`
page outline for the question where you think the disagreement is sharpest; and four sample items —
one `decision`, one `forecast`, one `counterfactual`, one cross-era transfer item — so I can see the
reasoning level before you generate hundreds. Then wait for `create chapter 1`.
