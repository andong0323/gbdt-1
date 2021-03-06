package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files([
    "LICENSE",
])

LINK_OPTS = [ "-lprotobuf", "-lglog", "-lgflags", "-pthread", "-ltcmalloc_minimal", "-lm" ]
C_TEST_OPTS = [ "-Iexternal/googletest/googletest/include",
	        "-Iexternal/googletest/googlemock/include" ]

cc_library(
    name = "loss_func_logloss",
    srcs = [ "loss_func_logloss.cc" ],
    hdrs = [ "loss_func_logloss.h" ],
    deps = [
        "//external:cppformat-lib",
	"//src/utils:utils",
        "//src/base:base",
	":loss_func_math",
        ":loss_func_pointwise",
    ],
)

cc_test(
    name = "loss_func_logloss_test",
    srcs = [ "loss_func_logloss_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/base:base",
	":loss_func_logloss",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_huberized_hinge",
    srcs = [ "loss_func_huberized_hinge.cc" ],
    hdrs = [ "loss_func_huberized_hinge.h" ],
    deps = [
        "//external:cppformat-lib",
	"//src/utils:utils",
        "//src/base:base",
	":loss_func_math",
        ":loss_func_pointwise",
    ],
)

cc_test(
    name = "loss_func_huberized_hinge_test",
    srcs = [ "loss_func_huberized_hinge_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/base:base",
	":loss_func_huberized_hinge",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_mse",
    hdrs = [ "loss_func_mse.h" ],
    deps = [
        "//external:cppformat-lib",
        "//src/base:base",
	":loss_func_math",
	":loss_func_pointwise",
    ],
)

cc_test(
    name = "loss_func_mse_test",
    srcs = [ "loss_func_mse_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/base:base",
	":loss_func_mse",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func",
    hdrs = [ "loss_func.h" ],
    deps = [
        "//src/base:base",
        "//src/proto:config_cc_proto",
        ":gradient_data"
    ],
)

cc_library(
    name = "loss_func_factory",
    srcs = [ "loss_func_factory.cc" ],
    hdrs = [ "loss_func_factory.h" ],
    deps = [
	"//src/base:base",
        "//src/proto:config_cc_proto",
        ":loss_func",
        ":loss_func_auc",
        ":loss_func_gbrank",
	":loss_func_huberized_hinge",
	":loss_func_lambdamart",
	":loss_func_logloss",
	":loss_func_mse",
        ":loss_func_pairwise_logloss",
    ],
)

cc_test(
    name = "loss_func_factory_test",
    srcs = [ "loss_func_factory_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/proto:config_cc_proto",
        ":loss_func_factory",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_pointwise",
    srcs = [ "loss_func_pointwise.cc" ],
    hdrs = [ "loss_func_pointwise.h" ],
    deps = [
        "//external:cppformat-lib",
        "//src/base:base",
        "//src/utils:subsampling",
        "//src/utils:threadpool",
        "//src:flags",
        ":loss_func",
        ":loss_func_math",
    ],
)

cc_library(
    name = "group",
    srcs = [ "group.cc" ],
    hdrs = [ "group.h" ],
    deps = [
        "//src/base:base",
        "//src/data_store:column",
        "//external:glog"
    ]
)

cc_test(
    name = "group_test",
    srcs = [ "group_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/base:base",
        ":group",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_pairwise",
    srcs = [ "loss_func_pairwise.cc" ],
    hdrs = [ "loss_func_pairwise.h" ],
    deps = [
        "//external:cppformat-lib",
        "//src/base:base",
        "//src/data_store:column",
        "//src:flags",
        "//src/utils:subsampling",
        "//src/utils:threadpool",
        ":group",
        ":loss_func",
        ":loss_func_math",
    ],
)

cc_test(
    name = "loss_func_pairwise_test",
    srcs = [ "loss_func_pairwise_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/proto:config_cc_proto",
        "//src/base:base",
	"//src/data_store:column",
        "//src/data_store:data_store",
	":loss_func_math",
        ":loss_func_pairwise",
        ":loss_func_pairwise_logloss",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_pairwise_logloss",
    hdrs = [ "loss_func_pairwise_logloss.h" ],
    deps = [
        "//src/base:base",
        "//src/data_store:column",
        ":loss_func_pairwise",
        ":loss_func_math",
    ],
)

cc_library(
    name = "loss_func_auc",
    hdrs = [ "loss_func_auc.h" ],
    deps = [
        "//src/base:base",
        ":loss_func_pairwise",
        ":loss_func_math",
    ],
)

cc_library(
    name = "loss_func_gbrank",
    hdrs = [ "loss_func_gbrank.h" ],
    deps = [
        "//src/base:base",
        ":loss_func_pairwise",
        ":loss_func_math",
    ],
)

cc_library(
    name = "loss_func_lambdamart",
    srcs = [ "loss_func_lambdamart.cc" ],
    hdrs = [ "loss_func_lambdamart.h" ],
    deps = [
        "//external:cppformat-lib",
        "//src/base:base",
        "//src/data_store:data_store",
	":loss_func_math",
        ":loss_func_pairwise",
    ],
)

cc_test(
    name = "loss_func_lambdamart_test",
    srcs = [ "loss_func_lambdamart_test.cc" ],
    deps = [
        "//external:gtest_main",
        "//src/proto:config_cc_proto",
        "//src/base:base",
	"//src/data_store:column",
        "//src/data_store:data_store",
	":loss_func_lambdamart",
    ],
    copts = C_TEST_OPTS,
    linkopts = LINK_OPTS,
    linkstatic = 1
)

cc_library(
    name = "loss_func_math",
    srcs = [ "loss_func_math.cc" ],
    hdrs = [ "loss_func_math.h" ],
    deps = [
        ":loss_func"
    ],
)

cc_library(
    name = "gradient_data",
    hdrs = [ "gradient_data.h" ],
    deps = [
    ],
)
