# Legacy Host — detailed tutorial (EN)

Step-by-step guide: what to tap in the app and what to answer when the userbot asks for data.

## 0. Prepare in advance

1. **A Telegram account** — the one the userbot will run on.
2. **An inline bot** — a separate bot whose username ends with `bot` (e.g. `@my_cool_bot`).
   Create it in one minute via [@BotFather](https://t.me/BotFather): send `/newbot` → name → username.
   You do NOT need the token from BotFather — the app only needs the username.
3. **API ID and API HASH** — get them once at https://my.telegram.org/apps
   (log in with your phone number → App configuration → `api_id` is digits, `api_hash` is a string).
   Needed only for the very first setup.
4. Charged phone and Wi-Fi: installing Linux and packages downloads hundreds of megabytes.
   When the app asks to disable battery optimization — allow it, otherwise Android will kill the long install.

## 1. Buttons in order

| Step | Button | What happens |
|------|--------|--------------|
| 1 | `INSTALL LINUX` | Downloads and extracts Ubuntu on the phone. Slow (5–20 minutes). Don't touch anything, watch the log. |
| 2 | `INSTALL LEGACY` / `UPDATE TO LEGACY` | Clones the userbot into `/root/Legacy`, creates a virtual environment, installs packages. If Ratko/Heroku was installed before — data (sessions, database) migrates automatically. |
| 3 | `START BOT` | Starts the userbot. Before the first start it asks for the inline bot username. |

Other buttons: `UPDATE LEGACY` — update userbot code; `REAPPLY PATCHES` — re-apply patches; `STOP PROCESS` — stop; `COPY LOGS` — copy the log.

## 2. What to answer — every prompt explained

### "inline bot username, e.g. my_cool_bot" (asked by the app)

Answer with **your inline bot username from step 0**, for example:

```
my_cool_bot
```

No `@`, lowercase, must end with `bot`. Create one in @BotFather with `/newbot`.

### "Enter API ID" / "Enter API HASH" (first start)

Answer with the digits from my.telegram.org:

```
12345678
```

then the hash string:

```
abcdef1234567890abcdef1234567890
```

Asked once, saved into the config.

### "Use QR code? [y/N]"

Login method choice:

- Answer `y` — a QR code appears in the log. Scan it with the camera of **another** device where Telegram is open → confirm login there.
- Answer `N` (or just Enter) — classic phone-number login, see below.

### "Enter phone:"

Your number in international format, for example:

```
+79161234567
```

or

```
+380971234567
```

The leading `+` is optional — the main thing is the international format with the country code.

### The Telegram login code

After entering the number, the official Telegram app will deliver a message from **Telegram** with a 5-digit code. Type it into the app terminal:

```
48392
```

The code lives for a few minutes. If it expires — restart the bot (`STOP PROCESS` → `START BOT`) and start over.

### "Enter 2FA password" / two-step verification password

If two-step verification is enabled in Telegram (Settings → Privacy → Two-Step Verification), enter **that password** (not the SMS code!):

```
mySecretPassword123
```

If you don't have 2FA — this question never appears.

### "session name" / "terminal name" (app menu)

These are NOT Telegram credentials, just profile names inside the host:

- `session name` — account profile (`main` is the primary one; for a second account invent a latin name, e.g. `second`).
- `terminal name` — a named terminal tab, any latin name.

## 3. Common mistakes

- **"Invalid phone number"** — forgot the leading `+` or a typo in digits.
- **"Code expired / Invalid code"** — the code expired or was mistyped. Restart the login.
- **"FloodWait"** — too many attempts in a short time. Wait the given seconds/minutes and retry.
- **Bot keeps asking for API ID in a loop** — `api_hash` was pasted wrong (check it is complete, no spaces).
- **App dies after `.update` / `.restart`** — fixed in the current APK version, update the app.
- **Keyboard covers the input field** — fixed: the field lifts itself above the keyboard.

## 4. Updates

- Userbot: the `.update` command right in Telegram (the bot notifies you when an update is out).
- App: the Releases section of the `legacy-apk` repository, installs on top, data is kept.
