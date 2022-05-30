# Introduction

[KTLint](https://ktlint.github.io) is a static code analysis tool that is used to analyze the Kotlin code. 
The whole ktlint process can be divided into two parts:
1. **linting tool**: The lining tool is based on the [kotlin standard style guide](https://developer.android.com/kotlin/style-guide), and it will validate and make sure that your code adheres to that style guide.
2. **formatter**: If ktlint detects any issue in your code you can then run the formatter and have ktlint try to automatically fix those issues.
It formats the code if some formatting is needed.

>ktlint is an anti-bikeshedding Kotlin linter with built-in formatter.

# Prerequisite

* [Android Studio Bumblebee 2021.1.1](https://android-developers.googleblog.com/2022/01/android-studio-bumblebee-202111-stable.html)
* [Kotlin 1.6.20](https://kotlinlang.org/docs/whatsnew1620.html)
<br /><br />An existing application or new application developed using Kotlin.

# Installation
### Ktlint Gradle
**Step 1.**
Add the dependency in the project gradle.
```kotlin
// root-level build.gradle
plugins {
	id "org.jlleitschuh.gradle.ktlint" version "10.3.0"
}

// root-level build.gradle
buildscript {
repositories {
	maven {
	url "https://plugins.gradle.org/m2/"
	}
}
dependencies {
	classpath "org.jlleitschuh.gradle:ktlint-gradle:10.3.0"
}
}
```
**Step 2.**
Then under all projects apply the above plugin
```kotlin
// root-level build.gradle
allprojects {
	...
	apply plugin: "org.jlleitschuh.gradle.ktlint"
}
```
# Configuration
There is no configuration file in Ktlint.That means `ktlint` tries to capture **official code style** from 
[kotlinlang.org](https://kotlinlang.org/docs/reference/coding-conventions.html) and 
[Android Kotlin Style Guide](https://android.github.io/kotlin-guides/style.html).
However we can set our own custom rules using extension.
> For now default rules are enough for us. we can create our custom rules if needed.

# Usage
To check your code’s formatting, run the following command from the command line:
```kotlin
./gradlew ktlintCheck
```
This will run through your project and report back any errors which are found using the default ktlint-gradle plugin configuration.
<br/>To automatically fix any errors which are reported by `ktlintCheck` , you can run the following command from the command line: 
```kotlin
./gradlew ktlintFormat
```
This will attempt to auto-fix any errors and will report back any issues that could not automatically be fixed.# Introduction
