# 🦁 Simba Copilot

### An AI copilot interface that shows its work.

---

## What it is

Simba Copilot is an AI assistant interface built on one simple idea: **you should be able to see how an answer was produced, not just read the answer.**

Most AI assistants today work the same way. You type a question, text appears, and you have no idea what happened in between — which model answered, how much thinking went into it, what information it looked at, or whether it took a fraction of a second or twenty seconds. You're asked to trust a black box. And when the answer is wrong, which eventually it will be, you have no way of telling why.

There's a second problem underneath that one. Almost every assistant sends every question to the same model. So a trivial question — "what's the capital of Japan?" — burns the same expensive, slow reasoning power as a genuinely hard one. Meanwhile, if the system is tuned to be fast instead, the hard questions get shallow, confident, wrong answers. One model for everything is either wasteful or inadequate. It's never both right.

Simba solves both at once.

---

## How it thinks

Before Simba answers anything, it reads the question and decides what kind of work it actually is — a quick lookup, a rewrite, a calculation, or real multi-step reasoning. Then it routes the work across three tiers of model:

**Nano** handles the instant work — understanding the question, pulling up relevant information, formatting. It responds in under a quarter of a second.

**Super** handles everyday work — drafting, rewriting, summarising, explaining. About a second.

**Ultra** handles the genuinely hard work — root-cause analysis, planning, anything that requires following a chain of reasoning several steps deep. It takes six to eight seconds, and it's only used when the question earns it.

A single answer often uses all three: nano to understand what you asked, nano again to gather the data, ultra to reason about what it found.

---

## Why it's different

Here's the part that matters. Above every single answer, Simba shows a small panel called the **routing trace**. It lists each step it took, which model tier ran it, and how long that step took. Nothing is hidden, and nothing has to be clicked open to reveal it.

That means before you even read the answer, you already know how much thought went into it. A one-line reply that took 180 milliseconds and a considered analysis that took seven seconds look visibly different — so you calibrate your trust correctly, automatically, without having to think about it.

Transparency here is treated as a feature of the product, not a debugging tool for developers.

And underneath the message box, permanently on screen, sits a plain admission: *"Simba can be wrong. Check anything that matters before you act on it."* Not buried in a settings page, not a warning you can dismiss and forget. Always visible, right where you're already looking.

---

## What it can do

### 💬 Have a real conversation
Ask questions, get answers that stream in as they're written, and follow up naturally. Answers come back properly formatted — headings, bullet points, emphasis, and syntax-highlighted code — rather than as a wall of plain text.

### 🎚 Let you control how hard it thinks
Three depth settings sit right next to the message box, one click away:

- **Auto** — Simba decides for itself. Quick questions stay quick; hard ones escalate automatically. This is the default and handles almost everything.
- **Fast** — Skips deep reasoning entirely. Use it when you want a draft, not a verdict.
- **Deep** — Forces the most capable tier and adds an extra information-gathering step. Use it for analysis, planning, or anything you're actually going to act on.

### 🔍 Show its reasoning, every time
The routing trace appears above every answer, automatically. You never have to ask for it or go looking.

### 🗂 Keep your conversations organised
A sidebar holds your conversation history, grouped by when it happened — Today, Earlier this week — so you can pick up an old thread without hunting for it.

### 🚀 Get you started when you're stuck
Starting a new conversation offers four ready-made prompts: explain an error, turn messy notes into a task list with owners and dates, review a draft for tone and clarity, or plan a change including its risks and how to roll it back. One click drops it into the box, ready to edit.

### ⌨️ Stay out of your way while you type
The message box grows as you write and stops before it swallows the screen. Enter sends, Shift+Enter starts a new line — the convention your hands already know. The send button greys itself out when there's nothing to send or when an answer is still arriving, so you can't accidentally fire the same question twice.

### 🌗 Look right at any hour
Simba follows your device's light or dark setting on its own, and one click overrides it if you disagree. It remembers your choice next time. The dark theme isn't the light theme with the colours flipped — the shadows, contrast, and accents are all re-tuned so it's genuinely comfortable at night.

### 📱 Work properly on a phone
On a desktop, the sidebar sits beside the conversation. On a phone, it slides away into a drawer you pull open when you need it, and the layout accounts for notches and rounded screen corners. It isn't a squeezed desktop site.

### ♿ Work for everyone
Every control can be reached and operated by keyboard alone. Screen readers are told which depth mode is active and which conversation is open, not just shown a colour change. Focus is always clearly visible. And if you've told your device you prefer reduced motion, all the animation switches off — including the typing effect, so answers simply appear at once.

---

## The design

Simba deliberately avoids the cold blue-grey that nearly every AI product uses. Instead it's built on a warm paper-and-ink palette — soft creams and deep browns in daylight, near-black and warm amber at night. It's easier on the eyes over a long session, and it makes the product feel like a tool you work with rather than a machine you query.

Everything is set in three typefaces chosen for a reason: a geometric, confident face for headings, a highly legible one for reading, and a monospaced one for code and timings — the last of which keeps the numbers in the routing trace aligned in a clean column instead of jittering as they change.

---

## Where it stands today

The interface is complete and fully interactive — you can open it and use every feature immediately, with nothing to install and nothing to configure. The responses in the demo are written samples rather than live AI output, and the app says so plainly on screen. Everything around them — the routing display, the depth control, the streaming, the history, the theming — is real and working.

Connecting it to an actual model is a small, well-defined change, because the interface was built to display whatever routing decisions it's handed rather than having them baked in.

---

## What's coming

Live model responses. Conversations that save and sync. Expandable trace steps, so you can click any line and see exactly what was asked at that stage. A running cost estimate next to each latency. Attachments. Export to a document. A keyboard shortcut palette.

---

**Simba is Swahili for lion, and the mark is a stylised sun.** The idea is a copilot that's confident and quick — but one that works in the open rather than in the dark.

    
   
      
