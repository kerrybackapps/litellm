# LiteLLM Proxy Admin Guide

## Proxy URL
```
https://litellm-kerrybackapps-cd4f3edf.koyeb.app
```

## Admin Panel Access

1. Navigate to: `https://litellm-kerrybackapps-cd4f3edf.koyeb.app/ui`
2. Login with the master key: `sk-litellm-mgmt675-2026`

## Switching the Course Model

The proxy exposes a single model alias `course-model` to students. To change which backend model this points to:

1. Go to the **Models** section in the admin panel
2. Find `course-model` in the model list
3. Click **Edit** to modify the configuration
4. Change the `model` parameter to any OpenRouter model ID, for example:
   - `openrouter/moonshotai/kimi-k2.5` (default - Kimi K2.5)
   - `openrouter/anthropic/claude-3.5-sonnet` (Claude 3.5 Sonnet)
   - `openrouter/openai/gpt-4o` (GPT-4o)
   - See all options at https://openrouter.ai/models
5. Save the changes

Students do not need to update their configurations—their `course-model` requests will automatically route to the new backend.

## Creating Student API Keys (Optional)

To issue individual keys with spend limits:

1. Go to the **Virtual Keys** section
2. Click **Create Key**
3. Set:
   - **Key Alias**: Student name or identifier
   - **Max Budget**: Spend limit (e.g., $10)
   - **Budget Duration**: Reset period (e.g., 30 days)
   - **Models**: Select `course-model`
4. Share the generated key with the student

Students use their individual key in place of the master key in their settings.

## Monitoring Usage

- **Dashboard**: View total requests, tokens, and spend at `/ui`
- **Logs**: Access detailed request logs per key
- **Alerts**: Set up spend alerts in the Settings section

## Cost Control

The proxy connects to OpenRouter, which provides unified pricing across providers. Current pricing examples:
- Kimi K2.5: $0.45/M input, $2.20/M output
- Claude 3.5 Sonnet: ~$3/M input, $15/M output
- GPT-4o: ~$2.50/M input, $10/M output

Monitor the dashboard regularly. Revoke keys or change the master key if costs exceed expectations.

## Troubleshooting

**Students report "Authentication Error"**
- Verify they're using the correct key (`sk-litellm-mgmt675-2026` or their individual key)
- Check that their `ANTHROPIC_BASE_URL` is set correctly

**Model not responding**
- Check OpenRouter status: https://status.openrouter.ai
- Verify the model ID in the proxy configuration
- Check proxy logs in the Koyeb dashboard

**Need to revoke access immediately**
- Rotate the master key in Koyeb secrets
- Restart the service to apply changes
- All students must update their configs
