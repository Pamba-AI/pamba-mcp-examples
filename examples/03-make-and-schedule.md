# Make a video and schedule it

Connection: `https://api.pamba.app/mcp?max_credits=1000`

This spends credits and publishes a public post. Run it in a workspace whose accounts you are happy to post from.

Prompt:

> Using my avatar Maya, write a 20-second talking video about our app's new budgeting feature, generate it, and show it to me before scheduling anything. If I approve it, schedule it to Maya's TikTok tomorrow at 6pm Pacific with the AI label on.

What happens: the model creates a project for the avatar, generates and renders the video, and waits for your approval. On approval it calls `schedule_post` with `scheduled_at`, `tiktok_username` and `ai_label: true`. A post goes out only if its project is approved at its slot.

Replace "Maya" and the topic with your own avatar and product.
