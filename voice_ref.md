# Voice Assistant Reference

## Core Components
- **Assistant (Assist)**: Native voice assistant integrated into Home Assistant for local or cloud processing.
- **Processing Modes**: 
  - **Local**: Privacy-focused, runs on home hardware.
  - **Home Assistant Cloud**: Easier setup using HA's hosted voice infrastructure.

## Features & Customization
- **Sense of Voice**: Support for multiple languages and core intents.
- **Expanded Assist**: Options for custom sentences, AI personalities (OpenAI integration), and specialized sentence starters.
- **Hardware Integration**: Use with various hardware including ESP32-S3-BOX, Android/Apple mobile apps, and DIY satellites.

## Implementation Checklist
- Determine local vs cloud requirements.
- Define required intents via "Sentence" list.
- Configuration of names (aliases) for entities and areas to simplify voice commands.
