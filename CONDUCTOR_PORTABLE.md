# Conductor Portable - Cross-Platform Implementation Guide

**YOUR JOB**: Bootstrap Conductor for OpenCode. Execute the steps below, then hand control to the user.

---

## EXECUTE THESE STEPS NOW

### 1. Create Directory Structure
```bash
mkdir -p .opencode/commands/conductor
```

### 2. Convert Commands (Automated)
Run this to convert all 6 TOML commands:
```bash
python3 -c "
import tomllib
for f in ['setup','newTrack','implement','status','revert','review']:
    with open(f'commands/conductor/{f}.toml', 'rb') as g: d = tomllib.load(g)
    with open(f'.opencode/commands/conductor/{f}.md', 'w') as h:
        h.write('---\n')
        h.write(f'description: \"{d[\"description\"]}\"\n')
        h.write('---\n')
        h.write(d['prompt'].replace('{{args}}', '\$ARGUMENTS'))
"
```

### 3. Create opencode.json
```bash
cat > .opencode/opencode.json << 'EOF'
{
  "permission": { "*": "ask", "bash": "allow" },
  "agent": { "plan": { "mode": "primary", "permission": { "edit": "ask", "write": "ask", "bash": "ask" } } }
}
EOF
```

### 4. Verify Commands Loaded
Confirm the commands are recognized:
```bash
ls -la .opencode/commands/conductor/
```

---

## WHAT'S DONE

- **Commands converted**: setup, newTrack, implement, status, revert, review
- **Permissions configured**: Plan mode enabled for conductor/ directory
- **Source of truth**: `commands/conductor/*.toml` (upstream)

---

## NEXT STEP - HAND TO USER

Tell the user:

> **Conductor is ready!** Run `/conductor:setup` to initialize your project.
> 
> You're now interoperable with Gemini CLI teammates using the same Conductor workflow.

That's it. Done.