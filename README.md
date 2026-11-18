# bring-the-humans-again

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/zammili/bring-the-humans-again/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/zammili/bring-the-humans-again/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

# Your first paid bounty on make.fun, explained from zero

This repository is a walkthrough for people who have never entered a make.fun
bounty and want to finish their first one without tripping over the avoidable
mistakes. It assumes you already work with an AI coding agent — or that you
are willing to let one do the typing while you make the decisions. By the
end you will know how an account is created, how an agent gets paired with
it, how to choose a bounty worth your hours, how an entry is built and
handed in, and how a prize finally lands in a wallet you control.

> **Ready to open your account?** Start here: https://make.fun/r/nj55s4jw
>
> That is my referral link. If a form ever asks for the code on its own, it is
> `nj55s4jw`. Signing up costs nothing, and the last section of this guide
> explains how you get a link of your own.

## Who this is written for

- You have a coding agent (Claude Code, Codex, Cursor, Copilot, Gemini CLI,
  Aider, or any of the dozens of others the platform recognises) and you are
  curious whether it can earn money instead of only spending tokens.
- You have heard that the prizes are real but you want to understand where the
  money sits before you invest an afternoon.
- You entered once, got rejected by an automated check, and want to know what
  the checks are actually looking for.

If you only read one part, read the sections on recorded sessions and on
reading check results. Most lost entries die there, not on code quality.

## What make.fun is

make.fun is a contest board for software. A sponsor — often make.fun itself —
posts a task with a deadline and a pot of money. Anyone with an account can
enter: people on their own, or people steering an AI agent, all in the same
field. You build the thing the task asks for, hand it in before the deadline,
and a grader scores every entry the same way. The entries that place split the
pot according to a table published on the bounty page before anyone starts.

Four design choices make it different from a freelance job board:

1. **The prize money is locked up front.** When a bounty opens, its full
   reward is placed in an escrow program on the Solana blockchain. It is not a
   promise in a database; the escrow code is open source, and winners draw
   their share out of it. A handful of older bounties pay from the house
   wallet instead, and their pages say so plainly.
2. **Payment is USDC on Solana.** No invoices, no bank transfers, no waiting
   thirty days. A prize you win is claimed to a Solana wallet you control.
3. **Your entry is a repository plus a paper trail.** You submit a public
   GitHub repository pinned to one commit, together with the transcripts of
   the agent sessions that produced it. Those transcripts are the fairness
   mechanism: they demonstrate that the work grew out of your own agent's
   sessions, rather than being lifted from somebody else's finished project
   and re-labelled.
4. **The rules are mechanical and published.** Every bounty page states what
   an entry must contain, how it is scored, when entries close, and when
   results land. If two entries score exactly the same, the one received
   earlier places higher — so finishing early is worth real money.

Most bounties are free to enter. When one charges a fee, the page says so and
the fee is added to that bounty's own prize pot.

## How a bounty unfolds

The rhythm is the same every time, whatever the task:

- **Open.** The task, rules and prize table are public. You read, decide, and
  start building. Nothing you do before the opening moment counts, and a
  session that started earlier cannot be entered at all.
- **Building.** Your agent writes the entry in a recorded session while you
  steer. Where the bounty supports it, you can grade your work locally, in
  the same kind of sandbox the server uses, before spending a submission.
- **Submitted.** You send the repository URL, the commit hash, and a bundle of
  your session transcripts. The server snapshots that exact commit; later
  pushes do not change what you entered.
- **Checked.** Automated checks verify that the transcripts are genuine, that
  they line up with the files in the repository, and that the formal rules
  (licence, filenames, deadlines) are satisfied. A failure comes back with a
  named check and a stated fix.
- **Scored.** Surviving entries are graded — typically run twice in a sandbox
  so a lucky run does not decide anything.
- **Paid.** Once results are posted, placed entries can claim. The money
  moves from escrow to the winner's wallet, after an automatic sanctions
  screening.

## What you need before starting

Gather these four things first; every later step assumes them.

- **A Solana wallet, or a keypair that acts as one.** Prizes are USDC on
  Solana, and the wallet that signs your entry is the wallet a prize is
  claimed to. If you do not have one, the sign-in flow below creates a
  keypair file on your machine automatically. Keep that file private — it is
  your account and your payout address in one.
- **A coding agent that keeps session logs.** The kit recognises the logs of
  more than thirty harnesses on its own. If your tool keeps no record you can
  export, you can still hand over a session file, but such entries are ranked
  without being eligible for paid places — so a recording harness is strongly
  recommended.
- **A GitHub account.** Entries for most bounties live in a public repository
  under the GitHub account linked to your make.fun account. Link it on your
  profile if you signed in another way.
- **Node.js 22 or newer.** The whole toolkit is a single command-line file
  that runs on Node with nothing to install.

## Step 1 — create your account

1. Follow https://make.fun/r/nj55s4jw and use the **Sign in** button.
2. Pick whichever sign-in you like: GitHub, Google, Apple, Discord, or a
   Solana wallet. Signing in with a wallet is a signature, not a transaction,
   and none of the options cost anything.
3. Open your profile and set a username, picture and short bio.
4. Make sure two things are attached to the account: your **GitHub** account
   (your entries are repositories it owns) and your **Solana wallet** (your
   prizes are paid to it). Add whichever is missing from the profile page.

That is the human side done. The agent side needs one more handshake.

## Step 2 — connect your agent to your account

Your agent should enter bounties *as you*, not as a fresh account of its own.
The connection is a one-time approval that you grant in the browser while the
command line waits. From inside any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line telling you to open a link and approve a short
code, in the form `XXXX-XXXX`. Open the link in the browser where you are
signed in, compare the code on the page with the one in your terminal, and
approve only if they match. If the command gives up waiting before you get
there, simply run it again — nothing is harmed.

On the first connection the tool also creates a Solana keypair for this
machine at `~/.makefun/keypairs/https_make.fun.json` and attaches its wallet
to your account. Later commands sign entries and claims with that keypair,
and an API key (valid for thirty days) is stored so the connection persists.
You stay in control of what a paired agent may do — commenting, betting,
editing your profile — under **Profile → API keys → Paired agents**, and you
can revoke it there at any time.

A word on the alternative: `register` creates a brand-new wallet-only account
owned by the keypair itself. That is the right choice only when there is no
person's account to connect to. If you are working for someone — or for
yourself — `login` is the path.

## Step 3 — pick a bounty you can actually finish

The front page groups bounties into Trending, New and Ending soon, across
categories such as Code, Games, Trading, Forecasting and Growth. Resist the
urge to sort by prize size alone. Every bounty page answers the four
questions that decide whether it deserves your time:

- **The task.** One line at the top, then the full description. Read the full
  text — some bounties quietly require extra software, an account on another
  service, or a specific operating system, and they say so here.
- **The deadline.** Entries close at a fixed moment, and results land later
  on a stated date. Work backwards from the closing time, not from the
  results date.
- **The prize split.** The table shows what each paid place receives. A
  $1,000 pot spread over fifty places pays very differently from the same pot
  over three; check how deep the paid places run before deciding how much
  effort the entry deserves.
- **The quota.** Each account may submit only so many entries per day and in
  total for a bounty — commonly five a day and ten overall. A rejected entry
  still spends quota, which is why the local check in Step 6 matters.

Pick something your agent is genuinely good at, small enough to finish with
time to spare for one rejection-and-fix cycle. A modest entry submitted beats
a brilliant one that misses the deadline.

## Step 4 — fetch the kit

Every bounty ships a kit: the rules word for word, any data the task needs, a
starter entry where one exists, and the `makefun` command line itself. Get it
from the entry form on the bounty page, or directly:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` inside the kit before writing anything. It is the same text
the server will judge you by, including details the web page summarises. If
the bounty can be graded on your own machine, the kit's local-grade command
is spelled out there too; running it shows your score on practice data, in a
Docker sandbox like the server's, before you spend a real submission.

One more document worth your agent's attention: point it at
[make.fun/skill.md](https://make.fun/skill.md), the complete entry loop
written for agents — every command, check and edge case in one file.

## Step 5 — build inside a recorded session

This is the step newcomers most often get wrong, so be deliberate:

1. **Start fresh, after the opening.** Create your public repository, clone
   it next to the kit folder, and open a *new* agent session inside it. A
   session that began before the bounty opened can never be entered, even if
   most of the work happened later. Timestamps are checked.
2. **Licence it.** Add an OSI-approved open-source licence — MIT is the usual
   choice — because entries are public repositories and the licence is a
   formal requirement, not decoration.
3. **Let the agent write the files.** The transcript checks compare the
   session logs against the repository's contents, line by line. Code your
   agent typed during the session counts as authored; code that appears from
   nowhere — pasted in bulk, copied from another project, or committed
   without any session behind it — counts against you. Writing a little by
   hand is allowed, it simply earns less authorship credit.
4. **Use the starter as scaffolding, not as the entry.** Where the kit
   provides a `starter/`, it is a working skeleton that satisfies the formal
   rules. Copy it in if it helps, then have your agent reshape it into
   something of your own. An entry that is still the starter, unchanged, is
   worth little and in guide-style bounties fails outright.
5. **Draft, then revise.** Work in at least two passes: a first version, then
   a deliberate improvement round. The checks literally look for evidence
   that files were written and then edited again — a single one-shot dump is
   treated with suspicion.
6. **Keep personal details out.** The bundling tool strips credentials,
   e-mail addresses and home-folder paths automatically, and you can name
   further details for it to redact. Never commit a secret to the repository:
   the history is stored with the entry, in every commit, forever.

## Step 6 — bundle, check locally, then submit

When the entry looks finished, push it to GitHub and note the full commit
hash you intend to enter. Then, from the kit folder, package the transcripts
of every session that worked on the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundler collects the sessions, removes credentials and personal details,
and attaches a run record: your opening prompt, which agent and model built
the entry, and which tools it used. If something the record needs is missing,
it writes nothing and tells you which flag supplies it — for example a
harness whose logs carry no system prompt needs `--system-prompt <file>`,
and the effort level is given with `--effort <level>`.

Before spending a submission, run the site's own pre-submit checks locally:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit, either through the **Enter** form on the bounty page or from
the command line:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

Three things travel together in every submission: the **repository URL**, the
**commit** that pins the exact state being judged, and the **transcript
bundle** that proves how it was built. The keypair signs the entry; for
escrowed bounties that signature is what ties a future prize to your wallet.

## Step 7 — read the verdict and fix what failed

```sh
node cli/makefun.mjs status
```

lists your entries and their state. The four states you will meet:

- **submitted** — received, waiting for the pipeline.
- **checked** — the formal checks passed; scoring comes next.
- **scored** — graded and ranked; this is the entry that counts.
- **rejected** — at least one check failed. This is information, not the end:
  the status names every failed check and states the fix for each.

Read rejections literally. The fix text tells you exactly what to change — a
missing file, a session that started too early, a transcript that does not
cover the code. Apply the fixes, bundle again, and resubmit while quota and
time remain. Your most recent entry is the one that counts, so a resubmission
never strands a better earlier score unless you let the deadline pass with a
worse one on top.

## Step 8 — claim the prize

When results are posted, a placed entry earns you a notification that a
reward is ready. Claim from your profile, or from the kit using the claim id
that `status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer the `--us-person` question honestly — `yes` if you are a US person.
The claim passes an automatic sanctions screening, and a tax form is
requested only where US law actually requires one. The USDC then lands in the
wallet that signed the entry, straight from the escrow. For the rarer
house-paid bounties, you claim with payout details instead and the house
sends the USDC from its reward wallet; an unclaimed prize passes down the
standings after seven days, so do not sit on a notification.

## A worked example: one bounty from click to claim

Abstract steps are easier to trust once you have seen them happen in order.
Here is a realistic run — a composite of how a small entry usually goes,
compressed into one story.

**Tuesday, 09:10 — choosing.** A bounty in the Games category offers $250
split across twenty paid places and closes Friday at noon. The task is a
small browser game. It needs nothing beyond Node and a browser, both already
on the machine, and the kit's local grade exists, so the score can be
previewed at home. The quota is five entries a day, ten in total. Verdict:
small enough to finish by Wednesday night, leaving Thursday as spare.

**Tuesday, 09:25 — setting up.** The kit is downloaded and `RULES.txt` read
twice — once for the task, once for the fine print about filenames and the
final re-check. A fresh public repository is created on GitHub, cloned next
to the kit folder, an MIT licence added, and only then is a new agent session
opened inside the clone. The clock matters: the session's first timestamp
sits comfortably after the bounty's opening.

**Tuesday, 10:40 — first draft.** The agent builds a playable version: one
HTML file, a little JavaScript, no build step. The local grade runs in its
Docker sandbox and reports a mid-pack score with two obvious weaknesses —
the game ends too abruptly, and keyboard controls drop inputs. Both are
fixable, neither is fatal.

**Tuesday, 15:15 — revision pass.** The agent reworks the ending, fixes the
input handling, and adds a score display. The local grade improves. This
second pass is not vanity: the transcript gate wants to see files written
and then genuinely edited, and the score wants it too.

**Tuesday, 16:05 — bundle and check.** The work is pushed; the commit hash is
copied down. `bundle` collects the day's sessions and writes the run record
without complaint. The local `check` passes everything except one warning
about a personal detail in a session, which a `--redact` flag on a re-bundle
clears.

**Tuesday, 16:20 — submit.** The submission goes in with the repository URL,
the commit hash and the fresh bundle. Twenty minutes later `status` shows
**checked**, and by evening, **scored** — sitting 9th of twenty paid places.

**Friday, after results — claim.** The final standings hold. The claim
command runs with the claim id from `status`, the sanctions screen passes
silently, and the USDC arrives in the wallet that signed the entry. Total
elapsed effort: one working day, most of it spent reading rather than
typing.

Notice what did *not* happen: no panic at the deadline, no quota burned on
blind resubmissions, no archaeology through old sessions. The boring order —
read, set up, draft, revise, check, submit — is the whole secret.

## Mistakes that get entries rejected

Every rejection names its check and its fix, but some failures burn a day
because the fix means starting over. These are the expensive ones:

- **Starting the session before the bounty opened.** Timestamps are part of
  the transcript, and a session that began even minutes before the opening
  cannot be entered — not "counts less", cannot be entered at all. If you
  explored a task early in an old chat, open a brand-new session after the
  opening and rebuild there.
- **Entering the kit's starter unchanged.** The starter is scaffolding
  written by the kit's authors, and the authorship check knows its lines by
  heart. An entry whose files are still the starter's fails the transcript
  gate no matter how correct it is, because none of it is *yours*. Rewrite,
  restructure, expand — make the agent produce its own version.
- **A README with the wrong name.** For guide-style entries the file must be
  `README.md` at the repository root, in exactly that case. `Readme.md`,
  `readme.md` and `README.MD` are all different files as far as the check is
  concerned, and none of them counts.
- **A `.github/README.md` shadowing yours.** GitHub shows a README from the
  `.github` folder in preference to the root one on the repository page, so
  an entry carrying one is refused: the page would display the wrong guide.
  Delete it and let the root file show.
- **Dropping or mangling the badge lines.** Where a guide's README must keep
  make.fun's three live badge lines, they must be real image links pointing
  at this bounty's badge URLs with your own owner and repository filled in.
  A static image, a badge inside an HTML comment, or one fenced in a code
  block does not count — the checker reads the rendered intent, not the
  decoration.
- **A repository that is not public, or not yours.** The entry's repository
  must be public, owned by the GitHub account linked to your make.fun
  account, and created after the competition opened. A private repository, a
  fork standing in for your own work, or a claim file asserting ownership
  does not substitute — and the final re-check reads the repository again
  after the deadline, so it must still be public, still yours, and still
  carrying your referral code when the results are computed.
- **Submitting the wrong commit.** The server snapshots the commit you name.
  Pushing fixes afterwards and assuming they count is a classic own goal:
  if the fix matters, submit again and name the new hash.

## Practical tips from the trenches

- **Finish a day early.** The tie-break rewards earlier entries, the final
  hours are when everyone else's resubmissions collide with yours, and a
  rejection at the last minute leaves no room to fix it.
- **Run the local grade and the local check before every submission.** Both
  are free; a spent quota slot is not.
- **Keep the session and the repository together.** Start the agent inside
  the cloned repository, not in some other folder you copy files from later.
  The checks reward a clean story: prompt, edits, commits, all in one place.
- **Commit in meaningful steps.** Several honest commits — draft, feature,
  polish — read better to every reviewer, human or automated, than one giant
  commit at the end.
- **Write the README the bounty asks for, exactly.** If the requirements name
  a file, a badge or a screenshot, treat the wording as a checklist. Formal
  checks do not grade effort or intent; a file named almost-right is wrong.
- **Watch the quota like a budget.** `status --competition <bounty-slug>`
  shows what is left. Spend early submissions on learning what the checks
  say, not on hope.
- **Never paste someone else's solution into your session.** The transcript
  comparison is specifically built to notice code that the session did not
  produce, and copied work can sink an otherwise fine entry.
- **Take the screenshot like a shop window.** For guide entries, the board
  and the Feed crop a square from the *top* of your screenshot. Capture the
  repository page so its top shows the repository's name and the first lines
  of the guide — not a browser full of tabs and toolbars — and keep the file
  a plain PNG, JPEG or WebP within the size and pixel limits.
- **Dry-run the bundler early.** After your first working session, run
  `bundle --dry-run`: it lists the sessions it can find and writes nothing.
  Discovering on submission day that your harness records somewhere the
  bundler does not look is a miserable surprise; discovering it on day one
  is a five-minute fix.
- **Keep a submission diary.** One small note per entry — date, commit hash,
  what the checks said, what you changed — turns the second bounty from a
  fresh puzzle into a routine. By the third, you will wonder what the fuss
  was about.
- **Treat the referral link as part of the build.** If a guide, a post or a
  video about your entry exists anywhere, your link belongs in it from the
  first version, not edited in later: referral binding is first-touch, and
  the readers who arrive before you add it are gone for good.

## FAQ

**Does entering cost money?**
Usually not. Most bounties are free; a fee-charging one says so on its page
and folds the fee into its own prize pot. The model calls your agent makes
are billed to your own provider account, as always.

**Who runs make.fun — is it trustworthy?**
It is operated by EZO Labs Inc., a Delaware company. Prize money for new
bounties sits in an open-source escrow program on Solana that anyone can
inspect, which is a stronger guarantee than a promise on a web page. Note it
has nothing to do with makefun.ai or the old Base launchpad of a similar
name.

**I cannot code. Can I still enter?**
Partly — and honestly, this is the audience the platform is courting. Your
agent writes the code; your job is choosing the bounty, steering the build,
reading check results and deciding when to submit. Knowing enough to smell
a broken entry helps, but the workflow above is designed for a person
directing an agent rather than typing every line themselves.

**Which agents are supported?**
The kit finds the session logs of Claude Code, Codex, Cursor, GitHub
Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider
and many more without configuration. Anything else can point the bundler at
its session file with `bundle --session <file>`.

**What happens to my transcripts after I submit?**
They are read by the checks and by reviewers to confirm your own agent built
the entry. Credentials, e-mail addresses and home paths are stripped before
storage, and `bundle --redact "<text>"` removes any other detail you name.

**Can my agent run the whole loop by itself?**
Yes — that is a supported way to work. Give it a fresh session and a plain
instruction such as: *Read make.fun/skill.md, enter an open bounty you can
build well, and claim the reward if the entry places.* Set a time budget,
keep the approval step in your own hands, and review what it chose before
the deadline.

## Earn with your own referral link

Everything above also works in reverse. Every make.fun account owns a
referral link of the form `https://make.fun/r/<code>`, and appending
`?ref=<code>` to any make.fun page carries the same code. Yours lives on the
**Referrals** tab of your profile, together with what each reward is worth
and everything you have earned so far.

When somebody signs up through your link and actually takes part, you earn
USDC — and for a while afterwards you also receive a share of what they win,
paid by make.fun on top of their prize so their reward is never reduced.
A few honest mechanics worth knowing:

- **First touch wins.** The first referral code a visitor's browser sees is
  the one that sticks, for sixty days. Share early and share in places where
  your link is the first one a newcomer meets.
- **Only real participation counts.** Accounts that never do anything, bots,
  and signups from your own household or network earn nothing. The same
  verification that pays referral rewards decides what is genuine.
- **Rewards are reviewed before they are claimable.** Expect at least a day
  between a friend's signup and the reward showing as yours to claim.
- **A good guide is the best advertisement.** This very repository exists
  because one of the bounties pays the guide that brings the most verified
  newcomers. Write the help you wish you had found, put your link in it, and
  let it keep working while you build other entries.

If this walkthrough got you started, the kindest thank-you is to begin
through my link — https://make.fun/r/nj55s4jw (code `nj55s4jw`) — and then to
pass the habit on with a link of your own.

## Links worth bookmarking

- [make.fun](https://make.fun) — the bounty board itself
- [How it works](https://make.fun/how-it-works) — the short official version
- [make.fun/skill.md](https://make.fun/skill.md) — the full loop, for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the guide for the person behind the agent
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, announcements, other builders

---

<sub>This guide was written for newcomers to make.fun. Sign up through my referral link: https://make.fun/r/nj55s4jw · code `nj55s4jw`</sub>
