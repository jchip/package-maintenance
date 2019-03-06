# What?

This is guidelines for unmaintained packages.

# Why?

To ensure that packages in the Node.js ecosystem are up to date or gracefully deprecated.

# How?

These guidelines exist to help with the course of actions for package consumers and owners to take in the event that a package becomes unmaintained.

- Provide a baseline and common practices for identifying unmaintained packages
- Give package consumers some help with unmaintained packages.
- Give package owners some help with handling and deprecating packages.

## What consititutes an unmaintained package?

It's not always obvious if a package is unmaintained. Many packages are small and considered completed as published. Long period of no activity does not mean unmaintain.

Generally the question "is this package unmaintained?" arises when users found it to have issues that are not getting reponse or being addressed.

Some criterias to determine if it's unmaintained:

- The author is no longer responding to questions, issues, PRs, or making any updates, and specifically repeat "are you there inquries" for critical issues.
- The author may have explicitly indicated that they will stop all activities on the package.
- A different package that's more active and the author acknowledged as the replacement.
- Critical issues exist for the package and not being addressed
  - Known vulnerabilities identified by `npm audit` or other parties
  - Package is known to fail for LTS Node.js

## For Users

If you are using a package that meets your requirements but you found issues or need enhancements, then these are some actions you can follow:

- Note the deprecation messages during `npm install` and follow the instruction if the message offered any.
- Check the package's npm page at `https://www.npmjs.com/package/<package-name>`. ie: <https://www.npmjs.com/package/express>
  - Check the "last publish" date and versions history to get a sense of its latest activies.
  - Open the "repository" link if it has one to view development activities.

### Identifying unmaintained package?

When you've opened the package's repo, to further check development activities:

- Check README or issues to see if the author indicated they are no longer interested in maintaining the package

- Search through existing issues and PRs to see if anyone else has submitted inquries similar to what you are seeking.

- Check for or file issue in the repo to encourage author to deprecate a version that:

  - Has known critical bugs and should be avoided
  - Known to fail for LTS Node.js
  - Has known critical vulnerabilities

- Check if high priority issues in the package's repo are getting responses from owner

  - if npm audit identified vulnerabilities that are critical
  - if package fails to install/build for an LTS release of node.js

- Check last activity on github issues and PRs. If there're no responses within some reasonable time to high priority issues or PRs, then consider the package as an unmaintained candidate.

### Taking Further Actions

Once you've identified a package may be unmaintained, please open an issue for the Node.js package-maintenance working group to check and identify path forward.

## For Package Owners

If you own a package and you want to stop maintaining it, then please help your users by making it known. Some simple actions you can take:

- Use the `npm deprecate` command to mark package as unmaintained.
- Add a note to your repo's `README.md` file.
- Reach out to the Node.js package-maintenance working group to offer us ownership so we can hand it off to a new owner.

### `npm deprecate` command

- npm has the "deprecate" command, you can utilize this.
- deprecate your latest version with a message that includes `"abandoned and unmaintained"`.
  - It allows updating the message so you can change it later - verified as of 02/05/2019
  - It can be undone by setting an empty message.
    - ie: `npm deprecate package@1.0.0 ""`
- Even if you are still maintaining the package, please consider marking an old version as deprecated.

### Mark abandoned/unmaintained

- Use a special `npm deprecate` message such as `"abandoned and unmaintained"` to mark a package as abandoned.

  - no need to publish a new package to mark it abandoned.
  - but only owners can `npm deprecate` a package.
  - please consider giving the package-maintenance working group ownership to the package on npm.

### Identify replacement

- If a package is fully unmaintained, then a replacement should be identified and added to the deprecation message.
- If no replacement exists, then please identify the safe versions to use in the deprecation message.

## Further Ideas and Tools

There are some ongoing discussion related to npm to make managing unmaintained packages easier.

- Package override RFC https://github.com/aeschright/rfcs/blob/ca127d7c5fb7ecde534172d771351c0b8f819e79/accepted/0009-package-overrides.md

Other ideas for tools that could help:

- A cli to allow `npm deprecate` a range of versions on a package.
- or request new support of `npm deprecate` to allow deprecating versions published before a given time
- allow consumer to specify a specific version to use for a package through an `override` field in their package.json
- if author simply can't be reached and package is very outdated, then need to contact npm to get access to deprecate package.