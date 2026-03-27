# Arcady Firebase Setup

This chat page now uses:

- Firebase Authentication for username + password sign-in
- Cloud Firestore for servers, channels, users, announcements, and messages
- Firebase Storage for profile pictures and image uploads
- Private direct messages between two users

## What changed

- The embedded page at `features/arcadyhangout.html` is now a Discord-style Firebase chat app.
- Starter servers are seeded automatically:
  - `general`
  - `study talk`
  - `random`
  - `suggestions`
- Starter channels are seeded automatically:
  - `chat`
  - `media`
- The first account that registers becomes the `owner`.
- Owners can promote admins, ban users, and edit or delete any message.
- Admins can post announcements and ban users.
- Members can click profiles and open direct messages.

## Important security note

The original request asked for a hidden admin trigger and a shared hardcoded password. That was intentionally replaced with visible role-based access. Use the provided Firestore and Storage rules so moderation powers stay restricted to actual owner/admin accounts.

## Firebase console steps

1. Turn on `Authentication -> Email/Password`.
2. Create Firestore in production mode.
3. Replace Firestore rules with the contents of `firebase.rules`.
4. Replace Storage rules with the contents of `storage.rules`.
5. Deploy or host the project where the page can reach Firebase and `features/gifs/index.json`.

## GIF folder

The app reads GIF entries from `features/gifs/index.json`.

Example:

```json
{
  "gifs": [
    { "file": "party-cat.gif", "label": "Party Cat" },
    { "file": "thumbs-up.gif", "label": "Thumbs Up" }
  ]
}
```

Place the actual GIF files in:

- `features/gifs/party-cat.gif`
- `features/gifs/thumbs-up.gif`

## Username behavior

Firebase Auth still uses email/password under the hood, but the page maps usernames to a hidden synthetic email format so users only see username/password in the UI.
