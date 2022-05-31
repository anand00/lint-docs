# Introduction

[PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) is a set of two PHP scripts; the main `phpcs` script that tokenizes PHP, JavaScript and CSS files to detect violations of a defined coding standard, and a second `phpcbf` script to automatically correct coding standard violations. PHP_CodeSniffer is an essential development tool that ensures your code remains clean and consistent.

# Prerequisites

- [PHP 8.1](https://www.php.net/releases/8.1/en.php)
- [Composer](https://getcomposer.org/)
- [Laravel 8](https://laravel.com/docs/8.x/releases)

Laravel 8 is used for the development of web applications in PHP.

> Lumen a micro-framework can also be used depending on project need. This document is only verified with Laravel 8.

# Installation

Install the following packages:

- [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [slevomat/coding-standard](https://github.com/slevomat/coding-standard)

**`squizlabs/PHP_CodeSniffe`**

```sh
composer require squizlabs/php_codesniffer --dev
```

**`slevomat/coding-standard`**

```sh
composer require slevomat/coding-standard --dev
```

You will come across the following query when installing `slevomat/coding-standard`,

```sh
Do you trust "dealerdirect/phpcodesniffer-composer-installer" to execute code and wish to enable it now? (writes "allow-plugins" to composer.json) [y,n,d,?]
```

Press `y`

# Configuration

Create `.phpcs.xml` file in the root directory of your project.

Then add the below configuration in this file.

```xml
<?xml version="1.0"?>
<ruleset name="PHP_CodeSniffer">
    <file>app</file>
    <file>config</file>
    <file>database</file>
    <file>resources</file>
    <file>routes</file>
    <file>tests</file>

    <!-- exclude our migrations directory from the violation check-->
    <exclude-pattern>*/migrations/*</exclude-pattern>

	<arg name="tab-width" value="4"/>
	<rule ref="PSR12">
		<exclude name="Generic.WhiteSpace.DisallowTabIndent"/>
	</rule>
	<rule ref="Generic.WhiteSpace.DisallowSpaceIndent"/>
	<rule ref="Generic.WhiteSpace.ScopeIndent">
		<properties>
			<property name="indent" value="4"/>
			<property name="tabIndent" value="true"/>
		</properties>
	</rule>

	<!-- See https://github.com/slevomat/coding-standard#sniffs-included-in-this-standard -->
	<config name="installed_paths" value="../../slevomat/coding-standard"/>
	<rule ref="SlevomatCodingStandard.TypeHints.UselessConstantTypeHint" />
	<rule ref="SlevomatCodingStandard.Arrays.DisallowImplicitArrayCreation" />
	<rule ref="SlevomatCodingStandard.ControlStructures.RequireNullCoalesceOperator" />
	<rule ref="SlevomatCodingStandard.PHP.UselessSemicolon" />
	<rule ref="SlevomatCodingStandard.Variables.UnusedVariable">
		<properties>
			<property name="ignoreUnusedValuesWhenOnlyKeysAreUsedInForeach" value="true" />
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.Variables.UselessVariable" />
	<rule ref="SlevomatCodingStandard.Exceptions.DeadCatch" />
	<rule ref="SlevomatCodingStandard.Classes.MethodSpacing" >
		<properties>
			<property name="minLinesCount" value="1"/>
			<property name="maxLinesCount" value="1"/>
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.Classes.PropertySpacing">
		<properties>
			<property name="minLinesCountBeforeWithComment" value="0"/>
			<property name="maxLinesCountBeforeWithComment" value="0"/>
			<property name="minLinesCountBeforeWithoutComment" value="0"/>
			<property name="maxLinesCountBeforeWithoutComment" value="0"/>
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.ControlStructures.BlockControlStructureSpacing">
		<properties>
			<property name="linesCountBeforeFirst" value="1"/>
			<property name="linesCountAfterLast" value="1"/>
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.Namespaces.UnusedUses">
		<properties>
			<property name="searchAnnotations" value="true"/>
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.Namespaces.AlphabeticallySortedUses" />
	<rule ref="SlevomatCodingStandard.Whitespaces.DuplicateSpaces" />
	<rule ref="SlevomatCodingStandard.TypeHints.ReturnTypeHintSpacing">
		<properties>
			<property name="spacesCountBeforeColon" value="0"/>
		</properties>
	</rule>
	<rule ref="SlevomatCodingStandard.Commenting.DisallowCommentAfterCode" />
	<rule ref="SlevomatCodingStandard.Commenting.EmptyComment" />
	<rule ref="SlevomatCodingStandard.Commenting.RequireOneLineDocComment" />
	<rule ref="SlevomatCodingStandard.ControlStructures.UselessIfConditionWithReturn" />
	<rule ref="SlevomatCodingStandard.ControlStructures.UselessTernaryOperator" />
</ruleset>
```

# Usage

Add couple of script commands to run `phpcs` and `phpcbf` in `composer.json` file.

```json
"scripts": {
    // ..<existing scripts>
    "lint": "phpcs",
    "lint:fix": "phpcbf",
  },
```

**`composer run lint`**

This command will tokenize PHP, JavaScript and CSS files to detect violations of a defined coding standard.

**`composer run lint:fix`**

This command will automatically correct coding standard violations.
