# DMWipe

Bulk-delete every message in a DM or group DM, from the channel context menu or `/wipe`.

Progress is shown in a live status message in the channel, with Pause and Cancel buttons.
<img width="1250" height="156" alt="image" src="https://github.com/user-attachments/assets/d43b7fe8-e97d-478f-a7f9-1c37426a924f" />

## Usage

Right click a DM in the sidebar.

| Option | |
|---|---|
| Delete All Messages | Confirms, then wipes. Run it again to stop |
| Dry Run (preview) | Scans and reports without deleting |
| Pause / Resume Wipe | Holds all requests |
| Cancel Wipe | Stops after the current request |
| Add / Remove from Wipe Queue | Queues this channel |
| Run Wipe Queue | Wipes every queued channel in order |
| Send Crash Report | Files a report from current state |
| DMWipe Stats | Lifetime counters and recent runs |

Or run `/wipe` in the channel, with optional `limit`, `delay` and `dry` args.

## Settings

| Setting | Default | |
|---|---|---|
| `delay` | 25 | Minimum gap between requests in ms |
| `adaptive` | on | Pace off Discord's rate limit headers |
| `concurrency` | 4 | Requests in flight, hides round-trip latency |
| `countFirst` | on | Scan first so progress and ETA are accurate |
| `backup` | off | Write every message to JSON before deleting |
| `keepPinned` | off | Filter: keep pinned messages |
| `keepLast` | 0 | Filter: keep the newest N messages |
| `keepDays` | 0 | Filter: keep messages newer than N days |
| `keepLinks` | off | Filter: keep messages containing a link |
| `keepAttachments` | off | Filter: keep messages with attachments |
| `keepReactions` | off | Filter: keep messages that have reactions |
| `keepBots` | off | Filter: keep messages sent by bots |
| `keepRegex` | | Filter: keep messages matching this regex |
| `stuckPasses` | 5 | Empty passes before giving up |
| `confirm` | on | Ask before deleting |
| `notifyOnFinish` | on | Desktop notification when a run ends |

## Notes

- DMs only, guild channels are not handled.
- Deleting is permanent and there is no undo. A dry run plus a backup costs about a minute.
- Bulk deletes are used where Discord allows it, but only cover messages under two weeks old.
- Messages you cannot delete in group DMs are counted as failed rather than stopping the run.
- the backups wont "restore" your message go into settings to enable confirmation first.
