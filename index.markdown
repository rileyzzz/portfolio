---
layout: default
---

# My Portfolio

My passion for creating digital media stems from my drive to innovate upon the experiences I love while also creating something new for audiences to enjoy.

In my projects, I am motivated by a few core principles:
- Always do something new.
- Make a point of going outside the box.
- Work on things people will love - creators AND players.
- "Wow" the audience. With every project, my audience should always have at least one interesting takeaway.

I'm inspired by beauty of a project that "just works". Whether that means a [simple Python script](https://github.com/rileyzzz/BlenderIMExporter) or a [custom-built compiler](https://github.com/rileyzzz/dextr), I excel at making lots of tiny pieces work in tandem to form an impressive whole.


## DEX

An LLVM driver/Emscripten fork I wrote that can take C/C++ source code and translate it into *safe C#*.
The IR translator is a C++ commandline app, and the encompassing tooling etc. are all written in Python.

#### Quake running in pure C#????
![Quake in C#](img/dex_2.png)

### Why?

The same reason Emscripten (in its original incarnation, before the days of WebAssembly) was created: "why not?"

But the real reason is also the same as Emscripten's; JavaScript was created to solve the question of "how can we make a language that's safe enough to run unsupervised in your browser?", and Emscripten is the compiler nerd's way of getting around that so they can run unsafe pointer-heavy code in a "safe" way.

Facepunch Studios has been working on this new game platform called [s&box](https://sbox.game/about).
If you haven't heard of s&box, it's basically just Roblox but with C# instead of Lua, and it runs on Source 2.
Facepunch's way of making it safe to run untrusted C# on potentially thousands of computers is by using Roslyn and some fancy code analyzers to enforce a pretty restrictive code whitelist.

And DEX is my way of getting around that, so I can run unsafe code in an environment where it's not supposed to be possible to run unsafe code.
[You can read more here. There's a ton of s&box-specific stuff I've added to the toolset, like a shader compiler, graphics commands, filesystem integration, and even a faux OpenGL driver - definitely worth a read.](https://sbox.game/rileyzzz/retrobox/news/dex-8601de05)

![Snippet from a generated DEX module](img/dex_0.png)

### How?

It's a lot like the original version of Emscripten before WebAssembly, but built from the ground up for C#; it'll take all of your C/C++ source code, compile it with clang, then instead of generating machine code, it hoists the LLVM IR instructions back up into C# expressions and tidies it up into a nice minfied module for you.

The best part is it's completely safe. No pointers, syscalls, etc. Memory in DEX is a managed byte array.

And it'll accept whatever you throw at it, because it's running clang under the hood.
If clang can compile it, DEX can compile it too.
It's even a drop-in replacement for most projects' build systems, because I've put together custom commandline tooling which mirrors that of GCC/clang/Emscripten.
Replace gcc/emcc/g++/em++ with dexcc/dex++ and it'll just work.

So far I've ported Doom and Quake, emulators like snes9x and mupen64plus, and LuaC.
And turns out - the generated modules are actually wicked fast.
Like, faster than they should be.
.NET's JIT compiler has been kind of superpowered lately and somehow it's made DEX modules not only viable, but fast as hell.

![Snippet from DEX's IR translator](img/dex_1.png)

## Retrogression

Unity, C#, HLSL, Art, and Music

Retrogression was my course project for CSC 4263 'Video Game Design' at LSU over the Spring 2023 semester.
I was responsible for gameplay programming, low-level physics programming, and sound design in a team of four students.


<iframe width="700" height="315" src="https://www.youtube.com/embed/bPfSPVumTkA?si=lqp75K9fnN-iilnX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


Getting the physics to work in the game was a challenge.
Unity's physics engine (PhysX) wouldn't support the kinds of complex interactions that our gameplay required.
So, I wrote a little **homebrew physics engine** on top of Unity's PhysX that allowed us to subtract matter from walls at runtime and have all the game's physics bodies react.

I also put together a **fully custom player controller** to replace Unity's builtin player movement physics.
Valve's Portal was a heavy inpiration for this project, so I researched the Source engine movement behavior and took the time to emulate the classic Half-Life walk and run speed, crouch-jumping, ground friction, etc in the game. We wanted to subconsciously trick the player into thinking they were playing Portal despite our game being made in Unity 😃

## TMCCInterface

[C++, available on GitHub](https://github.com/rileyzzz/TMCCInterface)

TMCCInteface is a software driver for **Lionel’s Trainmaster Command Control** (TMCC) protocol.
It allows the programmer to control locomotives on a Lionel trainset via the official TMCC serial protocol.
I created this code library in late 2022 and updated it throughout 2023 with various demo projects.

![TMCCInterface Demo](img/tmcc_thingy.png)

One of the demo projects was a fun social experiment I organized, **Twitch Plays Lionel**.
This was an ongoing Twitch livestream where chat members could type in commands (!throttle, !bell, !junction) to move a locomotive around a model train layout.

We tested TwitchPlaysLionel at a model railway club using a Lionel camera car.
Chat members could get a first person view as they drove the train around the layout, and I put together a speedometer display and command log for some extra flair.

All of the stream HUD was updated in realtime based on data received from the locomotive. The backend was written in JavaScript using NodeJS, interacting with a C++ program listening for commands over a local socket.
The frontend stream display used HTML5 web panels to make the experience responsive, which also involved some JavaScript and CSS styling.

## Rogue Arena

C#, Razor, HLSL

I built Rogue Arena with the wonderful folks at [Eagle One](https://eagleone.dev/). The project was created over the course of a month, using the closed beta of [Facepunch's new 's&box' game engine](https://sbox.game/).

The game was entered into Facepunch's first game contest [and won 3rd place](https://sbox.game/c/gamejam1/results) (£2,500!) out of nearly 100 entries.

<iframe width="700" height="315" src="https://www.youtube.com/embed/3VZJULzSe_4?si=kbfhiKexCl5EltWg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My role on this project was mainly the UI design and implementation, though I helped workshop gameplay elements aswell.
UI in S&box is written in ASP.NET Razor, which is HTML/CSS based but mixes in C# instead of JavaScript to control visual elements.
The result is a responsive, web-based UI that looks pretty while scaling effortlessly across devices.

![Rogue Arena shop](img/rogue_shop.png)

I was also responsible for the game's medieval dartboard-style shop interface.
The shop boards are generated dynamically based on your progress in the game, and clicking on the boards fires an arrow in the 3d world that causes them to react.
On day 1, players were immediately drawn to the shop interface and it became one of the iconic elements of the game 😃

In the early stages of development, I also put together a 'Diablo 2'-style health and mana display that would react to the player's movements in the world.

<video height="300" controls>
  <source src="img/rogue_health_low.mp4" type="video/mp4">
</video>

The effect is a 2D HLSL shader built right into the UI (under the hood, it's actually a mini-raymarcher!) that I was quite proud of.
We decided to cut it from the final game, but it was a very unique effect which I plan to reuse at some point.

## Trainzmesh

In early 2020, I put together a set of tools to view and modify the mesh format used by content in [N3V Games'](https://n3vgames.com/) **Trainz** series.

![Trainzmesh Viewer](img/trainzmesh.webp)

The tools filled a gap in the content creation pipeline for Trainz, as issues with meshes were often tricky and complicated for artists to debug. The tools save them significant time by giving them a realtime display of their mesh as it's interpreted by the game engine to help them diagnose issues.

The tools were written in C++, and used OpenGL and Dear ImGUI to display a 3d preview of the mesh file, as well as a listing of its fields for content creators to edit. The renderer is fully PBR to match the game engine, and is integrated with the game's content formats through some heavy reverse engineering.

I made the tools available to content creators in 2020, and they accumulated hundreds of downloads over several years.
Since creating these tools, I have been employed as a developer at N3V Games.
<!-- 
## Music Projects

As a classically trained musician and Ableton enthusiast, I've created several original compositions, many for personal use in my game projects. Here are a few of them.

### 'The Dearth'

<iframe src="https://drive.google.com/file/d/1dLwxx5pF0J6GYMl4_ijm9TyAmRYmZbNM/preview" width="500" height="80" allow="autoplay"></iframe>

A synthwave-heavy pop song, full of little harmonic surprises.
The song layers onto itself as it progresses, then it explodes at the end with a fun little guitar solo.
One of my (inadvertent) inspirations for this was Murray Gold's orchestral stuff in Doctor Who (particularly Season 4).
Plenty of bittersweet tubular bells.

### Signal Crew

<iframe src="https://drive.google.com/file/d/1qDF2kcz_uT7kzIaf857kzf3vFP1daiDC/preview" width="500" height="80" allow="autoplay"></iframe>

This was the menu theme for a gamejam project that fizzled out.
The game was a class based co-op alien hunting game (similar to Signal Simulator, Voices of the Void). You can hear some of that alien inspiration reflected in the song 😃

### Ridicule

<iframe src="https://drive.google.com/file/d/1yMMcuxu3FMhJX2IQ471KhTOm6rDKldiK/preview" width="500" height="80" allow="autoplay"></iframe>

Looping menu music for my Global Game Jam 2024 project at LSU, created start-to-finish in just under a week. A modern-ish lead with a funky driving piano backing it up (the result of a short-lived [Robbie Nevil obsession](https://www.youtube.com/watch?v=CGtf9QfITQw)).

### '80's Thing'

<iframe src="https://drive.google.com/file/d/1sSxiyDA5UPnhsNQMXgQqWL9eD3qukbue/preview" width="500" height="80" allow="autoplay"></iframe>

As the name suggests, heavy 80's/early-90's influence, with a cheesy steel drum and a pan flute to boot. Mall-core? The main section is loosely inspired by David Gamson's style of counterpoint (Al Jarreau, Scritti), but the B section draws its melody from Shanice's 'I Love Your Smile'. Then I mix them both together at the end 😃

### Clock Level

<iframe src="https://drive.google.com/file/d/1doh7rZ547CeC8nmf9RQ0abiMC8WFT3K8/preview" width="500" height="80" allow="autoplay"></iframe>

Couldn't resist making this when a friend sent me a pack of steam whistle sound effects.
Very metal... slow buildup and then boom! Reminds me of a kettle boiling over.
My main inspiration for the track was Mario Kart's 'Tick Tock Clock' level, as well as Animusic's 'Drum Machine' music video. -->