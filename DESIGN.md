# Design Plan - Nydo

## Design Read

Nydo should read as a trust-first student housing landing and product brand for incoming international students, with a warm premium consumer language. The visual system should feel custom to Nydo rather than like a generic SaaS template.

Design dials:

- DESIGN_VARIANCE: 7
- MOTION_INTENSITY: 5
- VISUAL_DENSITY: 4

Rationale: Nydo needs to feel calmer and more trustworthy than a social app, but warmer and more human than a housing marketplace. Motion should guide attention and show state changes.

## Core Feeling

Nydo should feel like the first calm moment in a chaotic housing search. The design needs to say: verified people, better fit, less pressure, safer decisions. The brand should feel warm enough for students and polished enough for parents, universities, agencies, and investors.

Avoid startup-template energy. No purple AI gradients, no fake product screenshots made of rectangles, no three equal feature cards, no dark mesh hero, no decorative status dots, no scroll cues, and no housing stress jokes.

## Visual System

Primary surface: `#FFFFFF`. Use white generously so the product feels open, clean, and safe.

Primary accent: `#3557F0`. Use this blue for primary CTAs, active states, selected filters, compatibility highlights, and key links. Do not introduce a second decorative accent on marketing pages.

Supporting neutrals:

- Ink: `#101522` for primary text.
- Slate: `#4B5565` for body copy.
- Mist: `#F4F7FF` for soft panels and quiet section backgrounds.
- Line: `#DCE3F2` for dividers, input borders, and card outlines.
- Cloud: `#FAFBFF` for page depth without beige warmth.

Functional colours are allowed only when they carry meaning inside the product: success, warning, error, pending. Do not use them as decorative accents.

## Typography

Use Cormorant Garamond for major brand moments because the company direction names it directly. Keep it for the hero headline, major section titles, and occasional short pull quotes. Do not use serif for dense UI, forms, dashboards, or small labels.

Use DM Sans for body copy, navigation, buttons, forms, product UI, captions, and tables. UI should feel crisp and readable on mobile.

Type rules:

- Hero headline: 48-72px desktop, max 2 lines.
- Hero subtext: max 20 words, max 4 lines.
- Section headline: 32-48px desktop.
- Body text: 16-18px, max width 65ch.
- Buttons: short labels, one line only.
- Do not mix random serif words into sans headlines for decoration.

## Layout Direction

The first viewport should make Nydo unmistakable: name, tagline, student housing context, university verification, and the primary action. Use an asymmetric split hero rather than a centred generic SaaS block.

Recommended hero structure:

- Left side: Nydo wordmark, headline, short value statement, primary signup action, secondary demo or learn-more action.
- Right side: real visual asset showing student arrival, shared apartment life, or a polished product moment.
- Under hero: a separate trust strip for university verification and launch cities. Keep it outside the hero stack.

Page rhythm:

1. Hero with human housing stakes.
2. Problem section based on WhatsApp chaos and flatmate risk.
3. How Nydo works: Verify, Match, Lock, Stay.
4. Compatibility explanation with profile and score examples.
5. Locked group and co-living suite.
6. Launch cities and school networks.
7. Early traction and credibility.
8. Final signup CTA.

Do not repeat the same section layout twice in a row. Alternate between split layouts, full-width editorial sections, bento grids with real visual variation, and compact proof sections.

## Imagery And Assets

Nydo needs real images. Pure text is not enough.

Use photography or generated imagery that shows:

- Incoming international students arriving in European cities.
- Calm shared apartment moments.
- Realistic student profiles and group formation.
- City texture from Madrid, Paris, Milan, and Lisbon.

Avoid generic dorm-room stock, staged smiling flatmate photos, fake dashboard screenshots, and dark blurred city backgrounds. If product UI is shown, use a real component preview or a generated polished screen mockup, not div-based fake UI.

Image treatment:

- Rounded corners: 18px for marketing imagery.
- Soft blue-tinted shadows only when elevation matters.
- No image overlay pills or decorative photo captions.
- Reserve image space to prevent layout shift.

## Components

Navigation:

- Single-line desktop nav, max 72px tall.
- Logo left, three to four links centred or right-aligned, CTA right.
- Mobile uses a clean menu sheet.

Buttons:

- Primary: blue fill, white text, 999px radius.
- Secondary: white or transparent fill, blue or ink text, visible border.
- Active state: subtle downward movement or scale.
- One label per intent. Use the same signup label everywhere.

Cards and panels:

- Use cards only when they group a real object: student profile, compatibility reason, group, city, or agency lead.
- Default radius: 18px for marketing cards, 12px for app UI cards, full pill for buttons.
- Avoid card-inside-card layouts.

Forms:

- Labels above inputs.
- No placeholder-as-label.
- Clear helper and error text.
- Strong focus rings using `#3557F0`.
- Mobile-first spacing.

## Motion

Motion should reduce anxiety by making progress and state clear.

Use:

- Gentle hero entry for headline, image, and CTA.
- Scroll reveal for major sections only.
- Tactile button feedback.
- Smooth state transitions for onboarding, matching, group lock, and dashboard activation.

Avoid:

- Scroll hijacking for core flows.
- Infinite animations on every card.
- Custom cursor effects.
- Motion that delays signup or verification.

Honour reduced motion. If the user prefers reduced motion, all reveal and decorative motion becomes static.

## Product UI Direction

The product experience should be quieter than the landing page. Use DM Sans, compact but breathable spacing, and strong form clarity.

Core screens:

- Onboarding: one decision group per screen, progress visible, save state clear.
- Match feed: profile cards with compatibility reasons, not endless swipe behaviour.
- Profile detail: verified identity and lifestyle fit first.
- Group room: member status and private lock state should be obvious but calm.
- Co-living dashboard: simple tabs, lists, assignment controls, and status badges.

## Copy Rules

Use student-centred clarity. Lead with relief and trust, not hype.

Preferred words: verified, compatible, flatmate, group, home, match, lock, shared bills, university email, arrival, co-living.

Avoid: Tinder, cheap, hustle, random, crashpad, seamless, revolutionary, next-gen, unlock your potential.

Use "flatmate" by default for student-facing European copy. Use "roommate" only when needed for a broader audience.

## Accessibility And Quality Checks

Before shipping a page or screen:

- Check button and form contrast.
- Check hero fits the first viewport on desktop and mobile.
- Check navigation stays on one line at desktop.
- Check all CTAs use one-line labels.
- Check there are no em dashes in visible copy.
- Check every image has useful alt text.
- Check mobile collapse for every multi-column section.
- Check dark mode only if the product implements dark mode from the start. Otherwise keep the brand light and do not mix themes mid-page.

## What Good Looks Like

A student should understand within 5 seconds that Nydo helps them find a verified, compatible flatmate before moving abroad. The page should feel premium, but not cold. It should feel safe, but not institutional. It should make the user think: these people know exactly what this moment feels like.
