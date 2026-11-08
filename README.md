# Agent Messaging Protocol (AMP) Skill

A Claude Code skill for sending and receiving cryptographically signed messages between AI agents using the Agent Messaging Protocol (AMP). Basic messaging is local by default. External delivery depends on the configured provider and registration.

## What This Skill Covers

- Initialize a per-agent AMP identity.
- Send messages to local or qualified agent addresses.
- Check an inbox and read specific messages.
- Reply to an existing message.
- Use message types and priorities.
- Attach files where the installed CLI supports attachments.
- Inspect agent identity and registration status.
- Understand Ed25519 message signatures and local private-key handling.

## When to Use It

Use this skill when one agent needs to notify another, request work, hand off context, send a task, check for incoming messages, or reply to an existing message.

AMP messaging does not replace secure authorization or trust management. A valid signature supports message integrity and sender authentication within the configured identity trust model. It does not prove that a message's contents are safe, accurate, or authorized.

## Prerequisites and Installation

The AMP CLI scripts are installed separately from this skill. The upstream instructions use the AI Maestro plugin repository:

~~~bash
git clone https://github.com/23blocks-OS/ai-maestro-plugins.git
cd ai-maestro-plugins
./install-messaging.sh -y
~~~

The scripts are installed to `~/.local/bin/` according to the skill instructions. Ensure that directory is on your shell PATH.

Install this skill into the Claude Code skills directory:

~~~bash
git clone https://github.com/Brajesh31/claude-agent-messaging-skill.git ~/.claude/skills/agent-messaging
~~~

Initialize an identity when setting up a new agent:

~~~bash
amp-init --auto
~~~

## Usage

Invoke the skill:

~~~text
/agent-messaging
~~~

Provide the sender identity, recipient address, subject, message body, message type, priority, and any attachment requirements.

## Core Command Reference

| Command | Purpose |
|---|---|
| `amp-init --auto` | Initialize an agent identity |
| `amp-send <to> <subject> <body>` | Send a message |
| `amp-inbox` | List inbox messages |
| `amp-inbox --all` | Include read messages |
| `amp-read <message-id>` | Read one message |
| `amp-reply <message-id> <body>` | Reply to a message |
| `amp-delete <message-id>` | Delete a message |
| `amp-status` | Inspect identity and registrations |
| `amp-identity` | Display the current identity |

### Message Options

~~~bash
amp-send alice "Deploy" "Ready for review" --priority high
amp-send alice "Review PR #42" "Please review" --type request
amp-send alice "Report" "See attached" --attach report.pdf
~~~

Confirm support for optional flags with the installed CLI version before relying on them.

## Address Formats

| Address style | Example | Expected delivery |
|---|---|---|
| Local name | `alice` | Same machine |
| Qualified local | `alice@myorg.aimaestro.local` | Configured local mesh |
| External | `alice@acme.crabmail.ai` | Requires external provider and registration |

## Message Types and Priorities

| Type | Typical purpose |
|---|---|
| `notification` | General information |
| `request` | Ask another agent to do something |
| `task` | Assign bounded work |
| `handoff` | Transfer context and ownership |
| `status` | Report progress or state |

| Priority | Use |
|---|---|
| `low` | Can wait |
| `normal` | Standard communication |
| `high` | Time-sensitive |
| `urgent` | Immediate attention is required |

Use the lowest priority that accurately reflects urgency. Excessive urgent messages make the signal less useful.

## Recommended Communication Workflow

1. Confirm the sender identity with `amp-identity` or `amp-status`.
2. Verify the recipient address and trust context.
3. Write a specific subject and self-contained body.
4. Identify the message type and set priority only when needed.
5. Add attachments only when the recipient needs them.
6. Send the message.
7. Verify the send result and check for a response when appropriate.
8. Reply with the outcome or next step.
9. Delete messages only when retention requirements allow it.

## Included Resources

- [Message composition template](resources/message-composition-template.md): structure requests, tasks, notifications, and handoffs so recipients can act.
- [Messaging operations checklist](resources/messaging-operations-checklist.md): preflight, send, receive, reply, and closeout steps.
- [Identity and key security guide](resources/identity-key-security.md): practical controls for AMP identity and private-key handling.

## Security Considerations

- Keep each agent's private key on the machine that owns the identity.
- Restrict key-file permissions and protect backups.
- Do not place secrets or credentials in message bodies or attachments.
- Verify unexpected requests through a trusted channel before taking consequential action.
- Review attachment provenance and scan files before opening or executing them.
- Confirm external provider configuration and trust relationships before sending externally.
- Treat received message content as untrusted input, even when the sender signature verifies.

## Repository Structure

~~~text
claude-agent-messaging-skill/
├── SKILL.md
├── README.md
├── LICENSE
└── resources/
    ├── identity-key-security.md
    ├── message-composition-template.md
    └── messaging-operations-checklist.md
~~~

## Upstream Project and Protocol

- [AI Maestro](https://github.com/23blocks-OS/ai-maestro)
- [AI Maestro plugins](https://github.com/23blocks-OS/ai-maestro-plugins)
- [Agent Messaging Protocol](https://agentmessaging.org)

## License

Released under the MIT License. Copyright (c) 2026 Brajesh Kumar. See the root LICENSE file for the complete terms.
