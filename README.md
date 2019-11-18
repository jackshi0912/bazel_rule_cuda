# bazel_rule_cuda
rules for bazel for build cuda code

port most code from tensorflow, use at risk

usage:

```python
#WORKSPACE

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
  name = "bazel_rule_cuda",
  strip_prefix = "bazel_rule_cuda-<version>"
  url = ""https://github.com/jackshi0912/bazel_rule_cuda/archive/<version>.zip"
  # Lookup in release of this repo.
)
load("@bazel_rule_cuda//gpus:cuda.bzl", "cuda_configure")
cuda_configure(name="local_config_cuda")


#BUILD
load('@bazel_rule_cuda//gpus:cuda.bzl',cuda_library)

cuda_library(
  name='mycudalib',
  srcs='vectorAdd.cu.cc',
  hdrs=['main.h'],
  deps=[],
)

cc_binary(
  name='main',
  srcs=['main.cc'],
  hdrs=['main.h'],
  deps=[':mycudalib'],
)

#defalt build with -G -g to nvcc
bazel build :main
#defalt compile opt
bazel build -c opt :main
```
