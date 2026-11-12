# Backend setup (about 20 minutes)

## 1. Create the script
1. Go to script.google.com > New project. Paste all of `Code.gs`.
2. Project Settings > Script properties > add:
   - `SECRET` = any long random text (also type the same in the app: Settings > Backend secret)
   - News push: `TG_TOKEN`, `TG_CHAT_ID`; optional `GEMINI_KEY` (Bengali headlines), `FEEDS` (one RSS URL per line)
   - Facebook Page: `FB_PAGE_ID`, `FB_PAGE_TOKEN`
   - WhatsApp: `WA_PHONE_ID`, `WA_TOKEN`
3. Deploy > New deployment > Web app > Execute as: Me, Access: Anyone. Copy the /exec URL into the app (Settings > Backend URL).
4. Select `setupTrigger` in the editor and press Run once (allow permissions). News now arrives every 30 min, even with the app closed.

## 2. Telegram (news notifications)
Open @BotFather in Telegram > /newbot > copy token (`TG_TOKEN`). Send any message to your bot, then open
`https://api.telegram.org/bot<TOKEN>/getUpdates` and copy `chat.id` (`TG_CHAT_ID`).

## 3. Facebook Page post and Messenger
developers.facebook.com > Create app (Business) > add Messenger and Pages. Use Graph API Explorer to get a Page access token
with `pages_manage_posts`, `pages_messaging`, `pages_read_engagement`; exchange it for a long-lived token. `FB_PAGE_ID` is on your Page's About section.
Messenger contacts need their PSID (page-scoped ID); put `name=PSID` in Contacts.

## 4. WhatsApp
developers.facebook.com > your app > add WhatsApp > API Setup gives `WA_PHONE_ID` and a token (make a permanent system-user token for production).
Test mode can message only numbers you add to the allowed list.

## Platform rules
Messenger and WhatsApp free-form text works only within 24 hours after that person messaged your Page/number; otherwise WhatsApp needs an approved template.
Personal profiles cannot be posted to automatically; posting is to a Facebook Page you manage.
