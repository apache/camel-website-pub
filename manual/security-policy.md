# Security Policy Enforcement

Camel includes a built-in security policy enforcement mechanism that detects insecure configuration at startup time — before your application processes any messages. It catches common mistakes like plain-text passwords, disabled SSL verification, unsafe deserialization settings, and development features left enabled in production.

## Security categories

The framework checks four categories of security concerns:

  
| Category | Description | Example properties |
| --- | --- | --- |
| `secret` | Plain-text sensitive values that should use property placeholders, vault references, or environment variables | `password`, `apiKey`, `token`, `secretKey` |
| `insecure:ssl` | SSL/TLS settings that weaken transport security | `trustAllCertificates=true`, `hostnameVerification=false` |
| `insecure:serialization` | Enabling Java object deserialization, a known attack vector | `allowJavaSerializedObject=true`, `transferException=true` |
| `insecure:dev` | Development or debug features that should not be enabled in production | `devConsoleEnabled=true`, `uploadEnabled=true` |

## Policy levels

Each category can be set to one of three enforcement levels:

 
| Level | Behavior |
| --- | --- |
| `allow` | Silently permit the configuration — no warning, no error. |
| `warn` | Log a warning at startup but allow the application to start. This is the **default**. |
| `fail` | Prevent the application from starting and report all violations. |

## Configuration

Configure policies using the `camel.security.*` properties:

```properties
# Global policy applied to all categories unless overridden
camel.security.policy = warn

# Per-category overrides
camel.security.secretPolicy = fail
camel.security.insecureSslPolicy = fail
camel.security.insecureSerializationPolicy = fail
camel.security.insecureDevPolicy = allow

# Exempt specific properties from all checks
camel.security.allowedProperties = camel.component.http.trustAllCertificates
```

  
| Property | Description | Default |
| --- | --- | --- |
| `camel.security.policy` | Global security policy applied to all categories unless overridden. | `warn` |
| `camel.security.secretPolicy` | Overrides the global policy for plain-text secrets. |  |
| `camel.security.insecureSslPolicy` | Overrides the global policy for insecure SSL/TLS settings. |  |
| `camel.security.insecureSerializationPolicy` | Overrides the global policy for insecure deserialization settings. |  |
| `camel.security.insecureDevPolicy` | Overrides the global policy for development-only features. |  |
| `camel.security.allowedProperties` | Comma-separated list of property keys to exclude from all checks. |  |

When a per-category policy is not set, it falls back to the global `camel.security.policy` value.

## Profile defaults

The enforcement level changes automatically based on the active Camel profile:

 
| Profile | Behavior |
| --- | --- |
| No profile | Global policy defaults to `warn` — backward compatible. |
| `dev` | `insecureDevPolicy` defaults to `allow` so development features work without warnings. Other categories remain at `warn`. |
| `prod` | Global policy defaults to `fail` — the application refuses to start with any insecure configuration unless explicitly overridden. |

Set the profile with:

```properties
camel.main.profile = prod
```

## What is NOT flagged

The `secret` category only flags values that look like plain-text literals. The following patterns are considered safe and are not flagged:

-   `{{vault:…​}}` — vault references
    
-   `${env:…​}` or `${ENV:…​}` — environment variables
    
-   `${sys:…​}` or `${SYS:…​}` — system properties
    
-   `{{…​}}` — general property placeholders
    

## Examples

### Production: strict enforcement

```properties
camel.main.profile = prod
# Implicit: camel.security.policy = fail

# Allow one specific exception where self-signed certs are needed
camel.security.allowedProperties = camel.component.https.trustAllCertificates
```

With this configuration, the application will refuse to start if any plain-text secret, insecure SSL setting, unsafe deserialization option, or dev feature is detected — except the one explicitly allowed property.

### Development: relaxed

```properties
camel.main.profile = dev
# Implicit: camel.security.insecureDevPolicy = allow
# Other categories default to warn
```

### Custom: strict secrets, warn on everything else

```properties
camel.security.policy = warn
camel.security.secretPolicy = fail
```

The application will fail to start if any plain-text secret is detected, but will only log warnings for insecure SSL, serialization, or dev feature settings.