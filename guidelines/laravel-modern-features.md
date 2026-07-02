# Laravel Modern Features Guidelines

## Purpose

Capture the modern Laravel features the project should prefer when they are installed and supported.

## Required Standards

- Prefer `afterCommit()` and after-commit interfaces for transaction-sensitive dispatches.
- Prefer container attributes when they reduce boilerplate.
- Prefer form requests for HTTP boundary validation where a request class is the cleanest fit.
- Prefer version-specific framework APIs and the newest supported component conventions.
- Use generated commands instead of manual files when a command exists.
- Keep features reusable across web, API, Livewire, jobs, and commands.

## Allowed Patterns

- Form Requests.
- Container attributes.
- After-commit jobs, events, listeners, and notifications.
- Modern Livewire 4 loading and async features.
- Modern Filament v5 schema-based APIs.

## Forbidden Patterns

- Copying older major-version examples without checking the installed docs.
- Using newer features in a way that breaks the current project version.

## Testing Expectations

- Add tests for features that rely on framework-specific behavior.

## Review Checklist

- Are we using the current installed version?
- Is the feature actually supported here?
- Did we choose the cleanest modern API?

## Acceptable Examples

- `ProcessPodcast::dispatch($podcast)->afterCommit();`
- `php artisan make:request StoreOrderRequest`

## Unacceptable Examples

- Using old examples just because they are familiar.
