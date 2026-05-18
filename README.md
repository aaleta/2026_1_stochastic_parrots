# 2026 Computational Physics – 1 Stochastic Parrots

This repository contains exercises and exams from the 2026 *Computational Physics* course of the Physics Degree at the University of Zaragoza. The problem statements are written in Spanish, but the code and comments are in English. For more details and examples, [click here](https://aaleta.github.io/teaching/).

This is an implementation of Llama 2 inference in C, based on Andrej Karpathy's [llama2.c](https://github.com/karpathy/llama2.c). This version works **only with the int8-quantized format** (`runq.c` style checkpoints), so any model you want to run must be exported using the quantization procedure documented in the original repository.

---

## Contents
- 📄 **Problem statement** (in Spanish)
- 💻 **Starter code** with automated tests
- 🧪 **Short exams** that build upon the original problem (in Spanish)
- 📊 **Plot scripts** (Gnuplot) to visualize the model output

## Model Weights

You need a model checkpoint compatible with the Llama 2 architecture, **exported in the int8-quantized format** used by `llama2.c`. To produce one, follow the export/quantization instructions in the [llama2.c README](https://github.com/karpathy/llama2.c) (look for the `export.py` script and the `--version 2` quantized export option). Place the resulting `.bin` file in the `models/` folder.

Suggested models to start from:

- **[TinyLlama](https://github.com/jzhang38/TinyLlama)**: A small language model trained on 3 trillion tokens. Download the weights from the original repository and export them in quantized form using `llama2.c`.
- **[TinyStories](https://huggingface.co/datasets/roneneldan/TinyStories)**: A compact model trained on children's stories. Karpathy's repo provides links to pre-trained TinyStories checkpoints; export the one you choose in quantized form.

Non-quantized checkpoints will **not** load with this code.

---

## How to Use

1. **Clone this repository**.

2. **Check the problem statement** (`docs/enunciado.pdf`) to understand the task.

3. **Open the starter code** and complete the missing functions.
The code is split across several files (`dynamics.c`, `transformer.c`, `sampler.c`, etc.), and tests are included to verify correctness.

4. **Run the tests** using the VS Code play button (see Compilation Notes below).
Make sure all tests pass before moving on.

5. **Download a model** and place it in the `models/` folder.

6. **Run the model** in either *generate* or *chat* mode (see Running the Code below).

7. **Optional**: try the short exams (`docs/examenA.pdf`, ...), which require extending your code to new features.

8. **Visualize results**:
Use the Gnuplot script in the `plots/` folder to plot the logits produced by the model.

## Compilation Notes

The `.vscode/` folder contains `launch.json` and `tasks.json` configurations so that everything can be built and run directly from Visual Studio Code using the play button (F5):

- **Compile and Run Tests** — builds `tests/public_tests` and launches it under the debugger.
- **Compile Parrot Only** — builds the `parrot` executable.

Platform notes:

- ✅ **Windows**: ready to compile out of the box with the provided `.vscode` configuration (you may need to update the compiler path).

- 🐧 **Linux / macOS**: it should also work out of the box, but it hasn't been tested on macOS. If it doesn't work, you may need to make small changes in the `.vscode` configuration files.

## Running the Code

Once compiled, the `parrot` executable can be run from the command line.

### Generate Mode

Generates text starting from a prompt.

```bash
./parrot <model> -m generate -i "Your prompt here" [extra options]
```

### Chat Mode

Engages the model in a conversation.

```bash
./parrot <model> -m chat -i "Initial message" -y "System prompt" [extra options]
```

### Parameters

- `<model>`: Path to the model checkpoint file (e.g. `models/tinyLlama.bin`)
- `-m <string>`: Mode: `generate` or `chat` (default: `generate`)
- `-i <string>`: Input prompt
- `-y <string>`: System prompt for chat mode (optional)
- `-t <float>`: Temperature for sampling (default `1.0`). Lower values make output more deterministic.
- `-s <int>`: Random seed (default: current time)
- `-n <int>`: Number of steps to generate (default `256`). `0` means maximum sequence length.

> On Windows the executable is `parrot.exe` instead of `parrot`.

## Requirements

- A C compiler (e.g. gcc)

- Visual Studio Code (recommended)

- Gnuplot (for the plotting scripts)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
