workspace(
    name = "create-react-app-ejected-bazel",
    managed_directories = {"@npm": ["node_modules"]},
)

node = {
    "version": "12.22.1",
    "sha256_macos": "de5e317580732530961d83b0fb9b2c370d222bd0c5a1b331900e9ddc0fdfe086",
    "sha256_linux": "8b537282c222ae4a40e019a52f769ca27b6640699bdde1510375e8d72da7d041",
    "sha256_win64": "0cf3545c1ff9717bf3196eed6a423d878709ed4560125fdc29b42bd80ee661c3",
    "sha256_arm64": "65145e6c2aa047ee5f83aadf9546116a6da70c21a649ed5f24dce412d2c202dc",
    "sha256_s390x": "c24dedddedf1a6aaff4ef40c2196f8f3c2cf99702c0be2ce6f77f740919f7dbf",
}

yarn = {
    "version": "1.22.10",
    "sha256": "7e433d4a77e2c79e6a7ae4866782608a8e8bcad3ec6783580577c59538381a6e",
}

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "8f5f192ba02319254aaf2cdcca00ec12eaafeb979a80a1e946773c520ae0a2c9",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/3.7.0/rules_nodejs-3.7.0.tar.gz"],
)

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

node_repositories(
    node_repositories = {
        "%s-darwin_amd64" % node.get("version"): (
            "node-v%s-darwin-x64.tar.xz" % node.get("version"),
            "node-v%s-darwin-x64" % node.get("version"),
            node.get("sha256_macos"),
        ),
        "%s-linux_amd64" % node.get("version"): (
            "node-v%s-linux-x64.tar.xz" % node.get("version"),
            "node-v%s-linux-x64" % node.get("version"),
            node.get("sha256_linux"),
        ),
        "%s-windows_amd64" % node.get("version"): (
            "node-v%s-win-x64.zip" % node.get("version"),
            "node-v%s-win-x64" % node.get("version"),
            node.get("sha256_win64"),
        ),
        "%s-linux_arm64" % node.get("version"): (
            "node-v%s-linux-arm64.tar.xz" % node.get("version"),
            "node-v%s-linux-arm64" % node.get("version"),
            node.get("sha256_arm64"),
        ),
        "%s-linux_s390x" % node.get("version"): (
            "node-v%s-linux-s390x.tar.xz" % node.get("version"),
            "node-v%s-linux-s390x" % node.get("version"),
            node.get("sha256_s390x"),
        ),
    },
    node_urls = ["https://nodejs.org/dist/v{version}/{filename}"],
    node_version = node.get("version"),
    yarn_repositories = {
        yarn.get("version"): (
            "yarn-v%s.tar.gz" % yarn.get("version"),
            "yarn-v%s" % yarn.get("version"),
            yarn.get("sha256"),
        ),
    },
    yarn_urls = ["https://github.com/yarnpkg/yarn/releases/download/v{version}/{filename}"],
    yarn_version = yarn.get("version"),
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    exports_directories_only = True,
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)
