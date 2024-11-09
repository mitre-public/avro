
> [!IMPORTANT]  
> The Rust SDK is moving to https://github.com/apache/avro-rs. Please use it for [new issues](https://github.com/apache/avro-rs/issues/new)
 and [pull requests](https://github.com/apache/avro-rs/pulls)!
 
 Apache Avro™<img align="right" height="160" src="doc/assets/images/logo.svg" alt="Avro Logo"/>
============

### Current CI status (Github servers)
[![test c][test c img]][test c]
[![test c#][test c# img]][test c#]
[![test c++][test c++ img]][test c++]
[![test java][test java img]][test java]
[![test javascript][test javascript img]][test javascript]
[![test perl][test perl img]][test perl]
[![test ruby][test ruby img]][test ruby]
[![test python][test python img]][test python]
[![test php][test php img]][test php]

### Current CI status (ARM based servers)
[![test c ARM][test c ARM img]][test c ARM]
[![test c# ARM][test c# ARM img]][test c# ARM]
[![test c++ ARM][test c++ ARM img]][test c++ ARM]
[![test java ARM][test java ARM img]][test java ARM]
[![test javascript ARM][test javascript ARM img]][test javascript ARM]
[![test perl ARM][test perl ARM img]][test perl ARM]
[![test ruby ARM][test ruby ARM img]][test ruby ARM]
[![test python ARM][test python ARM img]][test python ARM]
[![test php ARM][test php ARM img]][test php ARM]

### Current CodeQL status
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

[test c ARM]:          https://github.com/apache/avro/actions/workflows/test-lang-c-ARM.yml
[test c# ARM]:         https://github.com/apache/avro/actions/workflows/test-lang-csharp-ARM.yml
[test c++ ARM]:        https://github.com/apache/avro/actions/workflows/test-lang-c++-ARM.yml
[test java ARM]:       https://github.com/apache/avro/actions/workflows/test-lang-java-ARM.yml
[test javascript ARM]: https://github.com/apache/avro/actions/workflows/test-lang-js-ARM.yml
[test perl ARM]:       https://github.com/apache/avro/actions/workflows/test-lang-perl-ARM.yml
[test ruby ARM]:       https://github.com/apache/avro/actions/workflows/test-lang-ruby-ARM.yml
[test python ARM]:     https://github.com/apache/avro/actions/workflows/test-lang-py-ARM.yml
[test php ARM]:        https://github.com/apache/avro/actions/workflows/test-lang-php-ARM.yml

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

[test c ARM img]:          https://github.com/apache/avro/actions/workflows/test-lang-c-ARM.yml/badge.svg
[test c# ARM img]:         https://github.com/apache/avro/actions/workflows/test-lang-csharp-ARM.yml/badge.svg
[test c++ ARM img]:        https://github.com/apache/avro/actions/workflows/test-lang-c++-ARM.yml/badge.svg
[test java ARM img]:       https://github.com/apache/avro/actions/workflows/test-lang-java-ARM.yml/badge.svg
[test javascript ARM img]: https://github.com/apache/avro/actions/workflows/test-lang-js-ARM.yml/badge.svg
[test perl ARM img]:       https://github.com/apache/avro/actions/workflows/test-lang-perl-ARM.yml/badge.svg
[test ruby ARM img]:       https://github.com/apache/avro/actions/workflows/test-lang-ruby-ARM.yml/badge.svg
[test python ARM img]:     https://github.com/apache/avro/actions/workflows/test-lang-py-ARM.yml/badge.svg
[test php ARM img]:        https://github.com/apache/avro/actions/workflows/test-lang-php-ARM.yml/badge.svg

[codeql c# img]:         https://github.com/apache/avro/actions/workflows/codeql-csharp-analysis.yml/badge.svg
[codeql java img]:       https://github.com/apache/avro/actions/workflows/codeql-java-analysis.yml/badge.svg
[codeql javascript img]: https://github.com/apache/avro/actions/workflows/codeql-js-analysis.yml/badge.svg
[codeql python img]:     https://github.com/apache/avro/actions/workflows/codeql-py-analysis.yml/badge.svg

You can use devcontainers to develop Avro:

* [![Open in Visual Studio Code](https://img.shields.io/static/v1?label=&message=Open%20in%20Visual%20Studio%20Code&color=blue&logo=visualstudiocode&style=flat)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/apache/avro)
* [![Open in Github Codespaces](https://img.shields.io/static/v1?label=&message=Open%20in%20Github%20Codespaces&color=2f362d&logo=github)](https://codespaces.new/apache/avro?quickstart=1&hide_repo_select=true)


### Trademark & logos
Apache®, Apache Avro and the Apache Avro airplane logo are trademarks of The Apache Software Foundation.

The Apache Avro airplane logo on this page has been designed by [Emma Kellam](https://github.com/emmak3l) for use by this project.
