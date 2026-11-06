# ai-sub-showcase

Automated repository showcasing audio-synchronized, bilingual AI subtitles produced by **[ai-sub](https://github.com/FlippFuzz/ai-sub)**.

All subtitles in this collection are generated for publicly available YouTube videos. This repository does not contain content from private or members-only videos.

> [!WARNING]  
> **Accuracy Disclaimer:** These subtitles are generated entirely by AI and have **not been manually reviewed**. AI models can make transcription or translation mistakes. Text may be inaccurate, hallucinated, or misrepresent the original audio. Please use them accordingly.

---

## ▶️ Watch Online (AI Sub Player)

You can watch any video in this showcase with synchronized subtitles directly in your browser using the **[AI Sub Player](https://flippfuzz.github.io/ai-sub-player/)**:

- **1-Click Playback:** Navigate to any channel directory (e.g., [`/kazamairoha`](./kazamairoha/README.md)) and click on a video title in the channel index table.
- **Direct URL Navigation:** Load any video directly via query parameters:
  ```text
  https://flippfuzz.github.io/ai-sub-player/?uploader=<uploader_id>&v=<video_id>
  ```
- **Player Features:**
  - **Bilingual Display Modes:** View both languages stacked at the bottom, split across top (Original) and bottom (English), or toggle single-language display.
  - **Multiple Track Selection:** Switch between different model pipelines (e.g. Gemini 3.8 Flash vs 3.6 Flash) or view raw unrefined drafts.
  - **Customizable Appearance:** Real-time font scaling, background opacity, custom text colors, and responsive positioning.

---

## 📁 Repository Structure

Subtitles and intermediate job states are organized hierarchically by channel **Uploader Handle** and **Video ID**:

```text
<uploader_id>/
├── README.md                              # Chronological channel index with dates, thumbnails, and player links
└── v/
    └── <video_id>/
        ├── video_meta.json                # Video metadata & manifest of available subtitle tracks
        ├── <title> [<video_id>].<shortcode>.srt   # Primary refined subtitle file
        └── .int/
            └── <shortcode>/
                ├── <title> [<video_id>].raw-<shortcode>.srt   # Raw dialogue draft (pre-lyrics refinement)
                ├── summary.<shortcode>.yaml                   # Macroscopic video summary, entities & chapters
                ├── part_000.subtitles.<shortcode>.yaml        # 5-minute chunk dialogue transcriptions
                ├── part_000.lyrics.<shortcode>.yaml           # Refined song lyrics & search queries
                └── ...
```

### File & Directory Roles

| Path / File | Description |
| :--- | :--- |
| **`<uploader>/README.md`** | Auto-generated channel catalog sorted newest-to-oldest (in JST) linking directly to the web player. |
| **`v/<video_id>/<filename>.<shortcode>.srt`** | **Primary Subtitles:** The final, synchronized bilingual subtitle track ready for video playback. Includes official song lyrics if musical performances occurred. |
| **`v/<video_id>/video_meta.json`** | Public manifest recording video title, publication timestamp, channel metadata, and a ranked list of available subtitle tracks consumed by the player. |
| **`.int/<shortcode>/<filename>.raw-<shortcode>.srt`** | **Raw Draft Subtitles:** Dialogue-only transcription before lyrics substitution (available whenever musical performances are detected and refined). |
| **`.int/<shortcode>/*.yaml`** | **Trace Logs:** Intermediate phase outputs containing whole-video summaries, detected musical events, web search queries, and raw AI reasoning (`thoughts`). |

---

## 🏷️ Shortcode & Versioning System

Each subtitle filename embeds a compact **composite shortcode tag** encoding the model and prompt iterations employed across all generation phases:

```text
<title> [<video_id>].<model_code>-<summary_v><lyrics_v><subtitles_v>.srt
```

### Breakdown Example: `g38f-011019`

```text
  g38f   -    01         10          19
 ──────      ────       ────        ────
 Model     Summary     Lyrics     Subtitles
 Code      Prompt v1  Prompt v10  Prompt v19
```

| Component | Code | Meaning |
| :--- | :--- | :--- |
| **Model Code** | `g38f` | Subtitles transcribed using **Gemini 3.8 Flash** |
| **Summary Version** | `01` | Phase 1 whole-video summary generated using Prompt Version `1` |
| **Lyrics Version** | `10` | Phase 3 song lyrics searched and refined using Prompt Version `10` |
| **Subtitles Version** | `19` | Phase 2 audio-visual subtitles generated using Prompt Version `19` |

### Model Shortcode Reference

Model tags follow the pattern `g<version><tier>`:

| Shortcode | Model Tier | Full Model Identifier |
| :--- | :--- | :--- |
| **`g38f`** | Flash | `google-gla:gemini-3.8-flash` |
| **`g37f`** | Flash | `google-gla:gemini-3.7-flash` |
| **`g36f`** | Flash | `google-gla:gemini-3.6-flash` |
| **`g35l`** | Flash-Lite | `google-gla:gemini-3.5-flash-lite` |
| **`g30p`** / **`g3p`** | Pro | `google-gla:gemini-3.0-pro` |

---

## ⚙️ Embedded Metadata Header

Every stitched `.srt` file includes a safely escaped 1-millisecond configuration header at **Event 0** (`00:00:00,000 --> 00:00:00,001`). This header preserves reproducibility parameters without interfering with standard media players:

```text
1
00:00:00,000 --> 00:00:00,001
(
  "ai_sub_version": "1.2.0",
  "generated_at": "2026-03-30T14:22:00.000000",
  "summary_prompt_version": 1,
  "subtitles_prompt_version": 19,
  "lyrics_prompt_version": 10,
  "status": "Completed",
  "settings": { ... }
)
```

---

## 💡 How to Use These Subtitles

### Option 1: Web Player (Recommended)
Open any channel index (e.g. [`kazamairoha/README.md`](./kazamairoha/README.md)) and click a video title to stream the video on YouTube with synchronized bilingual subtitles.

### Option 2: Local Video Players (VLC, MPV, PotPlayer)
1. Download the primary `.srt` file from the video's directory (`/v/<video_id>/`).
2. Place it in the same folder as your downloaded video file with a matching filename, or drag-and-drop the `.srt` directly into the video player during playback.

### Option 3: Browser Extension (YouTube In-Browser Overlay)
Use browser extensions such as **[Substital](https://substital.com/)** to load and overlay the raw `.srt` URL directly over the native YouTube player.

### Option 4: Inspect AI Reasoning & Prompts
To audit or research how the AI transcribed tricky names, translated jokes, or searched for song lyrics:
1. Navigate to `.int/<shortcode>/` for any video.
2. Open `summary.<shortcode>.yaml` to inspect extracted entities, participants, and timeline chapters.
3. Open `part_XXX.lyrics.<shortcode>.yaml` to inspect LRCLIB queries, web search snippets, and the AI's internal step-by-step thinking traces.

