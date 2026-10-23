---
name: second-world-collage
description: >-
  Use when the user wants a second-world paper collage from a photo (travel
  still → half photo / half warm-paper collage), a scrapbook poster, an animated
  GIF of one, or "拼贴第二世界" without configuring any API key.
---
# Second-world collage (@uselesssoso)

Turn one still photo into a 3:4 vertical collage: upper half = the same photo (faithful), lower half = a warm-paper second world invented from that photo. Optionally animate it into a looping GIF. No vendor keys, no PowerTokens branding. Sign work @uselesssoso when you publish or caption it.

## Intake
- Need: the photo (attachment path or URL).
- Optional: mood, caption language (default English), figures (default auto: 0–3), whether they want a GIF.
- Do **not** ask the user for Base URL, API keys, or model paths. Use the assistant’s own image and video tools.
- Do **not** dump the long model prompt into chat. Keep observe → invent → prompt internal.
- If the source is a social-app screenshot, crop out the app UI before using it as reference.

## Pipeline (always)
1. **Observe** the photo. List 3–6 structures (wave, road, reflection, cloud edge, branch, light shaft, shadow, ridge, building line, pose, boat…). Pick **one** that can become touchable or usable.
2. **Invent** one second-world beat that only works for **this** photo (pull, enter, scoop, measure, mend, unfold, climb, connect, gather, sail…). Never reuse a fixed torn-edge + stick-figure template.
3. **Caption**: one short handwritten-feel English line. Light humor. Not motivational. Not “Same… different.” Do not invent facts (crowd sizes, dates); if a number is used, look it up or keep it vague.
4. Build the image prompt from the template below (~<500 English words).
5. Generate with the photo as a **reference image** so the upper half stays the same still.
6. Deliver the image. One or two sentences in chat: what structure you used + the caption. Offer a redo, and offer the GIF step.
7. **Iterate by editing, not redrawing**: when the user asks for a change, pass the previous collage as the reference and change only what they asked for.

## Canvas (always)
- 3:4 vertical (prefer 1536×2048 when the tool allows; otherwise closest portrait ratio).
- Split exactly in half: upper photo / lower paper.
- Upper: faithful original (subject, pose, space, color, natural light). Crop only if needed. No recolor, no filter, no redraw of the photo.
- Lower: warm off-white / cream **paper base** (not sand beach), with large empty margins. Not a second photo. Not a dense illustration.

## Supporting mini-world (required on lower half)
Warm paper alone is not enough. From the chosen structure at the collage cut, **spread a small supporting ground onto the paper** so the structure feels held. Do this on the same composition; do **not** redraw the structure as a separate ink sketch floating lower down.
- Boat / vessel → a small patch of blue sea watercolor bleeding out from under the hull onto the cream paper
- Path / road / runway → a short continuation of the road spilling from the cut onto the paper
- Door / window / screen → a small threshold, step, or room floor spreading from the opening
- Tree / branch → a little mound of paper earth or root lines under it at the cut
- Light / lamp / stage light → a soft pool of light on the paper near the source
- Mountain / dune / ridge → a thin paper contour continuing the ridge past the cut
Keep it **minimal**: one small bloom near the structure, restrained wash, not a full landscape. Apply the same idea to any other entity.

## Collage edge
The cut must **read** the photo (pond silhouette, light rectangle, road band, cloud fan, building outline, hull line). Do not use the same generic jagged tear every time.

## Figures (0–3)
Minimal black line figures only if they are **using** the chosen structure. If the upper half already has strong action, skip figures. Never crowd into comic panels.

## Prompt template (for the model, not the user)
```
3:4 vertical poster, canvas split exactly in half.
Upper half: [faithful description of the uploaded photo — keep subject, pose, space, color, natural light; only necessary crop]. Use the reference image as the upper photograph.
Lower half: warm off-white cream paper base, large empty margins (paper, not beach sand).
[One sentence: the photo-specific second-world beat + how the cut shape follows the photo.]
[Required: from the structure at the cut edge, spread a SMALL supporting mini-world onto the paper — e.g. blue sea watercolor bleeding from under a boat hull; do NOT redraw the structure as a separate sketch lower on the page; keep most paper empty.]
[0–3 line figures and what they are doing, or "no added figures".]
Handwritten English caption "[line]" placed [where].
Style: real photo + warm paper + small supporting ground blooming from the cut + minimal black ink doodle; clean bright restrained handmade collage, indie magazine print.
Avoid: empty bare paper with floating objects, redrawing the main structure as a second ink drawing, full beach/sand or full ocean fill of the lower half, ad look, dense illustration, crowded figures, generic torn edge, random stickers, recoloring the original photo, logos, watermarks, famous landmarks not in the photo.
```

## GIF step (when the user wants it to move)
1. Image-to-video from the **approved still**: set it as both first frame and last frame so the clip loops seamlessly. 3:4, ~4 s, 720p.
2. Motion rules:
   - **Motion split (default):** the upper photo subject stays still or only micro-moves (tiny shimmer, almost a still). The **lower collage / splice** is what moves — sand drifts, sea ripples, figures walk, light pulses. No camera move, no zoom.
   - **Decide lower-half motion from the situation.** Ask: in this second world, what would naturally happen on the paper side? Then animate that, clearly visible but quiet mood (not spectacle; no big floating or bouncing unless asked).
     - Boat collage → the paper sea ripples; the photo boat stays put (or micro-tilt only if asked).
     - Dune / sand collage → sand drifts down the paper dune; tiny paper figures climb.
     - Road collage → a tiny walker or car moves along the paper road.
     - Door / window collage → the paper threshold or light inside shifts slightly.
     - Lamp collage → the paper light pool soft-pulses.
     - Tree collage → paper leaves or wind lines sway.
     These are examples for the **lower half**. Upper photo stays still unless the user asks otherwise.
   - Keep layout and caption locked; motion lives in the splice world.
   - Paper, layout and caption stay locked.
3. Motion prompt shape: `Subtle seamless loop of this exact collage. Upper photo subject still or micro-move only. Lower collage clearly moves: [what naturally happens on the paper side], quiet mood. Paper and caption fixed. No camera move, keep layout locked, calm handmade feel.`
4. If image-to-video leaves the lower half still (check by comparing frames), fall back to **programmatic motion** on the paper mini-world only (wave displace / shimmer the sea, sand, light pool). Keep the upper photo pixel-locked.
5. Convert to GIF: `ffmpeg -y -i in.mp4 -vf "fps=12,scale=540:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=128[p];[s1][p]paletteuse=dither=bayer:bayer_scale=3" out.gif` (about 4 MB). Offer the MP4 too.
6. Deliver the GIF as an attachment, then one line on what moves.

## QA before sending
- [ ] 3:4, upper/lower ~1:1
- [ ] Upper half is recognizably **this** photo
- [ ] Lower half is warm paper + whitespace (not full sand/beach)
- [ ] Supporting mini-world blooms from the structure at the cut (not a separate redrawn object)
- [ ] Second-world beat names a structure from the photo
- [ ] Collage edge relates to the photo
- [ ] ≤3 figures, and they are doing something
- [ ] One short English caption, no invented facts
- [ ] No logo / travel-ad look / PowerTokens branding
- [ ] GIF: loops cleanly, the motion fits what the subject would really do in that setting, mini-world reacts with it, photo and caption stay put

## Out of scope
- Do not require user-supplied API keys.
- Do not route through PowerTokens media-skills or company billing.
