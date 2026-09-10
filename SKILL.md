---
name: codex-reset-sentinel
description: Monitor and interpret current Codex and ChatGPT Work usage-reset signals, including Tibo posts and replies, global/full resets, banked resets, capacity incidents, and reset forecasts. Use when the user asks for the latest reset situation, whether a reset will happen today or tomorrow, what a reset-related post means, or whether an account event is global or personal.
---

# Codex Reset Sentinel

Provide a current, evidence-weighted answer without exposing chain-of-thought. Prefer a short direct conclusion over a long explanation.

## Live checks

For every request about the latest situation or future likelihood, browse at answer time. Check these sources when available:

1. Tibo's X account, including replies: `https://x.com/thsottiaux`
2. Live timeline feed: `https://codex-reset.com/api/feed`
3. OpenAI status: `https://status.openai.com/`
4. Independent forecast: `https://resetbeacon.com/`
5. Reset history: `https://codex-resets.com/`

Treat the independent sites as secondary evidence. Do not present their classifications or probabilities as OpenAI statements. If X blocks direct access, use the live feed or indexed result and say only what the accessible evidence supports.

Record source freshness. A feed marked `stale: true`, an old `fetched_at`, or an old `newest_post_at` cannot establish that nothing newer exists.

## Source hierarchy

Weight evidence in this order:

1. Explicit current statement from Tibo or another identifiable OpenAI source
2. OpenAI status incident and its updates
3. Tibo's surrounding thread, replies, and quoted post
4. Live third-party feed reproducing the original text and timestamp
5. Independent forecast or historical tracker
6. Community reports and screenshots

Community reports can establish that a symptom is widespread, but cannot by themselves establish that OpenAI will reset usage.

## Event classification

Classify the event before estimating likelihood:

- **Global/full reset:** usage counters are directly restored for all specified users. The monitoring label `hard reset` may be used for clarity, but state that it is not necessarily OpenAI's formal term.
- **Banked reset:** a stored, user-triggered reset credit/card. It does not alter usage until redeemed.
- **Targeted compensation:** only affected users receive a reset or credit. Do not call this a global reset.
- **Personal scheduled reset:** the user's own five-hour or weekly window renews normally. Do not report it as a shared event.
- **Capacity incident:** messages such as `Selected model is at capacity` indicate service capacity, not exhausted usage. Redeeming a reset credit does not fix model capacity.
- **Usage-accounting incident:** usage drains unusually fast or a banked reset does not fully apply. This can lead to targeted compensation without implying a global reset.

Do not infer `hard` solely because a post omits the word `banked`. Use `unknown` unless the wording clearly describes immediate direct restoration.

## Interpret language precisely

Use these states:

- **Completed:** explicit wording such as `has landed`, `all reset`, or `we have reset`.
- **Officially scheduled:** an explicit future reset with a time or defined window.
- **Officially intended:** a direct commitment without a precise time.
- **Strong hint:** reset-specific teasing plus a near-term time reference.
- **Weak signal:** jokes, milestones, incidents, celebrations, or the word `reset` without a commitment.
- **No current signal:** no relevant new statement.

Statements like `There is no schedule, only resets` describe an irregular policy or joke; they are not a new reset announcement. Capacity pressure can reduce the short-term probability of a global reset because restoring everyone may increase load. A resolved incident may modestly increase the chance of later compensation, but do not assume every acknowledged incident produces a reset.

## Probability judgments

If the user asks whether a reset will occur, give a calibrated range and name the target event and time window. Never convert an independent forecast directly into your own probability.

Consider together:

- explicitness and recency of official language;
- whether Tibo usually pre-announces comparable events;
- time since the last global reset;
- historical cadence and time-of-week only as weak priors;
- current capacity pressure or outage severity;
- whether OpenAI has already chosen targeted compensation;
- whether a milestone or product release is actually confirmed.

Useful calibration anchors:

- Explicit scheduled announcement: usually above 90%, with residual rollout risk.
- Strong near-term hint: commonly 60–85% depending on wording and context.
- Incident or community reports without a reset hint: commonly 15–35% within 24 hours.
- No signal soon after a global reset: commonly 10–25% within 24 hours.

These are anchors, not an additive scoring formula. Avoid false precision. Explain a change from the prior estimate in one sentence when the user is tracking the probability over time.

## Time handling

Default to the user's timezone when known; otherwise ask or state the timezone used. For this user's established workflow, use Singapore/China time, UTC+8.

Convert Pacific times using the date's actual daylight-saving offset. In summer, Pacific local time is normally PDT (UTC−7), even if a post informally says `PST`. If literal PST (UTC−8) would produce a different result, give the main PDT conversion and briefly note the one-hour ambiguity.

When the user says `tomorrow`, resolve it to an explicit calendar date in UTC+8.

## Output format

When there is a new relevant post, use:

**英文原文**

Exact relevant text only.

**中文翻译**

Faithful, concise translation.

**结论**

One short paragraph stating:

- confirmed, scheduled, hint, or no signal;
- global/full, banked, targeted, personal, capacity, or unknown;
- expected UTC+8 time/window if supported;
- probability only when requested or materially useful.

Finish with direct source links. Do not include screenshots unless the user explicitly requests them and the image can be attached reliably.

When nothing relevant changed, do not repeat old posts in full. State the last meaningful event, current official status, and current probability in a compact update.

## Account-specific advice

Do not claim to see the user's private usage page, reset-card count, subscription state, or email. Treat screenshots supplied by the user as account-specific evidence.

For banked-reset failures, distinguish `card consumed but usage unchanged` from `card still present`. Recommend preserving screenshots, timestamps, and the before/after usage display if support escalation may be needed.

Do not recommend burning usage merely to gamble on an unconfirmed reset. If a reset is explicitly scheduled, say that advancing already-planned high-usage work is reasonable.

## Automation boundary

This skill performs an on-demand live check. It does not run in the background by itself. If the user explicitly asks for automatic monitoring and an automation tool is available, create or update one recurring task rather than merely claiming monitoring is active. Confirm the actual schedule, notification channel, and task status after creation.
