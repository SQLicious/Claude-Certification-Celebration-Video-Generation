# Video Clip Drop Folder

Export Google Flow, Higgsfield, or other AI video clips into this folder.

Use these exact filenames:

```text
shot-01-exam-citadel.mp4
shot-02-agentic-architecture.mp4
shot-03-tools-mcp.mp4
shot-04-claude-code-workflows.mp4
shot-05-prompt-structured-output.mp4
shot-06-context-reliability.mp4
shot-07-final-boss.mp4
shot-08-victory-certified.mp4
```

Then run:

```powershell
npm run render
```

The render command runs `npm run sync:clips` first. Synced clips are copied to `public/assets/clips`, and Remotion uses clips when present. Missing clips fall back to still images.
