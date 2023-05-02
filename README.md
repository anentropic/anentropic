# Selected projects

- ### [twenty-questions-bot](https://github.com/anentropic/twenty-questions-bot)
  `python` Langchain chatbot (GPT-3.5) that plays the "20 Questions" game. Gradio app - run locally for now (set your OpenAI API key first).
  
  Inspired by this tweet https://twitter.com/goodside/status/1643123149406367745 which notes how ChatGPT is _unable_ to play 20 Questions due to lack of private memory.
  
  Adding the memory was easy, the harder part was getting it to validate that the player was asking a yes/no question, and for the bot to reply with only yes/no/sometimes/I don't know. Plenty of rough edges to polish, but have been able to successfully play some games of 20 Questions against the bot!
 
- ### [hft2ane](https://github.com/anentropic/hft2ane) 🤗🤖➔🍏🧠
  #### HuggingFace Transformers ➔ to ➔ Apple Neural Engine
  
  `python` Beginning in early 2023 there has been an explosion of interest in running LLMs locally (e.g. [llama.cpp](https://github.com/ggerganov/llama.cpp)). Recent Apple devices (M1, M2, iPhone) have a Neural Engine chip for accelerating ML model inference. My impression is this was mostly designed for camera/vision applications in the iPhone. But for language models with Transformer architecture it seems some tweaks are needed, hence this demo repo from Apple: https://github.com/apple/ml-ane-transformers
  
  Apple only implemented one variant of DistilBERT model (showing a 10x speedup), but there are hundreds of interesting models on HuggingFace Hub which could benefit from this.
  
  hft2ane implements more model types, and provides a convenient cli frontend for taking any pre-trained model of a supported type on HuggingFace Hub and exporting it in Neural Engine-optimised format.

- ### [chuckd](https://github.com/anentropic/chuckd)
  `java` (out of necessity more than choice)
  
  chuckd is a "schema evolution validation tool" supporting JSON Schema, Avro and Protobuf. It is a cli tool designed to be run as part of a CI/CD pipeline.
  
  In the context of a multi-service application backend you want to be able to validate that only backwards-compatible changes are made to the message schemas which different services use to communicate with each other. So you need a "schema evolution validation tool".
  
  chuckd repurposes some parts of Confluent Schema Registry as a backend-agnostic cli tool, to provide validation only without needing a Kafka cluster.
  
  This project has an extensive build pipeline in GitHub Actions which builds binaries, Docker images, and publishes to Homebrew package manager.
  
- ### [spectrum](https://github.com/anentropic/ocaml-spectrum)
  `ocaml` After 10+ years of intensive Python work at various companies I was curious to try something different. I was attracted to OCaml as a pragmatic functional language.
  
  Spectrum is a library for colour and formatting in the terminal, inspired by the many libs of that sort for Python and also [chalk.js](https://github.com/chalk/chalk)
  
  AFAIK it is different from any other OCaml terminal colours lib by leveraging the language's support for styling via format-string DSL, and also providing access to modern 256 and 24-bt colour palettes. It has been an useful learning project, exercising some interesting corners of the language including an [ocamllex](https://v2.ocaml.org/manual/lexyacc.html#s%3Aocamllex-overview) parser for the DSL and a customer PPX macro-preprocessor.
  
- ### [megaparsy](https://github.com/anentropic/megaparsy)
  `python` This library is a port of some of the parser combinators from Haskell's **Megaparsec** to the Python library **parsy**.
  
  It is surprising how smoothly these translated over, considering the difference between the two languages. I put this down to parsy's clever use of Python generators to mimic Haskell's monadic `do` notation.
  
  This was a yak I had to shave in order to complete https://github.com/anentropic/python-waterloo ...which is a parser (and refactor tool) to extract unchecked type info from Python docstrings and convert them to checkable type annotations.
  
- ### [glsl-shaderinfo](https://github.com/anentropic/python-glsl-shaderinfo)
  `rust`/`python` For a while I was experimenting with OpenGL graphics in Python (see also https://github.com/anentropic/pyglslify)
  
  I wanted a way to introspect the defined inputs and outputs of GLSL shader code. glsl-shaderinfo is a Python library built in Rust using the PyO3 toolchain, leveraging a GLSL parser crate that was superior to anything I could find on PyPI.
