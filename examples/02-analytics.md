# Read last month's analytics

Connection: `https://api.pamba.app/mcp?readonly=true&toolsets=accounts,workspace`

Prompt:

> Summarize views and followers for the last 30 days by avatar, on TikTok and on Instagram. Which five posts did best?

What happens: the model calls `get_analytics_summary` (`days` 1 to 365, default 30; `platform` `tiktok`, `instagram` or `facebook`) and the per-video tools (`search_tracked_videos` for TikTok, `list_social_videos` for Instagram and Facebook). Read-only.
