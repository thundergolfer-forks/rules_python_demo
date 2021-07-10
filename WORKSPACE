workspace(name = "demo")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

load("//tools/build/bazel/py_toolchain:py_interpreter.bzl", "python_build_standalone_interpreter")

python_build_standalone_interpreter(
    name = "python_interpreter",
)

# Public python rules for build/test
#http_archive(
#    name = "rules_python",
#    sha256 = "934c9ceb552e84577b0faf1e5a2f0450314985b4d8712b2b70717dc679fdc01b",
#    urls = [
#        "https://github.com/bazelbuild/rules_python/releases/download/0.3.0/rules_python-0.3.0.tar.gz",
#    ],
#)
local_repository(
    name = "rules_python",
    path = "/Users/jonathon/work/rules_python",
)
#http_archive(
#    name = "rules_python",
#    sha256 = "778197e26c5fbeb07ac2a2c5ae405b30f6cb7ad1f5510ea6fdac03bded96cc6f",
#    urls = [
#        "https://github.com/bazelbuild/rules_python/releases/download/0.2.0/rules_python-0.2.0.tar.gz",
#    ],
#)

##################
# Python toolchain
##################

# xxx

#####################
# Python dependencies
#####################

load("@rules_python//python:pip.bzl", "pip_parse")

# Create a central repo that knows about the dependencies needed from requirements.txt.
pip_parse(
   name = "deps",
   # Must be a locked requirements file
   requirements_lock = "//scripts/demo:requirements.txt",
   # Use the interpreter provided by the toolchain
   #  python_interpreter_target = "@tools_py_38//:dist/python/bin/python3",
   python_interpreter_target = "@python_interpreter//:python/install/bin/python3.8"
)
# Create repositories for every dependency so it can be lazily installed
load("@deps//:requirements.bzl", "install_deps")
install_deps()

register_toolchains("//tools/build/bazel/py_toolchain:py_toolchain")
