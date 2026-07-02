---
name: create-php-attribute
description: "Use when creating or reviewing a custom PHP 8 attribute for metadata, framework integration, architecture checks, tests, middleware, scanners, or support tooling in this Laravel application."
license: MIT
metadata:
  author: Ali Harb
---

# Create PHP Attribute

## When To Use

Use this skill when stable metadata should be declared with PHP 8 attributes and consumed by application code, tests, middleware, scanners, or tooling.

## Inputs Needed

- Attribute purpose, target, allowed arguments, consuming code, security impact, tests, and naming.

## Workflow

1. Confirm a custom attribute is better than a method, interface, config value, enum, policy, middleware, injection attribute, Eloquent attribute, queue attribute, Form Request attribute, resource attribute, or other Laravel built-in attribute.
2. Inspect existing attribute and support-class conventions.
3. Create the attribute under `app/Attributes` unless the project already has a different convention.
4. Use native PHP `#[Attribute(...)]` targets and repeatability flags.
5. Make the attribute class `final readonly` when possible.
6. Type every constructor parameter.
7. Keep the attribute as metadata only.
8. Create or update the consumer that reads the attribute via reflection, routing, middleware, tests, or support tooling.
9. Add tests for the consumer behavior.
10. Run Pint and focused tests.

## Files That May Be Created

- `app/Attributes/*.php`
- Consumer classes in middleware, support, testing, or scanner namespaces.
- Tests for the attribute consumer.

## Files That May Be Modified

- Classes or methods that receive the attribute.
- Middleware, Actions, Services, Providers, tests, or architecture tests that consume the attribute.

## Architecture Rules

- Attributes describe metadata; they do not perform business workflows.
- Do not use custom attributes to bypass Actions, Policies, DTOs, Events, Jobs, or Services.
- Prefer Laravel built-in attributes before custom attributes.
- Every custom attribute must have a real consumer when introduced.
- Custom attributes are metadata and must not be used to bypass dependency injection.

## Testing Requirements

- Test the consumer behavior.
- Test invalid or missing metadata where relevant.
- Add architecture tests when the attribute marks security, sensitivity, external integrations, or layer boundaries.

## Security Requirements

- Attributes must not store secrets.
- Attributes must not become the only authorization mechanism unless the consumer explicitly enforces policy or gate checks.
- Treat reflected metadata as code-level metadata, not trusted user input.

## Review Checklist

- Is an attribute the simplest clear tool?
- Is there a consumer?
- Are targets and repeatability correct?
- Is the class immutable and typed?
- Are tests focused on behavior?

## Common Mistakes

- Creating marker attributes that nothing reads.
- Hiding side effects behind attributes.
- Passing dynamic runtime data into attributes.
- Replacing simple Laravel middleware, policies, or container attributes with custom code.
- Replacing constructor or method injection with a custom attribute.
