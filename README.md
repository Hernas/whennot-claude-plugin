# WhenNOT for Claude

Find dates that work for everyone, and book calls, from Claude. This plugin connects Claude to your
WhenNOT account and adds four workflows:

| Skill | Ask for example |
|---|---|
| `plan-group-dates` | "Find a weekend in November for a team offsite." |
| `poll-follow-up` | "Who still hasn't answered my poll? Remind them, then pick the best dates." |
| `answer-invitation` | "I was invited to Board game night. I can't do the 14th." |
| `book-a-call` | "Book a 30-minute call on whennot.com/m/<page> next week." |

WhenNOT turns scheduling around: people mark the days they **cannot** make, and WhenNOT shows the
dates with the fewest conflicts. With this plugin Claude can create a poll for days or for time
slots, invite people by email, show who has answered and the best dates, remind the people who have
not answered and pick the final dates. It can answer a poll you were invited to, as you. For
one-to-one calls it lists your booking pages and bookings, finds the open times on any WhenNOT
booking page, and books, moves or cancels a time. Before Claude sends email, books or cancels
anything, it tells you what it will do and waits for your yes.

## Connect

1. Install the plugin. It adds the WhenNOT MCP server `https://whennot.com/api/mcp`.
2. In Claude, connect WhenNOT. A WhenNOT page opens: sign in with your email, Google or Apple.
3. Choose what Claude may use and select **Allow**.

WhenNOT works with a free account.

Install in Claude Code from this repository:

```
/plugin marketplace add Hernas/whennot-claude-plugin
/plugin install whennot@whennot
```

## Access (OAuth scopes)

You approve the two permissions separately:

- `polls`: create polls, read results, invite and remind people, pick final dates, answer polls.
- `bookings`: list your booking pages and bookings, find open times, book, move and cancel.

Claude never gets your password, and no tool returns a secret edit or manage link. WhenNOT does not
receive your conversation, only the arguments of the tool calls. To disconnect, open **Profile →
Connected apps** on whennot.com and select **Disconnect**, or remove the connection in Claude's
settings.

Account deletion is not part of the plugin: delete your account on
[whennot.com/account/delete](https://whennot.com/account/delete).

## Privacy and support

- About the integration: https://whennot.com/apps
- Privacy policy: https://whennot.com/privacy-policy
- Terms of service: https://whennot.com/terms-of-service
- Support: support@whennot.com, https://whennot.com/contact

## License

MIT. See [LICENSE](LICENSE).
