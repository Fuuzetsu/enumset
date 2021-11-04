# Version 1.0.8 (2021-11-04)
* Optimized `EnumSet` iteration. (Thanks @MinusKelvin)

# Version 1.0.7 (2021-07-05)
* Added the `#[repr(transparent)]` flag to `EnumSet<T>` to allow for safe usage
  in FFI code. Note that invalid bits being set in the bitset causes UB, so
  this should be done with care. (Thanks @Riey)

# Version 1.0.6 (2021-02-27)
* Fix an unneeded warning in the output for `enum_set!` for a single value.

# Version 1.0.5 (2021-02-24)
* Implemented `core::iter::Sum` for `EnumSet<T>`.
* Properly acknowledge that the minimum required Rust version is actually 1.34+
  and not 1.31+. An retroactive changelog entry has been added to 1.0.0.

# Version 1.0.4 (2021-02-07)
* Fixes a bug that caused `enumset_derive` to require an import of `EnumSet`
  in the scope to function.

# Version 1.0.3 (2021-01-27)
* (This version contains no code changes.)
* Redirected badges in the README to point at travis-ci.com instead of .org
* Added `README.md`, and the license files to the crate distribution.

# Version 1.0.2 (2021-01-25)
* Fixed critical error compiling on newer versions of `syn` caused by a
  mistaken import from a private module. (Thanks @ocboogie)

# Version 1.0.1 (2020-08-09)
* Implemented `ExactSizeIterator` for `EnumSetIter`. (Thanks @dmarcuse)

# Version 1.0.0 (2020-04-06)

## Breaking Changes
* **[WARNING: Potential silent breaking change]** Changed `EnumSet::insert` to
  return whether a value was newly  inserted, rather than whether the value
  already existed in the set. This corresponds better with the behavior of
  `HashSet::insert` and `BTreeSet::insert`.
* Renamed `to_bits`/`from_bits` to `as_u128`/`from_u128`.
* `EnumSet::bit_width` and `EnumSet::variant_count` now return a `u32` instead
  of a `u8` for future-proofing.
* Removed `nightly` feature flag, as it is no longer required.
* Minimum required Rust version is now 1.34+.

## New features
* Added a series of functions like `as_u128`/`from_u128` for other unsigned
  numeric types. (e.g. `as_u8`/`from_u8`, `as_u16`/`from_u16`, etc)
* Added variants of `as_u128`/`from_u128` that return an `Option` instead of
  panicking when the conversion cannot be done.
* Added variants of `as_u128`/`from_u128` that truncate unknown bits instead
  of panicking.
* Implemented `Extend<EnumSet<T>>` and `FromIterator<EnumSet<T>>` for
  `EnumSet<T>`. (Thanks @manuthambi)
* Added an `#[enumset(crate_name = "renamed_enumset")]` annotation for
  handling renamed crates.

## Bugfixes
* Fixed a bug where the procedural macro would fail on enums with a repr
  annotation set. While reprs larger than u8 are supported, negative enum
  variants or enum variants above 127 are still not currently supported.

# Version 0.4.5 (2020-02-19)
* Fixed a bug where compilation failed when the `serde` flag was enabled, and
  another trait that defined `serialize` or `deserialize` was in scope.

# Version 0.4.4 (2019-10-12)
* Fixed a bug where `#[enumset(serialize_as_list)]` did not work when `Result`
  is shadowed.

# Version 0.4.3 (2019-10-08)
* Implemented `Extend` and `FromIterator` for `EnumSet<T>`.

# Version 0.4.2 (2019-09-28)
* Fixed a bug preventing empty enums and enums with one value from compiling.

# Version 0.4.1 (2019-09-27)
* Fixed bug in `EnumSetIter::size_hint`. (Thanks @manuthambi)

# Version 0.4.0 (2019-05-06)
* Removed outdated macros and attributes.
* All attributes for the custom derive are now written as `#[enumset(...)]`
* Implemented `#[enumset(serialize_deny_unknown)]`
* Implemented `#[enumset(serialize_repr="...")]`
* `#[derive(EnumSetType)]` now only implements `Copy`, `Clone`, `PartialEq` and
  `Eq` automatically.

# Version 0.3.19 (2019-05-02)
* Fix a bug when deserializing enums containing invalid bits set.

# Version 0.3.18 (2019-03-11)
* Fix an off-by-one error causing enums with 9, 17, 33, etc variants to behave
  unexpectedly.

# Version 0.3.17 (2019-03-11)
* Add an `#[enumset_serialize_as_list]` attribute to cause the `Deserialize`
  and `Serialize` implementations for `EnumSet<T>` to serialize it as a seq
  of `T`s rather than an integer bitmask.

# Version 0.3.16 (2019-02-04)
* Added `Default` implementation for `EnumSet<T>` that returns an empty map.
  (Thanks @boxdot)

# Version 0.3.15 (2019-01-08)
* Added optional `serde` support.

# Version 0.3.14 (2018-11-09)

* Deprecated the `enum_set_type!` macro in favor of a custom derive.
* Added a way to avoid the automatic operator overloads derived from
  EnumSetTypes.
* Fixed a major issue that would have prevented `enumset` from being used in
  `#[no_std]` crates.
* Minimum required version is now 1.30.0+. There should be no more need to
  bump the minimum Rust version in the forseeable future.

# Prior versions

No release notes were kept for prior versions.
