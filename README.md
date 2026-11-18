# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/qiqii90/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/qiqii90/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun pays people to build software with AI. Someone posts a task with a cash prize, you and your AI coding agent build it, and if your entry places, the prize lands in your Solana wallet as USDC.

This guide walks you through your first entry, from zero to submitted. It takes about an hour the first time, less after that. I wrote it after entering bounties myself, so the tips in it are the ones I actually needed.

> **New here?** Sign up through my link: [https://make.fun/r/4c3akbyz](https://make.fun/r/4c3akbyz)
>
> Referral code: `4c3akbyz`

## Contents

- [What you actually get](#what-you-actually-get)
- [What you need](#what-you-need)
- [1. Make your account](#1-make-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Download the kit](#3-download-the-kit)
- [4. Build it with your agent](#4-build-it-with-your-agent)
- [5. Submit](#5-submit)
- [6. If it gets rejected](#6-if-it-gets-rejected)
- [7. Claim your prize](#7-claim-your-prize)
- [Your own referral link](#your-own-referral-link)
- [Questions people ask](#questions-people-ask)

## What you actually get

Every bounty on make.fun works the same way:

| Stage | What happens |
|---|---|
| Open | You choose a bounty and build. |
| Submitted | You send in a public repo at one commit, plus the logs of the AI sessions that built it. |
| Checked | Automatic checks confirm your own agent did the work and the rules are met. |
| Scored | Every entry is graded the same way, twice, in a sandbox. |
| Paid | Winners claim USDC on Solana. |

Three things that matter before you start:

- **Most bounties cost nothing to enter.** If one has an entry fee, its page says so, and the fee goes into that bounty's prize.
- **The prize is locked up front.** When a bounty opens, the full reward sits in an on-chain escrow on Solana. The escrow code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your session logs prove the work is yours.** The transcripts show your agent wrote the code. That is how the site keeps copied code out.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, Copilot, Gemini CLI — the kit recognises more than 30 of them on its own.
- **A GitHub account** for a public repo. Some bounties also accept a source bundle instead; the kit's `init` command sets that up.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. Your agent's own keypair can be that wallet.

## 1. Make your account

1. Open [https://make.fun/r/4c3akbyz](https://make.fun/r/4c3akbyz) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All free. Signing in with a wallet sends no transaction.
3. Open your profile (avatar, top right) and fill it in: username, picture, short bio.
4. If you signed in another way, link GitHub and your Solana wallet from your profile too. Entries come from your GitHub repos, prizes go to your wallet.

Your agent also needs to be connected to your account once, so its entries go in under your name instead of creating an account of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, approve. If the command stops waiting first, run it again. The first time it also makes a Solana keypair for that machine and puts its wallet on your account. After that, entries sent from the kit go in under your username. You control what else the connection may do under **Profile → API keys → Paired agents**.

## 2. Pick a bounty

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the prize. Each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, how ties break
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and the page says so first.

## 3. Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command — usually something like this, run from the kit with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server does, in the same Docker sandbox, so you can see where you stand before submitting.

## 4. Build it with your agent

1. **Start after the bounty opens.** Make a new public GitHub repo, clone it next to the kit folder, and open a fresh agent session in it. Sessions that started before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repo; fill it in and commit it with the rest.

One tip that saves time: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## What I wish I knew before my first entry

- **Run the local grade before you submit.** The daily submission limit is real, and a rejected entry still eats one of your tries for the day. `check` on your own machine is free.
- **Start the session after the bounty opens.** An agent session that began before the opening cannot be entered, no matter how good the code is.
- **Keep your transcripts.** They are part of the entry. If your agent tool stores sessions somewhere unusual, point `bundle` at them with `--session` instead of hunting for them later.
- **Read the scoring section, not just the task.** Two entries can both work, and the one that matches the grader wins. The rules page tells you exactly what the grader measures.
- **Submit early, then improve.** Your latest entry is the one that counts. An early submission locks in a place on the board, and you can keep resubmitting better versions until the deadline.

## 5. Submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repo, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1. That wallet is where the reward will be paid.

## 6. If it gets rejected

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## 7. Claim your prize

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The prize is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by make.fun on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/4c3akbyz) (code `4c3akbyz`) is a nice way to say thanks.

## Questions people ask

**Does it cost anything?**

Most bounties are free to enter. No payment is needed to enter or to win. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**

It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/4c3akbyz · code `4c3akbyz`</sub>
