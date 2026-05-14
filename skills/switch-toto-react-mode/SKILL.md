---
name: switch-toto-react-mode
description: Switches a Next.js project interchangeably between using the local `toto-react` source code and the published package, enabling development and testing against the latest changes in `toto-react`.
---

# Switch Toto React Mode

## Overview

This skill allows you to switch a Next.js project between using the local `toto-react` source code and the published package. This is useful for development and testing against the latest changes in `toto-react`.

There are two modes:
- **Local Mode**: The Next.js project uses the local source code of `toto-react` for development and testing.
- **Package Mode**: The Next.js project uses the published version of `toto-react

## When to Use
  
**Local Mode**: 
- You need to make a change to the `toto-react` package and want to test it in a local Next.js project before publishing.
- You need to debug an issue that may be caused by the latest changes in `toto-react` and want to test against the local source.
- You want to contribute to `toto-react` and need to test your changes in a real Next.js app before submitting a pull request.

**Package Mode**:
- You want to test your Next.js project against the latest published version of `toto-react
- You are done (and have tested) your changes in local mode and want to verify that everything works with the published package.

**When NOT to use:** 
- You are making changes to the Next.js project itself that are unrelated to `toto-react`. In this case, you should keep using package mode to ensure you're testing against the stable version of `toto-react`.

## How to Switch Modes
Follow the instructions in the [Switching between npm and local toto-react guide](./switching-toto-react-source.md) to switch between local and package modes. 
The guide covers all the necessary changes to `package.json` and any Next.js configuration required to use the local source code of `toto-react`.

You **MUST FOLLOW ALL STEPS** in the guide to ensure the switch is successful.

After you have switched modes, you should 
- run the appropriate test commands to verify that everything is working as expected
- **ALWAYS** ask the User to test the app after making changes to `toto-react` in local mode, and after switching back to package mode to ensure that the published version works as expected.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "I do not need to follow the guide." | You must follow the guide to ensure the switch is successful. |
| "I can safely modify `toto-react` source without switching to local mode." | If you make changes to `toto-react` you must have used local mode to test them. |

## Red Flags

- Changing the code in `toto-react` without switching to local node and asking the user to test it in the local mode
- Publishing changes to `toto-react` without testing them in local mode first
- Assuming that changes to `toto-react` will work without testing them in local mode first
- Assuming that the published version of `toto-react` will work without testing it in package
- Not asking the user to test the app after making changes to `toto-react` in local mode

## Verification

After completing any switch make sure that: 

- [ ] All tests pass: `npm test`
- [ ] The app builds with `npm run build`
- [ ] No tests were skipped or disabled
