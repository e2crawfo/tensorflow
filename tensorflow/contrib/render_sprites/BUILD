licenses(["notice"])  # Apache 2.0 License

exports_files(["LICENSE"])

package(default_visibility = ["//visibility:public"])

load(
    "//tensorflow:tensorflow.bzl",
    "tf_custom_op_library",
    "tf_custom_op_py_library",
    "tf_gen_op_libs",
    "tf_gen_op_wrapper_py",
    "tf_kernel_library",
)
load("//tensorflow:tensorflow.bzl", "cuda_py_test")

tf_custom_op_py_library(
    name = "render_sprites_py",
    srcs = ["__init__.py"] + glob(["python/ops/*.py"]),
    dso = [":python/ops/_render_sprites_ops.so"],
    kernels = [
        ":render_sprites_ops_kernels",
        ":render_sprites_ops_op_lib",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":render_sprites_ops",
        "//tensorflow/contrib/util:util_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:platform",
        "//tensorflow/python:util",
        "//third_party/py/numpy",
    ],
)

tf_kernel_library(
    name = "render_sprites_ops_kernels",
    prefix = "render_sprites_ops",
    deps = [
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
    ],
    alwayslink = 1,
)

tf_custom_op_library(
    name = "python/ops/_render_sprites_ops.so",
    srcs = [
        "kernels/render_sprites_ops.cc",
        "kernels/render_sprites_ops.h",
        "ops/render_sprites_ops.cc",
    ],
    gpu_srcs = [
        "kernels/render_sprites_ops_gpu.cu.cc",
        "kernels/render_sprites_ops.h",
    ],
)

tf_gen_op_libs(
    op_lib_names = [
        "render_sprites_ops",
    ],
)

tf_gen_op_wrapper_py(
    name = "render_sprites_ops",
    deps = [":render_sprites_ops_op_lib"],
)

cuda_py_test(
    name = "render_sprites_ops_test",
    size = "small",
    srcs = ["python/ops/render_sprites_ops_test.py"],
    additional_deps = [
        ":render_sprites_py",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:errors",
        "//tensorflow/python:array_ops",
    ],
)
