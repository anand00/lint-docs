# Introduction

[SwiftLint](https://github.com/realm/SwiftLint/blob/master/README.md) is a tool by Realm to enforce Swift style and conventions. SwiftLint hooks into Apple’s own SourceKit framework to parse your Swift code, which means it supports the full range of Swift syntax and remains up to date as Swift continues to evolve. It is based on guidelines from the Swift style guide.
<br /><br />
# Prerequisite

* [Swift 5.6](https://www.swift.org/blog/swift-5.6-released/)
  <br /><br />An existing application or new application developed using Swift.


* [XCode 13.3](https://developer.apple.com/documentation/Xcode-Release-Notes/xcode-13_3-release-notes)
* [CocoaPod](https://cocoapods.org)

# Installation

### Using [Homebrew](http://brew.sh/):

```
brew install swiftlint
```

### Using [CocoaPods](https://cocoapods.org):

Simply add the following line to your Podfile:

```ruby
pod 'SwiftLint'
```

This will download the SwiftLint binaries and dependencies in `Pods/` during next
`pod install` execution and will allow to invoke it via `${PODS_ROOT}/SwiftLint/swiftlint`
in Script Build Phases.

> This is the recommended way to install a specific version of SwiftLint since it supports
installing a pinned version rather than simply the latest (which is the case with Homebrew).

# Configuration
Create a file `.swiftlint.yml` file in the root directory of your project.
<br />Then add the below configuration in this file.

```yaml
disabled_rules: # rule identifiers to exclude from running
  - vertical_whitespace
  - line_length
  - type_body_length
  - colon
  - comma
opt_in_rules: # some rules are only opt-in
  - control_statement
  - empty_count
  - trailing_newline
  - convenience_type
  - empty_string
  - file_name
  - toggle_bool
  - force_unwrapping
  - unused_private_declaration
  - missing_docs
  - unused_declaration
  - unused_import
  - indentation_width
  - discouraged_optional_boolean
  - fallthrough

included: # paths to include during linting. `--path` is ignored if present.
  - Project
  - ProjectTests
  - ProjectUITests
  
excluded: # paths to ignore during linting. Takes precedence over `included`.
  - Pods
  - Carthage
  - Project/R.generated.swift

# configurable rules can be customized from this configuration file
# binary rules can set their severity level
force_cast: warning # implicitly. Give warning only for force casting

force_try:
  severity: warning # explicitly. Give warning only for force try
  
line_length:
  warning: 140
  error: 160

type_body_length:
  - 300 # warning
  - 400 # error

# or they can set both explicitly
file_length:
  warning: 600
  error: 800
  
indentation: 2

large_tuple: # warn user when using 3 values in tuple, give error if there are 4
   - 5
   - 6
   
 missing_docs:
  warning: 
  - private
  - open
  - fileprivate
  - public
  - internal
  
# naming rules can set warnings/errors for min_length and max_length
# additionally they can set excluded names
type_name:
  min_length: 3 # only warning
  max_length: # warning and error
    warning: 30
    error: 35
  excluded: iPhone # excluded via string
reporter: "xcode" # reporter type (xcode, json, csv, checkstyle, codeclimate, junit, html, emoji, sonarqube, markdown, github-actions-logging)
```

# Usage
If you've installed SwiftLint via CocoaPods, then 
1. Select Target 
2. Go to Build Phase 
3. Click on +
4. Add New Run Script Phase 
5. Copy & paste below script in Run Script

```bash
"${PODS_ROOT}/SwiftLint/swiftlint"
```
<img width="1200" alt="build-phaseimg" src="https://raw.githubusercontent.com/anand00/lint-docs/main/Xcode-runScript.png">

* Move the `Run Script` above the `Compile Sources` step by drag and drop, to detect errors quickly before compiling.
* Build the Project now to see warnings and errors 
