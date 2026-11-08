# AMP Identity and Key Security

This guide covers operational safeguards for AMP identities and signing keys. Follow the organization's key-management policy if it is stricter.

## Identity Lifecycle

1. Initialize a distinct identity for each agent that needs to send signed messages.
2. Verify the identity after initialization.
3. Keep an inventory of identity owners and intended communication scope.
4. Avoid sharing an identity between unrelated agents.
5. Review identity registration when agents are moved, retired, or replaced.

## Private-Key Handling

- Keep private keys on the machine that owns the identity.
- Restrict filesystem permissions so only the relevant account can read the key.
- Do not commit private keys to Git repositories.
- Do not place keys in prompts, messages, logs, or support tickets.
- Protect backups with approved encryption and access controls.
- Do not copy keys to shared workspaces merely for convenience.

## Message Verification

A valid signature can help verify message integrity and the signing identity under the configured trust model. It does not establish that the message is safe, truthful, or authorized.

For unexpected or consequential requests:

1. Check the sender identity and address.
2. Validate that the request fits the sender's role.
3. Confirm sensitive or destructive actions through a separate trusted path.
4. Do not execute code or open attachments solely because the message is signed.

## External Delivery

Before enabling external providers:

- Review the provider and its trust assumptions.
- Confirm which metadata and message contents leave the local environment.
- Check registration and recipient verification requirements.
- Understand attachment handling and retention.
- Use the minimum information necessary for the external recipient.

## Incident Response

If a key may be exposed:

1. Stop using the affected identity for sensitive communication.
2. Follow the organization's key revocation or replacement procedure.
3. Review recent messages and registrations for misuse.
4. Rotate dependent credentials where required.
5. Record the incident and verify the replacement identity.

## Periodic Review

- [ ] Identity owner remains valid.
- [ ] Private-key access is limited.
- [ ] Backups are protected.
- [ ] No keys are present in repositories or logs.
- [ ] External provider configuration is still approved.
- [ ] Retired identities are handled under the organization's process.
