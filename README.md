# Renovate fails to update Angular due to incompatible zone.js version #32606

## Current behavior

At the moment, Renovate fails to submit a working PR that updates Angular. I'm fairly confident it fails for everybody at this time.

You'll see a PR that contains updates to
@angular/* from e.g. version 18.2.0 to 18.2.12
zone.js from ~0.14.10 to ~0.15.0

The problem is that NPM reports "ERESOLVE unable to resolve dependency tree" because zone.js is a peer dependency of Angular, and needs to be LOWER than version 0.15:

```
npm error code ERESOLVE
npm error ERESOLVE unable to resolve dependency tree
npm error
npm error While resolving: my-app@0.0.0
npm error Found: zone.js@0.15.0
npm error node_modules/zone.js
npm error   zone.js@"~0.15.0" from the root project
npm error
npm error Could not resolve dependency:
npm error peer zone.js@"~0.14.10" from @angular/core@18.2.12
npm error node_modules/@angular/core
npm error   @angular/core@"^18.2.0" from the root project
npm error   peer @angular/core@"18.2.12" from @angular/animations@18.2.12
npm error   node_modules/@angular/animations
npm error     @angular/animations@"^18.2.0" from the root project
npm error
npm error Fix the upstream dependency conflict, or retry
npm error this command with --force or --legacy-peer-deps
npm error to accept an incorrect (and potentially broken) dependency resolution.
```

## Expected behavior

zone.js is left at a compatible version, preferably updated to the latest compatible one (i.e. a 0.14.x)

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/32606
