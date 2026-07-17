# Troubleshooting

This document records all incidents encountered during the development of the project, including their symptoms, root cause, solution, verification process, and current status.

---

# Incident 001 - GitHub displayed commits as "Unverified"

## Date

2026-07-17

## Symptoms

- Git locally reported:

```text
Good "git" signature
```

- GitHub displayed the commit as:

```text
Unverified
```

## Root Cause

The SSH key intended for commit signing was mistakenly registered in GitHub as an **Authentication Key** instead of a **Signing Key**.

## Diagnosis

Verify the commit signature locally:

```bash
git log --show-signature -1
```

Verify Git signing configuration:

```bash
git config --global --list | grep signing
```

## Resolution

1. Remove the SSH key registered as an Authentication Key.
2. Navigate to:

```
GitHub
→ Settings
→ SSH and GPG Keys
→ New SSH Key
```

3. Select:

```
Key Type
↓

Signing Key
```

4. Register the signing key:

```bash
cat ~/.ssh/id_ed25519_signing.pub
```

5. Create and push a new signed commit.

## Verification

```bash
git log --show-signature -1
```

Expected result:

```text
Good "git" signature
```

GitHub displays:

```text
Verified
```

## Status

Resolved

---

# Future Incidents

Every issue encountered during the project lifecycle should be documented using the same structure:

- Date
- Symptoms
- Root Cause
- Diagnosis
- Resolution
- Verification
- Status
