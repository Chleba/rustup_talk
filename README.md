---
title: "Rust + AI"
author: "Lukas Chleba"
date: "Rust Meetup Prague, 30.10.2025"
---

whoami
---

***Lukas "Chleba" Franek***

Open Source Developer

* https://github.com/Chleba
* netscanner, pixelartor, tui-slides, ..
* prusa, seznam.cz, geewa, ubiquiti, ..

<!-- pause -->
Also a dinasour🦕:
<!-- pause -->
<!-- column_layout: [1, 1, 1] -->

<!-- column: 0 -->
![image:width:100%](atari.jpg)
<!-- column: 1 -->
![image:width:100%](Netscape9logo.png)
<!-- column: 2 -->
![image:width:100%](floppy.jpg)
<!-- reset_layout -->

<!-- end_slide -->

@Chleba
---

![image:width:100%](hermit.png)

<!-- end_slide -->

Topics
---

<!-- font_size: 2 -->
## Local AI
<!-- font_size: 1 -->

<!-- pause -->
* **GUI/CLI/Web:** Points from making native GUI, CLI & Web AI Apps
<!-- pause -->
* **Libraries:** Used open sourced tools and libraries
<!-- pause -->
* **Models:** Experiences with open sourced models and their variants
<!-- pause -->
* **Constrains:** Limitations with using small, open sourced models
<!-- pause -->
* **Projects:** Showcase of developed projects


<!-- end_slide -->

Phylosophy
---

## Why local AI ?

* Privacy
* Can run offline
* No tokens limits
* No censorship (optional)
* Different models

<!-- end_slide -->

Reality
---

## State of today's models

Localy usable models are those with 32b instructions or less that needs to be loaded entirely into a GPU's VRAM.

Tested on HW:

* Macbook/MacStudio with min. 32GB of RAM
* ***Nvidia 5090 with 32GB VRAM***
* Radeon 6700 with 10GB VRAM (!?!)
* 1x Nvidia H200 with 141GB

<!-- pause -->

### Open sourced models

* ~124k - MIT
* ~338k - Apache2.0

<!-- pause -->

#### Localy usable models (32B and less)

* ~40k - MIT
* ~147k - Apache2.0

<!-- end_slide -->

Speed
---

## Models in numbers

Run on Nvidia RTX 5090 32GB VRAM using Ollama (v0.12.6)

| model            | params       |  tps     |
| ------           | ------       | ------   |
| gtp-oss          | 20b          | **~220** |
| mistral-small3.2 | 24b          | **~88**  |
| gemma3           | 27b          | **~77**  |
| qwen2.5vl        | 32b          | **~64**  |
| deepseek-r1      | 32b          | **~61**  |

<!-- end_slide -->

Limitations
---
<!-- font_size: 3 -->
# Memory
<!-- font_size: 1 -->
* Smaller models
* Smaller context window
* Less parallel context

<!-- pause -->
## Clustering
* MB HW
* Network bottleneck
* $$$ PRICE $$$

<!-- end_slide -->

Case example
---

### GPU:
Nvidia RTX 5090 **32GB** VRAM

-------

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->

| Model example | |
| -----         | -----  |
| ***Model***:        | Qwen2.5 |
| ***Parameters:***   | 32b |
| ***Quantization:*** | Q4_K_M |

<!-- column: 1 -->

| App case      | |
| -----         | -----  |
| ***Context window***:        | 10 192.tokens |
| ***Contexts:***   | 2 |

<!-- reset_layout -->

```
VRAM = MW + (KV * CW * PC)
```
<!-- pause -->

```
30GB = 22GB + (0.37MB * 10192 * 2)
```

<!-- end_slide -->

Tech stack
---

What I'm using for my AI projects

<!-- column_layout: [1, 1, 1] -->

<!-- column: 0 -->
# Languages
* Rust
* HTML
* JS
* SQL
* bash

## AI
* Ollama
* llama.cpp

<!-- column: 1 -->
### DB
* sqlite
* qdrant
* pqvector
* tantivy (bm25)

<!-- column: 2 -->
### Libraries
* langchain-rs
* ollama-rs
* pandoc
* pdfium
* egui
* ratatui
* rusqlite
* ...

<!-- end_slide -->

Showcase #1
---

## RAGChunker

Graph RAG chatbot & document chunker.

-----------

<!-- end_slide -->

Showcase #1
---
## RAGChunker
![image:width:100%](ragchunker1.png)

<!-- end_slide -->

Showcase #1
---
## RAGChunker
![image:width:100%](ragchunker2.png)

<!-- end_slide -->

Showcase #1
---
## RAGChunker - Tech stack

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
#### DB
* qdrant
* tantivy
* sqlite

#### Crates 
* ratatui
* **langchain-rust**
* **rust_search_fork**
* axum
* **rusqlite**
* qdrant-client
* tokio
* ...

<!-- column: 1 -->

| model | info |
| ---   | ---  |
| Parameters: | 24b |
| Contexts:   | 3   |
| Context Window: | 16384 |
| Tokens/secons | 60 |

<!-- end_slide -->

Showcase #2
---

## DocExtractor

Formatted data extraction from text or image documents.

---------

<!-- end_slide -->

Showcase #2
---
## DocExtractor
![image:width:100%](docextractor.png)

<!-- end_slide -->

Showcase #2
---
##  DocExtractor- Tech stack

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
#### DB
* sqlite

#### Crates 
* **langchain-rust**
* axum
* **rusqlite**
* **rusqlite_migration**
* tokio
* pandoc
* calamine
* lettre
* pdfium-render
* ...

<!-- column: 1 -->

| model | info |
| ---   | ---  |
| Parameters: | 32b |
| Contexts:   | 2   |
| Context Window: | 10192 |
| Tokens/secons | 64 |

<!-- end_slide -->

Showcase #3
---

## DeskVision

Local, Offline AI image search using Ollama with visual models.

---------

<!-- end_slide -->

Showcase #3
---
## DeskVision
![image:width:100%](deskvision.png)

<!-- end_slide -->

Showcase #3
---
## DeskVision- Tech stack

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->

#### Crates 
* **ollama-rs**
* rust_search_fork 
* ...

### GUI
* egui
* eframe
* egui_form
* egui_flex
* egui_extras
* open
* rfd (file dialogs)

#### egui themes
* egui-themer - https://github.com/grantshandy/egui-themer


<!-- column: 1 -->

| model | info |
| ---   | ---  |
| Model: | gemma3 |
| Parameters: | 7b - 32b |
| Contexts:   | 1-10   |
| Context Window: | 4192 - 10192 |
| Tokens/secons | 220 - 64 |

<!-- end_slide -->

Open Source Libs
---

# AI
* **ollama-rs** - https://github.com/pepperoni21/ollama-rs
* langchain-rust - https://github.com/Abraxas-365/langchain-rust

# DB
* **rusqlite** - https://github.com/rusqlite/rusqlite
* **rusqlite_migration** - https://github.com/cljoly/rusqlite_migration
* qdrant-client - https://github.com/qdrant/rust-client
* memvid-rs - https://github.com/AllenDang/memvid-rs

# System
* **rust_search_fork** - https://github.com/jjjermiah/Rust_Search/
* pdfium-render - https://github.com/ajrcarey/pdfium-render
* libreoffice-rs - https://github.com/undeflife/libreoffice-rs

# GUI / TUI
* **egui** - https://github.com/emilk/egui
* **ratatui** - https://github.com/ratatui/ratatui

<!-- end_slide -->

Questions
---

Thank You

https://github.com/Chleba/rustup_talk
