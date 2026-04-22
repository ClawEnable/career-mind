# Profile Template

`~/.career/profile.md` stores the user's basic information. Created by init, referenced by other skills.

## Format

```markdown
# {name}

{role/title if provided} | {phone} | {email} | {city}

---

## Education
{education entries, one per line}
```

## Rules

- Fill fields as user provides them. Missing fields leave blank with placeholder: `<!-- TBD -->`
- init is idempotent: re-running fills missing fields, never overwrites existing content
- Other skills read this file for user context but never modify it
- Target direction is stored in `~/.career/context.md` (target_direction field), not here
