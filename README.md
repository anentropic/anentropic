# Selected projects

- ### [anagrapheus](https://github.com/anentropic/anagrapheus)
  #### An event-sourced timeline, belief store and identity layer for long-running LLM agents.

  `python` on `pydantic-ai` framework, `sqlite` and `doxastica`.

  anagrapheus combines a belief store with event-sourced architecture.

  Imagine a game-playing agent. Across a series of turns it builds up state in external memory stores, one of which is a model of its own and other players' beliefs (doxastica). Event-sourcing gives us an audit log (sqlite) of how the current state was arrived at.

  It can be used to build agents or simulations that run for many turns, such as negotiations, games with non-player characters, or interactive fiction, where several agents hold private beliefs about each other and where a run is too expensive or too random to repeat by re-running it.

  It gives a long-running AI agent one authoritative event log, and builds everything else (beliefs, entity identity, a consolidated history, assembled prompts) as state derived from that log.

  anagrapheus rests on two ideas:

  1. **One log; everything else is a fold.** The event log is append-only and is the only thing that is authoritative. A _fold_ is a function that applies events in log order to build some state. The state a fold builds is a _projection_: it can be dropped and rebuilt from the log at any time. Each projection records its _position_, the sequence number of the last event it has consumed, so it can catch up from there. Per-agent beliefs, the entity registry and the chronicle (consolidated history) are all projections.
  2. **Every draw is pinned.** A model call returns a different answer each time, so it is a _draw_. _Pinning_ a draw records its result under a key built from what was asked: the conversation, the model, the tools and the settings. A retry with the same key gets the recorded result instead of a new draw. _Replay_ answers every request from the recorded results and never calls the model. That is different from re-running, which calls the model again and gets new answers. If your code now asks something different, the key changes and replay stops with a `PinMiss` instead of quietly drawing a new answer.
 
- ### [doxastica](https://github.com/anentropic/doxastica/)
  #### Belief revision system based on append-only property graph.

  `python` on LadybugDB (graph db)

  An implementation of the [_"Graph-Native Cognitive Memory for AI Agents: Formal Belief Revision Semantics for Versioned Memory Architectures"_](https://arxiv.org/pdf/2603.17244) paper by Young Bin Park, with a multi-scope extension (original paper is single agent).

  doxastica keeps beliefs on append-only revision chains, records what rests on what, and when something is retracted or superseded it tells you which conclusions stand on ground that just moved. Knowledge is held per scope, so several holders (several agents, or an agent and the world) can believe contradictory things at once, and where they diverge is a query rather than a guess.

- ### [faker-jsonschema](https://github.com/anentropic/python-faker-jsonschema)
  #### Random data generator

  faker-jsonschema is a [Faker](https://faker.readthedocs.io/) provider that generates random data conforming to a [JSON Schema](https://json-schema.org/).

  Pass any JSON Schema dict to `faker.from_jsonschema()` and get back a valid, randomly generated value.

  1800+ unit and PBT tests aiming to ensure correctness. Limitations of our strategies are acknowledged in the docs.

- ### [chuckd](https://github.com/anentropic/chuckd)
  #### Schema evolutions validator

  `java` (out of necessity more than choice)
  
  chuckd supports JSON Schema, Avro and Protobuf. It is a cli tool designed to be run as part of a CI/CD pipeline.
  
  In the context of a multi-service application backend you want to be able to validate that only backwards-compatible changes are made to the message schemas which different services use to communicate with each other. So you need a "schema evolution validation tool".
  
  chuckd repurposes some parts of Confluent Schema Registry as a backend-agnostic cli tool, to provide validation only without needing a Kafka cluster.
  
  This project has an extensive build pipeline in GitHub Actions which builds binaries, Docker images, and publishes to Homebrew package manager.
  
- ### [spectrum](https://github.com/anentropic/ocaml-spectrum)
  #### Library for color and formatting in the terminal
  `ocaml` After 10+ years of intensive Python work at various companies I was curious to try something different. I was attracted to OCaml as a pragmatic functional language.
  
  Spectrum is a library for colour and formatting in the terminal, inspired by the many libs of that sort for Python and also [chalk.js](https://github.com/chalk/chalk)
  
  AFAIK it is different from any other OCaml terminal colours lib by leveraging the language's own support for styling via its format-string DSL, and also providing access to modern 256 and 24-bt colour palettes. It has been an useful learning project, exercising some interesting corners of the language including an [ocamllex](https://v2.ocaml.org/manual/lexyacc.html#s%3Aocamllex-overview) parser for the DSL and a customer PPX macro-preprocessor.

- ### [oktree](https://github.com/anentropic/ocaml-oktree)
  `ocaml` After 10+ years of intensive Python work at various companies I was curious to try something different. I was attracted to OCaml as a pragmatic functional language.

  A simple octree implementation in OCaml, intended to efficiently find nearest match for an arbitrary point among a set of points in 3D coordinate space.

  Originally written and benchmarked by hand, but subsequently optimised with AI.
  
- ### [megaparsy](https://github.com/anentropic/megaparsy)
  `python` This library is a port of some of the parser combinators from Haskell's **Megaparsec** to the Python library **parsy**.
  
  It is surprising how smoothly these translated over, considering the difference between the two languages. I put this down to parsy's clever use of Python generators to mimic Haskell's monadic `do` notation.
  
  This was a yak I had to shave in order to complete https://github.com/anentropic/python-waterloo ...which is a parser (and refactor tool) to extract unchecked type info from Python docstrings and convert them to checkable type annotations.
  
- ### [glsl-shaderinfo](https://github.com/anentropic/python-glsl-shaderinfo)
  `rust`/`python` For a while I was experimenting with OpenGL graphics in Python (see also https://github.com/anentropic/pyglslify)
  
  I wanted a way to introspect the defined inputs and outputs of GLSL shader code. glsl-shaderinfo is a Python library built in Rust using the PyO3 toolchain, leveraging a GLSL parser crate that was superior to anything I could find on PyPI.
