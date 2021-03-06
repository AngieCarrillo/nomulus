package(
    default_visibility = ["//java/google/registry:registry_project"],
)

licenses(["notice"])  # Apache 2.0


java_library(
    name = "model",
    srcs = glob([
        "*.java",
        "*/*.java",
        "*/*/*.java",
    ]) + [
        "FieldExposerRegistry.java",
        ":field_exposers",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//java/com/google/common/annotations",
        "//java/com/google/common/base",
        "//java/com/google/common/cache",
        "//java/com/google/common/collect",
        "//java/com/google/common/hash",
        "//java/com/google/common/io",
        "//java/com/google/common/math",
        "//java/com/google/common/net",
        "//java/com/google/common/primitives",
        "//java/com/google/common/reflect",
        "//java/com/google/common/util/concurrent",
        "//third_party/java/appengine:appengine-api",
        "//third_party/java/dagger",
        "//third_party/java/joda_money",
        "//third_party/java/joda_time",
        "//third_party/java/jsr305_annotations",
        "//third_party/java/jsr330_inject",
        "//third_party/java/objectify:objectify-v4_1",
        "//third_party/java/re2j",
        "//third_party/java/servlet/servlet_api",
        "//java/google/registry/config",
        "//java/google/registry/util",
        "//java/google/registry/xml",
    ],
)

# Generate FieldExposer classes to work around AppEngine's security limitations.
genrule(
    name = "field_exposers",
    srcs = ["generate_field_exposer.sh"],
    outs = [
        "FieldExposer.java",
        "billing/FieldExposer.java",
        "common/FieldExposer.java",
        "contact/FieldExposer.java",
        "dns/FieldExposer.java",
        "domain/FieldExposer.java",
        "domain/allocate/FieldExposer.java",
        "domain/fee/FieldExposer.java",
        "domain/fee06/FieldExposer.java",
        "domain/fee11/FieldExposer.java",
        "domain/fee12/FieldExposer.java",
        "domain/flags/FieldExposer.java",
        "domain/launch/FieldExposer.java",
        "domain/rgp/FieldExposer.java",
        "domain/secdns/FieldExposer.java",
        "eppcommon/FieldExposer.java",
        "eppinput/FieldExposer.java",
        "eppoutput/FieldExposer.java",
        "export/FieldExposer.java",
        "host/FieldExposer.java",
        "index/FieldExposer.java",
        "mark/FieldExposer.java",
        "ofy/FieldExposer.java",
        "poll/FieldExposer.java",
        "rde/FieldExposer.java",
        "registrar/FieldExposer.java",
        "registry/FieldExposer.java",
        "registry/label/FieldExposer.java",
        "reporting/FieldExposer.java",
        "server/FieldExposer.java",
        "smd/FieldExposer.java",
        "tmch/FieldExposer.java",
        "transfer/FieldExposer.java",
        "translators/FieldExposer.java",
    ],
    cmd = "for FILE in $(OUTS); do\n" +
          "  $(location generate_field_exposer.sh) $$FILE >> $$FILE\n" +
          "done",
)

# Generate a registry of FieldExposers.
genrule(
    name = "field_exposer_registry",
    srcs = [":field_exposers"],
    outs = ["FieldExposerRegistry.java"],
    cmd = "$(location generate_field_exposer_registry.sh) $(SRCS) >$@",
    tools = ["generate_field_exposer_registry.sh"],
)
