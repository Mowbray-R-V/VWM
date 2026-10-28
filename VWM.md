# VWM

## Questions
1. VWM vs WAM ?
2. Agentic world action models ?

## World models definition

## Video generation model vs video world models
1. A typical video generation model (Sora 2, Veo 3, Runway Gen-4, Kling, Pika) is trained to produce visually convincing video from a text or image prompt. Its objective is aesthetic and statistical: generate pixels that look like plausible video. Whether the physics underneath is actually correct is incidental — it only needs to appear correct for a few seconds.
2. A video world model, by contrast, is trained to understand and predict the dynamics of an environment. World models are AI systems that understand the dynamics of the real world, including physics, spatio-temporal relationships, and environment properties.
3. video world models are used as simulators

###
1. **Objective: entertainment vs. prediction.** A video generator optimizes for a human viewer’s perception of quality. A world model optimizes for physical faithfulness and causal consistency — if a robot pushes a cup off a table in the simulated world, the cup must fall, roll, and come to rest in a way that matches reality, because a downstream robot policy will be trained on that outcome. A Sora clip where water flows slightly unnaturally is a fine creative output; the same clip would be a corrupted training sample for an autonomous vehicle.
2. **Conditioning: prompts vs. states and actions.** Video generators take text or an image (“a corgi surfing at sunset”). World models are typically action-conditional or state-conditional: they take the current world state plus an action and predict the next state. A world model predicts future visual or latent states from the current state plus an action or goal abstraction. This is what makes them usable for planning: an agent can “imagine” the consequence of action A vs. action B before committing. A text-to-video model has no notion of an agent acting in the scene turn by turn.
3. **Interactivity and memory.** Video generators produce a fixed clip in one shot, offline. Many world models run as closed-loop simulators: you act, the world responds, you act again.** Genie 3 (Google DeepMind)** learns a compressed action space from video without labeled action data, then generates interactive environments from that learned space — video that responds coherently to user inputs in real time. Genie maintains spatial continuity — turn 360 degrees, and the AI remembers what was behind you. That persistent spatial memory is exactly what standard video generators lack (objects that leave frame in a Sora video often morph or vanish when they return).
4. **Downstream use: content vs. embodied AI.** The output of a video generator is the product. A world model’s output is usually an input to something else — synthetic training data, a planning loop, or a robot policy. NVIDIA’s Cosmos is the clearest example: it generates photorealistic synthetic video of physical environments for robotics and autonomous vehicle training pipelines, and developers can feed Omniverse 3D simulations into Cosmos Transfer models to generate controllable, photorealistic synthetic data. Waymo already uses Genie 3 to train self-driving cars on rare events like tornadoes or unexpected encounters with elephants on the road — events too rare or dangerous to collect in the real world.
5. **Architecture and training data.** They can share machinery — diffusion transformers trained on huge video corpora — but world models diverge in what and how they learn. Training data can include large-scale video, images, text, 3D data, sensor observations, and sometimes actions or trajectories... **world models are typically multimodal or omnimodal.** Some don’t generate pixels at all: joint embeddin**g predictive architectures, such as JEPA, predict representations of future or missing observations rather than reconstructing every pixel**, allowing models to focus on higher-level structure and dynamics. Yann LeCun’s camp argues this is the right way to build a world model, since rendering every raindrop is wasted effort if your goal is to predict consequences, not make a movie. A pure video generator, by definition, must produce every pixel.
6. **VWM:** NVIDIA Cosmos, DeepMind Genie 2/3, Wayve GAIA-2, V-JEPA 2, World Action Models

## Resources
1. **Awesome robotics world models:** https://github.com/irom-princeton/awesome-robotics-video-world-model-papers#-world-models
2. https://videoworldmodel-workshop.github.io/
3. https://www.xunhuang.me/blogs/world_model.html
4. **WM definition:** https://www.nvidia.com/en-in/glossary/world-models/

## Benchmarks
1. **Robotic bechmark:** https://artificialanalysis.ai/articles/aa-robotics
2. https://artificialanalysis.ai/video/leaderboard/image-to-video?audio-output=false
3. **RBench:** https://huggingface.co/datasets/DAGroup-PKU/RBench
4. https://github.com/SHI-Labs/physical-ai-bench
5. 
