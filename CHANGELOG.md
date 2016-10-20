## v0.14.0-dev

## v0.13.2 (2016-09-19)

* Bug fixes
  * Only error on non-Hex dependencies when building

## v0.13.1 (2016-09-19)

* Enhancements
  * Most warnings on `hex.publish` are now errors

* Bug fixes
  * Fix bug where the old config format was not readable
  * Convert old config format to new format on every read
  * Fix `HEX_UNSAFE_REGISTRY` negation

## v0.13.0 (2016-07-30)

* Enhancements
  * Inform about new Hex version in `hex.info`
  * Support `extra` metadata field
  * Print package checksum when building and publishing
  * Warn if using registry from cache
  * Show creation time of API keys in `hex.keys list`
  * Improve the error message if OTP has broken SNI in `:ssl` application
  * Verify dependencies from registry against lock
  * Hex will now automatically encrypt your local API key, use `hex.user passphrase` to change the encryption passphrase
  * Improve resolver error message to mention behavior of pre-releases and overrides
  * Improve error message if a dependency has configured the OTP application name incorrectly for another dependency
  * `hex.publish` now also publishes docs by default, use `hex.publish package` and `hex.publish docs` to respectively publish package and docs independently
  * `hex.docs` will now open or fetch documentation tarballs
  * `hex.key remove` will now also de-auth the user if the local API key was removed
  * Add status messages when publishing and reverting

* Bug fixes
  * Fix bug where the client was fetching packages even when lock is OK
  * Fix resolver sometimes not producing any backtrack output
  * Verify certificate against correct hostname after redirect

## v0.12.1 (2016-05-31)

* Enhancements
  * Only show proxy settings when MIX_DEBUG=1
  * Add retries to idempotent requests

* Bug fixes
  * Fix crash when you get multiple backtrack messages

## v0.12.0 (2016-05-15)

* Enhancements
  * Add package checksums to lock, ensuring a locked package can not change its content
  * Add managers and deps to lock, allowing Hex to run without loading the registry
  * Align deps fetching output from scm
  * Update hex.pm repo URL to https://repo.hex.pm
  * Link to policies when registering account
  * Update CoC links
  * Improve conflict messages
  * Improve error messages when ex_doc is missing when publishing docs
  * Show app name of dependency in `hex.info`
  * Warn about long package descriptions

* Bug fixes
  * Fix `HEX_UNSAFE_HTTPS` environment variable and `unsafe_https` config

## v0.11.5 (2016-04-07)

* Enhancements
  * Add more registry metrics to `hex.info`

* Bug fixes
  * Fix a bug where Hex was about a bit too enthusiastic when informing the user of new versions
  * Fix some missing future-proofing of lock

## v0.11.4 (2016-04-06)

* Enhancements
  * Use HTTPS to Hex.pm repository
  * Make lock backwards compatible by treating it as a list and only matching on the front

* Bug fixes
  * Correctly show update notification
  * Remove duplicate parents from backtrack messages
  * Fix invalid message in `hex.outdated` if locked version is a pre-release

## v0.11.3 (2016-03-14)

* Bug fixes
  * Do not crash if registry fails to fetch
  * Remove force update of registry if it is more than a week old

## v0.11.2 (2016-03-11)

* Enhancements
  * Verify registry signature against public key
  * Improve missing registry error message
  * Deprecate `HEX_CDN` in favor of `HEX_REPO` and `HEX_MIRROR`. See the `hex` task for more information
  * Deprecate `:cdn_url` config in favor of `:repo_url` and `mirror_url`. See the `hex.config` task for more information
  * Improve performance of parallel package fetching
  * Use fastly instead of S3 for the Hex.pm repository
  * Add `--delete` option to `hex.config` task

* Bug fixes
  * Show local time in hex.info
  * Correctly unlock all dependencies on `deps.update`
  * Always fetch registry if it's missing or known to be old

## v0.11.1 (2016-03-03)

* Bug fixes
  * Fix incorrect build version check
  * Fix parsing of requirements without spaces

## v0.11.0 (2016-03-03)

* Enhancements
  * Append the OTP version to the user_agent function
  * Improve output of http request timeout errors
  * Warn if `:manager` or `:compile` is set on dependencies when publishing
  * Add `--pre` flag to `hex.outdated`
  * Use erlang binary term encoding for API instead of elixir encoding
  * Pull package name from correct source when publish docs
  * Pass canonical url to ex_doc task
  * Change hexdocs links to use https
  * Add `hex.outdated APP` to list all requirements on given dependency
  * Do not allow pre-releases for dependencies unless the requirement uses a pre-release version
  * Optimize version cache memory usage

* Bug fixes
  * Fix incorrect build version check for dev versions of Elixir
  * Fix loop when backtracking in resolver
  * Fix timeout errors on slow systems

## v0.10.4 (2016-01-26)

* Enhancements
  * Make the experimental resolver the default

* Bug fixes
  * Ensure registry can be opened/closed multiple times
  * Ensure `hex.search` task handles empty results
  * Fix experimental resolvers only backtracking on parents that had requirements that failed
  * Fix merging of overlapping parent and package versions in backtrack messages

## v0.10.3 (2016-01-23)

* Bug fixes
  * Fix bug when umbrella child has dependency with `:only`

## v0.10.2 (2016-01-22)

* Enhancements
  * General optimizations in dependency resolver
  * Add experimental faster backtracker that does more aggressive backtracking, set environment variable `HEX_EXPERIMENTAL_RESOLVER=1` to use it
  * Merge backtrack messages that have similar parents
  * Merge multiple versions into version ranges when possible for more succinct backtrack messages

* Bug fixes
  * Reduce memory usage when resolver produces many backtrack messages

## v0.10.1 (2016-01-15)

* Bug fixes
  * Fix a crash when a dependency is missing its version requirement

## v0.10.0 (2016-01-14)

* Enhancements
  * Add support for authentication when using HTTP proxies
  * Add more build information to `hex.info` task to ease debugging
  * Greatly improve backtracking error messages
  * Prevent packages for being published without a description
  * Improve error printing when S3 return errors
  * Improve output from `hex.outdated` task
  * Warn if a package dependency is missing its requirement
  * Improve error message from `hex.docs` task when `ex_doc` dependency is missing
  * Remove useless output when fetching dependencies
  * Improve package output in `hex.info` task

* Bug fixes
  * Fix a rare bug that could cause the resolver to go into an infinite loop
  * UTF8 encode package metadata
  * Only list missing files if `:files` is set
  * Fix bug when umbrella child has dependency with `:only`

## v0.9.0 (2015-09-25)

* Enhancements
  * Pass build tool information to Mix (supported in Elixir 1.1.0)
  * Make Hex a proper OTP application
  * Update CA store
  * Warn if files are missing when building package
  * Improve error message when resolution fails because of a locked dependency
  * Add `hex.registry` task for loading and dumping registry
  * Add `HEX_OFFLINE` for running in offline mode which skips fetching registry and packages
  * Add `hex.build` task for building package without publishing
  * Reduce noise when users gets lots of resolution errors and generally improve their output
  * Add Server Name Indication support for HTTPS requests
  * Add `HEX_UNSAFE_HTTPS` for disabling certificate checking
  * Rename `:contributors` metadata to `:maintainers` to better reflect purpose of field

* Bug fixes
  * `HEX_API` no longer automatically adds `api/` to URL
  * Fix crash when user doesn't explicitly override Hex package when needed
  * Fix bug where metadata in package tarball was not properly UTF8 encoded
  * Fix error message when registry file is missing
  * Support `hex.outdated` task for umbrella projects
  * Do not raise on bad data in a users old lock

## v0.8.3 (2015-07-17)

* Security fixes
  * Fix a bug that would trust any certificate in the certificate chain signed by a trusted CA, this could allow the certificate, that is not a CA, to issue and sign new certificates for any host

## v0.8.2 (2015-07-13)

* Enhancements
  * Sort dependency resolver results

* Bug fixes
  * Fix build_tools metadata being sent incorrectly

## v0.8.1 (2015-07-12)

* Enhancements
  * Warn if registry file is missing when loading deps

* Bug fixes
  * Consider new optional requirements for already activated dependency
  * Add multiple build tools to metadata

## v0.8.0 (2015-05-19)

* Enhancements
  * Warn if using insecure SSL because of old OTP version
  * Use yellow test for warning text
  * Include build_tools in release metadata
  * Print more metadata when publishing

* Bug fixes
  * Fix an error when printing an http status codes
  * Always fetch new registry if it's older than 7 days

## v0.7.5 (2015-04-12)

* Enhancements
  * Add task `hex.user test` for testing user authentication.
  * Add task `hex.outdated` for listing outdated packages compared to the registry.
  * Update CA store as of April 3.
  * Inform user if authentication failed because they did not confirm email.
  * Improve error message for unsupported tarball version.

* Bug fixes
  * Fix a bug where overriding a Hex dependency with a non-Hex dependency was ignored when the overriding at least two levels deep in the dependency tree

## v0.7.4 (2015-03-16)

* Bug fixes
  * Include all conflicting requirements in backtrack message
  * Fix a bug where backtrack message failed on optional requests

## v0.7.3 (2015-03-04)

* Bug fixes
  * Fix an error when merging locked and optional dependencies

## v0.7.2 (2015-03-04)

* Enhancements
  * Print messages on backtracks if dependency resolution failed, this is intended to help users resolve conflicts

* Bug fixes
  * Fix a bug where a dependency converged in mix did not consider all its requirements
  * Fix a bug where dependencies in the lock was considered even if they weren't requested

## v0.7.1 (2015-02-15)

* Bug fixes
  * Fix updating the registry

## v0.7.0 (2015-02-15)

* Enhancements
  * Print proxy options on startup
  * Add `mix hex.user password reset` and remove `mix hex.user update`
  * Create version 3 tarballs with erlang term encoded metadata

* Bug fixes
  * Verify peer certificate against CA certificate public key in `partial_chain`
  * Fix a bug where overriding a Hex dependency with a non-Hex dependency was ignored when the overriding happened in a sub-dependency
  * Create hex directory before writing registry

## v0.6.2 (2015-01-02)

* Enhancements
  * Add PKIX hostname verification according to RFC6125
  * Improve error messages from HTTP error codes
  * Improve HTTP performance
  * Add config options `api_url`, `cdn_url`, `http_proxy` and `https_proxy`
  * Support both doc/ and docs/ as documentation directory

## v0.6.1 (2014-12-11)

* Enhancements
  * Convert config file to erlang term file

## v0.6.0 (2014-10-12)

* Enhancements
  * Add support for packages with a different OTP application name than the package name
  * Add task `mix hex.docs` for uploading project documentation
  * Add email confirmation

* Bug fixes
  * Allow you to change your password with `mix hex.user update`
  * Correctly display dependencies in `mix hex.info PACKAGE VERSION`
  * Verify peer certificates when fetching tarball

## v0.5.0 (2014-09-19)

* Enhancements
  * Verify peer certificate for SSL (only available in OTP 17.3)
  * Reduce archive size with compiler option `debug_info: false`
  * Add support for config as an erlang term file
  * Warn if Hex was built against a different major.minor Elixir version

## v0.4.3 (2014-09-06)

## v0.4.2 (2014-08-31)

* Enhancements
  * Add task `hex.user whoami` that prints the locally authorized user
  * Add task `hex.user deauth` to deauthorize the local user
  * Rename environment variable `HEX_URL` to `HEX_API` to not confuse it with `HEX_CDN`

* Bug fixes
  * Print newline after progress bar

## v0.4.1 (2014-08-12)

* Enhancements
  * Add progress bar for uploading the tarball when publishing
  * Compare tarball checksum against checksum in registry
  * Bump tarball support to version 3
  * Rename task for authenticating on the local machine from `hex.key new` to `hex.user auth`
  * Remove the ability to pass password as a CLI parameter

* Bug fixes
  * Support lower-case proxy environment variables
  * Remove any timeouts when fetching package tarballs
