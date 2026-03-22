# foss-demo — Demo Content for FOSS Projects

Assess demo needs for the current project and either generate simple demos inline or delegate to demo-forge for full production.

## Trigger

User says `/foss-demo` or asks to create a demo, recording, GIF, video, or screencast for a project.

## Instructions

### Step 1: Assess What's Needed

Read the project to understand:
- **What type of tool is this?** (MCP server, CLI tool, library, API)
- **What's the hero feature?** The one thing that would make someone star the repo.
- **Does a demo already exist?** Check for `demo/` directory, existing GIFs/SVGs in the repo.

### Step 2: Determine Demo Type

| Project Type | Best Demo Format | Who Builds It |
|-------------|-----------------|---------------|
| CLI tool | Terminal recording (GIF/SVG) | demo-forge |
| MCP server | Screen recording of agent using the tool | demo-forge |
| Library | Code snippet with output screenshot | Can do inline |
| API | Request/response flow diagram | Can do inline |

### Step 3: For Simple Demos (inline)

If the demo is just a code snippet + output or a diagram, generate it directly:

- Write the demo script to `demo/demo-script.sh`
- Run it and capture output
- Format for README embedding

### Step 4: For Production Demos (delegate to demo-forge)

For terminal recordings, screen captures, video content, or polished visual assets:

> **demo-forge** (`~/repos-eidos-agi/demo-forge`) is the dedicated forge for creating demo videos, images, and visual content. It handles recording, editing, branding, and optimization.

Tell the user:
```
This project needs a [terminal recording / screen capture / video demo].
Use demo-forge to create it: cd ~/repos-eidos-agi/demo-forge && /demo
```

### Step 5: README Integration

Regardless of how the demo is created, provide the README markdown to embed it:

For GIF:
```markdown
<p align="center">
  <img src="demo/demo.gif" alt="{{PROJECT_NAME}} demo" width="700">
</p>
```

For SVG:
```markdown
<p align="center">
  <img src="demo/demo.svg" alt="{{PROJECT_NAME}} demo" width="700">
</p>
```

Place immediately after the hero line and badges — above the fold.

## Demo Requirements (what foss-forge checks for)

`/foss-check` will look for:
- A demo exists (GIF, SVG, PNG, or video in `demo/` or repo root)
- README embeds it above the fold
- Demo file is ≤5MB (GitHub renders up to 10MB but smaller = faster load)
- Demo is ≤30 seconds (for recordings)

## Rules

- Don't try to build production demo content here — that's demo-forge's job.
- Do assess what kind of demo the project needs and how it should appear in the README.
- If demo-forge doesn't exist yet, generate the demo script inline and provide recording instructions.
