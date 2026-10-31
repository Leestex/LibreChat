# QLANE.md

LibreChat is a chat app: people sign in, talk to AI models in conversations, and organise, reuse and share those conversations. In this test stack, every model reply comes from a local mock model ("Mock", models `mock-gpt` and `mock-gpt-mini`), so a reply always arrives and can be checked without real provider keys.

## Critical flows

### P0
- Sign in with email and password, see the chat screen, then use "Log out" and land back on the sign-in page.
- Sign up as a new user from the sign-in page, then sign in with the new account; it starts with no conversations.
- Start a "New chat", send a message, and see the reply stream in; the conversation then appears in the sidebar's conversation list.
- Open an earlier conversation from the sidebar and see its full message history; continue it with another message.
- Rename a conversation from its menu, and see the new name in the sidebar; delete a conversation, and see it disappear from the list.
- Stop a reply while it is still streaming, and see the partial reply kept.
- Share a conversation: "Share", then "Create a shared link"; open the link signed out and see the conversation read-only. The link is listed under Settings, "Shared chats", where deleting it makes the link stop working.

### P1
- Edit a sent message and resend it, or regenerate a reply, and see the new reply replace the old one in the conversation.
- "Fork" a conversation from a message, and see a new conversation with the history up to that message.
- "Archive" a conversation; it leaves the sidebar and appears under Settings, "Archived chats", where it can be restored.
- Save the current model and parameters as a preset, start a new chat from that preset, and see its settings applied.
- "Bookmarks": create a bookmark, add it to a conversation, and filter the sidebar by it.
- Prompts: create a prompt in the prompt library, then insert it into a new message.
- Agents: create an agent in the Agent Builder with a mock model, chat with it, and see it reply.
- "Temporary Chat": a conversation started this way is not kept in the sidebar.
- "Export conversation" downloads the conversation; importing an exported file adds it to the list.

## Accounts and roles
- **Admin User** (`admin@example.com`): LibreChat's admin role. Can do everything a user can, and sees "Admin Settings" in the Prompts, Agents and Memories panels, which set what the user role may do.
- **QA User** (`qa@example.com`): the user role. No "Admin Settings" anywhere; a refused or missing admin control is expected for this account, not a bug.
- New sign-ups get the user role. Email verification is off in this stack, so a new account can sign in straight away.
- Flows that check a permission boundary need both accounts.
- Conversations, presets, bookmarks and prompts belong to the account that made them: one user never sees another's, except through a shared link or a prompt or agent shared with them.

## Areas to skip
- Message search ("Search messages"): its search service is not part of this test stack, so search is unavailable here.
- File search and document uploads for answers: their retrieval service is not part of this test stack.
- Real model providers (OpenAI, Anthropic and others): no keys are configured; only the mock model answers.
- Social and single sign-on login: turned off in this stack.
- Password reset by email: this stack sends no email.
