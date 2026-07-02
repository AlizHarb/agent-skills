---
name: create-dto
description: "Use when creating or changing DTOs, data objects, value objects, or input/output contracts for Laravel features."
license: MIT
metadata:
  author: Ali Harb
---

# Create DTO Or Data Object

## When To Use

Use this skill when data crosses a boundary or must be reused by web, API, Livewire, jobs, commands, or integrations.

## Inputs Needed

- Fields, types, validation rules, source boundaries, output consumers, defaults, and serialization needs.

## Workflow

1. Inspect existing data object conventions.
2. Use Spatie Laravel Data by default now that it is installed. If a different data style already exists in a nearby module, follow the local convention.
3. Prefer `final readonly class` with constructor property promotion for immutable DTOs.
4. Use Spatie Data attributes where they fit the property:
   - `#[MapInputName]`
   - `#[MapOutputName]`
   - `#[WithCast]`
   - `#[WithTransformer]`
   - `#[Computed]`
   - `#[ValidationAttribute]` or package validation attributes
   - `#[DataCollectionOf]`
   - `#[Lazy]`
   - `#[Hidden]`
   - `#[LoadRelation]` and `#[LoadMissing]`
   - `#[Inject]` or property injection attributes when the package or project convention uses them
5. Use enums for closed sets and typed class constants for reusable scalar contracts.
6. Keep DTOs client-agnostic.
7. Add named constructors such as `fromArray`, `fromRequest`, or `fromModel` only when useful.
8. Place validation rules near DTOs when the project convention supports it.
9. Avoid persistence, authorization, or workflow logic.
10. Add tests for construction, validation rules, serialization, and edge cases.

## Files That May Be Created

- `app/Data/*.php`, `app/DTOs/*.php`, or the existing local equivalent.
- DTO tests.

## Files That May Be Modified

- Form Requests, Actions, Resources, Livewire components, controllers, jobs, and tests.

## Architecture Rules

- DTOs represent input or output contracts.
- DTOs support API and UI reuse.
- DTOs must not depend on Livewire, Blade, controllers, or responses.
- DTOs should use modern PHP typing instead of unstructured arrays whenever practical.
- Use Spatie Data collections/resources when a feature needs nested, transformed, or reusable data shapes.
- Prefer Spatie Data validation attributes before ad hoc array validation inside reusable code.

## Testing Requirements

- Test required fields, type conversion, defaults, invalid data, and serialization if exposed.

## Security Requirements

- Do not trust DTO construction as authorization.
- Avoid including sensitive fields in output DTOs unless explicitly intended.

## Review Checklist

- Is the DTO stable and client-agnostic?
- Are fields typed?
- Are validation rules close enough to stay synchronized?

## Common Mistakes

- Installing Spatie Laravel Data without approval.
- Turning DTOs into models or services.
- Passing raw request arrays deep into Actions instead of typed data.
