package(default_visibility = ["//visibility:public"])

load(
    "@io_bazel_rules_go//go:def.bzl",
    "go_library",
)

go_library(
    name = "go_default_library",
    srcs = [
        "ascii.go",
        "tc_other.go",
        "term.go",
        "term_unix.go",
    ] + select({
        "@io_bazel_rules_go//go/platform:darwin_amd64": [
            "termios_darwin.go",
        ],
        "@io_bazel_rules_go//go/platform:linux_amd64": [
            "tc_linux_cgo.go",
        ],
        "@io_bazel_rules_go//go/platform:windows_amd64": [
            "term_windows.go",
        ],
        "//conditions:default": [],
    }),
    cgo = True,
    deps = select({
        "@io_bazel_rules_go//go/platform:windows_amd64": [
            "//vendor/github.com/Azure/go-ansiterm/winterm:go_default_library",
            "//vendor/github.com/docker/docker/pkg/term/windows:go_default_library",
        ],
        "//conditions:default": [],
    }),
)

filegroup(
    name = "package-srcs",
    srcs = glob(["**"]),
    tags = ["automanaged"],
    visibility = ["//visibility:private"],
)

filegroup(
    name = "all-srcs",
    srcs = [
        ":package-srcs",
        "//vendor/github.com/docker/docker/pkg/term/windows:all-srcs",
    ],
    tags = ["automanaged"],
)
