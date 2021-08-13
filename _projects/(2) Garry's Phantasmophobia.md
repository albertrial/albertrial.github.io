---
name: Garry's Phantasmophobia
tools: [Procedural generation, Unity 3D, Agents, AI]
image: /assets/img/phantasmophobia/logo.png
description: Ghost searching 3D game with AI agents and a procedurally generated (PCG) map.
---

# Garry's Phantasmophobia

The goal of the project is to create a single player game, where we will have AI agents and a procedurally generated (PCG) environment: *Ghost hunter in a manor*. The game setting is located in an indoor environment: a manor. The player takes the role of a ghost hunter. There are small spirits that move around and we need to capture them to unhaunt the manor. This setting gives way for doing *Hide & Seek* in interior terrain. Spirits have human unusual abilities such as travelling through locked doors. This adds potential complexity to the PCG requirements, and the gameplay mechanics.

![preview](/assets/img/phantasmophobia/ingame.png)
![preview_2](/assets/img/phantasmophobia/ghostcapture.png)

We design the AI of the ghosts, which employs a Finite State Machine (FSM) technique for modelling different behaviors and exhibits smart strategies for hiding and fleeing within the manor.

![preview_3](/assets/img/phantasmophobia/fsm.png)

We also design a PCG algorithm based on cuboid rooms and inspired in a top-down approach, using prefabricated rooms which we assemble with our designed and tailored algorithm.

![preview_4](/assets/img/phantasmophobia/rooms.png)

The implementation of the game project is provided on [GitHub](https://github.com/jdecid/Garry-s-Phantasmophobia).

Developed together with **Josep de Cid**, **David Curto**, **Víctor Giménez** and **Arthur Müller**.
