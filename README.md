# Creative Pre-Flight

Score Meta ad creatives, video scripts and ad copy before they go live. Each item gets a verdict with the reasons and suggested fixes.

This version is a single web page hosted free on GitHub Pages. It has no server: the page calls Gemini or OpenRouter directly from your browser using API keys you paste into its Settings page.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole tool |
| `tools/tribe_preflight.py` | Optional brain-response scoring script (runs on a GPU, not on GitHub) |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Your API keys

Keys are **not** in these files, and must never be added to them. A GitHub Pages site is public: anything in its files can be read by anyone who opens it, and keys found there get copied and used.

Instead, paste your keys into the tool's **Settings** page. They're saved only in that browser on that device and sent only to the provider you pick. On a new device or browser, paste them again.

## Step-by-step: put it online

1. **Create the repository.** Sign in at github.com, click **+ → New repository**, name it `creative-preflight`, choose **Public**, and click **Create repository**. (GitHub Pages on a free account needs a public repo. That's safe here because no keys are in the files.)
2. **Upload the files.** On the new repo's page, click **uploading an existing file**. Drag in `index.html`, `README.md`, `.nojekyll` and the `tools` folder from this zip. Click **Commit changes**. If `.nojekyll` doesn't appear (hidden files are skipped on some computers), skip it; the site still works.
3. **Turn on GitHub Pages.** In the repo, open **Settings → Pages**. Under **Build and deployment**, set **Source** to **Deploy from a branch**, the branch to **main**, the folder to **/ (root)**, and click **Save**.
4. **Wait for the site.** After 1–2 minutes, refresh the Pages settings screen. It shows your address, for example `https://your-username.github.io/creative-preflight/`.
5. **Connect your AI.** Open the address and click **Settings** in the tool. Choose a provider, paste your API key, and click **Connect**. The tool loads the models your key can use, picks one, and sends a test request. You should see “Connected”. To add the other provider too, switch the provider dropdown, paste that key, and click **Connect** again.
6. **Use it.** Add creatives on the **Creatives** tab, or check a script or image text on **Scripts & copy**.

To update the tool later, upload the new `index.html` to the same repo; the site refreshes within a few minutes.

## Models

You never type a model name. When you click **Connect**, the tool asks the provider for the models your key can use and fills the **Model** dropdown, newest Gemini Flash model first. For OpenRouter, it lists only models that accept images, so creative frame checks work. Pick a different model from the dropdown at any time; the tool tests it straight away. If a provider retires a model, click **Connect** again to refresh the list.

## Updating rules when Meta changes something

Open Meta's announcement, copy the article text, paste it into the **Rules** tab, and click **Draft rule changes**. Review the proposed changes, then save. (This version can't read links, because it has no server.)

## Your saved work

Everything is saved in your browser on this device. Clearing browser data deletes it. Use **Settings → Download backup** regularly, and **Restore from backup** on another device. Backups never include your keys.

## Costs and privacy

AI usage is billed to your keys. Your creatives and text are sent to the provider you choose; free tiers may use inputs to improve their models, so check each provider's data policy before sending unreleased ads.

## Troubleshooting

| Message | Fix |
| --- | --- |
| “Add your … API key in Settings” | Paste the key in Settings and click Connect |
| “model isn’t available to your key” | Click Connect again and pick another model |
| “out of credits” | Add OpenRouter credits, or pick a free model |
| Settings doesn’t show “Tool version 2.0” | The old file is still cached: wait 2 minutes, then press Ctrl+F5 |
| “rejected the API key” | The key is wrong, expired or restricted; create a new one |
| “rate-limiting this key” | Wait a minute, or switch provider |
| “didn’t return valid JSON” | Try again, or use a stronger model |
| “Can’t reach …” | Check your internet connection or any ad/privacy blocker |
| “This browser can’t read the file” | Export the video as H.264 MP4 |
| Page shows 404 | Wait 2 minutes after turning on Pages; check `index.html` is in the repo’s top level |

## Brain-response script (optional)

`tools/tribe_preflight.py` scores videos with Meta's TRIBE v2 model on a GPU (for example Google Colab). Import the JSON it writes on the **Brain scores** tab. Check TRIBE v2's license before using it for paid ads, and fill in `predict_brain_response()` from its model card. Test the workflow with `--demo`.
