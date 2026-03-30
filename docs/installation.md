# Installation

## Precompiled Binaries

=== "Conda (recommended)"

    ```bash
    conda install -c conda-forge -c bioconda metabuli
    ```

=== "Linux AVX2"

    ```bash
    # Fast build — recommended for most Linux systems
    # Check AVX2 support: cat /proc/cpuinfo | grep avx2
    wget https://mmseqs.com/metabuli/metabuli-linux-avx2.tar.gz
    tar xvzf metabuli-linux-avx2.tar.gz
    export PATH=$(pwd)/metabuli/bin/:$PATH
    ```

=== "Linux SSE2"

    ```bash
    # Slower build for older systems
    wget https://mmseqs.com/metabuli/metabuli-linux-sse2.tar.gz
    tar xvzf metabuli-linux-sse2.tar.gz
    export PATH=$(pwd)/metabuli/bin/:$PATH
    ```

=== "macOS (Universal)"

    ```bash
    # Works on Apple Silicon and Intel Macs
    wget https://mmseqs.com/metabuli/metabuli-osx-universal.tar.gz
    tar xvzf metabuli-osx-universal.tar.gz
    export PATH=$(pwd)/metabuli/bin/:$PATH
    ```

Metabuli also works on Linux ARM64 and Windows systems. See [https://mmseqs.com/metabuli](https://mmseqs.com/metabuli) for static builds for other architectures.

---

## Compile from Source

```bash
git clone --recurse-submodules https://github.com/steineggerlab/Metabuli.git
cd Metabuli
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j 16
```

The built binary can be found in `./build/src`.

---

## GUI Application

The [Metabuli App](https://github.com/steineggerlab/Metabuli-App) provides a graphical interface for Windows, macOS, and Linux. Download it [here](https://github.com/steineggerlab/Metabuli-App/releases) — no separate Metabuli installation is needed.
