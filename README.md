# ResolveAI – Real-Time Voice Support Agent

A low-latency, real-time AI voice support assistant built with **Python**, **FastAPI**, and **LiveKit**. ResolveAI handles natural voice conversations—including mid-sentence interruptions—while executing authenticated backend actions and tracking system performance through automated evaluations.

## Key Features

- **Real-Time Voice Pipeline:** Full-duplex audio streaming powered by LiveKit, integrating Speech-to-Text (STT), LLM reasoning, and Text-to-Speech (TTS) with voice activity detection (VAD) and interruption handling.
- **Stateful Tool Calling:**
  - **Customer Authentication:** Verifies caller identity before exposing sensitive account or order details.
  - **Order Tracking:** Retrieves real-time order statuses and delivery updates.
  - **Replacement Requests:** Validates input parameters and requires explicit verbal confirmation before initiating order replacements.
  - **Human Handoff:** Seamlessly escalates complex or unresolved edge cases to a human agent with conversation context intact.
- **Automated Evaluations & Observability:**
  - End-to-end conversation testing measuring **tool-call correctness**, **task completion**, and **failure recovery**.
  - Real-time monitoring of end-to-end **response latency** (TTFT / voice-to-voice) and **token usage**.

## Tech Stack

- **Backend & API:** Python, FastAPI
- **Real-Time Audio & Transport:** LiveKit
- **AI & Orchestration:** Speech-to-Text (STT), Large Language Model (LLM) with structured tool calling, Text-to-Speech (TTS)
- **Evaluation & Monitoring:** Automated conversation test suite, latency & token telemetry

## Architecture Overview

```text
Caller Audio ──▶ LiveKit Room ──▶ STT ──▶ LLM Agent (State + Tool Calling) ──▶ TTS ──▶ Caller Audio
                                              │
                                              ├──▶ Auth & Order Service
                                              ├──▶ Replacement Workflow (Confirmed)
                                              └──▶ Human Handoff Escalation
