## Release 0.10.0 (2018-02-01)

```
Baseline: 22c2f9a7722e8c8b7fdf8f5d30a40f1c4118e993

Cherry picks:
   + f6ca78808722c8c119affdb33400838ee92d44b6:
     isable_presubmit
   + 65c13dd5a4c1b4b5a072f7680b8f1cf3c5079b52:
     Fix StreamResourceLeak error
   + e5436745e1732f5e43fc55f0deb5b19e23ce8524:
     windows: fix --symlink_prefix=/ throwing exception
   + 22ccdd1ebe1dc495e05d894a3325f6b05e681fb3:
     Fix turbine command lines with empty javacopts
   + 96c654d43eb2906177325cbc2fc2b1e90dbcc792:
     Remove EOL'd Linux flavours, bump CentOS to 6.9.
   + f0bec36864f10370cbbda4caa8beac2e0c5ee45b:
     Automated rollback of commit
     2aeaeba66857c561dd6d63c79a213f1cabc3650d.
   + 860af5be10b6bad68144d9d2d34173e86b40268c:
     Consolidate Error Prone resource handling
   + 2e631c99495f75270d2639542cefb531ec262d67:
     sandbox: properly add `tmpDir` to `writablePaths`
   + 5bfa5844d0d16d71e88002956e88402bfec88ef7:
     actions,temp: respect TMPDIR envvar
   + 6cc2ad8676d1ae0542b351a07a05ddbe5efac165:
     sandbox: add env[TMPDIR] instead of `tmpDir`
   + 40c757f4ab90214f95935672532a495c4551490a:
     Change git clone to pull all history, so all needed commits can
     be accessed.
```

Incompatible changes:

  - In order to access the template variables $(JAVA) and
    $(JAVABASE), @bazel_tools//tools/jdk:current_java_runtime needs
    to be added to the toolchains= attribute from now on.
  - The ctx.middle_man function is not supported anymore.
  - The flag --incompatible_list_plus_equals_inplace is removed, its
    default behavior is preserved. += on lists now always mutates the
    left hand
    side.
  - --android_sdk no longer supports filegroup targets.
  - android_* rules no longer support legacy_native_support attribute.

New features:

  - query: Add option --noproto:flatten_selects to turn off
    flattening of selector lists in proto output.
  - New android test rule, android_local_test.

Important changes:

  - The --remote_rest_cache flag now respects --remote_timeout.
  - --experimental_java_coverage is available for testing.
  - The deprecated builtin `set` is no longer allowed even from within
    unexecuted code in bzl files. It's temporarily possible to use
    --incompatible_disallow_uncalled_set_constructor=false if this
    change causes
    incompatibility issues.
  - Linkstamping is now a separate and full-blown CppCompileAction,
    it's
    no longer a part of linking command.
  - Using `+`, `|` or `.union` on depsets is now deprecated. Please
    use the new
      constructor instead (see
    https://docs.bazel.build/versions/master/skylark/depsets.html).
  - config_feature_flag's default_value is optional. It is
    only an error to have a config_feature_flag with no default_value
    if that config_feature_flag has not been set in the configuration
    it is being evaluated in.
  - --[no]keep_incrementality_data is gone, replaced by the
    enum-valued --incremental_state_retention_strategy
  - Linkstamping is now a separate and full-blown CppCompileAction,
    it's
    no longer a part of linking command.
  - Added --checkHashMismatch flag to ZipFilterAction. Valid values
    are IGNORE, WARN and ERROR. --errorOnHashMismatch is deprecated,
    please use this flag instead.
  - Set build jobs equivalent to number of logical processors by
    default. Should improve build times significantly.
  - Added --(no)expand_test_suites flag.
  - Rename --keep_incrementality_data to --track_incremental_state
  - --remote_rest_cache was renamed to --remote_http_cache. Both
    options keep working in this release, but --remote_rest_cache
    will be
    removed in the next release.
  - Aspects-on-aspect see and propagate over aspect attributes.
  - --auth_* flags were renamed to --google_* flags. The old names
    will continue to work for this release but will be removed in the
    next
    release.
  - Remote Caching and Execution support output directories.
  - Remove defunct flags
    --experimental_incremental_dexing_for_lite_proto and
    --experimental_incremental_dexing_error_on_missed_jars that have
    long been enabled by default
  - New version of aapt2 and Resources.proto.
  - Make PIC and non PIC outputs for C++ compilation with Tree
    Artifacts

## Release 0.9.0 (2017-12-19)

```
Baseline: ddd5ac16aeffa6c4693c348f73e7365240b1abc5

Cherry picks:
   + 2cf560f83922e6df9626ba3ee063c1caf6797548:
     Update version of re2
   + a2d2615362c65be98629b39ce39754a325ed1c42:
     Check for null build file returned from getBuildFileForPackage.
   + 68c577afc2fb33b5e66b820bcc9043fed1071456:
     Fix some broken targets and failing tests.
   + 766ba8adc4487f17ebfc081aeba6f34b18b53d6c:
     Automated rollback of commit
     337f19cc54e77c45daa1d5f61bf0a8d3daf8268f.
   + a22d0e9c14e58b29d81f5a83bdcc6e5fce52eafe:
     Fix: uploading artifacts of failed actions to remote cache
     stopped working.
   + 03964c8ccb20d673add76c7f37245e837c3899b6:
     [java_common.compile] Name output source jar relative to the
     output jar name
```

Incompatible changes:

  - The deprecated `set` constructor is removed, along with the
    migration flag --incompatible_disallow_set_constructor. It is
    still temporarily
    allowed to refer to `set` from within unexecuted code.
  - The flag --incompatible_disallow_set_constructor is no longer
    available, the deprecated `set` constructor is not available
    anymore.
  - The path to the JVM executable is not accessible anymore as
    ctx.{fragments,host_fragments}.jvm.java_executable. Use
    JavaRuntimeInfo.java_executable_exec_path instead.
  - --clean_style is no longer an option.

New features:

  - Users can use win_def_file attribute to specify a DEF file for
    exporting symbols when build a shared library on Windows.
  - Add --experimental_android_resource_cycle_shrinking option to
    allow for more aggressive code and resource shrinking.

Important changes:

  - Late-bound attributes are exposed to skylark. This is a new API
    (`configuration_field()`) to depend on certain
    configuration-defined targets from skylark rules.
  - Document interaction between test_suite and target exclusions
  - AAR manifest files will come from the processed resource APK if it
    exists.
    RELNOTES: None for Blaze users.
  - Document interaction between test_suite and target exclusions
  - --keep_incrementality_data flag allows Bazel servers to be run in
    memory-saving non-incremental mode independent of --batch and
    --discard_analysis_cache.
  - Add deps attribute to Skylark maven_aar and maven_jar workspace
    rules.
  - Use --expand_configs_in_place as a startup argument to change the
    order in which --config expansions are interpreted.
  - SOURCE_DATE_EPOCH
    (https://reproducible-builds.org/specs/source-date-epoch/) can
    be used to override the timestamp used for stamped target (when
    using --stamp).
  - Package specifications can now be prefixed with `-` to indicate
    negation
  - transitive_source_jars is now exposed on JavaInfo.
  - Add six to deps of has_services=1 py_proto_librarys.
  - java_tests no complain when use_testrunner is explicitly set to 1
    and main_class is set.
  - transitive_source_jars is now exposed on JavaInfo.
  - Debug messages generated by `print()` are not being filtered out
    by --output_filter anymore, it's recommended not to use them in
    production code.
  - in the Label() function, relative_to_caller_repository is now
    deprecated.
  - java_tests no complain when use_testrunner is explicitly set to 1
    and main_class is set.
  - Bazel's default hash function was changed from MD5 to SHA256.
    In particular, this affects users of remote caching and
    execution, as
    all hashes will be SHA256 by default.
  - Remove redirects for domains be.bazel.build and cr.bazel.build
    from the source for docs.bazel.build (because those subdomains
    don't resolve here; they resolve to bazel.build, which has the
    redirects for them)
  - First argument of 'load' must be a label. Path syntax is removed.
      (label should start with '//' or ':').
  - Document startup option --host_javabase
  - The --host_platform and --platform flags are no longer
    experimental.

## Release 0.8.0 (2017-11-27)

```
Baseline: cff0dc94f6a8e16492adf54c88d0b26abe903d4c

Cherry picks:
   + 8a49b156c4edf710e3e1e0acfde5a8d27cc3a086:
     Fix ImportError on tools.android for junction_lib
   + 275ae45b1228bdd0f912c4fbd634b29ba4180383:
     Automated rollback of commit
     4869c4e17d5b1410070a1570f3244148d8f97b5d.
   + d0bf589f2716b3d139c210930371a684c6e158eb:
     Add a random number to action temp dir
   + 9738f35abddb7ef7a7ef314b5d2a52a3be1b830a:
     CcProtoLibrary: Don't add dynamic librarys to filesToBuild on
     Windows
   + 0d6ff477099fdf6c8c1c7d4e2104f9184afe0a2b:
     Automated rollback of commit
     0ebb3e54fc890946ae6b3d059ecbd50e4b5ec840.
```

Incompatible changes:

  - ctx.fragments.apple.{xcode_version,ios_minimum_os} is not
    supported anymore. The same information is accessible through the
    target @bazel_tools//tools/osx:current_xcode_config: point an
    implicit attribute to it (i.e.
    attr.label(default=Label("@bazel_tools//tools/osx:current_xcode_co
    nfig")) then use
    ctx.attr._xcode_config[apple_common].XcodeVersionConfig].
  - ctx.fragments.apple.minimum_os_for_platform_type is not supported
    anymore. The same information is accessible through the target
    @bazel_tools//tools/osx:current_xcode_config: point an implicit
    attribute to it (i.e.
    attr.label(default=Label("@bazel_tools//tools/osx:current_xcode_co
    nfig")) then use
    ctx.attr._xcode_config[apple_common].XcodeVersionConfig].minimum_o
    s_for_platform_type .
  - ctx.fragments.apple.sdk_version_for_platform is not supported
    anymore. The same information is accessible through the target
    @bazel_tools//tools/osx:current_xcode_config: point an implicit
    attribute to it (i.e.
    attr.label(default=Label("@bazel_tools//tools/osx:current_xcode_co
    nfig")) then use
    ctx.attr._xcode_config[apple_common].XcodeVersionConfig].sdk_versi
    on_for_platform .
  - --javabase=<absolute path> and --host_javabase=<absolute path>
    are not supported anymore. If you need this functionality
    java_runtime_suite(name="suite", default=":runtime")
    java_runtime(name="runtime", java_home=<path to the JDK>) is an
    alternative.
  - The flag --incompatible_descriptive_string_representations is no
    longer available, old style string representations of objects are
    not supported
    anymore.
  - The flag --incompatible_disallow_set_constructor is no longer
    available, the deprecated `set` constructor is not available
    anymore.
  - += on lists now mutates them. `list1 += list2` is now equivalent
    to `list1.extend(list2)` and not equivalent to `list1 = list1 +
    list2` anymore.
  - the target_apple_env and apple_host_system_env methods on
    ctx.fragments.apple are not supported anymore. The same
    information is accessible through apple_common.target_apple_env
    and apple_common.apple_host_system_env . They need the Xcode
    configuration as an argument, which can be obtained by declaring
    an implicit dependency on it (i.e.
    attr.label(default=Label("@bazel_tools//tools/osx:current_xcode_co
    nfig")) and then calling e.g.
    apple_common.apple_host_system_env(ctx.attr._xcode_config[apple_co
    mmon.XcodeVersionConfig]).
  - C++ toolchain identifiers are not in the name of the output
    directory anymore.
  - Selecting on "xcode_version" and
    "{ios,tvos,macos,watchos}_sdk_version" is not supported anymore.
    What was config_setting(values={"$FOO_version": $VALUE}) is now
    config_setting(flag_values={"@bazel_tools//tools/osx:$FOO_version_
    flag": $VALUE}).
  - Selecting on "xcode_version" and
    "{ios,tvos,macos,watchos}_sdk_version" is not supported anymore.
    What was config_setting(values={"$FOO_version": $VALUE}) is now
    config_setting(flag_values={"@bazel_tools//tools/osx:$FOO_version_
    flag": $VALUE}).
  - The flag --incompatible_disallow_set_constructor is no longer
    available, the deprecated `set` constructor is not available
    anymore.
  - Selecting on "xcode_version" and
    "{ios,tvos,macos,watchos}_sdk_version" is not supported anymore.
    What was config_setting(values={"$FOO_version": $VALUE}) is now
    config_setting(flag_values={"@bazel_tools//tools/osx:$FOO_versi...

New features:

  - runfiles, sh: Shell scripts may now depend on
    //src/tools/runfiles:runfiles_sh_lib and source runfiles.sh. The
    script defines the `rlocation` function which returns runfile
    paths on every platform.
  - In addition to $(location), Bazel now also supports $(rootpath)
    to obtain
        the root-relative path (i.e., for runfiles locations), and
    $(execpath) to
        obtain the exec path (i.e., for build-time locations)

Important changes:

  - android_binary now supports custom debug keys via the debug_key
    attribute.
  - Updated Android proguard to 5.3.3. It now works with android-24+.
  - --experimental_use_parallel_android_resource_processing and
    --experimental_android_use_nocompress_extensions_on_apk are
    removed. These features are fully rolled out.
  - Fixes #2574
  - Fixes #3834
  - Enable experimental UI by default.
  - .
    RELNOTES: None.
    RELNOTES: No.
  - Add memory profiler.
  - [Bazel] {java,cc}_proto_library now look for dependencies in
    @com_google_protobuf, instead of in @com_google_protobuf_$LANG
  - Improved merge.sh script in cookbook.
  - Fixing regression to --experimental_remote_spawn_cache
  - Support for linker scripts in NativeDepsHelper (e.g.,
    android_binary)
  - Skylark semantics flags now affect WORKSPACE files and repository
    rules.
  - ctx.outputs.executable is deprecated. Use DefaultInfo(executable
    = ...) instead.
  - Update "mirror.bazel.build" urls to use https.
  - Improve --config logging when --announce_rc is present.
  - Document interaction between test_suite and target exclusions
  - Replace version numbers for Bazel installers with "<version>"
    (because this will change often)
  - Published command lines should have improved lists of effective
    options.
  - --incremental_dexing_binary_types has been removed. All builds
    are supported by incremental dexing (modulo proguard and some
    blacklisted dx flags).
  - Document --host_javabase, --host_java_toolchain

## Release 0.7.0 (2017-10-18)

```
Baseline: 5cc6246d429f7d9119b97ce263b4fd6893222e92

Cherry picks:
   + e79a1107d90380501102990d82cbfaa8f51a1778:
     Windows,bootstrapping: fix build_windows_jni.sh
```

Incompatible changes:

  - The --output=location flag to 'bazel query' cannot be used with
    query expressions that involve the 'buildfiles' or 'loadfiles'
    operators. This also applies to 'genquery' rules.
  - Operators for equality, comparison, 'in' and 'not in' are no
    longer associative,
      e.g.  x < y < z  is now a syntax error. Before, it was parsed
    as:  (x < y) < z.
  - In strings, octal sequences greater than \377 are now forbidden
    (e.g. "\\600").
      Previously, Blaze had the same behavior as Python 2, where
    "\\450" == "\050".
  - Using tabulation for identation is now fobidden in .bzl files
  - `load` is now a language keyword, it cannot be used as an
    identifier
  - lvalues must have define at least one variable (i.e. we forbid
    `[] = f()`).
  - Fixed a bug whereby multiple load() statements could appear on
    the same line
  - -extra_checks:off is no longer supported; use
    -XepDisableAllChecks instead
  - java_common.java_toolchain_attr is removed. Depend on the
    java_toolchain_alias() rule to accomplish the same thing.
  - cc_common.cc_toolchain_attr and java_common.java_runtime_attr are
    not supported anymore and were replaced with the
    cc_toolchain_alias() and java_runtime_alias() rules.
  - Noop flag --deprecated_generate_xcode_project deleted.
  - Objects in Skylark are converted to strings in a more descriptive
    and less harmful way (they don't leak information that shouldn't
    be accessed by Skylark code, e.g. nondeterministic memory addresses
    of objects).
  - `set` is deprecated in BUILD and .bzl files, please use `depset`
    instead. Ordering names have also been changed, please use "default",
    "postorder", "preorder", and "topological" instead of "stable",
    "compile", "naive_link", and "link" correspondingly.
  - Integer overflow (on signed 32 bit numbers) in BUILD/bzl files is
    an error.
  - Keyword-only syntax in a function definition is now forbidden
      e.g. `def foo(a, *, b)` or `def foo(a, *b, c)`
  - --incompatible_comprehension_variables_do_not_leak defaults to
    "true."
      Iteration variable becomes inaccessible after a list/dict
    comprehension.
  - @bazel_tools//tools/build_defs/docker:docker.bzl is no longer
    available, please see https://github.com/bazelbuild/rules_docker.

New features:

  - Zipped LLVM profiles are now supported.
  - LIPO maps to ThinLTO for LLVM builds.
  - Change to handle LLVM FDO zipped profile contents correctly.
  - Do not disable fully dynamic linking with ThinLTO when invoked
    via LIPO options.
  - There is now a 'siblings' query function. See the query
    documentation for more details.
  - Added the print_action command, which outputs the
    actions needed to build a given target in the form of an
    ExtraActionSummary proto in text format.
  - android_binary now supports proguard_apply_dictionary to specify
    a custom dictionary to use for choosing names to obfuscate
    classes and members to.

Important changes:

  - Windows: bazel clean --expunge works
  - First argument of 'load' should be a label. Path syntax is
    deprecated (label should start with '//' or ':').
  - Octal prefix '0' is deprecated in favor of '0o' (use 0o777
    instead of 0777).
  - The extension_safe attribute of apple_binary no longer validates
    transitive dependencies are compiled against extension_safe APIs.
  - Parentheses around the tuple are now mandatory in [a for b in c
    if 1, 2]
  - Adjust the thresholds for --test_verbose_timeout_warnings so that
    it can recommending timeout increases and won't recommend
    timeouts that are too close to the actual timeout.
  - Iterating on a `depset` object is deprecated. If you need an
    iterable, call the `.to_list()` method first.
  - Bazel now uses tools from action_configs in Crosstool by default
    (as oposed to using top level tools).
  - Incremental dexing errors on combination of --multidex=off and
    either --main-dex-list or --minimal-main-dex.
  - When using the dictionary literal syntax, it is now an error to
    have duplicated keys (e.g.  {'ab': 3, 'ab': 5}).
  - New property on android_sdk: aapt2
      Choose the version of aapt on android_binary
  - Add idl_preprocessed attribute to android_library, so that
    preprocessed aidl files can be passed to android_library for
    compiling
  - Bazel's remote_worker backend for remote execution supports
    sandboxing on Linux now. Check
    https://github.com/bazelbuild/bazel/blob/master/src/tools/remote_w
    orker/README.md for details.
  - Allows flags that expand to take values.
  - Make querying attributes formed by selector lists of list types
    more efficient by no longer listing every possible combination of
    attribute value but by more compactly storing the possible values
    of the list.
  - writing build events to a file is no longer experimental
  - set --rewrite_calls_to_long_compare to false by default.
  - ObjC and C++ coverage feature is unified under name 'coverage'
  - Enable --incremental_dexing for Android builds by default. Note
    that some dexopts are incompatible with incremental dexing,
    including --force-jumbo.
  - Evaluation will soon use checked arithmetics and throw an error
    instead of overflow/underflow.
  - Implicit iteration in the CROSSTOOL has been removed, use
    explicit 'iterate_over' message.
  - Add option for Android specific grte_top
  - Crosstool patches are only applied if the toolchain doesn't define
    'no_legacy_features' feature.
  - 'platform_type' is now a mandatory attribute on apple_binary and
    apple_static_library rules.
    If this change breaks your build, feel free to add platform_type
    = 'ios' to any apple_binary and apple_static_library
    targets in your project, as this was the previous default
    behavior.
  - Remove apple_watch2_extension build rule. Users should be using
    the skylark watchos_application and watchos_extension rules.
    https://github.com/bazelbuild/rules_apple has details.
  - Check stderr to detect if connected to a terminal.  Deprecate
    --isatty.
  - Commands that shut down the server (like "shutdown") now ensure
    that the server process has terminated before the client process
    terminates.
  - Remove apple_watch1_extension and apple_watch_extension_binary
    rules. Users should be using the skylark watchos_application and
    watchos_extension rules.
    https://github.com/bazelbuild/rules_apple has details.
  - Windows: Wrapper-less CROSSTOOL becomes default now.
    set USE_MSVC_WRAPPER=1 if you still want to use wrapper script.
  - Ignore --glibc in the Android transition.
  - Remove --experimental_android_use_singlejar_for_multidex.
  - nocopts now also filter copts
  - 'strip' action is now configured via feature configuration
  - The Build Event Service (BES) client now properly supports
    Google Applicaton Default Credentials.
  - Flags from action_config get added first to the command line
    first, before the flags from features.
  - update dexing tools to Android SDK 26.0.1
  - Bazel Android support now requires build-tools 26.0.1 or later.
  - `bazel info output_path` no longer relies on the root directory
    filename being equal to the workspace name.
  - The `print` function now prints debug messages instead of
    warnings.
  - speedup of incremental dexing tools
  - --announce_rc now controls whether bazelrc startup options are
    printed to stderr.
  - Removing a few unused objc_provider keys.
  - Improved logging when workers have to be restarted due to its
    files having changed.
  - Top-level `if` statements are now forbidden.
  - Java protos are compiled to Java 7 bytecode.
  - All Android builds now use the desugar tool to support some Java
    8 features by default. To disable, use the --nodesugar_for_android flag.
  - Skylark-related options may now appear as "common" command
    options in the .bazelrc
  - Python is now required to build bazel.
  - New --build_runfile_manifests flag controls production of
    runfiles manifests.
  - Enable debug info for Java builds
  - Allow java_lite_proto_library in the deps of android rules.
  - .so files in APKs will be memory-page aligned when
    android_binary.nocompress_extensions contains ".so" and
    --experimental_android_use_nocompress_extensions_on_apk is
    specified.
  - Skylark providers can specify allowed fields and their
    documentation.
  - Support ctx.actions.args() for more efficient Skylark command
    line construction.
  - The remote HTTP/1.1 caching client (--remote_rest_cache) now
    distinquishes between action cache and CAS. The request URL for
    the action cache is prefixed with 'ac' and the URL for the CAS
    is prefixed with 'cas'.
  - `JavaInfo` is a preferred alias to `java_common.provider`.
  - J2ObjC version updated to 2.0.3.
  - A new Java coverage implementation is available. Makes possible
    coverage for Skylark JVM rules.
  - Make proguard_apply_dictionary also apply to class and package
    obfuscation, not just class members.
  - android_binary.nocompress_extensions now applies to all files in
    the APK, not just resources and assets.
  - The apple_genrule rule that is distributed with Bazel has been
    deleted. Users who wish to use genrules with Xcode's
    DEVELOPER_DIR set should use the rules in
    https://github.com/bazelbuild/rules_apple instead.
  - The swift_library rule that is distributed with Bazel has been
    deleted. Users who wish to compile Swift should use the rules in
    https://github.com/bazelbuild/rules_apple instead.
  - The Build Event Protocol's File.uri field is now properly
    encoded according to RFC2396.
  - Deprecated: Using the android_library.deps attribute to
    implicitly export targets to dependent rules. If your code is
    using this feature, Bazel will raise a warning. To fix, please
    use android_library.exports to explicitly specify exported
    targets. Run with
    --experimental_allow_android_library_deps_without_srcs=false to
    ensure forward compatibility when this feature is removed in a
    future release.
  - java_common.create_provider is now supported with creating ijars
    by default. This introduces incompatibilities for existing users.
    Please set use_ijar=False if you don't want to use ijars.
  - Tests can now write files to TEST_UNDECLARED_OUTPUTS_DIR and
    TEST_UNDECLARED_OUTPUTS_ANNOTATIONS_DIR and these will be
    reflected under bazel-testlogs.
  - remove unused --host_incremental_dexing flag
  - Stop using --undefined dynamic_lookup in Apple links. Enables
    unresolved symbol errors.
  - All test output files included for cached, uncached, and multiple
    attempt tests.
  - Android rules no longer restrict the manifest file to be named
    "AndroidManifest.xml".
  - Boolean flag values will now get normalized to 1 or 0 in
    canonicalize-flags output.
  - added experimental --use_new_category_enum to the help command to
    output options grouped by the new type of category.
  - Expose output jars and jdeps in java_common.provider, when
    available.
  - android_library targets are no longer allowed to use deps to
    export targets implicitly; please use android_library.exports
    instead.
  - New depset API
  - apple_binary and apple_static_library no longer support
    compilation attributes such as 'srcs'. If this breaks any
    existing targets, you may migrate all such attributes to a new
    objc_library target and depend on that objc_library target via
    the 'deps' attribute of apple_binary or apple_static_library.

## Release 0.6.1 (2017-10-05)

```
Baseline: 87cc92e5df35d02a7c9bc50b229c513563dc1689

Cherry picks:
   + a615d288b008c36c659fdc17965207bb62d95d8d:
     Rollback context.actions.args() functionality.
   + 7b091c1397a82258e26ab5336df6c8dae1d97384:
     Add a global failure when a test is interrupted/cancelled.
   + 95b0467e3eb42a8ce8d1179c0c7e1aab040e8120:
     Cleanups for Skylark tracebacks
   + cc9c2f07127a832a88f27f5d72e5508000b53429:
     Remove the status xml attribute from AntXmlResultWriter
   + 471c0e1678d0471961f1dc467666991e4cce3846:
     Release 0.6.0 (2017-09-28)
   + 8bdd409f4900d4574667fed83d86b494debef467:
     Only compute hostname once per server lifetime
   + 0bc9b3e14f305706d72180371f73a98d6bfcdf35:
     Fix bug in NetUtil caching.
```

Important changes:
 - Only compute hostname once per server lifetime

## Release 0.6.0 (2017-09-28)

```
Baseline: 87cc92e5df35d02a7c9bc50b229c513563dc1689

Cherry picks:
   + a615d288b008c36c659fdc17965207bb62d95d8d:
     Rollback context.actions.args() functionality.
   + 7b091c1397a82258e26ab5336df6c8dae1d97384:
     Add a global failure when a test is interrupted/cancelled.
   + 95b0467e3eb42a8ce8d1179c0c7e1aab040e8120:
     Cleanups for Skylark tracebacks
   + cc9c2f07127a832a88f27f5d72e5508000b53429:
     Remove the status xml attribute from AntXmlResultWriter
```

Incompatible changes:

  - Noop flag --deprecated_generate_xcode_project deleted.
  - Objects in Skylark are converted to strings in a more descriptive
    and less harmful way (they don't leak information that shouldn't
    be accessed by Skylark code, e.g. nondeterministic memory addresses
    of objects).
  - `set` is deprecated in BUILD and .bzl files, please use `depset`
    instead. Ordering names have also been changed, please use
    "default", "postorder", "preorder", and "topological" instead of
    "stable", "compile", "naive_link", and "link" correspondingly.
  - Integer overflow (on signed 32 bit numbers) in BUILD/bzl files is
    an error.
  - Keyword-only syntax in a function definition is now forbidden
      e.g. `def foo(a, *, b)` or `def foo(a, *b, c)`
  - --incompatible_comprehension_variables_do_not_leak defaults to
    "true."
      Iteration variable becomes inaccessible after a list/dict
    comprehension.

New features:

  - There is now a 'siblings' query function. See the query
    documentation for more details.
  - Added the print_action command, which outputs the
    actions needed to build a given target in the form of an
    ExtraActionSummary proto in text format.
  - android_binary now supports proguard_apply_dictionary to specify
    a custom dictionary to use for choosing names to obfuscate
    classes and members to.

Important changes:

  - 'strip' action is now configured via feature configuration
  - Flags from action_config get added first to the command line
    first,
    before the flags from features.
  - `bazel info output_path` no longer relies on the root directory
    filename being equal to the workspace name.
  - The `print` function now prints debug messages instead of
    warnings.
  - speedup of incremental dexing tools
  - --announce_rc now controls whether bazelrc startup options are
    printed to stderr.
  - Removing a few unused objc_provider keys.
  - Improved logging when workers have to be restarted due to its
    files having changed.
  - Top-level `if` statements are now forbidden.
  - Java protos are compiled to Java 7 bytecode.
  - All Android builds now use the desugar tool to support some Java
    8 features by default. To disable, use the
    --nodesugar_for_android flag.
  - Skylark-related options may now appear as "common" command
    options in the .bazelrc
  - Python is now required to build bazel.
  - When the lvalue of an augmented assignment is a list, we now
    throw an error
      before evaluating the code (e.g. `a, b += 2, 3`).
  - New --build_runfile_manifests flag controls production of
    runfiles manifests.
  - Enable debug info for Java builds
  - Allow java_lite_proto_library in the deps of android rules.
  - .so files in APKs will be memory-page aligned when
    android_binary.nocompress_extensions contains ".so" and
    --experimental_android_use_nocompress_extensions_on_apk is
    specified.
  - Skylark providers can specify allowed fields and their
    documentation.
  - Support ctx.actions.args() for more efficient Skylark command
    line construction.
  - The remote HTTP/1.1 caching client (--remote_rest_cache) now
    distinquishes between action cache and CAS. The request URL for
    the action cache is prefixed with 'ac' and the URL for the CAS
    is prefixed with 'cas'.
  - `JavaInfo` is a preferred alias to `java_common.provider`.
  - J2ObjC version updated to 2.0.3.
  - A new Java coverage implementation is available. Makes possible
    coverage for Skylark JVM rules.
  - Make proguard_apply_dictionary also apply to class and package
    obfuscation, not just class members.
  - When using the dictionary literal syntax, it is now an error to
    have duplicated keys (e.g.  {'ab': 3, 'ab': 5}).
  - android_binary.nocompress_extensions now applies to all files in
    the APK, not just resources and assets.
  - The apple_genrule rule that is distributed with Bazel has been
    deleted. Users who wish to use genrules with Xcode's
    DEVELOPER_DIR set should use the rules in
    https://github.com/bazelbuild/rules_apple instead.
  - The swift_library rule that is distributed with Bazel has been
    deleted. Users who wish to compile Swift should use the rules in
    https://github.com/bazelbuild/rules_apple instead.

## Release 0.5.4 (2017-08-25)

```
Baseline: 6563b2d42d29196432d5fcafa0144b8371fbb028

Cherry picks:
   + d4fa181f8607c35230b7efa1ce94188b51508962:
     Use getExecPathString when getting bash_main_file
   + 837e1b3d4859140d29aaa6bbab8fbb008e6d701e:
     Windows, sh_bin. launcher: export runfiles envvars
   + fe9ba893c0ebec19228086356af5fa8d81f2809b:
     grpc: Consolidate gRPC code from BES and Remote Execution. Fixes
     #3460, #3486
   + e8d4366cd374fba92f1425de0d475411c8defda4:
     Automated rollback of commit
     496d3ded0bce12b7371a93e1183ba30e6aa88032.
   + 242a43449dd44a22857f6ce95f7cc6a7e134d298:
     bes,remote: update default auth scope.
   + 793b409eeae2b42be7fed58251afa87b5733ca4d:
     Windows, sh_bin. launcher: fix manifest path
   + 7e4fbbe4ab3915a57b2187408c3909e5cd6c6013:
     Add --windows_exe_launcher option
   + 91fb38e92ace6cf14ce5da6527d71320b4e3f3d2:
     remote_worker: Serialize fork() calls. Fixes #3356
   + b79a9fcd40f448d3aebb2b93a2ebe80d09b38408:
     Quote python_path and launcher in
     python_stub_template_windows.txt
   + 4a2e17f85fc8450aa084b201c5f24b30010c5987:
     Add build_windows_jni.sh back
   + ce61d638197251f71ed90db74843b55d9c2e9ae5:
     don't use methods and classes removed in upstream dx RELNOTES:
     update dexing tools to Android SDK 26.0.1
   + 5393a4996d701fa192964a35cbb75e558a0599c0:
     Make Bazel enforce requirement on build-tools 26.0.1 or later.
   + 5fac03570f80856c063c6019f5beb3bdc1672dee:
     Fix --verbose_failures w/ sandboxing to print the full command
     line
   + f7bd1acf1f96bb7e3e19edb9483d9e07eb5af070:
     Only patch in C++ compile features when they are not already
     defined in crosstool
   + d7f5c120417bc2d2344dfb285322355f225d9153:
     Bump python-gflags to 3.1.0, take two
   + 3cb136d5451e9d8af58f9a99990cad0592df101a:
     Add python to bazel's dockerfiles
```

New features:

  - Do not disable fully dynamic linking with ThinLTO when invoked
    via LIPO options.

Important changes:

  - Ignore --glibc in the Android transition.
  - Remove --experimental_android_use_singlejar_for_multidex.
  - nocopts now also filter copts
  - The Build Event Service (BES) client now properly supports
    Google Applicaton Default Credentials.
  - update dexing tools to Android SDK 26.0.1
  - Bazel Android support now requires build-tools 26.0.1 or later.
  - Fix a bug in the remote_worker that would at times make it crash on Linux. See #3356
  - The java_proto_library rule now supports generated sources. See #2265

## Release 0.5.3 (2017-07-27)

```
Baseline: 88518522a18df5788736be6151fc67992efe2aad

Cherry picks:
   + 820a46af10808396873c36d0f331e533118cf0c6:
     Automated rollback of commit
     6d6e87297fe8818e4c374fdfabfbcf538bca898a.
   + ccfb2df69ecf4746f5a15e1295af995c3a45aa94:
     Allow py_binary to be the executable of a Skylark action or any
     SpawnAction on Windows.
   + 06534911696838e720c8681f6f568c69d28da65e:
     Fix string representation for the Root class
   + cd159bcee72a7f377621b45409807231a636f9e2:
     sandbox: Allow UNIX sockets on macOS even when block-network is
     used.
   + ad73cba3caa2e08ad61ea9ca63f9111cde1f48d1:
     Fix python_stub_template.txt to be compatible with Python 2.4.
   + 9a63aff8bb771af8917903fbbc9df3b708e2c0ed:
     Create Windows ZIP release artifact using Bazel
   + 5e576637b5705aff0a7bf56b5077463dffcd712f:
     Automated rollback of commit
     820a46af10808396873c36d0f331e533118cf0c6.
   + b6e29ca217b02c3ba499b85479a3830f59c9b9b6:
     Use the correct function to generate the release notes
   + 0f3481ba6364f24ef76b839bdde06ae7883c9bd9:
     Include <cinttypes> instead of <stdint.h>
```

Incompatible changes:

  - The --output=location flag to 'bazel query' cannot be used with
    query expressions that involve the 'buildfiles' or 'loadfiles'
    operators. This also applies to 'genquery' rules.
  - Operators for equality, comparison, 'in' and 'not in' are no
    longer associative, e.g.  x < y < z  is now a syntax error.
    Before, it was parsed as:  (x < y) < z.
  - In strings, octal sequences greater than \377 are now forbidden
    (e.g. "\\600"). Previously, Blaze had the same behavior as Python 2,
    where "\\450" == "\050".
  - Using tabulation for identation is now fobidden in .bzl files
  - `load` is now a language keyword, it cannot be used as an
    identifier
  - lvalues must have define at least one variable (i.e. we forbid
    `[] = f()`).
  - Fixed a bug whereby multiple load() statements could appear on
    the same line
  - -extra_checks:off is no longer supported; use
    -XepDisableAllChecks instead
  - java_common.java_toolchain_attr is removed. Depend on the
    java_toolchain_alias() rule to accomplish the same thing.
  - cc_common.cc_toolchain_attr and java_common.java_runtime_attr are
    not supported anymore and were replaced with the
    cc_toolchain_alias() and java_runtime_alias() rules.

New features:

  - Zipped LLVM profiles are now supported.
  - LIPO maps to ThinLTO for LLVM builds.
  - Change to handle LLVM FDO zipped profile contents correctly.

Important changes:

  - Windows: bazel clean --expunge works
  - First argument of 'load' should be a label. Path syntax is
    deprecated (label should start with '//' or ':').
  - Octal prefix '0' is deprecated in favor of '0o' (use 0o777
    instead of 0777).
  - The extension_safe attribute of apple_binary no longer validates
    transitive dependencies are compiled against extension_safe APIs.
  - Parentheses around the tuple are now mandatory in [a for b in c
    if 1, 2]
  - Adjust the thresholds for --test_verbose_timeout_warnings so that
    it can recommending timeout increases and won't recommend
    timeouts that are too close to the actual timeout.
  - Iterating on a `depset` object is deprecated. If you need an
    iterable, call the `.to_list()` method first.
  - Bazel now uses tools from action_configs in Crosstool by default
    (as oposed to using top level tools).
  - Incremental dexing errors on combination of --multidex=off and
    either --main-dex-list or --minimal-main-dex.
  - When using the dictionary literal syntax, it is now an error to
    have duplicated keys (e.g.  {'ab': 3, 'ab': 5}).
  - New property on android_sdk: aapt2
      Choose the version of aapt on android_binary
  - Add idl_preprocessed attribute to android_library, so that
    preprocessed aidl files can be passed to android_library for
    compiling
  - Bazel's remote_worker backend for remote execution supports
    sandboxing on Linux now. Check
    https://github.com/bazelbuild/bazel/blob/master/src/tools/remote_w
    orker/README.md for details.
  - Allows flags that expand to take values.
  - Make querying attributes formed by selector lists of list types
    more efficient by no longer listing every possible combination of
    attribute value but by more compactly storing the possible values
    of the list.
  - Writing build events to a file is no longer experimental
  - set --rewrite_calls_to_long_compare to false by default.
  - ObjC and C++ coverage feature is unified under name 'coverage'
  - Enable --incremental_dexing for Android builds by default. Note
    that some dexopts are incompatible with incremental dexing,
    including --force-jumbo.
  - Evaluation will soon use checked arithmetics and throw an error
    instead of overflow/underflow.
  - Implicit iteration in the CROSSTOOL has been removed, use
    explicit 'iterate_over' message.
  - Add option for Android specific grte_top
  - Crosstool patches are only applied if the toolchain doesn't define
    'no_legacy_features' feature.
  - 'platform_type' is now a mandatory attribute on apple_binary and
    apple_static_library rules.
    If this change breaks your build, feel free to add platform_type
    = 'ios' to any apple_binary and apple_static_library
    targets in your project, as this was the previous default
    behavior.
  - Remove apple_watch2_extension build rule. Users should be using
    the skylark watchos_application and watchos_extension rules.
    https://github.com/bazelbuild/rules_apple has details.
  - Check stderr to detect if connected to a terminal.  Deprecate
    --isatty.
  - Commands that shut down the server (like "shutdown") now ensure
    that the server process has terminated before the client process
    terminates.
  - Remove apple_watch1_extension and apple_watch_extension_binary
    rules. Users should be using the skylark watchos_application and
    watchos_extension rules.
    https://github.com/bazelbuild/rules_apple has details.
  - Windows: Wrapper-less CROSSTOOL becomes default now.
    set USE_MSVC_WRAPPER=1 if you still want to use wrapper script.

## Release 0.5.2 (2017-06-27)

```
Baseline: e78ad83ded6e9c6d639793827e27b6570e6e9f65

Cherry picks:
   + 68028317c1d3d831a24f90e2b25d1410ce045c54:
     experimental UI: move stopUpdateThread() out of synchronized,
     again
   + 019935dfbb61e61d08d1351b0365fb4e2d0df305:
     Fix bug in URI computation in RemoteModule
   + e9424cf9b9d72b98594966d5ac0f15bb018ec639:
     Automated rollback of commit
     7dec00574aa91327693f6ba7e90bff5bc834253e.
   + 9eea05d068a06ab642dd9d86d46ee5fa2e36b02e:
     Switching to Watcher API instead of wait_for_completion, in
     preparation for deprecating the wait_for_completion field.
   + 89659810e3048782dfb5e308e39aa8a0727e464e:
     Set correct execroot for info
   + 716b527266f47f59a2b7fb2e5fc52cb45e1691b1:
     Only create a single per-build instance of the remote cache /
     executor
   + 1d82d199f82409f217a42bcefebb96f723f91caa:
     protobuf: Update protobuf jars to be binary compatible with Java
     6. Fixes #3198
   + 524b90d9e5acc4fa568f215c9415eaa902e979f8:
     Change CAS URI to use the "bytestream" scheme instead of being
     scheme-less
   + 4929ad79865f8c13ef3b33c827040f4a037e4afe:
     Automated g4 rollback of commit
     923d7df521f67d031b288180560848bd35e20976.
   + 68b9a7e2dc17e32b194238d287e79bee1ba035b9:
     Automated g4 rollback of commit
     da56606563ee9df438db93392f681bf2abb4ac97.
   + 2ba693ffbe824136a0ca5f47d34710612f6302c3:
     Automated rollback of commit
     ce7c4deda60a307bba5f0c9421738e2a375cf44e.
```

Incompatible changes:

  - Blaze no longer generates xcode projects. Use tulsi.bazel.build
    instead.

Important changes:

  - Keyword-only syntax in a function definition is deprecated
      (e.g. `def foo(a, *, b)` or `def foo(a, *b, c)`) and will be
    removed in the future.
  - Attempting to build an Android target without setting up
    android_sdk_repository will now produce a helpful error message.
  - Adds a sha256 attribute to git_repository and new_git_repository.
    This can only be used if the remote is a public GitHub
    repository. It forces
    Bazel to download the repository as a tarball, which will often
    be faster and
    more robust than cloning it.
  - Sandboxing is now enabled by default on FreeBSD (via
    processwrapper-sandbox).
  - android_test may use manifest placeholders with 'manifest_merger
    = "android"'.
  - load() statements should be called at the top of .bzl files,
    before any
      other statement. This convention will be enforced in the future.
  - Effectively remove sysroot from CppConfiguration and allow it to
    use select statements.
  - proto_library.strict_proto_deps no longer exists.
  - Flag --explicit_jre_deps is now a noop.
  - The 'legacy' Android manifest merger is deprecated. Please
    upgrade to the 'android' manifest merger, which is the same
    merger used by Gradle.
    https://developer.android.com/studio/build/manifest-merge.html
  - Using $(CC_FLAGS) in a GenRule adds a dependency to the c++
    toolchain
  - add one-version enforcement to android_local_test
  - Skylark support (apple_common.dotted_version(string)) for
    building DottedVersion objects to interface with native apple
    rules
  - CC_FLAGS can be defined using 'cc-flags-make-variable' action_config in
    CROSSTOOL
  - ios_framework native rule has been removed. This rule had been
    essentially broken for several months now; users should be using
    the skylark ios framework rule.
    https://github.com/bazelbuild/rules_apple has details.
  - Clean command no longer uses boolean values for --async,
    --expunge, and --expunge_async options.
  - Partially fixes external J2ObjC support.
  - '--aspects' can occur more than once on the command line.
  - --no_ prefix no longer recognized.
  - Use action_config in crosstool for static library archiving,
    remove ar_flag.
  - Added a new flag --sandbox_writable_path, which asks the sandbox
    to
    make an existing directory writable when running actions.
  - bazel test now also computes a default instrumentation filter if
    --collect_code_coverage is enabled
  - n/na
  - In .bzl files, top-level `if` statements are deprecated and will
    be forbidden
      in the future. Move them in a function body instead (or use a
    conditional
      expression instead: `x if condition else y`).
  - ios_device and ios_test are deprecated. Please use the new testing
    rules in https://github.com/bazelbuild/rules_apple instead.
  - bazel query --output package now displays packages from external
    repository with the format "@reponame//package". Packages in the
    main repository continue to have the format "package".
  - ctx.expand_make_variables is deprecated.
  - Bazel posts links to the CAS to the BEP if remote caching /
    execution is enabled
  - `bazel info execution_root` returns the corrrect directory name
    for the execution root.

## Release 0.5.1 (2017-06-06)

```
Baseline: f3ae88ee043846e7acdffd645137075a4e72c573

Cherry picks:
   + c58ba098526b748f9c73e6229cafd74748205aa1:
     Release to GCS: put the final release in its own directory
   + 0acead4ea3631240659836ce6ecd6d7f67fd352b:
     Update protobuf to latest master at a64497c and apply
     @laszlocsomor's latest changes from
     https://github.com/google/protobuf/pull/2969 on top of it.
   + d0242ce4a87929f2528f4602d0fb09d1ccfcea94:
     Make symlinks consistent
   + d953ca8b87a46decbce385cebb446ae0dd390881:
     Clean VanillaJavaBuilder output directories
   + 755669fb5de1f4e762f27c19776cac9f410fcb94:
     Pass all the environment variable to Bazel during bootstrapping
   + 6f041661ca159903691fcb443d86dc7b6454253d:
     Do not mark the JDK7 installer -without-jdk-installer
   + 720561113bfa702acfc2ca24ce3cc3fd7ee9c115:
     Fix #2958: Installer should not overwrite bazelrc
   + 511c35b46cead500d4e76706e0a709e50995ceba:
     Bootstrap: move the fail function to the top
   + 8470be1122825aae8ad0903dd1e1e2a90cce47d2:
     Clean up javac and Error Prone targets
   + 4a404de2c6c38735167e17ab41be45ef6fc4713a:
     Update javac version to 9-dev-r4023-2
   + 36ce4b433e19498a78c34540d5a166d4e0006b22:
     Update javac version to 9-dev-r4023-2
   + 38949b8526bdb3e6db22f3846aac87162c28c33f:
     Migrate off versioned javac and Error Prone targets
   + 1a57d298f8aa6ea8136d93223902104f2479cd2a:
     Re-enabling passing -sourcepath via javacopts.
   + eb565f408e03125e92d42b00756e519795be6593:
     Make make sure that msys build actually builds msys version
   + 39f328cf392056618d1a3ead4835a138b189a06d:
     Fix typo. Also do not override host_cpu for msvc.
   + 624802893f4fe72118f00a78452605d41a2e1c6f:
     Select correct JDK for windows_msys
   + c4f271d1a68366b6fa5ff38ea7d951b6a22af044:
     Automated g4 rollback of commit
     3e5edafa2a04a71cd3596e929e83222da725f3f9.
   + 926180997a0f296a5a009326aead887279ce0a90:
     Remove process-tools.cc which I forgot to delete during the last
     rollback.
   + baca6e4cb023649920871b74810927d304729e59:
     Fix #2982: Bazel installer should not check for installed JDK if
     using a bundled JDK.
   + 866ecc8c3d5e0b899e3f0c9c6b2265f16daae842:
     Disable msys path conversion on Windows.
   + cc21998c299b4d1f97df37b961552ff8168da17f:
     Rollforward #2 of: Basic open-source crosstool to support
     targeting apple platform types.
   + 0f0ccc4fc8229c1860a9c9b58089d6cfb2ee971f:
     Escape % in strings that will appear in Crosstool
   + 3b08f774e7938928e3a240a47a0a7554cdc8d50b:
     Adding feature for linking C Run-Time library on Windows
   + 3566474202d1978acfdcb7e5ff73ee03ea6f3df9:
     Do not use sed -E in bootstrap/compile.sh
   + c3cf7d917afd02d71de3800cd46ad8d14f1ddf55:
     Reverts non-xcode-available darwin crosstool generation.
```

Important changes:

  - Fixes regression in 0.5.0 requiring Xcode to build C++ on OSX.

## Release 0.5.0 (2017-05-26)

```
Baseline: f3ae88ee043846e7acdffd645137075a4e72c573

Cherry picks:
   + c58ba098526b748f9c73e6229cafd74748205aa1:
     Release to GCS: put the final release in its own directory
   + 0acead4ea3631240659836ce6ecd6d7f67fd352b:
     Update protobuf to latest master at a64497c and apply
     @laszlocsomor's latest changes from
     https://github.com/google/protobuf/pull/2969 on top of it.
   + d0242ce4a87929f2528f4602d0fb09d1ccfcea94:
     Make symlinks consistent
   + d953ca8b87a46decbce385cebb446ae0dd390881:
     Clean VanillaJavaBuilder output directories
   + 755669fb5de1f4e762f27c19776cac9f410fcb94:
     Pass all the environment variable to Bazel during bootstrapping
   + 6f041661ca159903691fcb443d86dc7b6454253d:
     Do not mark the JDK7 installer -without-jdk-installer
   + 720561113bfa702acfc2ca24ce3cc3fd7ee9c115:
     Fix #2958: Installer should not overwrite bazelrc
   + 511c35b46cead500d4e76706e0a709e50995ceba:
     Bootstrap: move the fail function to the top
   + 8470be1122825aae8ad0903dd1e1e2a90cce47d2:
     Clean up javac and Error Prone targets
   + 4a404de2c6c38735167e17ab41be45ef6fc4713a:
     Update javac version to 9-dev-r4023-2
   + 36ce4b433e19498a78c34540d5a166d4e0006b22:
     Update javac version to 9-dev-r4023-2
   + 38949b8526bdb3e6db22f3846aac87162c28c33f:
     Migrate off versioned javac and Error Prone targets
   + 1a57d298f8aa6ea8136d93223902104f2479cd2a:
     Re-enabling passing -sourcepath via javacopts.
   + eb565f408e03125e92d42b00756e519795be6593:
     Make make sure that msys build actually builds msys version
   + 39f328cf392056618d1a3ead4835a138b189a06d:
     Fix typo. Also do not override host_cpu for msvc.
   + 624802893f4fe72118f00a78452605d41a2e1c6f:
     Select correct JDK for windows_msys
   + c4f271d1a68366b6fa5ff38ea7d951b6a22af044:
     Automated g4 rollback of commit
     3e5edafa2a04a71cd3596e929e83222da725f3f9.
   + 926180997a0f296a5a009326aead887279ce0a90:
     Remove process-tools.cc which I forgot to delete during the last
     rollback.
   + baca6e4cb023649920871b74810927d304729e59:
     Fix #2982: Bazel installer should not check for installed JDK if
     using a bundled JDK.
   + 866ecc8c3d5e0b899e3f0c9c6b2265f16daae842:
     Disable msys path conversion on Windows.
   + cc21998c299b4d1f97df37b961552ff8168da17f:
     Rollforward #2 of: Basic open-source crosstool to support
     targeting apple platform types.
   + 0f0ccc4fc8229c1860a9c9b58089d6cfb2ee971f:
     Escape % in strings that will appear in Crosstool
   + 3b08f774e7938928e3a240a47a0a7554cdc8d50b:
     Adding feature for linking C Run-Time library on Windows
```

Incompatible changes:

  - Bazel's Linux sandbox no longer mounts an empty tmpfs on /tmp,
    instead the existing /tmp is mounted read-write. If you prefer
    to have a tmpfs on /tmp for sandboxed actions for increased
    hermeticity, please use the flag --sandbox_tmpfs_path=/tmp.
  - Converting artifacts to strings and printing them now return
    "File" instead of "Artifact" to be consistent with the type name.
  - The return type of depset.to_list() is now a list rather than a
    frozen list. (Modifying the list has no effect on the depset.)
  - Bazel now prints logs in single lines to java.log
  - --use_dash, --dash_url and --dash_secret are removed.
  - Remote repositories must define any remote repositories they
    themselves use (e.g., if @x//:foo depends on @y//:bar, @y must be
    defined
    in @x's WORKSPACE file).
  - Remote repositories must define any remote repositories they
    themselves use (e.g., if @x//:foo depends on @y//:bar, @y must be
    defined
    in @x's WORKSPACE file).
  - objc_xcodeproj has been removed, use tulsi.bazel.build instead.

New features:

  - If grte_top is a label, it can now follow non-configurable
    redirects.
  - Optional coverage_files attribute to cc_toolchain
  - "query --output=build" now includes select()s
  - Raw LLVM profiles are now supported.

Important changes:

  - Automatically generate Proguard mapping when resource shrinking
    and Proguard are enabled.
  - New rules in Bazel: proto_library, java_lite_proto_library,
    java_proto_library and cc_proto_library
  - Activate the "dead_strip" feature if objc binary stripping is
    enabled.
  - More stable naming scheme for lambda classes in desugared android
    code
  - Convert --use_action_cache to a regular option
  - Per-architecture dSYM binaries are now propagated by
    apple_binary's AppleDebugOutputsProvider.
  - Avoid factory methods when desugaring stateless lambdas for
    Android
  - desugar calls to Objects.requireNonNull(Object o) with
    o.getClass() for android
  - Add an --copy_bridges_from_classpath argument to android
    desugaring tool
  - Change how desugar finds desugared classes to have it working on
    Windows
  - Evaluation of commands on TargetsBelowDirectory patterns
    (e.g. //foo/...) matching packages that fail to load now report
    more
    detailed error messages in keep_going mode.
  - Allow to have several inputs and outputs
  - Repository context's execute() function can print stdout/stderr
    while running. To enable, pass quiet=False.
  - Bazel can now be built with a bundled version of the OpenJDK.
    This makes it possible to use Bazel on systems without a JDK, or
    where
    the installed JDK is too old.
  - The --jobs flag now defaults to "auto", which causes Bazel to
    use a reasonable degree of parallelism based on the local
    machine's
    capacity.
  - Bazel benchmark (perf.bazel.build) supports Java and Cpp targets.
  - no factory methods generated for lambda expressions on android
  - The Linux sandbox no longer changes the user to 'nobody' by
    default, instead the current user is used as is. The old behavior
    can be
    restored via the --sandbox_fake_username flag.
  - /tmp and /dev/shm are now writable by default inside the
    Linux sandbox.
  - Bazel can now use the process-wrapper + symlink tree based
    sandbox implementation in FreeBSD.
  - turn on --experimental_incremental_dexing_error_on_missed_jars by
    default.
  - All android_binarys are now signed with both Apk Signature V1 and
    V2. See https://source.android.com/security/apksigning/v2.html
    for more details.
  - Windows MSVC wrappers: Not filtering warning messages anymore,
    use --copt=-w and --host_copt=-w to suppress them.
  - A downloader bug was fixed that prevented RFC 7233 Range
    connection resumes from working with certain HTTP servers
  - Introduces experimental android_device rule for configuring and
    launching Android emulators.
  - For boolean flags, setting them to false using --no_<flag_name>
    is deprecated. Use --no<flag_name> without the underscore, or
    --<flag_name>=false instead.
  - Add --experimental_android_compress_java_resources flag to store
    java
    resources as compressed inside the APK.
  - Removed --experimental_use_jack_for_dexing and libname.jack
    output of
    android_library.
  - blaze canonicalize-flags now takes a --show_warnings flag
  - Changing --invocation_policy will no longer force a server
    restart.
  - Bazel now supports Android NDK14.
  - android_binary multidex should now work without additional flags.
  - Use action_config in crosstool for static library archiving,
    remove ar_flag.
  - new option for bazel canonicalize-flags, --canonicalize_policy
  - Use action_config in crosstool for static library archiving,
    remove ar_flag.
  - android_library exports_manifest now defaults to True.
  - Fix select condition intersections.
  - Adds a --override_repository option that takes a repository
    name and path. This forces Bazel to use the directory at that path
    for the repository. Example usage:
    `--override_repository=foo=/home/user/gitroot/foo`.
  - fix idempotency issue with desugaring lambdas in interface
    initializers for android
  - --experimental_android_use_singlejar_for_multidex is now a no-op
    and will eventually be removed.
  - Every local_repository now requires a WORKSPACE file.
  - Remove jack and jill attributes of the android_sdk rule.
  - Add Skylark stubs needed to remove sysroot from CppConfiguration.
  - Desugar try-with-resources so that this language feature is
    available
    to deveces with API level under 19.
  - The flag --worker_max_retries was removed. The
    WorkerSpawnStrategy no longer retries execution of failed Spawns,
    the reason being that this just masks compiler bugs and isn't
    done for any other execution strategy either.
  - Bazel will no longer gracefully restart workers that crashed /
    quit, instead this triggers a build failure.
  - All java resources are now compressed in android_binary APKs by
    default.
  - All java resources are now compressed in android_binary APKs by
    default.
  - android_ndk_repository now creates a cc_library
    (@androidndk//:cpufeatures) for the cpufeatures library that is
    bundled in the Android NDK. See
    https://developer.android.com/ndk/guides/cpu-features.html for
    more details.
  - 'output_groups' and 'instrumented_files' cannot be specified in
    DefaultInfo.
  - You can increase the CPU reservation for tests by adding a
    "cpu:<n>" (e.g. "cpu:4" for four cores) tag to their rule in a
    BUILD file. This can be used if tests would otherwise overwhelm
    your system if there's too much parallelism.
  - Deprecate use_singlejar_for_proguard_libraryjars and force
    behavior to always on.

## Release 0.4.5 (2017-03-16)

```
Baseline: 2e689c29d5fc8a747216563235e905b1b62d63b0

Cherry picks:
   + a28b54033227d930672ec7f2714de52e5e0a67eb:
     Fix Cpp action caching
   + 6d1d424b4c0da724e20e14235de8012f05c470f8:
     Fix paths of binaries in .deb packages.
   + 0785cbb672357d950e0c045770c4567df9fbdc43:
     Update to guava 21.0 and Error Prone version 2.0.18-20160224
   + 30490512eb0e48a3774cc4e4ef78680e77dd4e47:
     Update to latest javac and Error Prone
   + 867d16eab3bfabae070567ecd878c291978ff338:
     Allow ' ', '(', ')' and '$' in labels
   + 7b295d34f3a4f42c13aafc1cc8afba3cb4aa2985:
     Pass through -sourcepath to the JavaBuilder
   + 14e4755ce554cdfc685fc9cc2bfb5b699a3b48f4:
     PathFragment comparisons are now platform-aware
   + ed7795234ca7ccd2567007f2c502f853cd947e50:
     Flag to import external repositories in python import path
   + 81ae08bbc13f5f4a04f18caae339ca77ae2699c1:
     Suppress error for non-exhaustive switches
   + e8d1177eef9a9798d2b971630b8cea59471eec33:
     Correctly returns null if an environment variables is missing
   + 869d52f145c077e3499b88df752cebc60af51d66:
     Fix NPE in Android{S,N}dkRepositoryFunction.
   + d72bc57b60b26245e64f5ccafe023a5ede81cc7f:
     Select the good guava jars for JDK7 build
   + 92ecbaeaf6fa11dff161254df38d743d48be8c61:
     Windows: Assist JNI builds with a target for jni_md.h.
   + 36958806f2cd38dc51e64cd7bcc557bd143bbdb6:
     Add java_common.create_provider to allow creating a
     java_common.provider
   + 8c00f398d7be863c4f502bde3f5d282b1e18f504:
     Improve handling of unknown NDK revisions in
     android_ndk_repository.
   + b6ea0d33d3ab72922c8fb3ec1ff0e437af09584d:
     Add the appropriate cxx_builtin_include_directory entries for
     clang to the Android NDK crosstool created by
     android_ndk_repository.
```

Incompatible changes:

  - Depsets (former sets) are converted to strings as "depset(...)"
    instead of
    "set(...)".
  - Using --symlink_prefix is now applied to the output
    symlink (e.g. bazel-out) and the exec root symlink (e.g.
    bazel-workspace).
  - Bazel now uses the test's PATH for commands specified as
        --run_under; this can affect users who explicitly set PATH to
    a more
        restrictive value than the default, which is to forward the
    local PATH
  - It's not allowed anymore to compare objects of different types
    (i.e. a string to an integer) and objects for which comparison
    rules are not
    defined (i.e. a dict to another dict) using order operators.

New features:

  - environ parameter to the repository_rule function let
    defines a list of environment variables for which a change of
    value
    will trigger a repository refetching.

Important changes:

  - android_ndk_repository now supports Android NDK R13.
  - Android resource shrinking is now available for android_binary
    rules. To enable, set the attribute 'shrink_resources = 1'. See
    https://bazel.build/versions/master/docs/be/android.html#android_b
    inary.shrink_resources.
  - resolve_command/action's input_manifest return/parameter is now
    list
  - For increased compatibility with environments where UTS
    namespaces are not available, the Linux sandbox no longer hides
    the hostname of the local machine by default. Use
    --sandbox_fake_hostname to re-enable this feature.
  - proto_library: alias libraries produce empty files for descriptor
    sets.
  - Adds pkg_rpm rule for generating RPM packages.
  - Allow CROSSTOOL files to have linker flags specific to static
    shared libraries.
  - Make it mandatory for Java test suites in bazel codebase, to
    contain at least one test.
  - Support for Java 8 lambdas, method references, type annotations
    and repeated annotations in Android builds with
    --experimental_desugar_for_android.
  - Removed .xcodeproj automatic output from objc rules. It can still
    be generated by requesting it explicitly on the command line.
  - Flips --explicit_jre_deps flag on by default.
  - Activate the "dbg", "fastbuild", and "opt" features in the objc
    CROSSTOOL.
  - Remove support for configuring JDKs with filegroups; use
    java_runtime and java_runtime_suite instead
  - android_ndk_repository api_level attribute is now optional. If not
    specified, the highest api level in the ndk/platforms directory
    is used.

## Release 0.4.4 (2017-02-01)

```
Baseline: 4bf8cc30a

Cherry picks:
   + ef1c6fd33: msvc_tools.py.tpl: Change default runtime library to
              static
```

Incompatible changes:

  - Only targets with public visibility can be bound to something in
    //external: .
  - The deprecated -x startup option has been removed.
  - docker_build: change the repository names embedded by
    docker_build. You can revert to the old behavior by setting
    legacy_repository_naming=True.
  - The string methods strip(), lstrip(), and rstrip() now
    by default remove the same whitespace characters as Python 3
    does, and accept
    None as an argument.
  - Deprecated globals HOST_CFG and DATA_CFG are removed. Use strings
    "host" and "data" instead.
  - repository_ctx environment is now affected by --action_env flag
    (value from the
    client environment will be replaced by value given on the command
    line through --action_env).
  - All executable labels must also have a cfg parameter specified.
  - Removed the cmd_helper.template function.
      The function was equivalent to:
        def template(items, template):
          return [template.format(path = i.path, short_path =
    i.short_path)
                    for i in items]
  - Tuples that end with a trailing comma must now be inside parens,
      e.g. (1,) instead of 1,
  - The traversal orders for depsets have been renamed. The old names
    are deprecated and will be removed in the future. New names:
    "stable" -> "default", "compile" -> "postorder", "link" ->
    "topological", "naive_link" -> "preorder".

New features:

  - Skylark: you can now multiply a list by an integer to get the
    concatenation of N copies of this list, e.g. [a,b] * 3 =
    [a,b,a,b,a,b]
  - Allow Android aidl tool to add a jar to the program's classpath,
    such as if needed to support generated sources.
  - Add transitive proguard_specs when android_sdk.aidl_lib is
    specified
  - Windows: "/dev/null" is now a supported path, e.g.
    --bazelrc=/dev/null now works

Important changes:

  - Bazel Android builds use the apksigner tool from the Android SDK
    build-tools. Bazel Android builds now require build-tools version
    24.0.3 or
    later.
  - Android SDK external bindings for support libraries, e.g.
    //external:android/appcompat_v4, are removed because the support
    library JARs that they referenced no longer ship with the Android
    SDK.
  - aar_import rule is now documented.
  - An IE bug was fixed in repository_ctx.download_and_extract
  - Update "-I" to "-isystem" in documentation to reflect current
    behavior.
  - android_sdk_repository build_tools_version is now optional. The
    highest installed build-tools will be used if none is specified.
  - New flag --sandbox_add_mount_pair to specify customized
    source:target path pairs to bind mount inside the sandbox.
  - expose proto_library descriptor set to skylark via
    <dep>.proto.descriptor_set
  - The `set` constructor is deprecated in favor of `depset`
  - Autodetect gold linker in cc_configure.bzl
  - Remove build flag --experimental_j2objc_annotation_processing. It
    is on by default now.
  - Set clang's -mwatchos-version-min correctly using the value of
    --watchos_minimum_os, not --watchos_sdk_version.
  - singlejar can now create jar files larger than 4GB.
  - android_sdk_repository and android_ndk_repository now read
    $ANDROID_HOME and $ANDROID_NDK_HOME if the path attribute is not
    set.
  - Removed broken api levels 3, 4 and 5 from Android NDK 12.
  - Default --android_dynamic_mode to off.
  - android_sdk_repository no longer requires api_level. If one is
    not specified, the highest android platform installed will be
    used. Furthermore, android_sdk's are created for all android
    platforms installed and can be specified with the --android_sdk
    flag.
  - To iterate over or test for membership in a set, prefer using the
    new to_list() method. E.g., "for x in myset.to_list():", or
    "print(x in myset.to_list())". Iteration/membership-test on the
    raw set itself is deprecated.
  - Remove support for --javawarn; use e.g. --javacopt=-Xlint:all
    instead

## Release 0.4.3 (2016-12-22)

```
Baseline: c645a45

Cherry picks:
   + af878d0: Add coverage support for java test. (series 4/4 of
              open-sourcing coverage command for java test)
   + 09b92a8: Rollback of commit
              67b4d5250edcefa7220e928e529b1f385e2dc464.
   + b11dd48: Fix bad bug with the parallel implementation of
              BinaryOperatorExpression. Turns out that
              ForkJoinTask#adapt(Callable) returns a ForkJoinTask
              whose Future#get on error throws a ExecutionException
              wrapping a RuntimeException wrapping the thrown checked
              exception from the callable. This is documented
              behavior [1] that I incorrectly didn't know about.
   + 9012bf1: Fix scripts/packages/convert_changelog to read the
              changelog correctly
   + 55c97bc: Release script: if master branch does not exist, fall
              back on origin/master
   + 4fb378c: Debian repository: override section and priority fields
   + acbcbc2: Fix release notes in emails
   + 4975760: Fix PathFragment to not use Java8-only static hashCode
              methods.
   + 05fd076: Disable sandboxing for XibCompile actions.
```

Incompatible changes:

  - Skylark maven_jar and maven_aar settings attribute is now a label
    so it can be checked into your workspace.
  - --{no}experimental_use_rclass_generator is now a nop.

New features:

  - Coverage support (*experimental*) for pure Java target.
    Use `bazel coverage //my:target` to generate coverage information
    from a `java_test`.

Important changes:

  - Enable fallback URLs in Skylark http rules.
  - cc_proto_library generates C++ code from proto_library rules.
  - cc_library now supports the strip_prefix and strip_include_prefix
    attributes for control of include paths.
  - Skylark dicts internally don't rely on keys order anymore and
    accept any hashable values (i.e. structs with immutable values)
    as keys. Iteration order of dictionaries is no longer specified.

## Release 0.4.2 (2016-12-02)

```
Baseline: 6331a94

Cherry picks:
   + 7b835d9: Do not patch WORKSPACE in the release process
```

Incompatible changes:

  - Callback functions in Skylark no longer support the cfg
    parameter. This is a cleanup and only affects the signatures of
    callbacks, since the parameter hasn't been set since September
    2016.

Important changes:

  - Alias proto_library's produce a descriptor set that contains all
    srcs of its dependencies.
  - proto_library supports strict proto deps.
  - Top level @androidsdk support library targets have been replaced
    by @androidsdk//<group id>:<artifact id>-<version> for Android
    SDK Support and Google Play Services libraries.

## Release 0.4.1 (2016-11-21)

```
Baseline: 9a796de

Cherry picks:
   + 88bfe85: Description redacted. -- MOS_MIGRATED_REVID=139219934
   + b09ea94: Rollback of commit
              a3f5f576cd35798140ba3e81d03d919dd4ecb847.
```

New features:

  - android_library now has a "exported_plugins" attribute just like
    java_library
  - Use --strict_system_includes to apply hdrs_check=strict also to
        cc_library.includes, even if sandboxing is disabled.
  - Bazel on Windows: java_binary can now be the executable of
    Skylark rule actions (ctx.action's executable argument)
  - Packages are defined in BUILD.bazel as well as BUILD files.

Important changes:

  - getattr()'s 3-arg form no longer raises an error when the
    retrieved field is a built-in method.
  - --apk_signing_method default changed to v1. Android APKs are now
    signed with the new ApkSignerTool by default.
  - New rule: proto_lang_toolchain(), to support LANG_proto_library
    rules on multiple platforms.
  - Fix for Android clang++ std::stack segfault on 32bit x86. See
    https://code.google.com/p/android/issues/detail?id=220159
  - Default android_manifest_merger is now "android" which uses the
    official Android manifest merger.
    http://tools.android.com/tech-docs/new-build-system/user-guide/man
    ifest-merger
  - Do not propagate aspect to its own attributes when using '*'.
  - Comparing sets (`if set1 < set2:`) is not allowed anymore in
    Skylark because it didn't work correctly anyway.
  - When --experimental_extra_action_top_level_only, Bazel reports
    extra-actions for actions registered by Aspects injected by a
    top-level rule (approximately).
  - Blacklists for proto_lang_toolchain() no longer have to be
    proto_library's.
  - Extra actions now contain aspect-related information.
  - Fix slicing bug where "abc"[:-4:-1] would give wrong answer

## Release 0.4.0 (2016-10-26)

```
Baseline: 088bbc6

Cherry picks:
   + b01160c: Stamp Windows release.
   + 2d6736e: Add --no-tty for gpg signing
   + 9b1dfb8: Remove .sig file before gpg signing
   + 81aede1: Reimplement whole archive on Windows
```

Incompatible changes:

  - Skylark: updating list/dicts while they are being looped over is not
    allowed. Use an explicit copy if needed ("for x in list(mylist):").
  - Bazel now uses the --cpu flag to look up Jvms; it falls back
    to "default" if it can't find a Jvm matching the CPU value.
  - --command_port=-1 to use AF_UNIX for client/server communications
    is not supported anymore.
  - Sandboxed actions can access the network by default, unless their
    target has a "block-network" tag.

New features:

  - Files now have an "extension" property in Skylark.

Important changes:

  - Added a new flag --sandbox_tmpfs_path, which asks the sandbox to
    mount an empty, writable directory at a specified path when
    running actions. (Supported on Linux only for now.)
  - Update protoc-3.0.0-mingw.exe to a working (statically linked)
    binary
  - apple_static_library rule to create multi-architecture static
    archive files from Objc/C++/Swift dependencies on apple platforms
  - JS: Add support for localization with closure managed rules.
  - Create a flag --android_dynamic_mode to turn off dynamic mode
    during the Android split transition.
  - Darwin sandboxing is default.
  - Remove flag --experimental_zip_tree_artifact from j2objc Java
    annotation processing support.
  - A few functions are added to BUILD files for consistency (hash,
    dir,
      hasattr, getattr) with .bzl files, although they are not very
    useful.
  - --watchfs is now a command option; the startup option of the same
        name is deprecated. I.e., use bazel build --watchfs, not
    blaze --watchfs
        build.

## Release 0.3.2 (2016-10-07)

```
Baseline: 023a7bd

Cherry picks:
   + bebbbe5: Fix dependency on libtool's helper script
              make_hashed_objlist.py.
   + 8a0d45f: Add the version information to the bazel.exe file
   + 2bc0939: Allow new_ rules to overwrited BUILD files in
              downloaded repos
   + c5545fd: Rollback of commit
              96d46280bc5a4803ba2242a4ad16939f85a3b212.
   + eb87208: Make cc_configure on Windows more robust
   + c30432c: Fix cc_configure on Windows
   + 95b16a8: sandbox: Replace the error-prone lazy cleanup of
              sandbox directories by a simple synchronous cleanup.
   + e898023: Fix #1849: Sandboxing on OS X should be turned off by
              default for 0.3.2.
   + ffdc05d: Add action_config and feature for linking on Windows
```

Incompatible changes:

  - If you maintain a rule that uses persistent workers, you'll have
    to specify execution_requirements={"supports-workers": 1} in the
    ctx.action that intends to run a tool with workers. The
    WorkerSpawnStrategy will alert you with a warning message if you
    forget to make this change and fallback to non-worker based
    execution.
  - It is now an error to include a precompiled library (.a, .lo, .so)
    in a cc_library which would generate a library with the same name
    (e.g., libfoo.so in cc_library foo) if that library also contains
    other linkable
    sources.
  - The main repository's execution root is under the main
    repository's workspace name, not the source directory's basename.
    This shouldn't
    have any effect on most builds, but it's possible it could break
    someone doing
    weird things with paths in actions.
  - Blaze doesn't support Unix domain sockets for communication
    between its client and server anymore. Therefore, the
    --command_port command line argument doesn't accept -1 as a valid
    value anymore.
  - Skylark: It is an error to shadow a global variable with a local
    variable after the global has already been accessed in the
    function.
  - bin_dir and genfiles_dir are now properties of ctx, not
    configuration. That is, to access the bin or genfiles directory
    from a
    Skylark rule, use ctx.bin_dir or ctx.genfiles_dir (not
    ctx.configuration.{bin,genfiles}_dir).  At the moment, you can
    access
    {bin,genfiles}_dir from either, but the ctx.configuration version
    will
    stop working in a future release.
  - filegroup-based C++ toolchains are not supported anymore.
    --*_crosstool_top options must always point to a
    cc_toolchain_suite rule (or an alias of one).
  - repository_ctx.{download,download_and_extract,execute} API now use
                   named parameters for optional parameters and no
    longer uses argument
                   type to distinguished between arguments
    (executable attribute name
                   must be specified when preceding optional
    arguments are missing).

New features:

  - print and fail are now available in BUILD files.

Important changes:

  - Added @bazel_tools//tools/build_defs/repo/git.bzl as a Skylark
    rule for Git repositories.
  - Added @bazel_tools//tools/build_defs/repo/maven_rules.bzl as a
    Skylark rule for Maven repositories.
  - Add global hash() function for strings (only)
  - Improve Android split transition handling.
  - Removes exports_manifest attribute from android_binary rule.
  - java_proto_library: control strict-deps through a rule-level and
    a package-level attribute.
  - Persistent workers are now used by default for Java compilation
    in Bazel, which should speed up your Java builds by ~4x. You can
    switch back to the old behavior via --strategy=Javac=standalone.
    Check out http://www.bazel.io/blog/2015/12/10/java-workers.html
    for more details.
  - objc_* rules can now depend on any target that returns an "objc"
    provider.
  - Adds support for NDK12 to `android_ndk_repository` rule in Bazel.
  - Test targets can disable the JUnit4 test security manager via a
    property.
  - Disable the Android split transition if --android_cpu and
    fat_apk_cpu are both empty.
  - New sandboxing implementation for Linux in which all actions run
    in a separate execroot that contains input files as symlinks back
    to the originals in the workspace. The running action now has
    read-write access to its execroot and /tmp only and can no longer
    write in arbitrary other places in the file system.
  - Add worker support to single jar.
  - Invoke source jar action as a worker.
  - Sandboxed builds allow network access for builds by default.
    Tests will still be run without networking, unless
    "requires-network" is specified as a tag.
  - Add path.realpath() method for Skylark repositories.
  - On Mac devices, detect locally installed versions of xcode to:
     1. Use a sensible default if xcode is required but
    --xcode_version is unspecified.
     2. Use sensible default iOS SDK version for the targeted version
    of xcode if ios_sdk_version is unspecified.
  - Emacs' [C-x `], a.k.a. next-error, works again in emacsen >= 25.1
  - swift_library can be used to build watchOS apps.
  - Exposes the is_device field on Apple platform objects and adds
    the apple_common.platform_type(name) method to retrieve a
    platform_type value that can be passed to methods like the Apple
    fragment's multi_arch_platform.
  - Move Skylark git_repository rules to git.bzl
  - Add support for aspects to attr.label() attributes
  - Global varaiables HOST_CFG and DATA_CFG are deprecated in favor
    of strings "host"
    and "data.
    Argument `cfg = "host"` or `cfg = "data"` is mandatory if
    `executable = True` is provided for a label.
  - The deprecation attribute of all rules now causes warnings
    to be printed when other targets depend on a target with that
    attribute set.
  - Change default of --[no]instrument_test_targets to false, change
    default --instrumentation_filter (which previously tried to
    exclude test targets by heuristic) to only exclude targets in
    javatests.
  - Remove deprecated absolute paths in blaze IDE artifacts
  - When using android_binary.manifest_merger="android" the merger
    produces a summary log next to the merged manifest artifact.
  - Allow different default mallocs per configuration.

## Release 0.3.1 (2016-07-29)

```
Baseline: 792a9d6

Cherry picks:
   + 25e5995: Rollback of commit
              a2770334ea3f3111026eb3e1368586921468710c.
   + 2479405: Fix NPE with unset maven_jar sha1
   + 3cf2126: Rewrite the extra action info files if the data within
              them changes.
   + 5a9c6b4: JavaBuilder: Reintroduce the -extra_checks flag.
```

Incompatible changes:

  - Removed predefined Python variable "generic_cpu".
  - Skylark rules: if you set "outputs" or an attribute to a
    function, this function must now list its required attributes as
    parameters (instead of an attribute map).
  - The host_platform and target_platform entries are not written to
    the master log anymore.
  - Bazel requires Hazelcast 3.6 or higher now for remote execution
    support, because we upgraded our client library and the protocol
    it uses is incompatible with older versions.

New features:

  - LIPO context (--lipo_context) can now also be a cc_test (in
    addition to cc_binary)

Important changes:

  - If --android_crosstool_top is set, native code compiled for
    android will always use --android_compiler and not --compiler in
    choosing the crosstool toolchain, and will use --android_cpu if
    --fat_apk_cpu is not set.
  - Add --instrument_test_targets option.
  - apple_binary supports a new platform_type attribute, which, if
    set to "watchos", will build dependencies for Apple's watchOS2.
  - objc_binary now supports late-loaded dynamic frameworks.
  - Native Swift rules no longer pull in module maps unconditionally.
    Use --experimental_objc_enable_module_maps for that.
  - Merged manifests are guaranteed to have the application element
    as the last child of the manifest element as required by Android
    N.
  - The Android manifest merger is now available as an option for
    android_binary rules. The merger will honor tools annotations in
    AndroidManifest.xml and will perform placeholder substitutions
    using the values specified in android_binary.manifest_values. The
    merger may be selected by setting the manifest_merger attribute
    on android_binary.
  - The progress message would not clear packages that need to be
    loaded twice.
  - Remove warning for high value of --jobs.
  - Use the correct build configuration for shared native deps during
    Android split transitions.
  - When building ObjectiveC++, pass the flag -std=gnu++11.
  - use xcrun simctl instead of iossim to launch the app for "blaze
    run".
  - Glob arguments 'exclude' and 'exclude_directories' must be named
  - Bazel no longer regards an empty file as changed if its mtime has
    changed.

## Release 0.3.0 (2016-06-10)

```
Baseline: a9301fa

Cherry picks:
   + ff30a73: Turn --legacy_external_runfiles back on by default
   + aeee3b8: Fix delete[] warning on fsevents.cc
```

Incompatible changes:

  - The --cwarn command line option is not supported anymore. Use
    --copt instead.

New features:

  - On OSX, --watchfs now uses FsEvents to be notified of changes
    from the filesystem (previously, this flag had no effect on OS X).
  - add support for the '-=', '*=', '/=', and'%=' operators to
    skylark.  Notably, we do not support '|=' because the semantics
    of skylark sets are sufficiently different from python sets.

Important changes:

  - Use singular form when appropriate in blaze's test result summary
    message.
  - Added supported for Android NDK revision 11
  - --objc_generate_debug_symbols is now deprecated.
  - swift_library now generates an Objective-C header for its @objc
    interfaces.
  - new_objc_provider can now set the USES_SWIFT flag.
  - objc_framework now supports dynamic frameworks.
  - Symlinks in zip files are now unzipped correctly by http_archive,
    download_and_extract, etc.
  - swift_library is now able to import framework rules such as
    objc_framework.
  - Adds "jre_deps" attribute to j2objc_library.
  - Release apple_binary rule, for creating multi-architecture
    ("fat") objc/cc binaries and libraries, targeting ios platforms.
  - Aspects documentation added.
  - The --ues_isystem_for_includes command line option is not
    supported anymore.
  - global function 'provider' is removed from .bzl files. Providers
    can only be accessed through fields in a 'target' object.

## Release 0.2.3 (2016-05-10)

```
Baseline: 5a2dd7a
```

Incompatible changes:

  - All repositories are now directly under the x.runfiles directory
    in the runfiles tree (previously, external repositories were at
    x.runfiles/main-repo/external/other-repo. This simplifies
    handling remote repository runfiles considerably, but will break
    existing references to external repository runfiles.
    Furthermore, if a Bazel project does not provide a workspace name
    in the WORKSPACE file, Bazel will now default to using __main__
    as the workspace name (instead of "", as previously). The
    repository's runfiles will appear under x.runfiles/__main__/.
  - Bazel does not embed protocol buffer-related rules anymore.
  - It is now an error for a cc rule's includes attribute to point to
    the workspace root.
  - Bazel warns if a cc rule's includes attribute points out of
    third_party.
  - Removed cc_* attributes: abi / abi_deps. Use select() instead.

New features:

  - select({"//some:condition": None }) is now possible (this "unsets"
    the attribute).

Important changes:

  - java_import now allows its 'jars' attribute to be empty.
  - adds crunch_png attribute to android_binary
  - Replace --java_langtools, --javabuilder_top, --singlejar_top,
    --genclass_top, and --ijar_top with
    java_toolchain.{javac,javabuilder,singlejar,genclass,ijar}
  - External repository correctness fix: adding a new file/directory
    as a child of a new_local_repository is now noticed.
  - iOS apps are signed with get-task-allow=1 unless building with -c
    opt.
  - Generate debug symbols (-g) is enabled for all dbg builds of
    objc_ rules.
  - Bazel's workspace name is now io_bazel. If you are using Bazel's
    source as an external repository, then you may want to update the
    name you're referring to it as or you'll begin seeing warnings
    about name mismatches in your code.
  - Fixes integer overflow in J2ObjC sources to be Java-compatible.
  - A FlagPolicy specified via the --invocation_policy flag will now
    match the current command if any of its commands matches any of
    the commands the current command inherits from, as opposed to
    just the current command.
  - The key for the map to cc_toolchain_suite.toolchains is now a
    string of the form "cpu|compiler" (previously, it was just "cpu").
  - Fix interaction between LIPO builds and C++ header modules.
  - Ctrl-C will now interrupt a download, instead of waiting for it to
    finish.
  - Proxy settings can now be specified in http_proxy and https_proxy
    environment variables (not just HTTP_PROXY and HTTPS_PROXY).
  - Skylark targets can now read include directories from
    ObjcProvider.
  - Expose parameterized aspects to Skylark.
  - Support alwayslink cc_library dependencies in objc binaries.
  - Import cc_library dependencies in generated Xcode project.

## Release 0.2.2b (2016-04-22)

```
Baseline: 759bbfe

Cherry picks:
   + 1250fda: Rollback of commit
              351475627b9e94e5afdf472cbf465f49c433a25e.
   + ba8700e: Correctly set up build variables for the correct pic
              mode for fake_binary rules.
   + 386f242: Automated [] rollback of commit
              525fa71b0d6f096e9bfb180f688a4418c4974eb4.
   + 97e5ab0: Fix cc_configure include path for Frameworks on OS X.
   + a20352e: cc_configure: always add -B/usr/bin to the list of gcc
              option
   + 0b26f44: cc_configure: Add piii to the list of supported
              cpu_value
   + 3e4e416: cc_configure: uses which on the CC environment variable
   + aa3dbd3: cc_configure.bzl: strip end of line when looking for
              the cpu
   + 810d60a: cc_configure: Add -B to compiler flag too
```

Patch release, only includes fixes to C++ auto-configuration.

## Release 0.2.1 (2016-03-21)

```
Baseline: 19b5675
```

Incompatible changes:

  - Skylark rules that are available from their own repository will
    now issue a warning when accessed through @bazel_tools.
  - Set --legacy_bazel_java_test to off by default. java_test will
    now have a slightly different behaviour, correctly emitting XML
    file but, as a downside, it needs correct declaration of the
    test suite (see https://github.com/bazelbuild/bazel/issues/1017).
  - Labels in .bzl files in remote repositories will be resolved
    relative to their repository (instead of the repository the
    Skylark rule is used in).
  - Renamed proto_java_library to java_proto_library.  The former
    is now deprecated and will print out a warning when used.
  - android_sdk now compiles android_jack on the fly from
    android_jar, which means android_jar must be a jar and
    android_jack is now deprecated. The Jack tools (jack, jill,
    resource_extractor) must be specified.
  - Any project that depended on the objc_options rule will be
    broken. Can be fixed by adding attrs (infoplists,copts) directly
    to rules depending on the options.
  - .aidl files correctly require import statements for types
    defined in the same package and the same android_library.

New features:

  - Experimental Windows support is available.
  - Experimental support for writing remote repository rules in
    Skylark is available.
  - iOS ipa_post_processor attribute allows for user-defined IPA
    edits.
  - Adds a to_json method to Skylark structs, providing conversion to
    JSON format.
  - Native python rule can depend on skylark rule as long as skylark
    rule provides 'py' provider.
  - When using both --verbose_failures and --sandbox_debug, Bazel
    prints instructions how to spawn a debugging shell inside the
    sandbox.
  - add flag --sandbox_add_path, which takes a list of additional
    paths as argument and mount these paths to sandbox.

Important changes:

  - @androidsdk//:org_apache_http_legacy added for the legacy Apache
    classes for android sdk version 23 and above.
  - Genrules correctly work when used with bazel run.
  - When namespace-sandbox is run with the -D (debug) flag and
    inside a terminal, it spawns a shell inside the sandbox to aid in
    debugging when the sandboxed command fails.
  - Added --artifact to workspace generator for generating workspace
    and build file rules from artifact coodrinates.
  - Specifying --experimental_android_resource_shrinking on the
    command line will enable a resource shrinking pass on
    android_binary targets that already use Proguard.
  - J2ObjC updated to 1.0.1 release.
  - Added "root_symlinks" and "symlinks" parameters to Skylark
    runfiles() method.
  - You can no longer use objc_binary targets for the xctest_app
    attribute of an ios_test rule.
  - Enable overriding jsonnet binaries and stdlib for Jsonnet rules.
  - mount target of /etc/resolv.conf if it is a symlink.
  - Tests that failed to build because execution was halted no longer
    print their status.
  - Bazel warns if a cc rule's includes attribute contains up-level
    references that escape its package.
  - Add repository_ctx.download and repository_ctx.download_and_extract
    function.

## Release 0.2.0 (2016-02-18)

```
Baseline: 9e100ac
```

Incompatible changes:

  - ObjC compile actions for J2ObjC-translated code now only has
    access to headers from the java deps of the associated original
    java rule.
    These compile actions no longer takes the compiler options
    specified in "copts" attribute on objc_binary/ios_test rules.
    J2ObjC dead code removal (enabled through flag
    "--j2objc_dead_code_removal") now happens *after* ObjC
    compilation.
  - maven_jar no longer supports separate artifact_id, group_id, and
    verison fields. This information should be provided in the
    artifact field,
    instead.

New features:

  - Better support for toolchains that don't have a dynamic linker.
  - build_file_content attribute added to new_git_repository,
    new_http_archive, and new_local_repository.
  - Add support for .tar.bz2 archives to http_archive rules.

Important changes:

  - The --skyframe flag is no longer available for the build command.
  - The --artifacts flag was removed from the dump command.
  - The sha256 attribute is now optional (although recommended!) for
    remote repository rules.
  - Add instrumented file provider support to Skylark rules.
  - Add imports attribute to native Python rules.
  - Allow overriding -gsplit-dwarf from copts.
  - Improved sandbox performance on XFS filesystems.

## Release 0.1.5 (2016-02-05)

```
Baseline: 3a95f35
   + 8378cd8: Rollback of commit
              a9b84575a32476a5faf991da22b44661d75c19b6.
```

Incompatible changes:

  - Set stamping to false by default (i.e., --nostamp)
  - Removed --objc_dump_syms_binary.
  - Removes --objc_gcov_binary flag.
  - Remove JAVAC "Make" variable
  - The startup flag --blaze_cpu is removed,

New features:

  - A new java test runner that support XML output and test filtering
    is supported. It can be used by specifying --nolegacy_bazel_java_test
    or by specifying the test_class attribute on a java_test.
  - Skylark aspects can now specify configuration fragment
    dependencies with fragments and host_fragments like rules can.

Important changes:

  - Support for downloading remote resources through proxies by
    setting HTTP_PROXY (or HTTPS_PROXY).
  - Timestamps within Android apks are removed to make apks
    deterministic.
  - Support aggregation over existing rules in Skylark extensions
    through native.rules and native.rule.
  - A tools/bazel script in the workspace will be executed
    as an opportunity to use a fixed version of Bazel (not
    implemented for the homebrew recipe yet).
  - --noimplicit_deps and --nohost_deps work correctly for Aspect
    attributes.
  - JDK-related targets are now available via @local_jdk (instead of
    @local-jdk).
  - j2objc tools can now be accessed via @bazel_j2objc, not
    @bazel-j2objc.
  - Repository rules must use names that are valid workspace names.
  - [rust] Update to Rust 1.6
  - Add support for .tar.xz archives to http_archive rules.
  - Make C++ modules compatible with tools using
    --compilation_prerequisites_only
  - [d] Update to DMD 2.070.0

## Release 0.1.4 (2016-01-15)

```
Baseline: e933d5e
   + 3d796fe: Rollback of commit
              ac6ed79e1a3fa6b0ca91657b28e2a35f7e49758c.
   + 7a02e5d: Fix installer under OS X
   + 848740c: Fix bazel version for debian package
   + 7751d43: Add a method for getting the root of a rule workspace
              to the Label method
```

Important changes:

  - add loadfiles() query operator, to find skylark files loaded by
    targets.
  - Added ability to declare and use aspects in Skylark.
  - Skylark load statements may now reference .bzl files via build
    labels, in addition to paths. In particular, such labels can be
    used to reference Skylark files in external repositories; e.g.,
    load("@my_external_repo//some_pkg:some_file.bzl", ...).
    Path-based loads are now deprecated and may be disabled in the
    future. Caveats: Skylark files currently do not respect package
    visibility; i.e., all Skylark files are effectively public. Also,
    loads may not reference the special //external package.
  - Relative paths can now be used for 'path' with
    new_local_repository and local_repository.

## Release 0.1.3 (2016-01-07)

```
Baseline: 23ad8f6
   + de2183d: Only depend on the WORKSPACE file for external files
              that are under the external/ directory, i.e. were
              created by Bazel.
   + f8f855c: Rollback of commit
              12bad3af0eade9c4b79d76f9e1c950ad2e3214c2.
   + f627562: Stop parsing the WORKSPACE file when a parse error is
              detected
   + 763f139: Add -fno-canonical-system-headers to CROSSTOOL files so
              that gcc doesn't resolve symlinks in .d files, which
              would confuse Blaze.
   + b95995b: Use openjdk7 as dependency for debian package of jdk7
              flavor
```

New features:

  - Skylark macros are now enabled in WORKSPACE file.
  - .bazelrc allows workspace-relative imports as "import
    %workspace%/path/to/rcfile"
  - Evaluate the query expression in a file by passing
    --query_file=<file> to query

Important changes:

  - Remove obsolete --objc_per_proto_includes flag.
  - iOS apps and extensions now have launch_storyboard
  - Passing multiple JVM options via a single --host_jvm_args flag is
    now deprecated. Pass each JVM option behind its own
    --host_jvm_args flag.
  - Resources defined locally on an android_library rule will respect
    the neverlink attribute.
  - Update Rust to 1.4
  - Fix resource handling for exported android_library rules
  - Files in external repositories are now treated as mutable, which
    will make the correctness guarantees of using external
    repositories stronger (existent), but may cause performance
    penalties.

## Release 0.1.2 (2015-11-20)

```
Baseline: ee0ade3
   + 1e66ccd: RELNOTES: Symlink dirents of directories containing a
              file named
              "DONT_FOLLOW_SYMLINKS_WHEN_TRAVERSING_THIS_DIRECTORY_VIA
              _A_RECURSIVE_TARGET_PATTERN" will *not* be traversed
              for transitive target patterns. The motivation here is
              to allow directories that intentionally contain wonky
              symlinks (e.g. foo/bar -> foo) to opt out of being
              consumed by Blaze. For example, given
   + f5773fc: Set the ijar MAX_BUFFER_SIZE to 256 MB
```

New features:

  - java_library now supports the proguard_specs attribute for
    passing Proguard configuration up to Android (not Java) binaries.
  - http_file can specify "executable" to make the downloaded file
    runnable.
  - Debian and tar packaging is now supported
    (see tools/build_defs/pkg/README.md).
  - cpxx_builtin_include_directory specifications allow more
    flexibility.
  - accept %crosstool_top% in cxx_builtin_include_directory
  - android_binary now supports proguard_apply_mapping to re-use a
    previously generated proguard mapping.

Important changes:

  - remove webstatusserver (--use_webstatusserver).
  - Add support for objc textual headers, which will not be compiled
    when modules are enabled.
  - actoolzip, momczip and swiftstdlibtoolzip have all been made into
    bash scripts and have been renamed to actoolwrapper, momcwrapper
    and swiftstdlibtoolwrapper respectively. The old versions will be
    deleted in a later change.
  - [rust] Add rust_bench_test and rust_doc_test rules and improve
    usability of rust_test tule.
  - Java rules now support a resource_strip_prefix attribute that
    allows the removal of path prefixes from Java resources.
  - [docker_build] incremental loading is default now.
    Specify explicitly //package:target.tar (with the .tar extension)
    to obtain the full image.
  - --ios_signing_cert_name allows specifying a cert for iOS app
    signing
  - Go rules for Bazel.
  - [jsonnet] Update to Jsonnet 0.8.1.
  - [jsonnet] Add vars and code_vars attributes to jsonnet_to_json to
    allow passing external variables to Jsonnet via --var and
    --code_var.
  - Adds --override_workspace_root blaze flag to hand-set
    workspace_root and mainGroup in xcodeproj.
  - Allow dots in package names.
  - When used as a forwarding rule (i.e., has no sources),
    android_library
    will also forward any exported_plugins in its dependencies.
  - Add support for Windows-created zip files with non-posix
    permissions.
  - [jsonnet] Add jsonnet_to_json_test rule for testing Jsonnet code.
  - C++ compile actions run in a sandbox now on systems that support
    sandboxed execution.
  - The names of the clang compilers in the Android NDK crosstool no
    longer reference gcc.
  - 420 dpi is now a valid density for andoid_binary.densities.
  - Bazel does strict validation of include files now to ensure
    correct incremental builds. If you see compilation errors when
    building C++ code, please make sure that you explicitly declare
    all header files in the srcs or hdrs attribute of your cc_*
    targets and that your cc_* targets have correct "deps" on
    cc_library's that they use.
  - [jsonnet] Fix jsonnet_to_json rule to read code_vars from
    code_vars instead of vars.
  - Tests, genrules, and Skylark actions without the
    "requires-network" tag will no longer be able to access the
    network.
  - C++ libraries no longer need includes = ["."] (or similar copts)
    to include paths relative to a remote repository's root.
  - Support exports attribute for android_library
  - Symlink dirents of directories containing a file named
    "DONT_FOLLOW_SYMLINKS_WHEN_TRAVERSING_THIS_DIRECTORY_VIA_A_RECURSI
    VE_TARGET_PATTERN" will *not* be traversed for transitive target
    patterns. The motivation here is to allow directories that
    intentionally contain wonky symlinks (e.g. foo/bar -> foo) to opt
    out of being consumed by Blaze.

## Release 0.1.1 (2015-10-05)

```
Baseline: 22616ae
   + 1ef338f: Rollback of "Propagates cc_library linkopts attribute
              to dependent objc_libraries.": breaks certain
              objc_binary build targets.
   + 5fb1073: Reintroduce an inconsistency check (albeit, in a weaker
              form) removed by a previous change that was trying to
              optimize away a filesystem call.
   + 6d00468b2eb976866cfb814d562e0d53a580a46f: Add IdlClass to the embedded default android tools
              repository and rearrange BuildJar's JarHelper so that
              it too can be embedded.
   + a5199039934a2e399a7201adc0d74e2f2d2b0ff3: Fixes Android integration tests by wiring up idlclass
              rules in integration environment.
```

Incompatible changes:

  - Bazel requires JDK 8 to run.
  - Attribute "copts" is removed from j2objc_library.

New features:

  - a cc_binary rule may list '.s' and '.asm' files in the srcs
  - Support for build with libsass.
  - labels in "linkopts" may match any label in either "deps" or
    "srcs" to be considered valid.
  - Maven servers that require username & password authentication are
    now supported (see maven_server documentation).

Important changes:

  - Support empty plist files
  - The <compatible-screens> section of the AndroidManifest.xml will
    not be overwritten if it already contains a <screen> tag for each
    of the densities specified on the android_binary rule.
  - Add Jsonnet rules to Bazel
  - Remove deprecated xcode_options flag.
  - Workspace names are now restricted to being in their base
    directory
    (that is, the names cannot contain up-level references or /./).
  - j2objc_library on Bazel now transpiles transitive proto_library
    dependencies. (Note that java_* rules in Bazel do not yet support
    protos; currently they ignore proto dependencies.)
  - new_http_archive can specify a root directory.
  - Adds support for dylibs on devices for Xcode 7.
  - [d] d_docs rules now depend on a d_binary, a d_library or
    d_source_library.
  - [docker] docker_build now set the permission to 0555 to files
    added to the layer, use `mode = "0644"` to use the legacy behavior.
  - android_binary now has a main_dex_proguard_specs attribute to
    specify which classes should be in the main dex.
  - [rust] Add rust_docs rule for generating rustdoc.
## Release 0.1.0 (2015-09-08)

```
Baseline: a0881e8
   + 87374e6: Make android_binary use a constant, hard-coded,
              checked-in debug key.
   + 2984f1c: Adds some safety checks in the Bazel installer
   + 4e21d90: Remove BUILD.glob and incorporate the necessary
              filegroups into the android_{ndk,sdk}_repository rules
              themselves.
   + 1ee813e: Fix Groovy rules to work with sandboxing
   + 8741978: Add initial D rules to Bazel.
   + 2c2e70d: Fix the installer and fixing the package shiped into
              binary version of Bazel.
```

Initial release.













