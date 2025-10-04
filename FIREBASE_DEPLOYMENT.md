# Firebase Deployment Guide for 1on1chess.com

## Prerequisites

1. **Firebase CLI** installed globally:
   ```bash
   npm install -g firebase-tools
   ```

2. **Firebase Project** created: `on1chess` (already done)

3. **Google AdSense Account** (optional, can be added later)

## Project Structure

```
.
├── public/                    # Firebase hosting directory
│   ├── index.html            # Main chess app (with AdSense placeholders)
│   ├── 404.html              # Custom 404 page
│   └── privacy.html          # Privacy policy (required for AdSense)
├── firebase-config.js         # Firebase configuration (NOT deployed)
├── .firebaserc               # Firebase project reference (created by init)
├── firebase.json             # Firebase hosting config (created by init)
└── README.md
```

## Step 1: Firebase Login

```bash
firebase login
```

This will open a browser window to authenticate with your Google account.

## Step 2: Initialize Firebase Hosting

Run from the project root directory:

```bash
firebase init hosting
```

When prompted, answer as follows:

1. **"What do you want to use as your public directory?"**
   - Answer: `public`

2. **"Configure as a single-page app (rewrite all urls to /index.html)?"**
   - Answer: `No` (we want separate pages for privacy policy and 404)

3. **"Set up automatic builds and deploys with GitHub?"**
   - Answer: `No` (can set up later if desired)

4. **"File public/index.html already exists. Overwrite?"**
   - Answer: `No` (IMPORTANT: don't overwrite!)

5. **"File public/404.html already exists. Overwrite?"**
   - Answer: `No` (IMPORTANT: don't overwrite!)

## Step 3: Review firebase.json

After init, check `firebase.json`. It should look something like:

```json
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```

You can optionally add custom headers or rewrites if needed.

## Step 4: Test Locally (Optional)

Before deploying, test locally:

```bash
firebase serve
```

This will start a local server at `http://localhost:5000`. Test:
- Main game works
- Privacy policy loads
- 404 page shows for invalid URLs
- All functionality works (timers, moves, fullscreen, etc.)

## Step 5: Deploy to Firebase

Deploy your site:

```bash
firebase deploy
```

After deployment, you'll get a URL like:
- `https://on1chess.firebaseapp.com`
- `https://on1chess.web.app`

## Step 6: Connect Custom Domain (1on1chess.com)

1. Go to Firebase Console: https://console.firebase.google.com
2. Select your project: `on1chess`
3. Go to **Hosting** → **Add custom domain**
4. Enter: `1on1chess.com`
5. Follow the verification steps:
   - Add a TXT record to your domain's DNS (at GoDaddy)
   - Wait for verification (can take a few minutes to hours)

6. Add the A records provided by Firebase to your GoDaddy DNS:
   - Usually 2 A records pointing to Firebase IPs
   - Example:
     ```
     @    A    151.101.1.195
     @    A    151.101.65.195
     ```

7. Wait for DNS propagation (can take up to 48 hours, usually faster)

8. Firebase will automatically provision an SSL certificate

9. Optionally add `www.1on1chess.com` as another custom domain

## Step 7: Configure Google AdSense

**IMPORTANT:** You need to replace the placeholder AdSense codes in `public/index.html`

### Before applying for AdSense:
1. Make sure your site is live and accessible
2. Have your privacy policy accessible
3. Have some content and regular traffic

### Applying for AdSense:
1. Go to https://www.google.com/adsense
2. Sign up with your Google account
3. Add your website: `1on1chess.com`
4. Wait for approval (can take days to weeks)

### After AdSense approval:
1. Get your AdSense Publisher ID (format: `ca-pub-XXXXXXXXXXXXXXXX`)
2. Create an ad unit and get the Ad Slot ID
3. Update `public/index.html`:
   - Replace `ca-pub-XXXXXXXXXXXXXXXX` with your Publisher ID (line 10)
   - Replace `YYYYYYYYYY` with your Ad Slot ID (line 506)
4. Deploy the changes:
   ```bash
   firebase deploy
   ```

### AdSense code locations in index.html:
- Line 10: AdSense script tag in `<head>`
- Lines 502-512: Ad unit in sidebar (after move history)

## Ongoing Deployment

After initial setup, deploying updates is simple:

```bash
firebase deploy
```

This will deploy only changed files.

## Useful Commands

```bash
# Deploy only hosting (faster)
firebase deploy --only hosting

# View deployment history
firebase hosting:list

# Rollback to previous deployment
firebase hosting:rollback

# Open Firebase Console
firebase open hosting:site

# View logs
firebase functions:log
```

## Troubleshooting

### Issue: "Permission denied" during deploy
- Solution: Run `firebase login --reauth`

### Issue: Custom domain not working
- Check DNS propagation: https://dnschecker.org
- Verify DNS records are correct in GoDaddy
- Wait up to 48 hours for full propagation

### Issue: AdSense ads not showing
- Make sure you replaced placeholder IDs
- AdSense can take 24-48 hours to start showing ads
- Check AdSense dashboard for approval status
- Ensure privacy policy is linked and accessible

### Issue: Game not saving state
- localStorage should work normally on custom domain
- Test in incognito mode to verify

## Security Notes

1. **firebase-config.js** is in `.gitignore` to protect API keys
2. Firebase API keys are safe to expose in client-side code (they're restricted by domain)
3. Make sure you've configured Firebase Security Rules if you add database features later

## Next Steps

1. Monitor traffic with Google Analytics (already included in firebase-config.js)
2. Apply for Google AdSense once site is live and has some traffic
3. Consider adding more features:
   - User accounts (anonymous auth)
   - Game history storage (Firestore)
   - Multiplayer (Firebase Realtime Database)

## Support

- Firebase Documentation: https://firebase.google.com/docs/hosting
- AdSense Help: https://support.google.com/adsense
- GitHub Issues: https://github.com/moshebeeri/1on1chess/issues
