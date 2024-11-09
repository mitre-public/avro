# Apache Avro™

[![test c][test c img]][test c]
[![test c#][test c# img]][test c#]
[![test c++][test c++ img]][test c++]
[![test java][test java img]][test java]
[![test javascript][test javascript img]][test javascript]
[![test perl][test perl img]][test perl]
[![test ruby][test ruby img]][test ruby]
[![test python][test python img]][test python]
[![test php][test php img]][test php]

[![rust continuous integration][rust continuous integration img]][rust continuous integration]
[![rust clippy check][rust clippy check img]][rust clippy check]
[![rust security audit][rust security audit img]][rust security audit]

[![codeql c#][codeql c# img]][codeql c#]
[![codeql java][codeql java img]][codeql java]
[![codeql javascript][codeql javascript img]][codeql javascript]
[![codeql python][codeql python img]][codeql python]

-----

This repository contains a **modified** Java implementation of [Apache Avro](https://github.com/apache/avro). It addresses the following
3 issues:

1. The changes in this version allow for the serialization of java generics in supertypes, such as the example below:
```java
class AbstractRecord<T> { T recordType; }

/**
 * The template type will be lost on write-out and deserialization will fail without this change
 * @param <Y> the concrete template type stored in {@link AbstractRecord#recordType}
 */
final class OutputRecord<Y> extends AbstractRecord<Y> {}
```
2. Support configuration of serialization field order via the `@AvroOrder` annotation
```java
final class OutputRecord {
  
  @AvroOrder(Schema.Field.Order.ASCENDING)
  final String outputField;
}
```
3. Prior to the introduction to the `@AvroAliases` annotation, support configuring multiple aliases via a single annotation. This feature has been removed for avro versions >= 1.10
```java
@AvroAlias({"org.mitre.A", "org.mitre.B"})
final class OutputRecord {}
```

Note: self-hosted ARM based java actions have been removed

### Releasing new versions

- Update main with the latest Avro changes and rebase the forked changes
- Ensure you have the upstream avro fork as a git remote and fetch tags
  ```shell
  git remote add fork-source https://github.com/apache/avro
  git fetch --tags fork-source
  ```
- Check out a new release branch from the relevant avro release tag  
  `git checkout -b release/1.0.0-1.12.0 release-1.12.0`
- Apply the most recent fork change to that branch  
  `git cherry-pick <ref-from-main>`
- **If** adjusting the fork itself, bump the version in `lang/java/avro/pom.xml` to match the forked changes. Otherwise,
you can rely on the project version itself.
- Deploy the final jars from `lang/java/avro`
  `mvn deploy -DskipTests -DaltDeploymentRepository=repository-id::repository-url`
- Push the release branch to remote

---

<p align=center><ins><b>NOTICE</b></ins></p>

<p>This work was produced for the U.S. Government under Contract 693KA8-22-C-00001 and is subject to Federal Aviation Administration Acquisition Management System Clause 3.5-13, Rights In Data-General (Oct. 2014), Alt. III and Alt. IV (Oct. 2009).</p>

<p>The contents of this document reflect the views of the author and The MITRE Corporation and do not necessarily reflect the views of the Federal Aviation Administration (FAA) or the Department of Transportation (DOT). Neither the FAA nor the DOT makes any warranty or guarantee, expressed or implied, concerning the content or accuracy of these views.</p>

<p>For further information, please contact The MITRE Corporation, Contracts Management Office, 7515 Colshire Drive, McLean, VA 22102-7539, (703) 983-6000.</p>

<p align=center><ins><b>&copy; 2024 The MITRE Corporation. All Rights Reserved.</b></ins></p>

---

<p align=center>Approved for Public Release; Distribution Unlimited. Public Release Case Number 24-3517</p>

---


Apache Avro™ is a data serialization system.

Learn more about Avro, please visit our website at:

  https://avro.apache.org/

To contribute to Avro, please read:

  https://cwiki.apache.org/confluence/display/AVRO/How+To+Contribute

<!-- Arranged this way for easy copy-pasting and editor string manipulation -->

[test c]:          https://github.com/apache/avro/actions/workflows/test-lang-c.yml
[test c#]:         https://github.com/apache/avro/actions/workflows/test-lang-csharp.yml
[test c++]:        https://github.com/apache/avro/actions/workflows/test-lang-c++.yml
[test java]:       https://github.com/apache/avro/actions/workflows/test-lang-java.yml
[test javascript]: https://github.com/apache/avro/actions/workflows/test-lang-js.yml
[test perl]:       https://github.com/apache/avro/actions/workflows/test-lang-perl.yml
[test ruby]:       https://github.com/apache/avro/actions/workflows/test-lang-ruby.yml
[test python]:     https://github.com/apache/avro/actions/workflows/test-lang-py.yml
[test php]:        https://github.com/apache/avro/actions/workflows/test-lang-php.yml

[rust continuous integration]: https://github.com/apache/avro/actions/workflows/test-lang-rust-ci.yml
[rust clippy check]:           https://github.com/apache/avro/actions/workflows/test-lang-rust-clippy.yml
[rust security audit]:         https://github.com/apache/avro/actions/workflows/test-lang-rust-audit.yml

[codeql c#]:         https://github.com/apache/avro/actions/workflows/codeql-csharp-analysis.yml
[codeql java]:       https://github.com/apache/avro/actions/workflows/codeql-java-analysis.yml
[codeql javascript]: https://github.com/apache/avro/actions/workflows/codeql-js-analysis.yml
[codeql python]:     https://github.com/apache/avro/actions/workflows/codeql-py-analysis.yml

[test c img]:          https://github.com/apache/avro/actions/workflows/test-lang-c.yml/badge.svg
[test c# img]:         https://github.com/apache/avro/actions/workflows/test-lang-csharp.yml/badge.svg
[test c++ img]:        https://github.com/apache/avro/actions/workflows/test-lang-c++.yml/badge.svg
[test java img]:       https://github.com/apache/avro/actions/workflows/test-lang-java.yml/badge.svg
[test javascript img]: https://github.com/apache/avro/actions/workflows/test-lang-js.yml/badge.svg
[test perl img]:       https://github.com/apache/avro/actions/workflows/test-lang-perl.yml/badge.svg
[test ruby img]:       https://github.com/apache/avro/actions/workflows/test-lang-ruby.yml/badge.svg
[test python img]:     https://github.com/apache/avro/actions/workflows/test-lang-py.yml/badge.svg
[test php img]:        https://github.com/apache/avro/actions/workflows/test-lang-php.yml/badge.svg

[rust continuous integration img]: https://github.com/apache/avro/actions/workflows/test-lang-rust-ci.yml/badge.svg
[rust clippy check img]:           https://github.com/apache/avro/actions/workflows/test-lang-rust-clippy.yml/badge.svg
[rust security audit img]:         https://github.com/apache/avro/actions/workflows/test-lang-rust-audit.yml/badge.svg

[codeql c# img]:         https://github.com/apache/avro/actions/workflows/codeql-csharp-analysis.yml/badge.svg
[codeql java img]:       https://github.com/apache/avro/actions/workflows/codeql-java-analysis.yml/badge.svg
[codeql javascript img]: https://github.com/apache/avro/actions/workflows/codeql-js-analysis.yml/badge.svg
[codeql python img]:     https://github.com/apache/avro/actions/workflows/codeql-py-analysis.yml/badge.svg
