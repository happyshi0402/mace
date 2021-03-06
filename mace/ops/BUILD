# Description:
#
package(
    default_visibility = ["//visibility:public"],
)

licenses(["notice"])  # Apache 2.0

load(
    "//mace:mace.bzl",
    "if_android",
    "if_neon_enabled",
    "if_openmp_enabled",
    "if_android_armv7",
    "if_hexagon_enabled",
    "if_opencl_enabled",
    "if_quantize_enabled",
)

cc_library(
    name = "common",
    srcs = glob(
        [
            "common/*.cc",
        ],
    ),
    hdrs = glob(
        [
            "common/*.h",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        "//mace/core",
    ],
)

cc_library(
    name = "testing",
    srcs = glob(
        [
            "testing/*.cc",
        ],
    ),
    hdrs = glob(
        [
            "testing/*.h",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        "//mace/core",
        "@gtest//:gtest",
    ],
)

cc_library(
    name = "ref_kernels",
    srcs = glob(
        [
            "ref/*.cc",
        ],
    ),
    hdrs = glob(
        [
            "ref/*.h",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        ":common",
        "//mace/core",
    ],
)

# After refactor, all arm neon kernels go here.
# Could be shipped to other product use.
cc_library(
    name = "arm_neon_kernels",
    srcs = glob(
        [
            "arm/fp32/*.cc",
        ],
        exclude = [
            "arm/fp32/*_test.cc",
        ],
    ) + if_quantize_enabled(glob(
        [
            "arm/q8/*.cc",
        ],
        exclude = [
            "arm/q8/*_test.cc",
        ],
    )),
    hdrs = glob(
        [
            "arm/fp32/*.h",
        ],
    ) + if_quantize_enabled(glob(
        [
            "arm/q8/*.h",
        ],
    )),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        ":common",
        "//mace/core",
    ],
)

# After refactor, all GPU OpenCL kernels go here.
# Could be shipped to other product use.
cc_library(
    name = "opencl_kernels",
    srcs = glob(
        [
            "opencl/*.cc",
            "opencl/**/*.cc",
            "buffer_transform.cc",
            "lstm_cell.cc",
        ],
        exclude = [
            "opencl/*_test.cc",
        ],
    ),
    hdrs = glob(
        [
            "opencl/*.h",
            "opencl/**/*.h",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        ":common",
        "//mace/core",
    ],
)

cc_library(
    name = "arm_neon_kernels_test",
    srcs = glob(
        [
            "arm/fp32/*_test.cc",
        ],
    ) + if_quantize_enabled(glob(
        [
            "arm/q8/*_test.cc",
        ],
    )),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        ":arm_neon_kernels",
        ":ref_kernels",
        ":testing",
        "@gtest//:gtest",
    ],
    alwayslink = 1,
)

cc_library(
    name = "opencl_kernels_test",
    srcs = glob(
        [
            "opencl/*_test.cc",
            "opencl/**/*_test.cc",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        ":opencl_kernels",
        ":ref_kernels",
        ":testing",
        "@gtest//:gtest",
    ],
    alwayslink = 1,
)

cc_library(
    name = "internal_ops",
    srcs = glob(
        [
            "*.cc",
            "arm/*.cc",  # remove it after refactor
        ],
        exclude = [
            "*_test.cc",
            "*_benchmark.cc",
            "ops_registry.cc",
            "ops_test_util.cc",
            "lstm_cell.cc",  # TODO: move it into opencl
            "buffer_transform.cc",  # TODO: move it into opencl
            "quantize.cc",
            "quantization_util.cc",
            "arm/*_test.cc",  # remove it after refactor
        ],
    ) + if_quantize_enabled(
        glob(
            [
                "quantize.cc",
                "quantization_util.cc",
            ],
        ),
    ),
    hdrs = glob(
        [
            "*.h",
            "arm/*.h",  # remove it after refactor
        ],
        exclude = [
            "ops_registry.h",
            "ops_test_util.h",
            "fixpoint.h",
            "gemmlowp_util.h",
            "quantization_util.h",
        ],
    ) + if_quantize_enabled(glob([
        "fixpoint.h",
        "gemmlowp_util.h",
        "quantization_util.h",
    ])),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = if_android(["-lm"]),
    deps = [
        ":ref_kernels",
        "//mace/core",
    ] + if_quantize_enabled([
        "@tflite",
        "@gemmlowp",
    ]) + if_neon_enabled([
        ":arm_neon_kernels",
    ]) + if_opencl_enabled([
        ":opencl_kernels",
    ]),
)

cc_library(
    name = "ops",
    srcs = glob(
        [
            "ops_registry.cc",
        ],
    ),
    hdrs = glob(
        [
            "ops_registry.h",
        ],
    ),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = if_android(["-lm"]),
    deps = [
        "internal_ops",
    ],
)

cc_library(
    name = "test",
    testonly = 1,
    srcs = [
        "ops_test_util.cc",
    ],
    hdrs = glob([
        "*_test_util.h",
    ]),
    copts = [
        "-Werror",
        "-Wextra",
    ] + if_openmp_enabled(["-fopenmp"]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
    ]) + if_android_armv7([
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        "ops",
        "testing",
        "@gtest",
    ],
)

cc_test(
    name = "ops_test",
    testonly = 1,
    srcs = glob(
        [
            "*_test.cc",
            "arm/*_test.cc",  # remove it after refactor
            "ops_test_util.cc",
        ],
        exclude = [
            "fixpoint_test.cc",
        ],
    ) + if_quantize_enabled(glob(
        [
            "fixpoint_test.cc",
        ],
    )),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = ["-fopenmp"],
    linkstatic = 1,
    deps = [
        ":ops",
        ":test",
        "@gtest//:gtest_main",
    ] + if_neon_enabled([
        ":arm_neon_kernels_test",
    ]) + if_opencl_enabled([
        ":opencl_kernels_test",
    ]),
)

cc_test(
    name = "ops_benchmark",
    testonly = 1,
    srcs = glob(["*_benchmark.cc"]),
    copts = [
        "-Werror",
        "-Wextra",
        "-Wno-missing-field-initializers",
    ] + if_openmp_enabled([
        "-fopenmp",
    ]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_quantize_enabled([
        "-DMACE_ENABLE_QUANTIZE",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = ["-fopenmp"],
    linkstatic = 1,
    deps = [
        ":ops",
        "//mace/benchmark:statistics",
        "//mace/core:test_benchmark_main",
        "//third_party/eigen3",
    ],
)
