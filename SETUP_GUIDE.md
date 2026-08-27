# Setup Guide (for Mac)

Follow these steps in order, top to bottom. Don't skip any.

Every gray box below is a command. To use it:
1. Click inside the gray box.
2. Copy it (Cmd+C).
3. Click into the Terminal window.
4. Paste it (Cmd+V).
5. Press Enter.
6. Wait for it to finish before doing the next box (you'll see the cursor blinking on a new line again when it's done).

This guide is for Apple Silicon Macs (M1, M2, M3, M4, or M5 chip — basically any Mac from 2020 or later).

---

## Step 0: Nothing to do here

The project is public, so there's no invite or account needed to download it &mdash; just start at Step 1.

---

## Step 1: Open Terminal

Terminal is an app already on your Mac. To open it:
1. Press **Cmd + Space** together. A search box pops up.
2. Type `Terminal`
3. Press Enter.

A black or white window with text opens. That's Terminal. Keep it open for everything below.

---

## Step 2: Install Homebrew

Homebrew is a tool that installs other programs for us. If you already have it, this is safe to run again — it'll just say it's already installed.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

It may ask for your Mac password while typing — that's normal, just type it (you won't see the letters appear, that's expected) and press Enter. It may also show instructions at the end telling you to run 1-2 more commands — if it does, copy-paste and run those too.

Check it worked:
```bash
brew --version
```
You should see a version number, like `Homebrew 4.x.x`.

---

## Step 3: Install the programs the app needs

Copy and run each of these one at a time (or all at once, they'll run one after another):

```bash
brew install python@3.14
brew install python-tk@3.14
brew install ffmpeg
brew install git
brew install --cask obs
```

What these are, in plain words:
- **python@3.14** — the programming language the app is written in.
- **python-tk@3.14** — lets the app draw its window/buttons on screen.
- **ffmpeg** — handles video files.
- **git** — downloads the project's code from GitHub.
- **obs** — a free app; we only need it once, to unlock a "virtual camera" feature (explained in Step 6).

This step can take several minutes. That's normal.

---

## Step 4: Download the app

```bash
cd ~/Desktop
git clone https://github.com/diyasharma200822-cloud/AC-DEEP-CAM.git
cd AC-DEEP-CAM
```

This creates a folder called `AC-DEEP-CAM` on your Desktop with all the code in it. No GitHub login needed &mdash; the project is public.

---

## Step 5: Set up the app's private toolbox

```bash
python3.14 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

In plain words: the first line creates a private, separate set of tools just for this app (so it doesn't mess with anything else on your Mac). The second line "switches on" that toolbox. The third line installs everything the app needs into it — this downloads a few gigabytes, so it can take 5-15 minutes depending on your internet. Just wait for it to finish.

You'll know Step 5 worked if the last few lines say something like `Successfully installed ...` with a long list of names.

---

## Step 6: One-time camera setup (so other apps can see the face-swapped video)

This step lets apps like Zoom, Google Meet, or FaceTime use the face-swapped video as if it were a regular webcam. You only ever have to do this once.

1. Open OBS: press **Cmd + Space**, type `OBS`, press Enter. A window opens.
2. In the bottom-right of the OBS window, click the button that says **Start Virtual Camera**.
3. macOS will interrupt with a popup about a "System Extension." Click **Open System Settings** (or if no popup appears, open **System Settings** yourself from the Apple menu  top-left).
4. In System Settings, go to **Privacy & Security**. Scroll down — you'll see a message about a blocked extension (something like "System software from application OBS was blocked"). Click **Allow**.
5. Your Mac may ask to restart. If it does, restart it, then come back here.
6. You can now close OBS completely (Cmd+Q). You will never need to open it again.

---

## Step 7: Run the app

Every single time you want to use the app, open Terminal and run these three lines:

```bash
cd ~/Desktop/AC-DEEP-CAM
source venv/bin/activate
python run.py --execution-provider coreml --max-memory 0
```

A window titled "Deep-Live-Cam" should pop up. If it does, you're ready.

---

## Step 8: Use the app

1. Click the button **Select a face** and choose a photo of the face you want to show up on camera. A clear front-facing photo works best.
2. Find the camera dropdown menu and pick your Mac's built-in camera — it's usually called **FaceTime HD Camera**.
   - Do **not** pick "OBS Virtual Camera" here — that one is the *output*, not a real camera, and picking it won't show anything.
3. Click the **Live** button. A small preview window opens showing your face, swapped.
4. In that small window, check the box that says **Send to Virtual Camera**.
5. That's it! Now open Zoom, Google Meet, FaceTime, or Photo Booth, go to its camera settings, and choose **OBS Virtual Camera**. You'll see the face-swapped video there.

To stop: close the small preview window, then close the main app window.

---

## If something goes wrong

- **"command not found: brew"** — Homebrew didn't finish installing (Step 2). Close Terminal, open a new one, and try `brew --version` again.
- **App won't open / crashes immediately** — make sure you typed the Step 7 command exactly, including `--max-memory 0` at the end. Without it, the app crashes on Mac on purpose-blocked memory setting (a known Mac-only quirk).
- **Camera dropdown is empty or says "No cameras found"** — quit the app, unplug/replug any external camera, and start it again.
- **"Send to Virtual Camera" doesn't work / other apps don't see it** — you probably missed a part of Step 6. Redo Step 6 from the beginning, making sure you click **Allow** in System Settings and restart if asked.
- **Anything else** — take a screenshot of the error text in Terminal and send it to whoever gave you this guide.
