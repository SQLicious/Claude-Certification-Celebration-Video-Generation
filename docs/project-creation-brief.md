# Project Creation Brief: Anthropic Claude Certified Architect Trailer

## Project Goal

Create a cinematic celebration trailer for passing the Anthropic Claude Certified Architect exam. The idea was to turn the certification journey into a futuristic game-style quest: entering an exam arena, clearing multiple skill domains, facing a final boss, and ending with a certified victory frame.

The final video is not a static slideshow. It is a Remotion-built trailer assembled from AI-generated video clips, timed to the full length of every uploaded clip, with cinematic overlays, level labels, topic callouts, loot/power-up language, and a corrected final certification badge.

Final export:

```text
out/certified-trailer.mp4
```

Final format:

```text
1920x1080
30 fps
2252 frames
About 75 seconds
```

## Original Creative Concept

The first idea was a Mario-style or action-game inspired journey where the main character moves through obstacles representing exam concepts. The tone evolved into a photorealistic futuristic arena: part game trailer, part professional certification celebration.

Core metaphor:

```text
Certification exam = final boss
Exam domains = game levels
Skills = power-ups
Concept mastery = loot drops
Passing = victory frame
```

The protagonist is based on a real photo reference, transformed into a futuristic professional character with a metallic burgundy jacket, cream blouse, black tactical trousers, and confident game-hero styling.

## Tools Used

- Gemini Nano Banana / image generation prompts for character and scene stills
- Higgsfield / AI video generation exploration for cinematic clips
- Uploaded AI video clips in `assets/video`
- Remotion for final programmable video assembly
- React / CSS for text overlays, masks, timing, and cinematic composition
- `@remotion/media-parser` to read real clip durations
- Local project folders for assets, stills, clips, prompts, docs, tests, and output

## Story Structure

The trailer became an 8-shot journey:

1. Arena Entry: The Exam Citadel
2. Level 1: Agentic Architecture
3. Level 2: Tools + MCP
4. Level 3: Claude Code Workflows
5. Level 4: Prompt Engineering + Structured Outputs
6. Level 5: Context + Reliability
7. Final Boss: Certified Architect Foundations Exam
8. Victory Frame: Anthropic Claude Certified Architect

The main game loop was:

```text
Enter chamber -> face obstacle -> defeat mini-boss -> collect artifact -> unlock next gate
```

Artifacts / power-ups:

```text
Orchestration Core
MCP Key
Workflow Gauntlet
Schema Lens
Memory Compass
Certification Emblem
```

## Production Evolution

The first Remotion version looked too much like static slides. The direction changed toward a real cinematic trailer by using the uploaded video clips as the primary visual layer and making Remotion handle only the editorial structure, overlays, timing, and final polish.

Important production decisions:

- Use all canonical uploaded MP4 clips.
- Do not trim or snip the videos.
- Let the final Remotion composition expand beyond 60 seconds if needed.
- Read actual clip duration from metadata.
- Build the timeline from real video length instead of a hardcoded duration.
- Keep overlays informative but not so heavy that they cover the cinematic scenes.

The final timeline synced 8 of 8 clips and rendered at about 75 seconds.

## Key Iterations

### Opening Shot

The original first frame was too busy. It had a large title, a lower-left card, `Cold Open`, topic chips, and artifact text. That made the rich citadel image feel blocked.

We simplified it in stages:

1. Removed `Cold Open`.
2. Removed the heavy lower-left intro card.
3. Added back just enough context: `CCA-F Exam Arena`, `Welcome to the Exam Citadel`, `5 Domains`, `1 Attempt`.
4. Moved the opening text to the upper-left.
5. Made it appear for about 3 seconds, then fade out.

Final opening behavior:

```text
Short HUD-style flash, then the citadel image is allowed to breathe.
```

### Level Overlays

Each level keeps a clear label, exam-topic chips, and a power-up/artifact line. These overlays are useful because they explain what each game level represents.

Examples:

```text
Agentic Architecture -> agent orchestration, planner-executor loops, multi-agent coordination
Tools + MCP -> MCP servers, tool schemas, connector contracts
Prompt Engineering + Structured Outputs -> clear constraints, examples and rubrics, JSON schemas
Context + Reliability -> context windows, memory and retrieval, evals and verification
```

### Final Certification Frame

The last uploaded victory video had incorrect text baked into the video: `Claude Code Certified Foundations`. Since the text was part of the generated video pixels, it could not be changed directly through normal Remotion text editing.

The practical fix was:

1. Add a cinematic matte over the left-side baked-in text.
2. Overlay the correct final title: `Anthropic Claude Certified Architect`.
3. Add a compact certificate badge preview using the local certificate image.
4. Keep the overlay visible through the entire final shot so the baked-in wrong text never reappears.

The badge was first tried as a circular crop, but that cut off the words inside the certificate image. It was changed to a compact rounded certificate preview so the badge renders cleanly.

Final certification overlay:

```text
Badge preview + Anthropic Claude Certified Architect
```

## Engineering Work

The Remotion project was updated so the video length is data-driven.

Implemented pieces:

- `scripts/sync-video-clips.mjs` copies canonical videos into `public/assets/clips`.
- The same script reads each MP4 duration with `@remotion/media-parser`.
- Generated metadata stores clip availability and frame duration.
- `src/timeline.js` calculates sequence start frames and total composition duration.
- `src/Root.tsx` uses the computed full timeline duration.
- `src/Trailer.tsx` renders every shot as a Remotion sequence.
- `OffthreadVideo` is used for the full video clips.
- CSS handles cinematic grading, letterbox, level cards, opening HUD flash, final matte, and certification badge.

Verification commands used repeatedly:

```text
npm test
npx remotion compositions src/index.ts
npm run render
```

Final verification:

```text
8/8 clips synced
3/3 tests passing
Composition: 2252 frames, 75.07 seconds, 1920x1080
Rendered MP4: about 75.115 seconds, 1920x1080
```

## Lessons From The Process

- AI video generation can create cinematic scenes, but programmatic assembly is still needed for consistency, timing, and corrections.
- Remotion is useful because it gives precise control over overlays, duration, and final export.
- Generated video text is risky because it can be wrong and hard to remove later.
- It is better to keep important text in Remotion overlays whenever possible.
- A short contextual overlay can be more effective than a full title card.
- The best final result came from iteration: storyboard -> generated stills -> generated video clips -> Remotion assembly -> visual review -> corrections.
