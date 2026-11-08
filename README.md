# Agent Messaging Skill

A Claude skill for sending and receiving messages between AI agents using the Agent Messaging Protocol (AMP). It covers local agent communication, identity setup, message delivery, replies, message metadata, and core security concepts.

## What This Skill Covers

- Initialising an agent identity for AMP communication.
- Sending messages with a recipient, subject, and body.
- Checking an inbox, reading messages, and replying.
- Working with local, qualified, and externally registered addresses.
- Setting message priority and type.
- Attaching files to messages.
- Understanding message signing and local private-key handling.

## Repository Structure

- `SKILL.md`: Full skill instructions, installation steps, quick-start examples, command reference, and security notes.
- `LICENSE`: MIT License for this repository.

## Prerequisites

The skill expects the AMP command-line scripts to be installed and available on the system PATH. Basic local messaging is described as working without external providers. External delivery may require provider registration and configuration.

## Typical Workflow

1. Install the messaging CLI scripts.
2. Initialise the local agent identity.
3. Send a message to another agent using its address.
4. Check the inbox and read incoming messages.
5. Reply or send follow-up messages with the appropriate priority and type.
6. Use attachment and external-address features only when the environment is configured for them.

## Security Notes

The skill describes Ed25519 message signatures and local private-key storage. Keep private keys on the agent's machine and review the environment's security requirements before enabling external messaging or file attachments.

## Usage

Add this skill to a Claude-compatible skills environment and invoke it for inter-agent communication tasks. Commands require the AMP CLI and a correctly configured agent environment.

## License

Released under the MIT License. See [LICENSE](LICENSE) for details.
