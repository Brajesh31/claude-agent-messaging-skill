# claude-agent-messaging-skill

A Claude Code skill for sending, receiving, and managing messages between AI agents using the Agent Messaging Protocol (AMP).

## Overview

This skill supports structured inter-agent communication. It covers agent identity initialization, message addressing, inbox operations, replies, priorities, attachments, and message-signing concepts.

The documented workflow supports local communication by default. External delivery requires the relevant provider and environment configuration.

## Main Capabilities

- Initialize a local agent identity.
- Send messages to another agent.
- Check and read incoming messages.
- Reply to existing messages.
- Use local and qualified agent addresses.
- Set message type and priority.
- Attach files where supported.
- Understand message signatures and identity verification.
- Manage private-key handling and communication boundaries.

## Prerequisites

The AMP command-line scripts must be installed and available on the system PATH. Basic local messaging can operate without an external delivery provider. External messaging may require additional configuration.

## Installation

Clone the repository into your skills directory:

```bash
git clone https://github.com/Brajesh31/claude-agent-messaging-skill.git ~/.claude/skills/agent-messaging
```

Install and configure the AMP CLI separately, following the setup steps in `SKILL.md`.

## Usage

Invoke the skill for agent communication tasks:

```text
/agent-messaging
```

Provide the sender identity, recipient address, subject, message body, priority, and any attachment requirements.

## Typical Workflow

1. Install the messaging command-line tools.
2. Initialize the local agent identity.
3. Confirm the recipient address.
4. Compose a message with a clear subject and body.
5. Send the message.
6. Check the inbox for replies.
7. Read and respond to relevant messages.
8. Verify delivery status where supported.

## Message Design

- Use stable agent identifiers.
- Keep subjects concise and specific.
- Include enough context for the recipient to act.
- State the expected response or next action.
- Use priority only when it reflects actual urgency.
- Avoid sending secrets or unnecessary personal data in message bodies.

## Security Considerations

The workflow describes signed messages and local private-key handling. Keep private keys on the machine that owns the identity. Restrict filesystem permissions, protect backups, and review the trust model before enabling external delivery or attachments.

## Repository Contents

- `SKILL.md`: Main AMP communication instructions.
- `README.md`: Setup assumptions, workflow, and security guidance.

## Troubleshooting

If a message cannot be sent, verify that the CLI is installed, the sender identity exists, the recipient address is valid, and the local environment has the required permissions. For external delivery, inspect provider configuration and service availability.

## Important Note

Message signatures help establish integrity and sender identity within the configured trust model. They do not guarantee that a message's contents are safe or trustworthy.
