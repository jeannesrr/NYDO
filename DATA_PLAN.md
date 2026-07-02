# Nido Data Plan

Last updated: July 2, 2026

This document explains what data Nido needs, what data is already stored in Supabase, and what additional data would make the matching and AI features more credible over time.

Nido is not a housing-listing platform. The important data is about students, lifestyle fit, trust, communication, and group formation.

## 1. Data Goals

Nido needs data for five main reasons:

1. Match students with compatible flatmates.
2. Help students understand whether someone is a good living fit.
3. Support safe messaging and group formation.
4. Power AI features like onboarding help, profile polishing, and the Nido assistant.
5. Measure whether the product is actually helping students form good flatmate groups.

The most important principle is simple: collect enough data to make useful matches, but avoid collecting sensitive data that is not needed.

## 2. Current Data We Already Use

Nido currently uses Supabase as the source of truth.

### User and Auth Data

Stored through Supabase Auth:

- User ID
- Email address
- Email confirmation status
- Login/session state

Purpose:

- Verify that users are real university students.
- Create a profile row for every new user.
- Protect signed-in pages and API routes.

Current automation:

- A database trigger creates a `profiles` row when a new auth user is created.
- A university email trigger rejects signups that do not look like student/university emails.

### Profile Data

Stored mainly in the `profiles` table:

- Full name
- Nickname
- University
- Program
- Nationality
- Languages
- Move-in date
- Budget range
- Gender
- Gender preference
- Profile photo URL
- Instagram handle
- Short bio
- Completed profile flag

Purpose:

- Show useful profile cards.
- Filter students by university.
- Help users evaluate trust and relevance.
- Give Gemini enough context to polish bios and help with onboarding.

### Lifestyle and Compatibility Data

Stored in the `profiles` table:

- Sleep schedule
- Smoking
- Cleanliness
- Sociability at home
- Guest policy
- Going out frequency
- Noise preference
- Diet
- Hobbies
- Introvert/extrovert score
- Social/independent score
- Conflict style
- Lifestyle match preference: similar or different

Purpose:

- Calculate compatibility scores.
- Generate lifestyle tags like `Tidy`, `Night owl`, or `Quiet at home`.
- Help students understand practical living fit.

Important note:

- The current match score is deterministic scoring in `src/lib/compatibility.ts`.
- It is not a trained AI model yet.
- That is acceptable for V1 because it is explainable and easier to debug.

### Connection Data

Stored in the `connections` table:

- Requester ID
- Recipient ID
- Status: pending, accepted, declined
- Created and updated timestamps

Purpose:

- Track who wants to connect.
- Unlock messaging only after accepted connections.
- Measure which matches are actually interesting to users.

### Messaging Data

Stored in the `messages` table:

- Sender ID
- Recipient ID
- Conversation key
- Message body
- Created timestamp

Purpose:

- Support direct messaging between accepted connections.
- Trigger realtime updates and push notifications.
- Measure whether accepted matches lead to actual conversations.

Privacy note:

- Messages should be treated as private communication.
- They should not be used for AI training or profile scoring by default.

### Group Data

Stored in `groups`, `group_members`, and `group_messages`:

- Group name
- Creator ID
- Group status: forming, locked, dissolved
- Lock deadline
- Member invite/confirm/decline status
- Group chat messages

Purpose:

- Let students form flatmate groups.
- Lock a group when everyone confirms.
- Dissolve groups when members decline or the deadline passes.
- Measure whether Nido is leading to actual flatmate group formation.

### Notification Data

Stored in `push_subscriptions`:

- User ID
- Browser push endpoint
- Push encryption keys
- Created timestamp

Purpose:

- Send message and connection notifications.
- Improve response speed between potential flatmates.

Privacy note:

- Push subscription data is technical delivery data.
- It should only be used for notifications.

## 3. AI Data Usage

Nido currently uses Gemini for visible AI features.

### AI Onboarding Chat

Data sent to Gemini:

- Student's chat message
- Current profile draft
- Recent onboarding chat history

Purpose:

- Ask follow-up questions.
- Extract structured profile fields.
- Make onboarding faster.

Stored result:

- Only the final structured profile fields are saved to Supabase when the profile is saved.

### Microphone Input

Data flow:

- Browser listens through the microphone.
- Browser speech recognition converts speech into text.
- Nido sends the text to the same onboarding chat endpoint.

Important privacy point:

- Raw audio is not sent to Gemini by Nido.
- Raw audio is not stored in Supabase by Nido.

### Profile Bio Polish

Data sent to Gemini:

- Draft bio
- Name
- University
- Program
- Nationality
- Hobbies

Purpose:

- Make the bio clearer and more useful for flatmate matching.

### Site Assistant

Data sent to Gemini:

- User question
- Current page path
- Recent assistant chat history

Purpose:

- Answer product questions.
- Send users to the right page, such as Matches, Messages, Groups, or Edit Profile.

Boundaries:

- The assistant should not invent housing availability.
- The assistant should not give legal, financial, or safety guarantees.
- The assistant should not expose private data about other users.

## 4. Data We Still Need

The current app has enough data for a credible V1. To make the matching stronger and more credible as a machine-learning/data project, Nido should collect outcome data.

### Match Feedback

Needed fields:

- User ID
- Matched profile ID
- Rating: good match, okay match, bad match
- Optional reason: lifestyle, budget, timing, personality, trust, other
- Timestamp

Why we need it:

- Current matching guesses compatibility from profile answers.
- Feedback tells us whether the score was actually useful.
- This is the most important data for improving the model later.

### Match Explanation Feedback

Needed fields:

- User ID
- Match ID
- AI explanation helpful: yes/no
- Optional correction

Why we need it:

- If we add AI match explanations, we need to know whether users trust and understand them.

### Conversation Outcome Data

Useful signals:

- Connection accepted
- First message sent
- First reply received
- Conversation length
- Time to first reply

Why we need it:

- A match is not only good because the score is high.
- A match is better if people actually talk.

Privacy boundary:

- Use metadata first.
- Do not analyze private message content unless users explicitly consent.

### Group Success Data

Useful signals:

- Group created
- Members invited
- Members confirmed
- Group locked
- Group dissolved
- Reason for dissolution, if known

Why we need it:

- The strongest product success metric is not profile completion.
- It is whether users form confirmed flatmate groups.

### Post-Group Survey

Needed fields:

- User ID
- Group ID
- Did this group feel like a good fit?
- Would you live with this group?
- What was the main issue if not?
- Timestamp

Why we need it:

- This gives Nido high-quality labels for future match improvement.
- It turns matching from assumptions into measured outcomes.

### Safety and Trust Data

Potential fields:

- Reported user ID
- Reporter user ID
- Report reason
- Admin status: open, reviewed, resolved
- Timestamp

Why we need it:

- Flatmate matching needs trust.
- Admin review needs structured information.

Careful boundary:

- Keep reports private.
- Only admins should access them.

## 5. Suggested Future Tables

These are credible additions if the project continues.

### `match_feedback`

Purpose:

- Store whether users think a suggested match is good.

Suggested columns:

- `id`
- `user_id`
- `matched_profile_id`
- `rating`
- `reason`
- `created_at`

### `match_explanations`

Purpose:

- Store generated AI explanations if we want history, auditing, or professor demos.

Suggested columns:

- `id`
- `user_id`
- `matched_profile_id`
- `explanation`
- `friction_points`
- `suggested_first_message`
- `created_at`

### `profile_quality_checks`

Purpose:

- Store AI feedback on whether a profile is complete and useful.

Suggested columns:

- `id`
- `user_id`
- `score`
- `missing_items`
- `suggestions`
- `created_at`

### `group_feedback`

Purpose:

- Measure whether locked groups actually feel viable.

Suggested columns:

- `id`
- `group_id`
- `user_id`
- `fit_rating`
- `would_live_together`
- `main_issue`
- `created_at`

### `user_reports`

Purpose:

- Support safety and admin review.

Suggested columns:

- `id`
- `reporter_id`
- `reported_user_id`
- `reason`
- `details`
- `status`
- `created_at`
- `reviewed_at`

### `ai_events`

Purpose:

- Track AI feature usage without storing unnecessary private content.

Suggested columns:

- `id`
- `user_id`
- `feature`
- `success`
- `error_type`
- `created_at`

Examples of `feature`:

- `bio_polish`
- `chat_onboarding`
- `site_assistant`
- `match_explanation`
- `first_message_generator`

## 6. Data Quality Rules

Nido matching is only as good as the profile data. The app should enforce:

- Required profile basics: name, nationality, languages, university, program, bio, move-in date, gender.
- Valid slider ranges: 1 to 10.
- Valid enum values for guest policy, connection status, group status, and lifestyle match type.
- University email verification before active use.
- Profile completion before appearing in matches.
- Photo storage through the `avatars` bucket only.
- No messaging unless a connection is accepted.
- No group chat unless a group is locked.

AI should help improve data quality by:

- Asking for missing onboarding details.
- Turning spoken answers into structured fields.
- Suggesting clearer bios.
- Warning users when a profile is too vague.

## 7. Privacy and Security Plan

Nido should follow these rules:

- Store only data that supports matching, trust, communication, or safety.
- Keep Gemini API keys server-side only.
- Use Supabase RLS for user-owned data.
- Treat messages as private by default.
- Do not send raw microphone audio to Nido servers.
- Do not use private messages for model training without explicit consent.
- Keep admin-only data behind admin checks.
- Store push subscription data only for notification delivery.
- Keep `/api/debug/env` boolean-only and never expose real secret values.

## 8. Retention Plan

Suggested retention approach:

- Profiles: keep while the account exists.
- Photos: delete when a user deletes or replaces their profile photo.
- Connection records: keep while the account exists for product history and safety.
- Messages: keep while both users/accounts exist unless a deletion feature is added.
- Group records: keep for product history unless deletion is requested.
- Push subscriptions: delete stale subscriptions automatically when push endpoints expire.
- AI event logs: keep only lightweight metadata, not full private prompts, unless needed for debugging.
- Reports: keep longer than normal product data because they may be needed for safety review.

## 9. Metrics We Should Track

Product metrics:

- Signup completion rate
- Onboarding completion rate
- Percentage of users using chat onboarding
- Percentage of users using microphone input
- Profile completion quality
- Matches viewed per user
- Connection request rate
- Connection acceptance rate
- First message rate after accepted connection
- Reply rate
- Group creation rate
- Group lock rate
- Group dissolution rate

AI metrics:

- Bio polish usage
- Chat onboarding usage
- Site assistant usage
- AI error rate
- Average number of onboarding messages before completion
- User edits after AI-generated profile fields
- Future: helpfulness rating for match explanations

Matching metrics:

- Average compatibility score shown
- Acceptance rate by score range
- Reply rate by score range
- Group lock rate by average group compatibility
- User feedback rating by score range

## 10. Minimum Data Needed for a Strong Demo

For a credible class demo, Nido should have:

- At least 15 to 30 complete student profiles.
- Varied lifestyle answers, not all default values.
- Several accepted and pending connections.
- A few message conversations.
- At least one group in `forming`, one in `locked`, and one in `dissolved`.
- A few profiles with photos.
- Examples of Gemini features:
  - chat onboarding
  - microphone input
  - bio polishing
  - site assistant navigation

If possible, add sample feedback data later:

- A few match ratings.
- A few group fit ratings.
- A few AI helpfulness ratings.

That would make the project look much more data-driven.

## 11. Future Machine Learning Plan

If Nido moves beyond rule-based matching, the future model should learn from outcomes, not just profile answers.

Potential training labels:

- User liked or disliked a match.
- Connection request accepted or declined.
- Conversation started.
- Conversation got a reply.
- Group formed.
- Group locked.
- Post-group survey rating.

Potential features:

- Lifestyle slider distance.
- Same or different program.
- Same or different nationality.
- Language overlap.
- Move-in date distance.
- Budget overlap.
- Smoking compatibility.
- Cleanliness compatibility.
- Guest policy compatibility.
- Social rhythm compatibility.

Recommended approach:

1. Keep the current deterministic score as the baseline.
2. Collect outcome and feedback data.
3. Compare outcomes across score ranges.
4. Add AI explanations before replacing the scoring model.
5. Only train a learned model once there is enough real usage data.

This keeps the project credible: V1 matching is explainable, and the data plan shows exactly how it could become a real machine-learning system later.
