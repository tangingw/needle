# Hacking Notes
**Note: This hack is for Raspberry Pi 4 with lower RAM (4 GB)**

This is an alternative hack on how you can add the `*.so` into the `needle/_init_.py`, through downloaded wheel files

For `cactus-needle` installation guide, you may refer [peppe8o.com](https://peppe8o.com/needle-2-raspberry-pi-benchmark-guide/)

## Easy Hack
You can refer to commit [`6e33cbd`](https://github.com/cactus-compute/needle/commit/6e33cbd42ea14d19de48317ffb17b15a88b9cbf0) by changing the value
```python
ENGINE_VERSIONS = {
    2: "2.0.4",
    3: "3.0.2",
}
```

## Hard Hack (The following hack was recommended by Gemini)
### Before You Start
1. Download wheel file
  ```bash
    cd needle
    wget https://huggingface.co/Cactus-Compute/needle3/resolve/main/python/cactus_needle-3.0.1-py3-none-manylinux2014_aarch64.whl

  ```
2. Check your wheel file
  ```bash
  file cactus_needle-3.0.0-py3-none-manylinux2014_aarch64.whl
  ```
The correct output should be: `cactus_needle-2.0.1-py3-none-manylinux2014_aarch64.whl: Zip archive data, at leas>

Please unzip the wheel file
  ```bash
  unzip ${HOME}/needle/cactus_needle-3.0.0-py3-none-manylinux2014_aarch64.whl \ 
    -d ${HOME}/needle/extract_whl_3

  ```
### Where to Find
You can add the following line to the function `def __load_cdll(generation)` in the path `needle/__init__.py`. Comment the line with `path = _library_path(generation)` in the function, and change the `path` as below:
  ```python
  def _load_cdll(generation):
      path = "<Your_home_directory>/needle/extract_whl_3/needle/libneedle.so"
      # path = _library_path(generation)
  ```
