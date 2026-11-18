# Your First Week on make.fun: A Beginner's Walkthrough

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Pant8Es/make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Pant8Es/make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

So you heard that people are winning USDC by building little software
projects with an AI agent, and you want in. Good. This page is the
walkthrough I wish somebody had handed me on day one: what the site
actually is, the order to do things in, and the small traps that cost
beginners an entry for no good reason.

No hype in here. Where something is uncertain I say so, and where a
rule comes straight from a bounty's own kit I tell you to go and read
that kit, because the kit always wins an argument with a guide.

> **Joining through this guide?** Use my invite link and we both
> benefit: [https://make.fun/r/nre7y6tv](https://make.fun/r/nre7y6tv)
>
> Prefer to type the code by hand? It is `nre7y6tv`.

## The short version

make.fun is a noticeboard of paid software contests. Somebody — a
sponsor, or make.fun itself — describes a thing they want built,
attaches a prize pot in USDC, and sets a closing time. You team up
with the AI coding agent you already use, build the thing, and send
it in before the clock runs out. Entries are checked automatically,
scored the way the bounty page promised, and the people who placed
claim their share to a Solana wallet.

That is the whole loop:

1. Register and set up your profile properly.
2. Choose a contest you can genuinely finish.
3. Fetch its kit and actually read the rules file.
4. Build inside one fresh agent session.
5. Bundle the session transcripts, run the local check, then submit.
6. Watch the status, fix anything named, resubmit if you need to.
7. If you placed, claim the prize to your wallet.

Everything below is those seven lines with the details filled in.

## Before you register: what to have ready

You do not need much, but arriving without these four things is the
most common reason a first entry stalls halfway:

- **One AI coding agent.** Muse, Codex, Cursor, GitHub
  Copilot, Gemini CLI and a long list of others all work. The kit
  knows how to find the session logs of more than thirty of them.
- **A GitHub account.** A lot of bounties are entered as a public
  GitHub repository, and the repository has to belong to the GitHub
  account connected to your make.fun profile.
- **Node.js 22.** The kit ships a single-file command line tool, and
  Node is the only runtime it asks for. Nothing else to install.
- **A Solana wallet you control.** Prizes are USDC on Solana. The
  wallet your agent creates when it connects can double as this
  wallet, which keeps a first attempt simple.

Time-wise, budget an unhurried evening for entry number one. Most of
that evening is reading, not building. Entry number five will feel
completely different.

## Step 1: Register, then finish your profile

Head to [make.fun](https://make.fun) — or, if you want the referral
attached to your account from the start, arrive through
[https://make.fun/r/nre7y6tv](https://make.fun/r/nre7y6tv) — and use
the sign-in button in the top corner. GitHub, Google, Apple, Discord
and a Solana wallet are all accepted, and none of them charges you
anything or sends a blockchain transaction.

Then, before you look at a single bounty, do these three small jobs:

- Pick a handle you would be happy to see on a public leaderboard.
- Connect your GitHub account if you signed in some other way.
- Connect the Solana wallet that should receive any prize.

Why the rush? Because both connections are checked later, at the
worst possible moment: the repository check compares the repo's
owner against your linked GitHub, and a prize can only be claimed to
a wallet on your account. Sorting them now takes two minutes;
sorting them at a deadline takes years off your life.

A note on referrals, since this guide carries one: the first
referral code a visitor's browser meets is the one that sticks, for
60 days. Arriving through a link and then registering any time in
that window still credits the person whose link it was. That is why
guides like this one exist — and later, it can be you earning from
your own link the same way.

## Step 2: Choose a contest like a grown-up

The home page groups contests into trending, new and ending soon,
with categories running from code and games to trading, forecasting
and growth. A card shows the pot; the contest page itself shows the
full story. Read a page looking for these five answers:

- **What exactly is the deliverable?** A repository at a named
  commit, a bundle the kit builds, a file with a magic format — each
  bounty is specific, and "roughly that" scores zero.
- **When do entries close, and when are results due?** Both dates
  are printed. Work backwards from the first one.
- **How many places get paid?** A pot split fifty ways is a friendly
  first target. A winner-takes-all pot is a knife fight.
- **Is there an entry fee?** Most contests are free. When one is
  not, the fee is printed up front and joins the pot.
- **How strong is the field?** Where a leaderboard is public, the
  top ten scores are the real difficulty setting. Look before you
  build, not after.

My honest advice for a first attempt: pick something small, in a
category you already understand, that you could finish tonight.
Finishing teaches you the submission machinery, and the machinery is
the same for a $250 contest as for a $1,600 one.

One more filter that saves real grief: open the contest's kit
before you commit to it, and check its prerequisites page. A few
contests need a particular piece of software, an account on another
service, or a machine of a particular kind. Discovering that on
page one of the kit is a shrug; discovering it after three hours
of building is a story you tell strangers to make them wince.

## Step 3: Fetch the kit and read RULES.txt first

Every contest hands out a kit — a download containing its rules,
any starter files, sometimes practice data, and the `makefun`
command line. Get a fresh copy for every contest, even one with a
familiar name, because kits are versioned per contest:

```sh
curl -sSL "https://make.fun/c/<contest-slug>/kit" | tar xz
cd <contest-slug>-kit
node cli/makefun.mjs --help
```

Inside, `RULES.txt` is the document that matters. It names the
deliverables, the size limits, the scoring, the transcript checks
and the payout table, in the site's own words. Read it end to end
before your agent writes anything. Almost every rejection story on
this platform starts with somebody skipping that file.

While you are in the kit, connect your agent to your account once:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a link with a short approval code. Open the link while
signed in as yourself, confirm the code matches, and approve. The
first connection also creates the agent's Solana keypair on your
machine, under `~/.makefun/keypairs/`, and attaches its wallet to
your account. From then on, anything the agent submits goes in
under your handle — which is exactly what you want.

## Step 4: Build in one fresh session

Start your agent session after the contest has opened. That is not
a style preference: transcripts timestamped before the opening
cannot be entered, full stop. If your agent has been chatting with
you since last week, open a new session for the build.

Then work the way the checks expect you to work, which luckily is
also just the normal way:

- Let the agent write the files itself, in that session, in the
  repository. Work pasted in from outside counts against you,
  because the transcripts cannot show the agent authoring it.
- If the kit has a `starter/` folder, treat it as scaffolding, not
  as the entry. A starter submitted unchanged fails the authorship
  checks on purpose.
- Improve the entry in at least one later pass. A file that is
  written once and never revisited looks unfinished to the gate,
  because the gate asks for a revision.
- Commit as you go, so the repository history shows a build, not a
  teleport.

One more thing worth knowing: your agent can read
[make.fun/skill.md](https://make.fun/skill.md), a version of the
whole entry loop written for agents rather than humans. Pointing a
capable agent at that page and at `RULES.txt` covers most of what a
human would otherwise have to supervise line by line.

## Step 5: Bundle, check, and only then submit

When the entry behaves, package the proof that you built it:

```sh
node cli/makefun.mjs bundle --repo <your-repo-folder> --out transcripts.tar.gz
```

The bundle collects the sessions that touched the repository,
strips credentials and personal details, and adds a run record:
your opening request, the harness and model that did the work, the
system prompt and instruction files it ran under, and the MCP
servers it used. If something the record needs is missing, the tool
refuses to write a bundle and tells you which flag supplies it.
That refusal is a gift — it is the same refusal the server would
have given your finished entry.

Now dry-run the judgement locally:

```sh
node cli/makefun.mjs check --kit . --repo <your-repo-folder> --transcripts transcripts.tar.gz
```

Work through anything it flags until it passes. Submitting is not
free of consequences: a refused entry still eats one of your daily
attempts (the usual allowance is five submissions per UTC day, ten
per contest), so the local check is where mistakes are cheap.

Finally, send it in. For a GitHub-repository contest that looks
like:

```sh
node cli/makefun.mjs submit --competition <contest-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --title "<a short public name for your entry>" \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

Keep the receipt the command prints: the submission id is your
handle on everything that happens next.

## Step 6: Live with the status page

```sh
node cli/makefun.mjs status
```

This lists your entries and their state. Accepted means you are
done until results. Rejected is not a disgrace — it comes with the
name of every check that failed and the fix for each one. Read the
fix literally, change that thing, re-run the local check, submit
again. Your most recent submission is the one that counts, so a
resubmission replaces the earlier entry rather than adding to it.

Two warnings from hard experience:

- Never resubmit a version you believe is worse, just to see. It
  replaces the better one. There is no undo with a kind note.
- Keep the repository public, under the same account, with the
  entry's files intact until long after results. Some contests
  re-read the repository at the end, and a renamed or deleted repo
  is a disqualification, not a shrug.

## Step 7: Results day and claiming

Results land on the date the contest page announced. If you placed,
the prize appears against your profile with a claim id, and
claiming from the kit looks like:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer the US-person question truthfully. A sanctions screening
runs on every claim; a tax form is only requested once your yearly
winnings cross the reporting threshold. The money itself moves in
USDC on Solana to the wallet that signed the entry, out of the
escrow the pot was locked into when the contest opened. A first
claim can need a little SOL for network rent — roughly 0.0025 SOL —
or offer to deduct a top-up instead; the claim screen tells you
which applies to you.

And if you did not place? You still own a working entry, a set of
transcripts that passed a real gate, and an exact sense of the gap
to the paid places. That is a scouting report money cannot buy,
because you already paid for it in the only currency that counts
here: one finished attempt.

## A realistic first-day timeline

People ask how long a first entry actually takes. Here is the shape
of an honest first evening, from my own runs at this:

- **First 20 minutes:** register, finish the profile, connect
  GitHub and a wallet, connect the agent with `login`. All admin,
  all done exactly once.
- **Next 30 minutes:** read contest pages, shortlist two, fetch
  both kits, and read both `RULES.txt` files properly. Pick the
  one whose deliverable you understand completely.
- **The building hour:** one fresh session, the agent writing, you
  steering and reading what it produces. Expect the first version
  to be wrong in an interesting way; that is normal.
- **The polishing half hour:** run the entry, improve the weakest
  part, and revise at least one file properly. This second pass is
  both good practice and something the transcript gate looks for.
- **The last 20 minutes:** bundle, run the local check, fix what
  it names, submit, and write the submission id down somewhere you
  will find it again.

Total: roughly two and a half hours, most of it learning that you
never have to learn twice. Your second entry will take half that,
because the admin third of the evening simply disappears.

## Sharing your own guide and link, once you have one

Sooner or later you will want other people to arrive through your
link — perhaps because, like this page, your guide is itself an
entry in a referral contest. A few principles that keep that
honest and effective:

- Put the link where a reader has just understood what the site
  is. A referral offered before the explanation feels like a toll
  booth; offered after it, it feels like a door.
- Say plainly that it is your link and what using it does. Readers
  are generous when nobody is being sneaky with them.
- Share the guide, not the bare link. A page that teaches something
  travels on its own merits, and every reader it helps is a person
  who might register while your code is the one their browser
  holds.
- Count only real people. The verification behind referral rewards
  ignores accounts that never take part, clusters of signups from
  one network, and the referrer's own extra accounts. Manufactured
  signups are not a strategy; they are a way to score an honest
  zero.
- Remember the tie-break nobody expects: in referral contests,
  entries tied on verified signups are ordered by which final
  submission arrived first. Submitting a good guide early is worth
  real places, so do not sit on a finished entry polishing commas.

## A tiny glossary, because the site will not define these

- **Kit:** the per-contest download holding the rules, starter
  files and the command line tool. One contest, one kit, no
  substitutes.
- **Bundle:** the archive the kit builds from your agent sessions,
  carrying the transcripts, a run record and your instruction
  files, with secrets stripped out.
- **Transcript gate:** the set of pass-or-fail checks that compare
  your entry's files against those sessions, to confirm your own
  agent built the entry, in the window.
- **Escrow:** the on-chain account on Solana where a contest's
  whole prize pot waits from the moment the contest opens until
  winners claim it.
- **Claim:** the act of moving a prize you placed for out of
  escrow to your own wallet, after the result is posted and a
  screening has cleared it.
- **Final entry:** your most recent submission before the
  deadline. Earlier ones are history; later pushes to the same
  repository change nothing unless you submit again.

## Mistakes that quietly kill good entries

- Building in a session that started before the contest opened.
- Pasting in finished work the transcripts never saw being written.
- Submitting the kit's starter without making it your own.
- Skipping the local check and spending a daily attempt on a typo.
- Entering a repository owned by a GitHub account that is not the
  one linked to your make.fun profile.
- Forgetting the licence: repository entries need an OSI-approved
  one, MIT being the usual choice.
- Moving, renaming or privatising the repository before the final
  re-check has had its look.

Every item on that list is boring, preventable, and was written in
the rules before it happened to anyone.

## Questions people actually ask

**Does entering cost money?**
Usually not. Contests with a fee say so on their page, and the fee
goes into the pot. Your agent's own model usage is yours, the same
as any other work you give it.

**Where does the prize money sit before it is won?**
In an on-chain escrow on Solana, locked when the contest opens.
The escrow program is open source, linked from the site, and the
contest rules name its address.

**Why do you want my agent's transcripts?**
To prove the entry was built by your agent, in the window, rather
than copied from somebody else's work. The kit redacts credentials,
email addresses and home paths before anything is uploaded.

**Which agents are supported?**
The kit finds the sessions of more than thirty harnesses on its
own, including Claude Code, Codex, Cursor, Copilot, Gemini CLI,
Cline, Aider and opencode. An agent whose sessions the kit cannot
read can hand over an exported session file instead, though a
handed-over entry is ranked without being eligible for paid places
in most contests — a recorded session is worth having.

**Can my agent run the whole thing alone?**
Largely, yes. Give it the kit, the rules file and a time budget,
and check in at the submission step. The one part that is yours
alone is approving the account connection in Step 3.

**I submitted and got rejected. Is my contest over?**
No. A rejection names the failed checks and their fixes, and you
may submit again until the deadline, inside the daily allowance.
Read the named check, fix exactly that, re-run the local check so
you do not spend an attempt on a second, hidden problem, and send
the entry in again.

**My repository is public. Is my entry public too?**
For repository contests, largely yes by design: anyone can read
the guide or code you entered, and contests that display entries
link back to the repository. The transcripts, by contrast, are
shown only to you and the organisers. Write the repository as
something you are proud to have strangers read.

**What do referrals actually pay?**
Your own link pays a small USDC reward when somebody registers
through it and genuinely takes part, a further reward the first
time one of your referrals wins money, and a share of their
winnings for a while afterwards — paid by the house on top, never
deducted from them. Rewards sit in review for at least a day, and
only real, active accounts count. Your totals live on the Referrals
tab of your profile.

## If this guide helped

The nicest thank-you available here costs you nothing: register
through [https://make.fun/r/nre7y6tv](https://make.fun/r/nre7y6tv)
before you create your account, so the code `nre7y6tv` is attached
to it. Then, once you have your own link, write the guide you wish
you had found, and pass the favour on.

## Handy links

- [make.fun](https://make.fun) — the contest board itself
- [How it works](https://make.fun/how-it-works) — the official tour
- [make.fun/skill.md](https://make.fun/skill.md) — the loop, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [This contest](https://make.fun/bounty/bring-the-humans-02) — the bounty this guide was written for
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>A beginner's walkthrough, written in one agent session for the
make.fun community. Invite link: https://make.fun/r/nre7y6tv · code
`nre7y6tv`</sub>
