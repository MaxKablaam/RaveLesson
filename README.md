# RAVE Intro Tutorial — Exploring the Black Box

**What this lesson is**
A demonstration of creative approaches to using AI for sound, focusing on exploration and experimentation.

**What this lesson is not**
A step-by-step DSP tutorial or a coding class on replicating everything exactly.  
The goal is to spark curiosity about how machine learning can transform sound.

## 1. What is RAVE?

**RAVE (Realtime Audio Variational autoEncoder)** is a machine-learning model for audio synthesis developed by the **ACIDS lab at IRCAM**.  
It uses deep learning to transform sound in real time, by learning a compact internal representation of timbre, texture, and dynamics.

RAVE learns to map: audio → numbers → audio again

Those numbers form the **latent space**, which we can explore to create entirely new sounds.

**Links:**
- [RAVE GitHub](https://github.com/acids-ircam/RAVE)
- [Pretrained Models (ACIDS)](https://acids-ircam.github.io/rave_models_download)
- [Pretrained Models (Hugging Face)](https://huggingface.co/Intelligent-Instruments-Lab/rave-models)

## 2. PlugData Overview

**PlugData** is a modern reimagining of **Pure Data (Pd)**, a visual programming language for sound.  
It’s open-source, modular, and integrates VST plugins, making it friendlier for musicians and artists.

**Key Concepts:**
- **Nodes (objects)** = modules or functions  
- **Patch cords** = signal or control connections  
- Process audio, generate synthesis, or control MIDI without writing text code.

⚠️ **Warning:**  
When using PlugData (or Pd), always start with your volume low and avoid headphones.  
Feedback loops or runaway signals can damage equipment or hearing.

### Demo 1: Quick PlugData Tour
1. Create a simple audio patch (`osc~`, `dac~`).
2. Show how to connect and start audio.
3. Highlight how modular patching works.

If students want to learn Pd fundamentals:  
📺 [Pure Data Lessons with Andrew Brown (YouTube)](https://www.youtube.com/watch?v=SLx7kjuFheY&list=PLuxj2jXSuTvvqYc)

## 3. nn~ — Using Neural Networks in Pure Data

**nn~** is a Pd/PlugData external that lets you load trained neural audio models (like RAVE).  
Think of it as the bridge between your patch and the AI model.

**Docs:** [nn~ Documentation](https://acids-ircam.github.io/nn_tilde/)  
*(It may require manual installation on macOS.)*

Once loaded, it behaves like any other Pd object — you can send it audio or control messages.

### Demo 2 — Timbre Transfer with nn~
1. Load a pretrained RAVE model (e.g., `vintage.ts` or `sol_ordinario_fast.ts`).
2. Route live audio or a sample into `nn~`.
3. Play with the parameters — the output will sound similar to your input, but filtered through the “language” of the model’s training data.

**Conceptual Note:**  
RAVE doesn’t copy the input; it *reinterprets* it using what it learned —  
like an impressionist painter capturing the essence of light rather than the exact details.

## 4. Encode / Decode Split

RAVE works in two steps:

1. **Encode** → Translates sound into numerical features, or “latent vectors.”  
2. **Decode** → Reconstructs audio from that vector.

In `nn~`, you can access these stages separately with `nn~ encode` and `nn~ decode`.  
Show how an audio signal can be encoded into numbers, displayed or modified, and then decoded back to sound.

## 5. Exploring the Latent Space

Now, remove the encoder and feed your own numbers into the decoder.  
Try **LFOs**, **noise**, or **manual sliders**.

The **latent space** is what the model has learned — every coordinate produces a sound that resembles the training data but doesn’t exist in the real world.

**Try out:**
- Randomize latent vectors  
- Interpolate between two latent points (morphing between sounds)  
- Modulate the inputs in real time for performance
