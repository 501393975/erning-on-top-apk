<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://ai.google.dev/static/site-assets/images/share-ais-513315318.png" />
</div>

# Erning on Top

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/880d4087-4a6b-42d3-b3a5-0532fef5e487

## Run locally

**Prerequisites:**  [Android Studio](https://developer.android.com/studio)


1. Open Android Studio and select this project directory.
2. Create `.env` in the project root using `.env.example` as a template.
3. Configure the Supabase project URL and **publishable** key in `.env`.
4. In Supabase, enable Email/Password authentication and choose whether email confirmation is required.
5. Run `supabase/migrations/202611050001_initial_app_backend.sql` in the Supabase SQL Editor.
6. Sync Gradle and run the app on an emulator or physical device.

The app requires a signed-in account before opening the wallet or earning screens. Its profile, points, point history, referrals, and withdrawals are stored in Supabase; the app refreshes cloud data every 15 seconds while open.

Never put a Supabase `service_role` key in the app. A publishable key is expected to be visible in a mobile application; row-level security and the server-side RPC functions in the migration enforce per-user access. The current session reward RPC can validate reward inputs and apply a cooldown, but it cannot independently prove that a WebView loaded or was viewed; do not treat this client-driven reward model as fraud-proof for money payouts.

Existing balances/history that were only stored on a device are not automatically imported into the cloud account. Cloud profiles start at zero to avoid trusting client-provided wallet balances.

For production email signup, configure Supabase email delivery and the confirmation redirect URLs in the Supabase dashboard. The Android app currently does not implement deep-link email confirmation; users can return to the app and sign in after confirming their address.

## App download website

The static download page is `index.html` at the project root. Its APK button downloads `mahin100-com.apk` from the same directory. Upload both `index.html` and `mahin100-com.apk` to the static web host's published directory; uploading only the HTML page will leave the download link without its APK file.

When publishing a newer app version, rebuild the APK and replace `mahin100-com.apk` with the new APK. The included APK is a debug build; make a release-signed build before distributing it publicly.
