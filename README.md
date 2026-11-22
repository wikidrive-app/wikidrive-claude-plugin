# WikiDrive for Claude

[WikiDrive](https://wikidrive.app) is a private wiki of your own working rules and documents. For each kind of work, such as reports, email, slides or code, it keeps the short rules you saved ("Put the conclusion in the first line") and the documents you asked to keep. The same WikiDrive works with the other AI apps you connect to it.

This plugin lets Claude use your WikiDrive. It contains the WikiDrive connector and seven skills. It has no hooks and no scripts: nothing in it runs on your computer, and it stores nothing on your computer.

## What Claude does with it

- **Loads your rules** for a kind of work when you ask ("use my WikiDrive report rules"), and may load them when you start a kind of work that is one of your WikiDrive topics, once per topic per conversation. What you say in the conversation wins over saved rules, and saved rules never authorize actions such as sending, publishing, buying or deleting.
- **Uses the Human Agents and prompts you enabled** in WikiDrive when they fit the task. A Human Agent is another person's shared way of working; you can share your own at [wikidrive.app/submit/agent](https://wikidrive.app/submit/agent) after admin approval.
- **Saves a rule** only when you ask ("save this to my WikiDrive"), and quotes what it saved in the chat.
- **Keeps a document** only when you ask ("keep this as a WikiDrive document"). Claude writes the document from the conversation; it never saves a transcript.
- **Finds and opens** your saved prompts and documents, and shows your usage counts, when you ask.
- **Undoes** the latest save when you say "undo". You can see, edit and delete everything at wikidrive.app.

## Get started

1. Create a WikiDrive account at [wikidrive.app](https://wikidrive.app). Signing up is free.
2. Add the plugin:
   - claude.ai, the desktop app and Cowork: Customize > Plugins > Discover, find WikiDrive, then Add.
   - Claude Code: `/plugin directory`, then WikiDrive. A plugin you add on claude.ai also reaches Claude Code.
3. Connect WikiDrive and sign in:
   - claude.ai, the desktop app and Cowork: open the plugin, select the Connectors tab, and connect WikiDrive.
   - Claude Code: type `/mcp`, choose `plugin:wikidrive:wikidrive`, then Authenticate.

If you used WikiDrive's own Claude Code plugin from wikidrive.app before, remove it first so Claude doesn't see the same tools twice: `claude plugin uninstall wikidrive@wikidrive`.

## Examples

- "Use my WikiDrive report rules and write this week's status report from these notes."
- "Save this to my WikiDrive: in every email, put the conclusion in the first line."
- "Keep the decisions from this meeting as a WikiDrive document."
- "Add today's decision to my Release checklist document in WikiDrive."
- "Find my onboarding checklist in WikiDrive."
- "Undo that." (right after a save)

## Commands

In Claude Code and Cowork, and from the `/` menu in chat, you can also run:

| Command | What it does |
|---|---|
| `/wikidrive:load report` | Loads your rules for a kind of work |
| `/wikidrive:save Put the conclusion first` | Saves a rule |
| `/wikidrive:keep Release checklist` | Keeps a write-up from the conversation as a document |
| `/wikidrive:undo` | Undoes the latest WikiDrive save in the conversation |
| `/wikidrive:find checklist` | Finds a saved prompt or document and opens it |
| `/wikidrive:stats` | Shows your WikiDrive usage counts |

Claude doesn't start these commands on its own: they run when you type them or ask for what they do.

## What is in this plugin

- `.mcp.json`: the WikiDrive connector, `https://wikidrive.app/mcp`, a remote MCP server with OAuth 2.0. You sign in on wikidrive.app; the plugin holds no password, key or token. The entry also sends the header `X-WikiDrive-Mode: directory`, which asks WikiDrive's server for the same instructions and tools it gives the WikiDrive connector in the Claude apps.
- `skills/wikidrive`: when and how Claude uses the WikiDrive tools, and what it never saves.
- `skills/load`, `skills/save`, `skills/keep`, `skills/undo`, `skills/find`, `skills/stats`: the commands above.

## Data

The plugin itself sends nothing and keeps nothing. Claude sends data to WikiDrive only through the connector's tools, over HTTPS, to your own WikiDrive account:

| When | What WikiDrive receives |
|---|---|
| Loading rules | a topic name of 1–3 words, and optionally a few words naming what is being made (not stored) |
| Searching | your search words (not stored) |
| Saving a rule | the short rules you asked to save |
| Changing or removing a rule | the rule as saved, and the new wording |
| Keeping or changing a document | the document text Claude wrote for you |
| Saving a prompt | the prompt you asked to save |
| Opening, undoing a document, usage counts | the ID of a prompt or document |

The plugin never sends your chat transcripts or files. WikiDrive refuses lines that look like passwords, keys or contact details. Saved rules and documents stay in your account until you delete them or close your account, and WikiDrive keeps usage counts without any text. Details and retention periods are in the [privacy policy](https://wikidrive.app/privacy). See also the [terms](https://wikidrive.app/terms).

## Same features in ChatGPT

The WikiDrive plugin for ChatGPT uses the same WikiDrive account and the same eleven tools. One difference is on purpose: in ChatGPT, WikiDrive can load and save on its own; in Claude, it saves only when you ask.

## Troubleshooting

- **Claude says WikiDrive isn't connected**: connect it as in Get started, step 3. A connection expires 90 days after it was last used; connect again.
- **Claude didn't use your rules**: say "use my WikiDrive rules for this", or run `/wikidrive:load` with the kind of work.
- **A save was refused**: WikiDrive refuses lines that look like secrets or contact details. Ask Claude to rewrite those lines.
- **A long document didn't save**: one call takes up to 12,000 characters. Ask Claude to save it in parts.
- **Something was saved by mistake**: say "undo", or delete it at wikidrive.app.

## Support

Open an issue at [github.com/wikidrive-app/wikidrive-claude-plugin](https://github.com/wikidrive-app/wikidrive-claude-plugin/issues), or email support@wikidrive.app.

## License

MIT, see LICENSE. The WikiDrive name and logo are not covered by the license.

## 한국어 안내

WikiDrive는 일의 종류마다 내가 정한 규칙과 남겨 둔 문서를 모아 두는 나만의 위키예요. 이 플러그인을 넣으면 Claude가 WikiDrive를 이렇게 써요.

- 내가 말하면 그 일의 규칙을 불러오고, 내 WikiDrive 주제에 있는 종류의 일을 시작할 때도 불러올 수 있어요. 대화마다 주제당 한 번이에요.
- 내 목록에 켜 둔 Human Agent와 담아 둔 프롬프트 중 지금 일에 맞는 것을 참고해요.
- 저장한 프롬프트·문서를 찾아 열고(`/wikidrive:find`), 사용량을 보여 줘요(`/wikidrive:stats`).
- 규칙 저장과 문서 정리는 내가 부탁할 때만 하고, 저장한 내용을 채팅에 보여 줘요. "취소"라고 하면 되돌려요.
- 플러그인 안에는 훅이나 스크립트가 없어요. 내 컴퓨터에서 아무것도 실행하지 않고, 컴퓨터에 아무것도 저장하지 않아요.
- 연결: claude.ai에서는 플러그인의 Connectors 탭에서 WikiDrive를 연결하고, Claude Code에서는 `/mcp` → `plugin:wikidrive:wikidrive` → Authenticate를 눌러요.
