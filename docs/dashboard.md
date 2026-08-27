# Using the Dashboard

The Dashboard is a website — nothing to install. Open the URL we sent you and log in. It's branded **Titan Operator Console**; that's the same thing this doc calls the Dashboard.

## Logging in

Your email and password came in your welcome email. If you can't find them, ask your contact at the company that gave you access. If the password doesn't work, try "Forgot password" first, then [file a bug](../../../issues/new?template=bug_report.yml).

Before you log in the app can't reach the farm, so pages may show errors or a "farm unreachable" banner. That clears once you're authenticated.

## What's in the sidebar

You only see the items your role allows, so your list will be shorter than this one. An admin sees all of them:

| Item | What it's for |
|---|---|
| Production Grid | Every job, with filters and the New Job dialog. This is where most work starts. |
| Orchestrator | Pipeline view of jobs in flight. |
| System Metrics | Throughput, queue depth, storage. |
| VA Analytics | Per-VA output and timing. |
| VA Roster | The VAs, their status and assignments. |
| Asset Packs | The generated packs (script, narration, scenes) per job. |
| QC Queue | Rendered videos waiting on a quality check. |
| Approvals | Jobs stopped at "awaiting approval". Nothing renders until someone approves here. |
| Blocked Jobs | Jobs that failed or need a human decision. |
| Upload Center | Finished videos, their SEO metadata, and publishing. |
| Payroll | VA payment tickets. |
| Diagnostics | Live health of the farm and its workers. |
| Users | Accounts and roles (admin only). |
| Grid Overlord | Worker nodes — restart, drain, inspect (admin only). |
| Settings | System settings (admin only). |

## Running a job

Open **Production Grid** and click **New Job**. Fill in a title and a source (a YouTube URL or pasted reference text) — **Create Job** stays disabled until both are there. Everything else has a working default.

The job lands in the grid and waits for a VA to claim it. The full field-by-field walkthrough is in the [user guide](user-guide.md).

## Following a job

Status moves roughly: **Intake → Queued → Assigned → Pack building → Pack ready → Recording → Ingesting → QC → Awaiting approval → Rendering → Done**. A job can also land on **Pending acceptance**, **Declined**, **Blocked**, **Failed** or **Cancelled**. The home page's log feed shows the same transitions in one list.

Click a row to open the job, or **Preview** / **Download** on a **Done** job to watch it or save `final_video.mp4`.

If a job sits in one status far longer than the rest, or the result looks wrong, [file a bug](../../../issues/new?template=bug_report.yml). The more specific you can be, the faster we can fix it.
