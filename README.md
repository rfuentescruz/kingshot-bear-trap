# Kingshot Bear Trap March Planner

A single-page calculator for the Kingshot **Bear Trap** event. It works out how to split your troops across your own rally and your joiner marches to get the most bear damage, and it can measure how strong each rally leader is from your hit list after an event.

Everything runs in the browser. There is no server, no build step and no tracking. Saved accounts live in your own browser's local storage.

## What it does

- **Best plan.** Decides which leaders to pin a march to (join the moment their rally opens), how many marches should rotate (join whichever rally leaves next with room), and how many troops of each tier go into each preset.
- **Presets.** Troop counts per march, in the game's order (highest tier first, then Infantry, Cavalry, Archers), with a Copy button.
- **Other plans.** Close alternatives ranked by damage. Tap one to use its presets instead.
- **Caps and minimums.** Joiner caps and minimums, per-leader overrides, and your own march's maximum. Rotating marches skip rallies whose minimum is above their size.
- **Measure leader strengths.** Paste the presets you used and your hits after a bear, and it works out each leader's strength relative to your own rally and updates the leader list.
- **Projected damage.** Once calibrated from your own rally's hits, the headline shows expected damage per event.

## How to use it

1. **Troops:** enter your troop counts from Troops Preview.
2. **Your marches:** march queues (your own rally doesn't use one), whether you lead a rally, how many hits your rally gets (5 if you open within the first ~3.5 minutes, otherwise 4), your march maximum if you have one, and the attack and lethality buffs you'll have running.
3. **Leaders you join:** one row per leader with their strength (you = 1.00). Untick **Joining** for anyone not playing. Tick **Full early** if their rally fills before your rotating marches can get in.
4. **How rallies launch:** staggered (rotate late) or all at once, rallies per leader, hits per rotating march, joiner cap and minimum.
5. After the event, use **Measure leader strengths** to update the strengths from your actual hits.

Use **Save as new** to keep separate accounts.

## The model

- Damage per march is modelled as leader strength × hits × √troops, **separately for each troop type**. Extra troops of one type in the same march add less and less.
- Each march gets troops roughly in proportion to (hits × strength)². A leader twice as strong gets about four times the troops, never all of them.
- Without caps, every march gets the same mix of troop types. When a march is at its cap, its slots go mostly to archers and cavalry, which hit hardest per troop.
- Troop base attack values come from the community-published base stat tables (T1–T11). Attack and lethality bonuses come from your stats screen.
- Assumes you can't put two of your own marches in the same rally.

This is a community model, not official game data. Measure strengths from your own hits and treat small differences between plans (about 1%) as noise.

## Hosting

It's one static file, `index.html`, with no build step, so any static host works.

**GitHub Pages**
1. In the repository, open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. The site appears at `https://<user>.github.io/kingshot-bear-trap/`.

**Cloudflare Pages**
1. In the Cloudflare dashboard, go to **Workers & Pages → Create → Pages → Connect to Git** and pick this repository.
2. Framework preset: **None**. Build command: leave empty. Build output directory: `/`.
3. Deploy. The site appears at `https://<project>.pages.dev/`.

The `.nojekyll` file stops GitHub Pages from running Jekyll on the repository; Cloudflare ignores it.
