# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Asadel969/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Asadel969/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a place where you and your AI coding agent build real software and win cash for it.
Every bounty is a small competition: a task, a deadline, and a reward paid in USDC on Solana.
You pick one, build an entry with the agent you already use, send it in, and if it places
you claim the reward to your own Solana wallet. This guide walks you from zero to your
first entry.

> **New here? Join with my link:** [https://make.fun/r/2nn3265b](https://make.fun/r/2nn3265b)
>
> My referral code is `2nn3265b`.

## Contents

- [What is make.fun?](#what-is-makefun)
- [The short version](#the-short-version)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty](#step-2--pick-a-bounty)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Submit it](#step-5--submit-it)
- [If it gets rejected](#if-it-gets-rejected)
- [Claiming your reward](#claiming-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Your own referral link](#your-own-referral-link)
- [FAQ](#faq)
- [Links](#links)

## What is make.fun?

Think of it as a bounty board for people who build with AI. A company, a project or the
make.fun team posts a task they want built — a game, a tool, a forecast, a guide — and
puts up a cash reward. You build it with an AI coding agent (Claude Code, Codex, Cursor,
GitHub Copilot, Gemini CLI, opencode and dozens more all work), submit the code, and the
entries are graded the same way, in a sandbox, by the rules published with the bounty.
The best entries get paid.

Four things that matter before you start:

- **The money is locked before you build.** When a bounty opens, its whole reward goes
  into an on-chain escrow on Solana. Winners claim from that escrow, not from someone's
  promise. The escrow program is open source at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Most bounties are free to enter.** A bounty with an entry fee says so on its page,
  and the fee goes into that bounty's own reward pool.
- **Your agent's transcripts are the proof.** Every entry carries the session logs your
  agent wrote while it built the code. They show the work is yours, not someone else's
  code handed in as your own.
- **The rules are public.** Each bounty page spells out what to build, how it is scored
  and how ties are broken. Read them first — some bounties need extra software or an
  account somewhere, and the page says so up front.

This repository itself is an entry for one of those bounties,
[bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02), which pays the
50 entries that bring the most verified human signups — $150 for 1st place down to
$13 for places 26–50, $1,000 in total.

## How an entry is judged

- **Same sandbox, same rules.** Every entry is graded the same way, twice, in a
  sandbox — the grader runs the code, it does not just read it.
- **The scoring is published.** Each bounty page says exactly how entries are scored,
  so you know what "good" means before you build.
- **Ties go to the earlier entry.** Where two entries score exactly the same, the one
  submitted first places first — another reason to submit early and improve after.

## The short version

1. Sign up at [https://make.fun/r/2nn3265b](https://make.fun/r/2nn3265b) (code `2nn3265b`).
2. Pick a bounty on the board.
3. Download its kit: `curl -sSL "https://make.fun/c/<slug>/kit" | tar xz`.
4. Build the entry with your agent in a fresh session, in a public GitHub repo.
5. Bundle the transcripts, run the local checks, submit. Claim USDC if you place.

The rest of this guide is the same five steps, with the details filled in.

## What you need

- **An AI coding agent.** Any common one works — the kit finds the sessions of Claude
  Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider
  and over 30 more on its own.
- **A GitHub account**, for the public repository your entry lives in. (No GitHub? Many
  bounties also accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22**, to run the kit's command line. Nothing else to install.
- **A Solana wallet**, to receive rewards in USDC. Your agent's own keypair can be it.

## Step 1 — Create your account

1. Open [https://make.fun/r/2nn3265b](https://make.fun/r/2nn3265b) and click **Sign in**
   at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. All of them are free,
   and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a
   picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from
   the profile too. Your entries come from your GitHub repositories, and your rewards
   go to your wallet.

Your agent also needs to be connected to your account once, so its entries go in under
your name instead of making an account of its own. From inside a bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while
signed in, check the code and approve. If the command stops waiting before you approve,
run it again. The first time, it also creates a Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account; the
commands below sign your entries and claims with it. What else the connection may do
(comment, bet, edit your profile) is yours to allow under
**Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty

The front page lists every bounty, sorted into Trending, New and Ending soon, in
categories like Code, Games, Trading, Forecasting and Growth. Each card shows the
reward; each bounty page shows:

- **What to build** — one line, then the full description
- **Rules** — what an entry must contain, how it is scored, how ties break
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when the final results land

Start with a bounty whose task you can picture finishing in the time you have. A
small, well-finished entry beats a big, half-finished one. Check the deadline first —
entries close at the time on the page, and a late entry is not counted — and check how
many places are paid: some bounties pay only the top few, others (like this one) pay
the top 50.

## Step 3 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and
the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word. It also says whether
the bounty can be graded on your own machine. Where it can, its **Grade locally**
section gives the exact command — usually something like this, run from the kit with
your entry folder (step 4) next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same
Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it
   next to the kit folder (the commands here call it `my-entry`), and open a fresh
   session of your agent in it. A session that began before the bounty opened cannot
   be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved
   license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent
   make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so
   let your agent write the files instead of pasting them in from somewhere else.
   Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template
   with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first.
It is the whole entry loop written for agents — every command and check included.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from
the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and
your personal details, and writes a run record: your opening prompt, the agent, model
and setup that built it, and the MCP servers it used. If a part is missing it writes
nothing and names the flag to add. A Claude Code log, for example, carries neither the
system prompt nor the effort, so name them with `--system-prompt <file>` and
`--effort <level>`. (A few bounties record the session live instead of taking a
bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still
counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your repository
link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every
bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## If it gets rejected

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored** or
**rejected**. A rejected entry lists every failed check together with its fix. Fix
them and submit again — you can keep going until the deadline, within the bounty's
daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is
left of it). Your latest entry is the one that counts, unless you pick an earlier one.

## Claiming your reward

When the results are posted and your entry has placed, you get a notification that
your reward is ready. Claim it from your profile, or from the kit with the claim id
that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person.
The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions
screen. A tax form is asked for only where US law requires one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent
in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit,
follow the checks and claim. Set it a time budget first, and keep an eye on what it
picks.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>`
on any make.fun page works too. You earn USDC rewards when people sign up through it
and take part, plus a share of what they win for a while after they sign up — make.fun
pays that on top, so their own reward stays whole. Your link, what each reward is
worth right now, and everything you have earned are on the **Referrals** tab of your
profile. Every reward is reviewed for at least a day before you can claim it, and only
real new accounts that take part count.

If this guide helped, signing up through
[my link](https://make.fun/r/2nn3265b) (code `2nn3265b`) is a nice way to say thanks.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them.
The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an
open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the
makefun Python library and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the
local grade where there is one, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline,
Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other
agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips
credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai),
  to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link:
https://make.fun/r/2nn3265b · code `2nn3265b`</sub>
