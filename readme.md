# WpFresher Sniffs

A comprehensive PHP_CodeSniffer ruleset that extends WordPress Coding Standards with WpFresher-specific conventions for modern PHP development.

## Features

- 🎯 **WordPress-First**: Built on top of WordPress Coding Standards (WPCS) 3.1.0
- 🐘 **PHP Compatibility**: Supports PHP 7.4 - 8.5 with PHPCompatibility checks
- ⚡ **Performance**: Configured for parallel processing with 8 threads
- 🎨 **Sensible Defaults**: Pre-configured with practical exclusions for real-world development
- 📝 **Tab Indentation**: Enforces consistent tab-based indentation
- 🔧 **Customizable**: Easy to extend and override rules per project

## What's Included

### Base Standards
- **WordPress**: Complete WordPress coding standards
- **WordPress-Extra**: Additional WordPress-specific rules
- **WordPress-Docs**: Documentation standards
- **PHPCompatibilityWP**: WordPress-specific PHP compatibility checks

### WpFresher Customizations
- Tab-based indentation (1 tab = 1 indent level)
- Space inside parentheses for better readability
- Relaxed file naming requirements
- Allowance for shorthand array syntax `[]`
- Sensible exclusions for database queries and nonce verification
- Comment and doc comment tokens ignored in indentation checks

## Installation

Install via Composer:

```bash
composer require wpfresher/wpfresher-sniffs
```

The package will automatically:
- Install PHP_CodeSniffer and required dependencies
- Register the `WpFresher-Default` standard
- Set it as the default standard for your project

## Usage

### Command Line

#### Quick Check
```bash
vendor/bin/phpcs .
```

#### Using Composer Script
```bash
composer run phpcs
```

#### Custom Configuration
```bash
vendor/bin/phpcs --standard=WpFresher-Default path/to/files
```

### IDE Integration

For better IDE integration, create a `.phpcs.xml.dist` file in your project root:

```xml
<?xml version="1.0"?>
<ruleset name="Project Coding Standards">
    <description>Project-specific coding standards based on WpFresher defaults.</description>

    <!-- Scan these directories -->
    <file>src/</file>
    <file>inc/</file>
    
    <!-- Exclude these paths -->
    <exclude-pattern>vendor/</exclude-pattern>
    <exclude-pattern>node_modules/</exclude-pattern>
    <exclude-pattern>*.min.js</exclude-pattern>

    <!-- Configuration -->
    <config name="minimum_supported_wp_version" value="6.2" />
    <config name="testVersion" value="7.4-8.5" />

    <!-- Use WpFresher standards -->
    <rule ref="WpFresher-Default" />

    <!-- Project-specific customizations -->
    <rule ref="WordPress.WP.I18n">
        <properties>
            <property name="text_domain" type="array">
                <element value="your-text-domain"/>
            </property>
        </properties>
    </rule>
</ruleset>
```

### Continuous Integration

Add to your CI workflow:

```yaml
# GitHub Actions example
- name: PHP CodeSniffer
  run: composer run phpcs
```

## Configuration Details

### PHP Version Support
- **Minimum**: PHP 7.4
- **Maximum**: PHP 8.5
- **Compatibility**: Uses PHPCompatibilityWP for WordPress-specific compatibility checks

### Key Rules Applied
- WordPress Coding Standards (with sensible exclusions)
- Tab indentation (1 tab per indent level)
- Space inside parentheses for readability
- Superfluous whitespace detection
- PHP compatibility checking for WordPress

### Excluded Rules
The following rules are excluded for practical development:
- File naming conventions (WordPress.Files.FileName)
- Nonce verification requirements
- Direct database query restrictions
- Global variable override prohibitions
- Some documentation capitalization requirements

## Customization

### Project-Level Overrides

Create a `phpcs.xml.dist` file to override or add rules:

```xml
<rule ref="WpFresher-Default">
    <!-- Enable a rule that's disabled by default -->
    <exclude name="WordPress.Files.FileName" />
</rule>

<!-- Add custom exclusions -->
<rule ref="WordPress.Security.NonceVerification.Missing">
    <exclude-pattern>admin/ajax-handlers/*</exclude-pattern>
</rule>
```

### Inline Annotations

Disable rules for specific code blocks:

```php
// phpcs:disable WordPress.Security.NonceVerification.Missing
if ( isset( $_POST['data'] ) ) {
    // Process data without nonce check
}
// phpcs:enable WordPress.Security.NonceVerification.Missing
```

## Requirements

- PHP 7.4 or higher
- Composer
- PHP_CodeSniffer 3.9.0 or higher

## Dependencies

- `dealerdirect/phpcodesniffer-composer-installer`: ^1.0
- `phpcompatibility/phpcompatibility-wp`: ^2.1  
- `wp-coding-standards/wpcs`: ^3.1.0

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with `composer run phpcs`
5. Submit a pull request

## License

GPL-3.0-only

## Author

**Kawsar Ahmed**  
Email: kawsar@wpfresher.com
Organization: WpFresher

---

*Part of the WpFresher development toolkit for WordPress and PHP projects.*
