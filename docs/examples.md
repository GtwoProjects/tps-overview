# Examples

Filling out a bug report or feature request can feel awkward the first time. Here's what good ones look like.

## Example bug report

**Title:** Dashboard freezes for ~10 seconds when I click "Start job"

**Which part of TPS?** Dashboard

**What happened?**
I filled in the new-job form and clicked "Start job". The whole page froze — I couldn't click anything, the cursor didn't change. About ten seconds later it unfroze and showed a red error banner that said "Job failed". The job didn't appear in my jobs list.

**What did you expect?**
The job to either start (and show up in the list) or fail with a clear message I could act on. Not a freeze.

**Steps to reproduce:**
1. Log in to the Dashboard.
2. Click "New job".
3. Pick the "Short test" template, leave the other fields default.
4. Click "Start job".
5. Watch the page freeze for ~10 seconds, then show the red error.

**How often does it happen?** Every time

**Screenshot or screen recording:** (screenshot of the red error attached)

**Your name / company:** Sara, Acme Corp

---

What makes this one good: it's specific (10 seconds, "red error banner that said 'Job failed'"), the steps are short and you could actually follow them, and the "what did you expect" makes the bug obvious. The "screenshot attached" line is a reminder that you can drop a screenshot straight into the textarea on GitHub — no Imgur, no Drive link needed.

## Example feature request

**Title:** Re-run a failed job without retyping the inputs

**Which part of TPS?** Dashboard

**What would you like to be able to do?**
When a job fails, I'd like a "Re-run" button on the results page that starts a new job with the same inputs. Right now I have to remember what I entered and type it all again, which gets old when I'm trying to confirm whether a fix actually worked.

**Why does this help you?**
I do a lot of "did this fix it?" testing. Each round means filling out the same form maybe twenty times. A re-run button saves me five minutes per round and stops me from making typos.

**Who else benefits?**
Anyone debugging — testers and the dev team when they're reproducing a bug.

**Have you tried a workaround?**
I keep the form fields in a text file and paste them back in. It works but it's clunky.

---

What this one does well: it says exactly what it wants ("a Re-run button on the results page"), explains the benefit in concrete terms (save five minutes per round), and admits to the workaround already in use. That last bit helps us judge how badly you need this versus how nice-to-have it is.
