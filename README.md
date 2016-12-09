## Gradle Thrift Plugin

[![Build Status](https://travis-ci.org/jruyi/thrift-gradle-plugin.svg?branch=master)](https://travis-ci.org/jruyi/thrift-gradle-plugin)

Gradle Thrift Plugin uses thrift compiler to compile Thrift IDL files.

### Usage

To use this plugin, add the following to your build script.

```groovy
buildscript {
	repositories {
		maven {
			url "https://plugins.gradle.org/m2/"
		}
	}
	dependencies {
		classpath "gradle.plugin.org.jruyi.gradle:thrift-gradle-plugin:0.3.2"
	}
}

apply plugin: "org.jruyi.thrift"
```

Or for Gradle 2.1+:

```groovy
plugins {
	id "org.jruyi.thrift" version "0.3.2"
}
```

### Example

See the `examples/test2` directory for a very simple example.

### Implicitly Applied Plugins

None.

### Tasks

The Thrift plugin adds compileThrift task which compiles Thrift IDL files using thrift compiler.

##### Table-1 Task Properties of compileThrift

Task Property     | Type                | Default Value
------------------|---------------------|---------------------------------------------------
thriftExecutable  | String              | thrift
sourceDir         | File                | src/main/thrift
outputDir         | File                | _buildDir_/generated-sources/thrift
thriftFiles       | Set<File>           | []
includeDirs       | Set<File>           | []
generators        | Map<String, String> | ['java':''] if JavaPlugin is applied, otherwise []
nowarn            | boolean             | false
strict            | boolean             | false
verbose           | boolean             | false
recurse           | boolean             | false
debug             | boolean             | false
allowNegKeys      | boolean             | false
allow64bitsConsts | boolean             | false
createGenFolder   | boolean             | true

If createGenFolder is set to false, no gen-* folder will be created.

If thriftFiles is empty then all .thrift files under sourceDir will be compiled.
If thriftFiles is not empty then only files in thriftFiles will be compiled. Relative paths are resolved against sourceDir.

##### Example

```groovy
compileThrift {
	recurse true

	generator 'html'
	generator 'java', 'private-members'
}
```

### Default Behaviors

When JavaPlugin is applied, generator 'java' will be created and the generated java code will be added to Java source automatically.

## Using Thrift on Travis

Ubuntu 14.04 (Trusty) provides [Thrift 0.9.0](http://packages.ubuntu.com/trusty/devel/thrift-compiler). If this version fits your requirements, you can use the following `.travis.yml` configuration file:

```
language: java
dist: trusty
sudo: required
before_install:
  - sudo apt-get install thrift-compiler
script:
  - ./gradlew check
  - ./gradlew assemble
```

## License

Gradle Thrift Plugin is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).
