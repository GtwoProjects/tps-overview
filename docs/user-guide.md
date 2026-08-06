# TPS user guide

The workflow, start to finish. Two apps are involved:

- The **Dashboard** - the website. Operators create jobs, approve them and download the finished videos there.
- The **Driver** - the Windows desktop app. Virtual Assistants (VAs) claim jobs and record in it. Installation is covered in the [Driver guide](driver.md).

TPS has no projects. One video = one **job**. Below is the life of one job.

## Step 1 - Create a job (Dashboard)

Log in with your **Email** and **Password**. In the sidebar, open **Production Grid** and click **New Job** (the **Initialize Job** button on the home page opens the same dialog).

In the **Create New Job** dialog, pick the source at the top: **YouTube URL** (TPS fetches that video and its transcript) or **Reference Text** (you paste the material in).

| Field | Required | Notes |
|---|---|---|
| Job Title | yes | The job's name. |
| YouTube URL / Reference Text | yes | Whichever source mode you picked. |
| Assign VA | no | Leave empty and the job waits in the queue for a VA to claim, or pick a specific VA. |
| Software | no | The program the tutorial covers, e.g. "OBS Studio". |
| TTS Engine | - | Narration voice engine. Default Fish Audio; also Edge TTS (free), AI33, ElevenLabs, Qwen3. |
| Fish Audio Model | - | The specific voice. Only shown when the engine is Fish Audio. |
| Target Length | - | Default **Auto** matches the reference video. Or 3 / 6 / 8 minutes, 1 hour, or custom (1–120 min). |
| Narration Speed | - | Default 1×. Range 0.75×–1.5×. |
| Description, Tags | no | Metadata for the job record. |

Click **Create Job**. The job appears in the grid and waits for a VA.

## Step 2 - Claim the job and get the pack (Driver)

The VA opens the Driver and logs in with their VA account email and password (**Login & Start Session**). On first run the Driver asks for the server URL - enter the one your team lead gave you.

Press **Ctrl+D** or click **Jobs** in the sidebar. The Jobs screen has three sections:

- **Pending Acceptance** - jobs assigned directly to this VA. **Accept** takes the job, **Decline** hands it back (a reason is required).
- **Available Jobs** - the open queue. **Claim** takes a job; checkboxes plus **Claim Selected** take several at once.
- **My Jobs** - everything this VA holds, with the next action per job.

Accepting or claiming starts pack generation automatically - there is no separate button for it. The job card shows the build stages as they run: **Generating script -> Synthesizing narration -> Transcribing audio -> Analyzing scenes -> Assembling pack**, and downloads the reference video alongside. When the card says the pack is ready, the button reads **Start Recording** (or **START WORK** once everything is synced).

If a job was claimed the night before, the pack is often already built - the card then goes straight to ready.

## Step 3 - Record (Driver)

OBS Studio must be running with its WebSocket server enabled - the Driver blocks recording with an **"OBS is not connected"** message until it is.

The session screen: the video in the middle, the **Teleprompter** panel on the right showing the script with word-by-word highlighting synced to the narration audio, and the controls in the left sidebar. A **Preview Mode / Recording Mode** toggle (Ctrl+Shift+R) switches between freely watching the reference and actually recording. Playback speed is locked to 1× the moment recording starts - narration must stay in sync with the final render.

Recording a job means recording a take for each scene:

- **START TAKE / STOP TAKE** (Alt+1) - start and stop recording the current scene.
- **Rollback Take** (Alt+2) - throw the current take away and record the scene again.
- **Next Scene** (Alt+->) - move on after stopping a take. The counter shows where you are, e.g. 3/12.
- **Ctrl+Space** - pause everything; the pause overlay offers **Resume Take**, **Restart Scene**, **Finish & Finalize**, **Rollback**.
- **Enter Patch Mode** (Alt+3) then **Record Patch** (Alt+4) - re-record a short piece from the current position instead of the whole scene.

Finished takes upload by themselves in the background - there is no upload button. The **Uploading Takes...** window shows the queue and progress.

## Step 4 - Send to render, then approve (Driver -> Dashboard)

When every scene has a take, the Driver sidebar shows **✓ Ready to render** (if scenes are missing it lists which ones, and the button stays disabled). The VA clicks **End Session & Start Rendering**. The Driver confirms with "Video sent to render farm" and the VA's part is done.

Back on the Dashboard, the job runs through **Ingesting** (stitching the takes) and **Quality check**, then stops at **Awaiting approval**. The **Approvals** page in the sidebar lists these jobs - the badge on the sidebar item is the count. Click **Approve for Rendering**. Nothing renders until an operator approves.

Grid statuses, in the order of a normal run: Intake -> Queued -> Assigned (or Pending acceptance) -> Building pack -> Pack ready -> Recording -> Ingesting -> Quality check -> Awaiting approval -> Rendering -> Done. Click a job's row, then **Open full job detail** - the banner there explains the current status in plain words.

## Step 5 - Download and publish (Dashboard)

On a **Done** job's row in the Production Grid: **Preview** plays the video in the browser, **Download** saves `final_video.mp4`.

TPS does not upload to YouTube. **Upload Center** prepares the manual upload - each finished job gets a card:

- **Washed 2K Video** - the main download, available once the forensic wash finishes. Until then the card offers **Master Video** instead.
- Generated SEO metadata - title, description, tags, hashtags, chapters - each with a copy button.
- After uploading to YouTube yourself, paste the video's link into the YouTube URL field and click **PUBLISH**. That marks the job as published and stores the link.

## When something goes wrong

- **Job Failed** - open it and read the reason in the status banner. If the recording uploaded fine and only rendering broke, **Retry rendering** re-runs stitching and rendering without re-recording.
- **Job Blocked** - a pipeline safety check paused it. **Return to recording** on the job page sends it back.
- **Driver won't record** - the button's tooltip says why: OBS not connected, pack not loaded, or files not synced. Fix that first; the OBS modal has an **Open OBS settings** shortcut.
- **Cancelling** - on the Dashboard: **Cancel** on the grid row, then **Confirm Cancel**; the current step finishes, then the job stops (Done and Failed jobs can't be cancelled). In the Driver: **Cancel Job** on the job card, reason required.
- **Stuck** - a job sitting on one status far longer than usual is a bug. [Report it](../../../issues/new?template=bug_report.yml) with the job ID and the status.

## Accounts

Admins create both account types on the Dashboard under **Users**:

- **New dashboard user** - a Dashboard login for operators (email, temporary password, role).
- **New Virtual Assistant** - a VA account for the Driver (display name, login email, temporary password). VAs log in through the Driver only, never the website.
