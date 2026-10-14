# Switchboard for iPhone

This folder turns the Switchboard web app into an iPhone app. An IPA can only be built on a Mac, so GitHub builds it for you on its own Mac servers. You don't need a Mac.

The IPA it produces is **unsigned**. Apple only lets signed apps run, so you sign it for your own phone with a free sideloading tool (steps below).

> This pipeline has not been run on a real Mac yet. If a step fails the first time, open the red step in the Actions log and send me the error text. It is usually a one-line fix.

## 1. Build the IPA on GitHub

1. Create a **public** GitHub repository (public repos get free Mac build time).
2. Upload everything in this folder to the repository root: `www`, `assets`, `package.json`, `capacitor.config.json`, `.gitignore`.
3. GitHub's web uploader skips hidden folders, so add the workflow by hand: **Add file → Create new file**, type the name `.github/workflows/build-ios.yml`, paste in the contents of `build-ios.yml` from this folder, and commit.
4. Open the **Actions** tab, choose **Build iPhone app (unsigned IPA)**, press **Run workflow**.
5. After about 10 to 15 minutes, open the finished run and download **Switchboard-unsigned-ipa** from the Artifacts section. Unzip it to get `Switchboard-unsigned.ipa`.

## 2. Put it on your iPhone

You need one of these tools. They sign the IPA with your Apple ID when installing:

- **AltStore** (altstore.io) or **Sideloadly** (sideloadly.io). Both need a Mac or Windows PC for the first setup.
- **SideStore** (sidestore.io) can refresh apps on the phone itself after a one-time setup on a computer.

With a free Apple ID the app stops opening after **7 days** and must be re-signed (AltStore and SideStore can refresh it automatically). Free accounts allow about 3 sideloaded apps. A paid Apple Developer account ($99 a year) gives a one-year signature and lets you use TestFlight, but that needs signing certificates added to the build, which this project doesn't set up.

On iOS 16 and later, also turn on **Developer Mode** (Settings → Privacy & Security) when asked.

## No computer? Use Add to Home Screen

If you have already put the web version on GitHub Pages, you get an app icon with no signing at all:

1. Open your site in **Safari** on the iPhone.
2. Tap **Share → Add to Home Screen**.

It opens full screen like an app and your data stays on the phone. It is not an IPA, but it is the quickest way to get an icon today.

## How the app behaves on iPhone

- Your API keys, chats and history stay on the phone, inside the app.
- **Downloads** (images, text, HTML) open the iPhone share sheet. Choose **Save to Files** or send them anywhere.
- Attach photos from your library. Voice dictation may not be available inside the app; the keyboard's own microphone button works in every text box.
- **Photos and the free AI** need internet. Ollama on your own computer can't be reached from the phone.
- Change the app name or bundle ID in `capacitor.config.json` (`appName`, `appId`).

## Updating

Replace `www/index.html` with a newer version of Switchboard and push to `main`. The workflow runs again and gives you a new IPA.
