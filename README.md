# 🤖 VIR — Virtual Identity Runtime

> *"I am building VIR — a fully local, fully free AI agent that runs on my laptop. It listens to my voice, thinks using my local AI models, controls my computer, creates videos with my face as the influencer, and posts content to YouTube and Facebook — completely automatically. Zero cloud. Zero cost. My laptop. My rules."*

![VIR](https://img.shields.io/badge/VIR-Virtual%20Identity%20Runtime-blue?style=for-the-badge)
![Local AI](https://img.shields.io/badge/AI-100%25%20Local-green?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-FREE-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Development-orange?style=for-the-badge)

---

## 📌 Table of Contents

- [What is VIR?](#what-is-vir)
- [Why I Built This](#why-i-built-this)
- [My Hardware](#my-hardware)
- [My Local AI Models](#my-local-ai-models)
- [System Architecture](#system-architecture)
- [The VIR Algorithm](#the-vir-algorithm)
  - [Master Control Algorithm](#master-control-algorithm)
  - [Video Pipeline Algorithm](#algorithm-1-video-pipeline)
  - [Web Search Algorithm](#algorithm-2-web-search--trend-hunter)
  - [Promotion Hunter Algorithm](#algorithm-3-promotion-hunter)
  - [Laptop Control Algorithm](#algorithm-4-laptop-control)
  - [Scheduler Algorithm](#algorithm-5-autonomous-scheduler)
- [Full Workflow](#full-workflow-step-by-step)
- [Tools I Use](#tools-i-use--all-free)
- [Project Structure](#project-structure)
- [Installation Roadmap](#installation-roadmap)
- [Daily Usage](#daily-usage)
- [Known Limitations](#known-limitations)
- [Future Roadmap](#future-roadmap)

---

## What is VIR?

**VIR (Virtual Identity Runtime)** is my personal AI agent system that I am building entirely from scratch on my own laptop. VIR is designed to act as my virtual identity on the internet — it researches trends, writes scripts, generates videos using my face, and manages my social media presence autonomously.

The name means exactly what it says:
- **Virtual** — It operates as a virtual version of me online
- **Identity** — It uses my actual face and voice as the content creator
- **Runtime** — It runs continuously in the background, always working

### What VIR Can Do

| Capability | Description |
|------------|-------------|
| 🎤 Voice Control | Listens to my voice commands via microphone |
| 🧠 Local AI Brain | Thinks using Dolphin LLaMA-3 via Ollama — no cloud |
| 🔍 Trend Research | Searches the internet for trending topics automatically |
| ✍️ Script Writing | Writes full video scripts using my local AI |
| 😄 Face Video | Generates talking-face videos using my photo via SadTalker |
| 🎬 Auto Editing | Assembles stock footage with my face in the corner via MoviePy |
| 📤 Auto Upload | Posts finished videos to YouTube and Facebook via APIs |
| 💰 Promo Hunting | Finds brand collaboration opportunities and drafts outreach emails |
| 💻 Laptop Control | Controls my mouse, keyboard, and opens apps via PyAutoGUI |
| 🗣️ Voice Response | Speaks back to me using Coqui TTS |

---

## Why I Built This

I wanted to build a system that could run my entire content creation pipeline while I focus on other things. Most AI tools cost money, require cloud access, or don't give full control. With VIR, everything runs on my own machine using models I already have downloaded. No subscriptions. No data leaving my laptop. No limits imposed by anyone else.

This project is also my way of learning how to build real AI agent systems from scratch — connecting voice recognition, language models, computer vision, video processing, and API automation into one unified pipeline.

---

## My Hardware

```
┌─────────────────────────────────────────┐
│           MY LAPTOP SPECS               │
│                                         │
│  GPU 0  →  AMD Radeon iGPU (4.2 GB)     │
│  GPU 1  →  NVIDIA RTX 3050 (4 GB VRAM)  │
│  RAM    →  7.3 GB Total                 │
│  DISK   →  NVMe SSD                     │
│  OS     →  Windows 11                   │
└─────────────────────────────────────────┘
```

> ⚠️ **My main constraint:** 4 GB VRAM means I cannot run the AI brain and SadTalker at the same time. I designed VIR to run tasks **sequentially** — each module loads, executes, then unloads before the next one starts.

---

## My Local AI Models

I already have these installed and running via Ollama:

| Model | VRAM Needed | My Use Case | Speed |
|-------|-------------|-------------|-------|
| `gemma3:1b` | ~1 GB | Fast decisions, quick classification | ⚡ Very Fast |
| `dolphin-llama3` | ~3-4 GB | Main brain — script writing, reasoning, planning | 🧠 Medium |
| `deepseek-r1:8b` | ~5 GB | Deep analysis (too heavy for my 4 GB VRAM) | 🐢 Slow |

**My primary model for VIR:** `dolphin-llama3`
- Uncensored — follows complex instructions without restrictions
- Fits inside my 4 GB VRAM
- Strong at creative writing, task planning, and reasoning

---

## System Architecture

```
╔══════════════════════════════════════════════════════════════╗
║                  VIR — VIRTUAL IDENTITY RUNTIME              ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   ┌─────────────┐         ┌─────────────────┐                ║
║   │  VOICE IN   │         │   TEXT INPUT    │                ║
║   │  (Whisper)  │         │   (Terminal)    │                ║
║   └──────┬──────┘         └────────┬────────┘                ║
║          └──────────┬──────────────┘                         ║
║                     ▼                                        ║
║          ┌──────────────────────┐                            ║
║          │      VIR BRAIN       │                            ║
║          │   Dolphin LLaMA-3    │  ← Ollama (local)          ║
║          │   Intent Classifier  │                            ║
║          │   Task Planner       │                            ║
║          └──────────┬───────────┘                            ║
║                     │                                        ║
║     ┌───────────────┼───────────────────┐                    ║
║     ▼               ▼                   ▼                    ║
║  ┌─────────┐  ┌───────────┐  ┌──────────────────┐            ║
║  │ SEARCH  │  │  LAPTOP   │  │  VIDEO PIPELINE  │            ║
║  │ MODULE  │  │  CONTROL  │  │                  │            ║
║  │         │  │           │  │  Script Writer   │            ║
║  │DuckDuckGo  │ PyAutoGUI │  │  Coqui TTS       │            ║
║  │Pexels   │  │ Keyboard  │  │  SadTalker       │            ║
║  │G.Trends │  │ Mouse     │  │  MoviePy         │            ║
║  └─────────┘  └───────────┘  │  YT / FB Upload  │            ║
║                              └──────────────────┘            ║
║                                                              ║
║   ┌────────────────────────────────────────────────┐         ║
║   │  OUTPUT: Coqui TTS Voice Response + Log File   │         ║
║   └────────────────────────────────────────────────┘         ║
╚══════════════════════════════════════════════════════════════╝
```

---

## The VIR Algorithm

This is the complete algorithmic design of VIR. Every module, every decision tree, every loop is documented here so I always know exactly how the system works.

---

### Master Control Algorithm

This is the top-level entry point of VIR. Every command — spoken or typed — enters here first.

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_MASTER_CONTROL
INPUT:      User command (voice audio OR text string)
OUTPUT:     Completed task + voice confirmation + log entry
══════════════════════════════════════════════════════════

BEGIN VIR_MASTER_CONTROL

  ── STAGE 1: BOOT & HEALTH CHECK ──────────────────────────
  CHECK ollama service is running       → if not: start it
  CHECK nvidia GPU is available         → if not: switch to CPU mode
  CHECK free disk space > 2 GB         → if not: warn user and exit
  CHECK internet connection             → set online_mode flag
  LOAD all settings from config.py
  LOG "VIR Started at " + current_timestamp

  ── STAGE 2: INPUT CAPTURE ────────────────────────────────
  DISPLAY menu:
    [1] Voice input   (speak into microphone)
    [2] Text input    (type in terminal)
    [3] Auto mode     (VIR decides task itself — no input needed)

  IF mode == VOICE:
    audio = microphone.record(
      silence_timeout = 2 seconds,
      max_duration    = 30 seconds
    )
    command = whisper.transcribe(audio, model="base", language="auto")
    LOG "Voice command captured: " + command

  ELSE IF mode == TEXT:
    command = terminal.read_input("VIR > ")
    LOG "Text command captured: " + command

  ELSE IF mode == AUTO:
    command = "find a trending topic and create a video about it"
    LOG "Auto mode — default command injected"

  END IF

  ── STAGE 3: INTENT CLASSIFICATION ───────────────────────
  // Use the small fast model for classification only
  intent_prompt = """
    Classify this user command into exactly ONE of these categories:
      VIDEO_CREATE    → user wants to make or post a video
      WEB_SEARCH      → user wants to search or research something
      LAPTOP_CONTROL  → user wants to open app, click, or type something
      PROMO_HUNT      → user wants to find sponsors or brand deals
      SCHEDULE_SET    → user wants to automate or schedule a task
      GENERAL_CHAT    → anything else, general conversation

    Command: """ + command + """
    Reply with ONLY the category name. Nothing else.
  """

  intent = ollama.generate(
    prompt = intent_prompt,
    model  = "gemma3:1b"
  ).strip().upper()

  LOG "Intent detected: " + intent

  ── STAGE 4: ROUTE TO MODULE ──────────────────────────────
  SWITCH intent:
    CASE "VIDEO_CREATE"   →  result = VIR_VIDEO_PIPELINE(command)
    CASE "WEB_SEARCH"     →  result = VIR_WEB_SEARCH(command)
    CASE "LAPTOP_CONTROL" →  result = VIR_LAPTOP_CONTROL(command)
    CASE "PROMO_HUNT"     →  result = VIR_PROMOTION_HUNTER(command)
    CASE "SCHEDULE_SET"   →  result = VIR_SCHEDULER(command)
    CASE "GENERAL_CHAT"   →  result = ollama.generate(command, model="dolphin-llama3")
    DEFAULT               →  result = "Command not understood. Please try again."
  END SWITCH

  ── STAGE 5: RESPOND & LOG ────────────────────────────────
  coqui_tts.speak(result.summary)

  log.write({
    "timestamp" : current_time(),
    "command"   : command,
    "intent"    : intent,
    "status"    : result.status,
    "details"   : result.details
  })

  RETURN result

END VIR_MASTER_CONTROL
```

---

### Algorithm 1: Video Pipeline

My most complex module. Takes a topic and produces a fully edited, uploaded video with my face in the corner.

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_VIDEO_PIPELINE
INPUT:      command string (contains topic OR "auto")
OUTPUT:     Uploaded video URL on YouTube and Facebook
══════════════════════════════════════════════════════════

BEGIN VIR_VIDEO_PIPELINE

  ── PHASE 1: TOPIC SELECTION ──────────────────────────────
  IF command contains a specific topic:
    topic = extract_topic_from(command)

  ELSE:
    // Auto-discover the best trending topic right now
    trends_search  = duckduckgo.search("most trending videos today " + date)
    google_trends  = scrape_google_trends(region="IN", category="all")
    combined       = trends_search + google_trends

    topic = ollama.generate(
      prompt = "From these trending results, pick the ONE topic that would
                make the most engaging YouTube video right now.
                Return only the topic name, nothing else.
                Topics: " + combined,
      model  = "gemma3:1b"
    )
  END IF

  keywords  = ollama.extract_keywords(topic, count=5)
  topic_slug = slugify(topic)
  LOG "Topic selected: " + topic

  ── PHASE 2: SCRIPT WRITING ───────────────────────────────
  script = ollama.generate(
    prompt = """Write a YouTube video script about: """ + topic + """
               Structure it exactly like this:
               [HOOK]       First 15 seconds. Grab attention immediately.
               [INTRO]      Brief intro. What this video is about.
               [POINT 1]    First key point with example.
               [POINT 2]    Second key point with example.
               [POINT 3]    Third key point with example.
               [CONCLUSION] Summarize main takeaways.
               [CTA]        Ask viewer to like, subscribe, comment.
               Total spoken length: 2 to 3 minutes.
               Tone: conversational, confident, engaging.
               Plain text only. No markdown.""",
    model      = "dolphin-llama3",
    max_tokens = 1000
  )

  save(script, path = "output/scripts/" + topic_slug + ".txt")
  LOG "Script written: " + word_count(script) + " words"

  ── PHASE 3: AUDIO NARRATION ──────────────────────────────
  narration = coqui_tts.synthesize(
    text        = script,
    output_path = "output/audio/narration.wav",
    speed       = 1.0
  )
  audio_duration = get_duration("output/audio/narration.wav")
  LOG "Narration audio created: " + audio_duration + " seconds"

  ── PHASE 4: FACE VIDEO GENERATION ───────────────────────
  // CRITICAL: Unload AI model from VRAM before running SadTalker
  // My GPU only has 4 GB — both cannot run together
  ollama.unload_all_models()
  wait(seconds = 3)

  face_video_path = sadtalker.generate(
    source_image = "assets/my_photo.jpg",
    driven_audio = "output/audio/narration.wav",
    output_path  = "output/face/face_video.mp4",
    preprocess   = "crop",
    still_mode   = True,       // reduces VRAM usage
    use_enhancer = False        // skip GFPGAN — saves VRAM
  )
  LOG "Face video generated"

  // Reload brain model after SadTalker finishes
  ollama.load_model("dolphin-llama3")

  ── PHASE 5: STOCK FOOTAGE DOWNLOAD ──────────────────────
  stock_clips = []

  FOR each keyword in keywords:
    results = pexels_api.search_videos(
      query       = keyword,
      orientation = "landscape",
      per_page    = 2
    )
    FOR each video in results:
      clip_path = download(video.hd_url, "output/stock/")
      clip_path = moviepy.trim(clip_path, max_duration = 12)
      stock_clips.append(clip_path)
    END FOR
  END FOR

  LOG "Stock clips downloaded: " + len(stock_clips)

  ── PHASE 6: VIDEO ASSEMBLY ───────────────────────────────
  // Background: stack stock clips to fill audio duration
  background = moviepy.concatenate(
    clips    = stock_clips,
    loop_if_short = True
  ).set_duration(audio_duration).resize("1920x1080")

  // My talking face: picture-in-picture, bottom-right corner
  face_clip = moviepy.VideoFileClip(face_video_path)
             .resize(width = 480)
             .set_position(pos = "bottom_right", padding = 20)

  // Dark background behind my face for clean look
  face_bg = moviepy.ColorClip(
    size     = (500, 300),
    color    = (0, 0, 0),
    opacity  = 0.45
  ).set_position("bottom_right").set_duration(audio_duration)

  // Title text overlay at top of video
  title_text = moviepy.TextClip(
    text         = topic.upper(),
    fontsize     = 60,
    color        = "white",
    stroke_color = "black",
    stroke_width = 2
  ).set_duration(5).set_position(("center", 80))

  // Background music at low volume mixed with narration
  music     = moviepy.AudioFileClip(pick_random("assets/background_music/"))
             .volumex(0.12).set_duration(audio_duration)
  narration = moviepy.AudioFileClip("output/audio/narration.wav")
  final_audio = moviepy.CompositeAudioClip([narration, music])

  // Assemble final video
  final_video = moviepy.concatenate([
    moviepy.VideoFileClip("assets/intro.mp4"),

    moviepy.CompositeVideoClip([
      background,
      face_bg,
      face_clip,
      title_text
    ]).set_audio(final_audio),

    moviepy.VideoFileClip("assets/outro.mp4")
  ])

  output_path = "output/videos/" + topic_slug + "_" + date + ".mp4"
  final_video.write_videofile(output_path, fps=30, codec="libx264")
  LOG "Final video exported: " + output_path

  ── PHASE 7: METADATA GENERATION ─────────────────────────
  title = ollama.generate(
    "Write ONE catchy YouTube title about: " + topic
    + ". Max 70 characters. No clickbait. No quotes.",
    model = "gemma3:1b"
  )

  description = ollama.generate(
    "Write a YouTube description for a video about: " + topic
    + ". Include summary, 3 key points, hashtags, subscribe CTA.",
    model = "gemma3:1b"
  )

  tags = ollama.generate(
    "Give 15 YouTube tags for: " + topic + ". Comma separated only.",
    model = "gemma3:1b"
  ).split(",")

  ── PHASE 8: UPLOAD TO PLATFORMS ─────────────────────────
  IF "youtube" in upload_targets:
    yt_url = youtube_api.upload(
      file        = output_path,
      title       = title,
      description = description,
      tags        = tags,
      category    = "22",        // People & Blogs
      privacy     = "public"
    )
    LOG "Uploaded to YouTube: " + yt_url

  IF "facebook" in upload_targets:
    fb_url = facebook_api.upload_video(
      file        = output_path,
      title       = title,
      description = description
    )
    LOG "Uploaded to Facebook: " + fb_url

  RETURN {
    status       : "SUCCESS",
    topic        : topic,
    video_path   : output_path,
    youtube_url  : yt_url,
    facebook_url : fb_url,
    summary      : "Video about '" + topic + "' is now live!"
  }

END VIR_VIDEO_PIPELINE
```

---

### Algorithm 2: Web Search & Trend Hunter

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_WEB_SEARCH
INPUT:      Search query string from user
OUTPUT:     Summarized results as clean readable text
══════════════════════════════════════════════════════════

BEGIN VIR_WEB_SEARCH

  raw_results = duckduckgo.search(
    query       = query,
    max_results = 10
  )

  IF raw_results is EMPTY:
    RETURN { status: "FAILED", summary: "No results found for: " + query }
  END IF

  // Filter out irrelevant results using AI scoring
  filtered = []
  FOR each result in raw_results:
    score = ollama.score_relevance(result.snippet, query, model="gemma3:1b")
    IF score > 0.5:
      filtered.append(result)
    END IF
  END FOR

  // Summarize all filtered results into clean output
  combined_text = join(all filtered snippets, separator = "\n---\n")
  summary = ollama.generate(
    prompt = "Summarize these search results clearly and concisely: " + combined_text,
    model  = "gemma3:1b"
  )

  RETURN {
    status  : "SUCCESS",
    query   : query,
    count   : len(filtered),
    results : filtered,
    summary : summary
  }

END VIR_WEB_SEARCH
```

---

### Algorithm 3: Promotion Hunter

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_PROMOTION_HUNTER
INPUT:      My content niche string (e.g. "tech", "AI")
OUTPUT:     Brand list + drafted outreach email files
══════════════════════════════════════════════════════════

BEGIN VIR_PROMOTION_HUNTER

  // Build targeted search queries for my niche
  search_queries = [
    niche + " brand collaboration 2025",
    niche + " influencer sponsorship apply",
    niche + " affiliate program small creator",
    niche + " sponsor YouTube channel",
    "companies paying " + niche + " content creators"
  ]

  brands     = []
  emails     = []

  FOR each query in search_queries:
    results = duckduckgo.search(query, max_results = 8)
    FOR each result in results:
      brand = extract_brand_name(result.title, result.url)
      email = extract_contact_email(result.snippet)
      IF brand NOT already in brands:
        brands.append(brand)
      END IF
      IF email is a VALID email:
        emails.append(email)
      END IF
    END FOR
  END FOR

  brands = deduplicate(brands) → keep top 20 only

  // Draft a custom outreach email for each brand
  FOR each brand in brands:
    draft = ollama.generate(
      prompt = """Write a short professional collaboration outreach email.
                  Sender:   A """ + niche + """ content creator on YouTube.
                  Receiver: """ + brand + """ marketing team.
                  Include:  brief self-intro, channel focus,
                            why we are a good fit,
                            what content I can create for them,
                            a clear call to action.
                  Length: under 150 words. Friendly but professional.""",
      model  = "dolphin-llama3"
    )
    save(draft, "output/outreach/" + brand + "_email.txt")
  END FOR

  summary = "Found " + len(brands) + " potential brands. "
          + len(emails) + " direct emails found. "
          + "All outreach drafts saved to output/outreach/"

  RETURN {
    status  : "SUCCESS",
    brands  : brands,
    emails  : emails,
    summary : summary
  }

END VIR_PROMOTION_HUNTER
```

---

### Algorithm 4: Laptop Control

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_LAPTOP_CONTROL
INPUT:      Natural language command string
OUTPUT:     Physical actions performed on my laptop
══════════════════════════════════════════════════════════

BEGIN VIR_LAPTOP_CONTROL

  // Ask AI to break natural language into atomic computer actions
  parse_prompt = """
    Convert this command into a JSON array of actions.
    Each action must have: "type", "target", "value".

    Available action types:
      open_app    → open an application     (target = app name)
      type_text   → type text on keyboard   (value  = text to type)
      press_key   → press a key             (value  = key name e.g. "enter")
      click       → click something         (value  = x,y coords or element name)
      scroll      → scroll the page         (value  = "up" or "down", amount = lines)
      wait        → pause execution         (value  = seconds to wait)
      screenshot  → take a screenshot       (no additional fields needed)

    Command: """ + command + """

    Return valid JSON array ONLY. No explanation. No extra text.
  """

  action_plan = JSON.parse(
    ollama.generate(parse_prompt, model = "gemma3:1b")
  )

  results = []

  FOR each action in action_plan:

    SWITCH action.type:

      CASE "open_app":
        pyautogui.hotkey("win")
        pyautogui.typewrite(action.target, interval = 0.05)
        pyautogui.press("enter")
        wait(2 seconds)
        results.append("Opened: " + action.target)

      CASE "type_text":
        pyautogui.typewrite(action.value, interval = 0.03)
        results.append("Typed: " + action.value)

      CASE "press_key":
        pyautogui.press(action.value)
        results.append("Pressed key: " + action.value)

      CASE "click":
        IF action.value contains x,y coordinates:
          pyautogui.click(x = action.x, y = action.y)
        ELSE:
          position = find_element_on_screen(action.value)
          pyautogui.click(position)
        END IF
        results.append("Clicked: " + action.value)

      CASE "scroll":
        direction = -1 IF action.value == "down" ELSE +1
        pyautogui.scroll(direction * action.amount)
        results.append("Scrolled: " + action.value)

      CASE "wait":
        time.sleep(action.value)
        results.append("Waited: " + action.value + "s")

      CASE "screenshot":
        img  = pyautogui.screenshot()
        path = "output/screenshots/" + timestamp() + ".png"
        save(img, path)
        results.append("Screenshot saved: " + path)

    END SWITCH

  END FOR

  RETURN {
    status  : "SUCCESS",
    actions : results,
    summary : "Completed " + len(results) + " actions on my laptop."
  }

END VIR_LAPTOP_CONTROL
```

---

### Algorithm 5: Autonomous Scheduler

```
══════════════════════════════════════════════════════════
ALGORITHM:  VIR_SCHEDULER
INPUT:      Schedule config file (JSON)
OUTPUT:     Runs VIR tasks automatically at set times
══════════════════════════════════════════════════════════

BEGIN VIR_SCHEDULER

  schedule = load_json("config/schedule.json")

  /*
    Example schedule.json structure:
    {
      "daily_video":  { "time": "09:00", "type": "daily",    "enabled": true  },
      "promo_hunt":   { "time": "18:00", "type": "daily",    "enabled": true  },
      "trend_check":  { "interval_hours": 3, "type": "interval", "enabled": true }
    }
  */

  LOOP forever:

    now = get_current_time()   // format: "HH:MM"

    FOR each task in schedule:

      IF task.enabled == false:
        CONTINUE to next task
      END IF

      IF task.type == "daily":
        IF now == task.time:
          LOG "Running scheduled daily task: " + task.name
          VIR_MASTER_CONTROL(command = "auto")
          task.last_run = now
        END IF

      ELSE IF task.type == "interval":
        hours_since = hours_since_last_run(task.name)
        IF hours_since >= task.interval_hours:
          LOG "Running interval task: " + task.name
          VIR_MASTER_CONTROL(command = task.default_command)
          task.last_run = now
        END IF

      END IF

    END FOR

    wait(60 seconds)   // check schedule every minute

  END LOOP

END VIR_SCHEDULER
```

---

## Full Workflow Step by Step

This is exactly what happens when I say: **"VIR, find today's trending topic and make a video."**

```
[00:00]  I speak the command into my microphone
[00:02]  Whisper transcribes my voice to text locally
[00:03]  Gemma 3 1b classifies intent → VIDEO_CREATE
[00:05]  DuckDuckGo searches trending topics for today
[00:08]  Ollama picks the best topic from search results
[00:10]  Dolphin LLaMA-3 writes a full 2-minute video script
[00:50]  Coqui TTS converts the script to narration audio
[01:30]  Ollama unloads from GPU — VRAM freed for SadTalker
[01:33]  SadTalker generates my talking face video from photo
[04:00]  Pexels API downloads 6 relevant HD stock clips
[04:30]  MoviePy assembles: stock video background + my face in corner
[06:00]  Final 1080p MP4 exported to output/videos/
[06:10]  Ollama writes title, description, and tags
[06:20]  YouTube API uploads the video automatically
[06:45]  Facebook API posts the video automatically
[06:50]  Coqui TTS says: "Done! Your video is now live."
[06:51]  Full activity log saved to output/logs/activity.log
```

**Total time: ~7 minutes. My effort: one voice sentence.**

---

## Tools I Use — All FREE

| Tool | Purpose | Install |
|------|---------|---------|
| [Ollama](https://ollama.ai) | Run local AI models | ollama.ai |
| [Dolphin LLaMA-3](https://ollama.ai/library/dolphin-llama3) | Main VIR brain | `ollama pull dolphin-llama3` |
| [Gemma 3 1b](https://ollama.ai/library/gemma3) | Fast task classification | `ollama pull gemma3:1b` |
| [Whisper](https://github.com/openai/whisper) | Local voice-to-text | `pip install openai-whisper` |
| [Coqui TTS](https://github.com/coqui-ai/TTS) | Local text-to-voice | `pip install TTS` |
| [SadTalker](https://github.com/OpenTalker/SadTalker) | Talking face video | git clone |
| [MoviePy](https://zulko.github.io/moviepy/) | Automated video editing | `pip install moviepy` |
| [Pexels API](https://www.pexels.com/api/) | Free stock footage | Free API key |
| [DuckDuckGo Search](https://pypi.org/project/duckduckgo-search/) | Internet search | `pip install duckduckgo-search` |
| [PyAutoGUI](https://pyautogui.readthedocs.io/) | Laptop control | `pip install pyautogui` |
| [YouTube Data API v3](https://console.cloud.google.com) | Auto upload to YouTube | Free via Google Cloud |
| [Facebook Graph API](https://developers.facebook.com) | Auto post to Facebook | Free via Meta Developers |
| Python 3.11+ | Core programming language | python.org |
| CUDA Toolkit | Enable my NVIDIA RTX 3050 | nvidia.com/cuda |

---

## Project Structure

```
VIR/
│
├── vir.py                    ← Main entry point — run this to start VIR
├── scheduler.py              ← Autonomous daily task scheduler
├── config.py                 ← All API keys and system settings
├── requirements.txt          ← All Python dependencies
│
├── modules/
│   ├── brain.py              ← Ollama connection + model load/unload manager
│   ├── voice_in.py           ← Whisper microphone input
│   ├── voice_out.py          ← Coqui TTS voice output
│   ├── search.py             ← DuckDuckGo + Google Trends search
│   ├── script_writer.py      ← AI video script generation
│   ├── face_video.py         ← SadTalker integration
│   ├── video_editor.py       ← MoviePy video assembly pipeline
│   ├── uploader.py           ← YouTube + Facebook upload
│   ├── laptop_control.py     ← PyAutoGUI keyboard and mouse control
│   └── promo_hunter.py       ← Brand deal finder + email drafter
│
├── assets/
│   ├── my_photo.jpg          ← MY FACE PHOTO — add your own clear photo here
│   ├── intro.mp4             ← Channel intro clip
│   ├── outro.mp4             ← Channel outro clip
│   └── background_music/    ← Free royalty-free music files (.mp3)
│
├── config/
│   ├── schedule.json         ← Daily auto-schedule configuration
│   └── platforms.json        ← Upload platform settings
│
├── output/
│   ├── videos/               ← All final exported videos saved here
│   ├── scripts/              ← All AI-generated scripts saved here
│   ├── audio/                ← Narration audio files
│   ├── face/                 ← SadTalker face video outputs
│   ├── stock/                ← Downloaded Pexels stock footage
│   ├── outreach/             ← Brand outreach email drafts
│   ├── screenshots/          ← Laptop control screenshots
│   └── logs/                 ← Full activity logs
│
└── SadTalker/                ← Cloned separately from GitHub
```

---

## Installation Roadmap

I am building VIR in 6 phases over 14 days:

### Phase 1 — Foundation (Day 1)
```bash
# Install all Python dependencies
pip install openai-whisper TTS pyautogui duckduckgo-search moviepy requests

# Install CUDA Toolkit from nvidia.com for GPU support
# Verify Ollama is working
curl http://localhost:11434
```

### Phase 2 — Voice System (Day 2)
```bash
# Test Whisper
python -c "import whisper; m = whisper.load_model('base'); print('Whisper OK')"

# Test Coqui TTS
python -c "from TTS.api import TTS; print('Coqui TTS OK')"
```

### Phase 3 — Face Video (Day 3-4)
```bash
# Clone SadTalker
git clone https://github.com/OpenTalker/SadTalker
cd SadTalker
pip install -r requirements.txt
# Model weights download automatically on first run
```

### Phase 4 — Video Pipeline (Day 5-7)
```bash
# Get free Pexels API key at pexels.com/api
# Add key to config.py
# Test full video generation end to end
python vir.py --test-video
```

### Phase 5 — Auto Upload (Day 8-10)
```bash
# YouTube API setup at console.cloud.google.com (free)
# Facebook API setup at developers.facebook.com (free)
# Add credentials to config.py
python vir.py --test-upload
```

### Phase 6 — Full Integration (Day 11-14)
```bash
# Full end-to-end test
python vir.py

# Enable autonomous daily scheduler
python scheduler.py --time 09:00 --enable
```

---

## Daily Usage

```bash
# Start VIR in interactive mode
python vir.py

# Force video creation with specific topic
python vir.py --mode video --topic "AI news today"

# Auto mode — VIR picks the topic itself
python vir.py --mode auto

# Run promotion hunting for my niche
python vir.py --mode promo --niche tech

# Enable daily auto-post at 9 AM
python scheduler.py --time 09:00

# Run system health check
python vir.py --test
```

---

## Known Limitations

| Limitation | Reason | My Workaround |
|------------|--------|---------------|
| Cannot run brain + SadTalker simultaneously | Only 4 GB VRAM | Sequential execution — unload model first |
| SadTalker face quality ~80% natural | Free local model limit | Acceptable quality for social media |
| Instagram auto-posting unreliable | Instagram aggressively blocks bots | Post manually or use Buffer app |
| DeepSeek R1:8b too slow on my GPU | Needs 5+ GB VRAM | Use Dolphin LLaMA-3 or Gemma 3 instead |
| High RAM usage at startup | Background Windows apps | Close Chrome and Discord before running VIR |

---

## Future Roadmap

- [ ] Phase 1 — Voice input + brain + laptop control working
- [ ] Phase 2 — Script writer + Coqui TTS voice output
- [ ] Phase 3 — SadTalker face video integration
- [ ] Phase 4 — Full video pipeline with stock footage overlay
- [ ] Phase 5 — YouTube + Facebook auto upload
- [ ] Phase 6 — Promotion hunter module
- [ ] Phase 7 — Fully autonomous daily scheduler
- [ ] Phase 8 — Upgrade RAM to 16 GB (enables parallel processing)
- [ ] Phase 9 — Instagram integration
- [ ] Phase 10 — Multi-language video support (Hindi + English)

---

<div align="center">

**Built by me. Powered by local AI. Running on my laptop. Cost = ₹0.**

*VIR — Virtual Identity Runtime*

</div>
