# ai-sub-showcase

Automated repository showcasing AI-generated subtitles produced by **[ai-sub](https://github.com/FlippFuzz/ai-sub)**.

All subtitles in this collection are generated for publicly available YouTube videos. This repository does not contain content from private or members-only videos.

> [!WARNING]  
> **Accuracy Disclaimer:** These subtitles are generated entirely by AI and have **not been manually reviewed**. AI models can make transcription or translation mistakes. Text may be inaccurate, hallucinated, or misrepresent the original audio. Please use them accordingly.

---

## 📁 Repository Structure

Subtitles are organized by YouTube **Uploader ID** and **Video ID**:

```text
<uploader_id>/
└── <video_id>/
    ├── <filename>.<shortcode>.srt
    └── .int/
        └── <shortcode>/
            ├── part_001.lyrics.<shortcode>.yaml 
            ├── part_001.subtitles.<shortcode>.yaml
            └── ...
```

### Example Path

```text
kazamairoha/
└── 23UEX1Yh43U/
    ├── 【3DLIVE】Wind Trails🍃#風真いろは生誕ライブ2026 告知&ゲストあり🎈【風真いろは/ホロライブ】[23UEX1Yh43U].g36f-0918.srt
    └── .int/
        └── g36f-0918/
            ├── part_001.lyrics.g35l-0918.yaml
            └── part_001.subtitles.g36f-0918.yaml
```

* **`.srt` File:** The final, usable subtitle file.
* **`.int/` Directory:** Internal execution logs containing chunked transcriptions, prompt history, and raw AI reasoning (`thinking` steps) in YAML format.

---

## 🏷️ Shortcode Format

Each subtitle filename includes a **shortcode tag** encoding the model and prompt versions used:

`<title> [<video_id>].<model_code>-<lyrics_v><subtitles_v>.srt`

### Breakdown Example: `g36f-0918`

| Tag Component | Value | Description |
| :--- | :--- | :--- |
| **Model Code** | `g36f` | Generated using `gemini-3.6-flash` |
| **Lyrics Version** | `09` | Version `9` of the lyrics lookup prompt |
| **Subtitles Version** | `18` | Version `18` of the subtitle timing/translation prompt |

### Model Shortcode Reference

| Shortcode | Full Model Identifier |
| :--- | :--- |
| **`g36f`** | `gemini-3.6-flash` |
| **`g35f`** | `gemini-3.5-flash` |
| **`g35l`** | `gemini-3.5-flash-lite` |

---

## 💡 How to Use These Subtitles

1. **Direct Download:** Download any `.srt` file directly from this repository.
2. **Video Players:** Load the `.srt` file into local media players like VLC, MPV, or PotPlayer alongside your downloaded video.
3. **YouTube Playback:** Use browser extensions (e.g., *Substital*) to overlay these `.srt` files directly onto YouTube videos while watching.
4. **Inspect AI Reasoning:** Check the `.int/<shortcode>/` folder for any video to analyze raw AI responses, prompt iterations, and internal step logs.