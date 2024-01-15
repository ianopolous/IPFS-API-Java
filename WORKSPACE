load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

RULES_JVM_EXTERNAL_TAG = "4.5"
RULES_JVM_EXTERNAL_SHA = "b17d7388feb9bfa7f2fa09031b32707df529f26c91ab9e5d909eb1676badd9a6"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "junit:junit:4.13.2",
        "org.hamcrest:hamcrest:2.2",
        "com.github.ipld:java-cid:v1.3.8",
    ],
    repositories = [
        # Private repositories are supported through HTTP Basic auth
        "https://jitpack.io",
        "https://repo1.maven.org/maven2",
    ],
)

load("@bazel_tools//tools/build_defs/repo:git.bzl", "new_git_repository")

MULTIADDR_BUILD_FILE = """
filegroup(
    name = "main_srcs",
    srcs = glob(["src/main/java/**"]),
)

java_library(
    name = "core",
    srcs = [":main_srcs"],
    deps = [
        "@maven//:com_github_multiformats_java_multihash",
        "@maven//:com_github_multiformats_java_multibase",
        "@maven//:com_github_ipld_java_cid",
    ],
    visibility = ["//visibility:public"],
)
"""

new_git_repository(
    name = "multiaddr",
    remote = "https://github.com/multiformats/java-multiaddr.git",
    tag = "v1.4.12",
    build_file_content = MULTIADDR_BUILD_FILE,
)