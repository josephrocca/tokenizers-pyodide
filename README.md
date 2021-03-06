# Tokenizers Pyodide/Wasm/Web Port
Web/Pyodide port of Hugging Face's Tokenizers lib. Will (hopefully) soon be integrated into the official Pyodide package list so this repo will hopefully become obsolete.

**Demo:** https://josephrocca.github.io/tokenizers-pyodide/demo

Thanks to @Narsil, @mbrunel, and @messense for making this possible.

 * @Narsil: https://github.com/huggingface/tokenizers/pull/1009
 * @mbrunel: https://github.com/mithril-security/tokenizers-wasm
 * Discussion: 
   * https://github.com/huggingface/tokenizers/issues/935
   * https://github.com/huggingface/tokenizers/issues/63
   * https://github.com/huggingface/tokenizers/issues/1010

## Build instructions:
Visit [this branch](https://github.com/josephrocca/tokenizers/tree/pyodide) and start a Github Codespace on it, then run these commands:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source $HOME/.cargo/env
rustup toolchain install nightly
rustup target add --toolchain nightly wasm32-unknown-emscripten
rustup component add rust-src --toolchain nightly-x86_64-unknown-linux-gnu
cargo install --git https://github.com/PyO3/maturin.git maturin # tested and working at commit hash 05169de
git clone https://github.com/emscripten-core/emsdk.git # tested and working at commit hash 517e02f
cd emsdk
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
cd ../bindings/python
RUSTUP_TOOLCHAIN=nightly maturin build --release -o dist --target wasm32-unknown-emscripten -i python3.10
```
That'll produce a `.whl` in the `dist` folder that should work with Pyodide.

Here's a Colab notebook to compare the demo against: https://colab.research.google.com/github/josephrocca/tokenizers-pyodide/blob/main/demo/Hugging_Face_Tokenizers_Minimal_Test_with_dalle_bart_mini.ipynb

## Notes:

* Here's the issue that tracks tokenizers' eventual addition to official Pyodide package repo: https://github.com/pyodide/pyodide/issues/2816
