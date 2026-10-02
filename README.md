# Overcomers Hymnal: setup guide

This folder is the complete app. It works offline, installs on Android phones like a regular app, and shares added hymns with everyone who uses it. You don't need to write any code.

## What's in the folder

- `index.html` is the app itself.
- `firebase-config.js` is the one file you edit, to connect the app to your free Firebase database (Part 2).
- `firestore.rules` lists who is allowed to add hymns. You copy it into Firebase (Part 2).
- `manifest.webmanifest` and `icons/` give Android the app's name, colors, and icon.
- `sw.js` lets the app open without an internet connection.

## How sharing works

Everyone who uses the app sees the hymns and Yoruba versions that leaders add, and they stay available offline after the app has synced once. Only leaders can add, edit, or delete. Leaders sign in inside the app with an email and password that you create for them in Firebase. Everyone else just uses the app, with no account needed.

## Part 1: Put the app online with GitHub Pages (free)

1. Go to github.com and create a free account.
2. Select **New repository**. Name it `hymnal`, choose **Public**, and select **Create repository**.
3. Select **uploading an existing file**, drag in everything from this folder (including the `icons` folder), and select **Commit changes**.
4. Open **Settings**, then **Pages**. Under **Branch**, choose `main` and select **Save**.
5. After a minute or two, refresh the page to see your app's address, such as `https://your-username.github.io/hymnal/`.

The app works right away. Until you finish Part 2, added hymns stay on each phone.

## Part 2: Turn on shared hymns with Firebase (free)

### Create the project

1. Go to console.firebase.google.com and sign in with a Google account.
2. Select **Create a project**, name it `overcomers-hymnal`, and follow the prompts. You can turn off Google Analytics.

### Create the database

1. In the left menu, open **Build**, then **Firestore Database**, and select **Create database**.
2. Choose a location near your church (for example, `europe-west` for Nigeria or the UK), then choose **Start in production mode**.
3. Open the **Rules** tab. Delete what's there and paste in everything from `firestore.rules`.
4. In the pasted rules, replace `leader1@example.com` and `leader2@example.com` with the email addresses of the people who should be able to add hymns. Add more addresses to the list the same way, each in quotes and separated by commas.
5. Select **Publish**.

### Create leader accounts

1. In the left menu, open **Build**, then **Authentication**, and select **Get started**.
2. Under **Sign-in method**, choose **Email/Password**, turn it on, and select **Save**.
3. Open the **Users** tab and select **Add user** for each leader, using the same email addresses you put in the rules. Choose a password for each and share it with them privately.
4. Open **Settings**, then **User actions**, and turn off **Enable create (sign-up)**. This stops strangers from creating their own accounts.

### Connect the app

1. Select the gear icon next to **Project Overview**, then **Project settings**.
2. Under **Your apps**, select the web icon (`</>`), name it `Hymnal`, and select **Register app**. You don't need Firebase Hosting.
3. Firebase shows a block of settings that starts with `const firebaseConfig = {`. Copy the part between the curly braces.
4. Open `firebase-config.js` in a text editor (Notepad works) and replace `null` with those settings, so it matches the example in the file.
5. In your GitHub repository, upload the edited `firebase-config.js`, replacing the old one.

### Check it works

1. Open your app's address, then select **Leader sign in** and sign in with a leader account.
2. Select **Add a hymn**, add a short test hymn, and save it.
3. Open the app on another phone. The hymn appears under **Added hymns** within a few seconds. You can then delete the test hymn.

If you added hymns on your phone before Part 2, sign in as a leader, and a notice lets you share them with everyone in one tap.

## Part 3: Install it on Android phones

1. Open your app's address in **Chrome** on the phone.
2. Select **Install app** in the hymnal, or open Chrome's menu (⋮) and choose **Install app** or **Add to Home screen**.
3. Share the address with your group so they can install it the same way.

## Updating the app later

Upload the new `index.html` to your repository, replacing the old one. Then open `sw.js`, change `hymnal-v2` to `hymnal-v3` (and so on each time), and upload it too. Phones get the update the next time they open the app online. Hymns added by leaders don't need an update, because they sync on their own.

## Good to know

The settings in `firebase-config.js` identify your project, and it is normal for them to be visible to anyone. Your rules are what protect the hymns, which is why only the leader emails listed there can make changes.

Firebase's free plan easily covers a church group. Firebase may ask you to add billing details for some features, but this app doesn't need any paid features.

Because anyone with the link can read the hymns, only add songs that are in the public domain or that you have permission to share. A church CCLI license generally covers congregational use, not publishing lyrics in a public app.
