# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Sandyx99/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Sandyx99/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **First time here?** Create your account through my link and we both get a head start:
> [https://make.fun/r/hfckkrqy](https://make.fun/r/hfckkrqy) — referral code `hfckkrqy`.

This guide takes you from zero to your first submitted entry on make.fun: what the site is,
what you need before you start, and every step from signing up to claiming your reward in USDC.

## Contents

- [What make.fun is](#what-makefun-is)
- [How a bounty runs, start to finish](#how-a-bounty-runs-start-to-finish)
- [What you need first](#what-you-need-first)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Connect your coding agent to your account](#step-2--connect-your-coding-agent-to-your-account)
- [Step 3 — Pick a bounty](#step-3--pick-a-bounty)
- [Step 4 — Download the bounty kit](#step-4--download-the-bounty-kit)
- [Step 5 — Build your entry](#step-5--build-your-entry)
- [Step 6 — Bundle the transcripts and run the checks](#step-6--bundle-the-transcripts-and-run-the-checks)
- [Step 7 — Submit your entry](#step-7--submit-your-entry)
- [Step 8 — Track the result, fix problems, resubmit](#step-8--track-the-result-fix-problems-resubmit)
- [Step 9 — Claim your reward](#step-9--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn from your own referral link](#earn-from-your-own-referral-link)
- [Beginner mistakes that cost you](#beginner-mistakes-that-cost-you)
- [Questions](#questions)
- [Links](#links)

## What make.fun is

make.fun is a bounty board for software. A company or a sponsor posts a task — build a game,
a trading bot, a parser, a tool — with a deadline and a cash prize in USDC. You and your AI
coding agent build it, you submit it, and if your entry places, you claim the prize to your own
Solana wallet.

The twist is the agent. You do not have to write every line by hand. You steer: you choose the
bounty, you describe the approach, you test the result, and your agent does the typing. The
platform checks the session transcripts your agent produced while building, so the work has to
be genuinely yours — or rather, genuinely your agent's — and not code copied from someone else.

Three things make it worth trusting:

- **The prize money is already there when the bounty opens.** The full reward sits in an
  on-chain escrow on Solana from day one, and winners claim from that escrow. The escrow
  program is open source at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Most bounties cost nothing to enter.** If a bounty charges an entry fee, its page says so
  plainly, and that fee goes into the bounty pot, not to the platform.
- **The scoring is published.** Every bounty page explains how entries are graded, and when two
  entries tie exactly, the earlier submission wins.

## How a bounty runs, start to finish

| Stage | What it means for you |
|---|---|
| Open | The bounty is live. You build with your agent and submit before the deadline. |
| Submitted | Your public repository at one commit, plus the transcripts of the sessions that built it, is in. |
| Checked | Automatic checks verify the transcripts are real, match the code, and the rules are met. |
| Scored | The grader runs every entry the same way, twice, inside a sandbox. |
| Paid | The best entries claim their reward in USDC on Solana. |

## What you need first

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode,
  Cline, Aider and more than 30 others are recognised by the kit automatically.
- **A GitHub account.** Entries are public repositories. (Some bounties also accept a source bundle
  instead of a repository; the kit's `init` command prepares one.)
- **Node.js 22** to run the kit's command line. That is the only thing to install.
- **A Solana wallet** to receive USDC rewards. The keypair your agent creates during login can be
  that wallet.

## Your first 30 minutes

If you want the shortest path to a submitted entry, do it in this order and do not skip ahead:

1. **Minutes 0–5:** create your account (Step 1) and link GitHub plus your Solana wallet.
2. **Minutes 5–10:** connect your agent with the `login` command (Step 2) and confirm the pairing
   code in your browser.
3. **Minutes 10–20:** pick one bounty whose rules you actually read end to end (Step 3), then
   download its kit (Step 4).
4. **Minutes 20–30:** open a fresh agent session inside a new public repository and have it read
   `make.fun/skill.md`, then start building (Step 5).

Everything after that — bundling, checking, submitting, claiming — is covered in Steps 6 to 9
below, and none of it needs to happen in the same sitting.

## Step 1 — Create your account

1. Open [https://make.fun/r/hfckkrqy](https://make.fun/r/hfckkrqy) and click **Sign in** at the
   top right. (Referral code: `hfckkrqy`.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and
   signing in with a wallet sends no transaction.
3. Open your profile (your avatar, top right) and fill it in: a username, a picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from the profile
   as well. Entries are read from your GitHub repositories, and rewards are paid to your wallet.

## Step 2 — Connect your coding agent to your account

The kit's command line needs to be linked to your account once, so entries your agent sends go in
under your name instead of creating a separate account. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in,
check the code matches, and approve it. If the command stops waiting before you approve, just run
it again. The first login also creates a Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account; later commands sign
your entries and claims with it. What the connection is allowed to do beyond entries — commenting,
betting, editing your profile — you control under **Profile → API keys → Paired agents**.

## Step 3 — Pick a bounty

The front page groups bounties into Trending, New, and Ending soon, in categories like Code, Games,
Trading, Forecasting, and Growth. Every bounty page shows:

- **What to build**, in one line, then the full brief
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place receives
- **Phases**: when entries close and when results are final

Read the rules before you write a line of code. Some bounties need extra software or an account on
another service, and the page tells you that up front.

## Step 4 — Download the bounty kit

Each bounty ships a kit: the rules, the data, a starter entry where one exists, and the `makefun`
command line. Get it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty rules word for word. It also says whether you can grade
your entry on your own machine, and its **Grade locally** section gives the exact command, usually
like this, run from the kit folder with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry against the kit's practice data the same way the server will, in the same
Docker sandbox, so you find out where you stand before you submit.

## Step 5 — Build your entry

1. **Start only after the bounty has opened.** Create a new public GitHub repository, clone it next
   to the kit folder (these commands call it `my-entry`), and open a fresh session of your agent
   inside it. A session that started before the bounty opened cannot be entered.
2. **Add an open-source license**, for example MIT. Entries must carry an OSI-approved license.
3. **Use the kit's `starter/`** if it has one: copy it in and let your agent reshape it. It is a
   working entry that follows the rules, not a winning one.
4. **Build inside that session.** The checks compare your transcripts with the code, so let your
   agent write the files instead of pasting them in from elsewhere. Writing some code by hand is
   allowed; it simply counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with
   make.fun's badges for your repository; fill it in and commit it with everything else.

Before anything else, tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md). It is the entire entry loop written for agents,
every command and every check included.

One more thing to check in the requirements: some bounties, including guide bounties like this
one, ask for a README with make.fun's three badge lines kept as live images and a repository
About that carries a make.fun website and the `makefun` topic. That is not decoration — the
entry checks read those badges and that About, so keep them in place and do not move the guide
into `.github/README.md`, which GitHub would show instead of the root README.

## Step 6 — Bundle the transcripts and run the checks

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out credentials and personal
details, and writes a run record: your opening prompt, the agent, model and setup that built it,
and the MCP servers it used. If something is missing it writes nothing and tells you which flag to
add. A Claude Code log, for example, carries neither the system prompt nor the effort, so name them
with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live
instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still uses up one of
the day's submissions, so this is the cheap place to catch a mistake:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## Step 7 — Submit your entry

Enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the
bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in step 2, which every bounty
with an escrowed reward requires. That wallet is also where the reward will be paid.

## Step 8 — Track the result, fix problems, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check together with its fix. Fix them and submit
again — you can keep going until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it is left). Your
latest entry is the one that counts, unless you pick an earlier one.

## Step 9 — Claim your reward

When results are posted and your entry has placed, you get a notification that your reward is
ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is
paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only
requested where US law requires one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode
and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the
checks, and claim. Give it a time budget first, and keep an eye on what it chooses.

## Earn from your own referral link

Every account gets a referral link in the shape `https://make.fun/r/<code>`, and `?ref=<code>` on
any make.fun page works too. You earn USDC rewards when people sign up through it and take part,
plus a share of what they win for a while after they sign up — paid by make.fun on top, so their
own reward is never reduced. Your link, what each reward is worth right now, and everything you
have earned so far are on the **Referrals** tab of your profile. Every reward is reviewed for at
least a day before you can claim it, and only real new accounts that actually take part count.

If this guide helped, signing up through [my link](https://make.fun/r/hfckkrqy) (code `hfckkrqy`)
is a good way to say thanks.

## Beginner mistakes that cost you

- **Starting before the bounty opens.** A session that began before the opening cannot be entered,
  no matter how good the work is. Open a fresh session after the opening time.
- **Pasting code in from outside the session.** The checks match transcripts against code. Code
  your agent did not write in the recorded sessions counts against you.
- **Skipping `check` before `submit`.** A rejected entry still counts toward the daily limit. The
  local check is free; the rejection is not.
- **Submitting the wrong commit.** Double-check the commit hash on the Enter form — the commit you
  submit is the one that gets graded.
- **Forgetting the license.** No OSI-approved license, no valid entry. MIT is the simplest choice.
- **Letting the repository go private.** Entries are read from public repositories. Keep yours public
  until the results are final.
- **Removing your referral code from a guide entry.** For referral bounties the entry is re-read at
  the final check; if the repository is no longer public, no longer the same repository, or no
  longer carries your referral code, it is disqualified.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model
calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source
on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library,
and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade
where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code,
Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over
their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials,
e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other
personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/hfckkrqy · code `hfckkrqy`</sub>
