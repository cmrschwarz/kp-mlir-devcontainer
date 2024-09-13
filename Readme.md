# Devcontainer Setup for KP MLIR

## Usage Instructions

0. Download this repository

1. Make sure the git submodules are initialized:

```
git submodule init
git submodule update
```

2. Make sure [VSCode](https://code.visualstudio.com/download?) and the [Devcontainer Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) are installed

3. Open the main folder of this repository in VSCode

4. Click the 'Reopen in Container' Popup

5. Wait for the Dev Container to be built (this can take quite a while, check the Debug Console Window to see a progress report)

You should now have a dev environment with the correct LLVM-Version, Compiler and
C++ / Scala Language Servers installed.

If you want to use github to manage your changes, fork the [kp-mlir-sigi-mlir](https://github.com/tud-ccc/kp-mlir-sigi-frontend.git) and [kp-mlir-sigi-mlir](https://github.com/tud-ccc/kp-mlir-sigi-mlir) repositories and change their urls in the `.gitmodules` file to your forks. You have to reinitialize the submodules afterwards.
