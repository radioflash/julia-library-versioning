# Why *every* public Julia library should be ≥v1.0.0

Julia uses [Semantic Versioning](https://semver.org/) conventions for its packages.
Semantic versioning requires any *public* interface to be [≥v1.0.0](https://semver.org/#spec-item-5).
This is *necessary* for SemVer to work properly, because any version below v1.0.0 **can not cleanly express** (backwards-compatible) **feature growth**.

This is because according to SemVer, every minor release (e.g. v0.1.5 => v0.2.0) is to be considered *breaking* (read: not backwards compatible)--but minor releases are what you would normally make when adding (compatible) features!

## Consequences

### <v1.0.0 libraries have no way to indicate feature growth

**Any** compatible change MUST be made as a "PATCH" release (which usually indicate pure bugfixes), regardless of content.
This is already confusing by itself, but made even worse when the library maintainer does not realise and pushes a (compatible) minor release: Because for <v1.0.0 libraries those are *always* assumed to be breaking, and thus require EVERY package that uses the library to update as well!

### Transitioning to v1.0.0 is always gonna be a breaking change

When the maintainer of a <v1.0.0 library decides that the lib is "good enough", and wants to assign v1.0.0, than that is *necessarily* going to be a breaking change.

This is really harmful because at that point the library has presumably numerous users, no critical bugs, everything is fine, but in order to make that version v1.0.0 every single user of the library will have to update their compatibility info-- potentially without any direct feature-gain/justification whatsoever.

## Objections

### I wanna stay <v1.0.0 because my library is not yet ready/finished/tested/good enough

This is perfectly fine--thats what a README is for!

If someone uses your library, the onus is on the user, **not** on the library author to determine suitability in any way.

And from personal experience it is futile to indicate "library readiness" with a v1.0.0 version number anyway, because this is  simply too subjective/context dependent.

If you got far enough to push your library into the Julia registry, then you **deserve** that v1.0!

### I want to stay <v1.0.0 because I sometimes break compatibility by mistake

This is fine--SemVer defines [how to deal with this](https://semver.org/#what-do-i-do-if-i-accidentally-release-a-backwards-incompatible-change-as-a-minor-version).

### I want to stay <v1.0.0  because transitioning to v1.0.0 would disrupt my users

Yes, but transitioning to v1.0.0 is *inevitably* going to disrupt. Better to make that break immediately with your next release (when there is *reason* for a release already), then at some future point where you presumably have *even more affected users* and there is literally no other justification for releasing than the fact that you now consider your library "proven enough".

You will gain the ability to clearly mark feature increments, and you *might* never have to make a breaking change ever again (as opposed to having that v1.0.0 change loom in the future)!

