# Blueprint: Intonation and Context Analysis

## ML Models for Intonation & Context Analysis

- **Intonation/Prosody Modeling**
  - Bidirectional LSTMs/GRUs using features like pitch, energy, and duration.
  - Transformer-based models such as wav2vec 2.0 or HuBERT with attention layers predicting F₀ contours or pitch accents.
  - End-to-end TTS models like Tacotron 2 or FastSpeech augmented with prosody encoders.

- **Contextual Understanding**
  - Text encoders: BERT, RoBERTa, or GPT-style transformers for semantic and pragmatic context.
  - Multimodal models combining text and speech encoders (e.g., wav2vec 2.0) to jointly reason about acoustic cues.
  - Discourse-level models: hierarchical transformers or RNNs processing multiple sentences for dialogue context.

## Dataset Size & Quality

- **Quantity**
  - Prosody/intonation analysis: approximately 50–300 hours of clean, single-speaker audio with aligned transcripts.
  - Context-aware dialogue: 100k+ utterances featuring multi-turn dialogue with intent, emotion, or discourse labels.
  - Prosody-annotated corpora: at least 10k–20k sentences annotated with F₀, stress, or intonation patterns.

- **Quality Guidelines**
  - Sampling rate of 16 kHz or higher, 16‑bit PCM.
  - High signal-to-noise ratio and minimal background noise.
  - Balanced phonetic coverage and speaker diversity for multi-speaker datasets.
  - Accurate time-aligned transcripts with manual or semi-automatic prosody annotations.
  - Consistent recording conditions to avoid non-linguistic prosodic variation.

## Compiling eSpeak-NG or Similar TTS Systems

1. **Prerequisites**
   - Build tools: `autoconf`, `automake`, `libtool`, `make`, `gcc/g++`.
   - Libraries: `pkg-config`, optional `portaudio` and `mbrola` for audio output and MBROLA voices.
   - Debian/Ubuntu example:
     ```bash
     sudo apt-get install git autoconf automake libtool make gcc g++ pkg-config \
                          libsonic-dev libasound2-dev
     ```

2. **Fetch the Source**
   ```bash
   git clone https://github.com/espeak-ng/espeak-ng.git
   cd espeak-ng
   ```

3. **Generate Build System**
   ```bash
   ./autogen.sh
   ```

4. **Configure**
   ```bash
   ./configure --prefix=/usr/local
   ```

5. **Build & Install**
   ```bash
   make
   sudo make install
   ```

6. **Optional Tests**
   ```bash
   make check
   espeak-ng "Hello"
   ```

*Notes*

- On macOS, install dependencies via Homebrew and follow the same steps.
- On Windows, use MSYS2 or Cygwin, installing required packages with `pacman` before running the build sequence.
