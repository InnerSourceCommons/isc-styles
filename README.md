# Vale Styles for the InnerSource Commons

This [vale](https://vale.sh) package contains the styles for the InnerSource Commons.

We use vale for two purposes:

1) to spell check our content (we use American English)
2) to keep a consistent style across all of our written resources (e.g. Patterns, Learning Path content, etc)

For now (May 2023) we only have a single custom rule ([InnerSource.yml](ISC/styles/ISC/InnerSource.yml)) that checks that "InnerSource" is spelled correctly. We expect to add further rules in the future.

## Using these vale styles in your project

1. install [vale](https://vale.sh/docs/vale-cli/installation/)
2. add a `.vale.ini` to the root of your project with this content:

```ini
StylesPath = .github/vale
MinAlertLevel = suggestion

Packages = https://github.com/InnerSourceCommons/isc-styles/releases/latest/download/ISC.zip

[*]
BasedOnStyles = ISC

; If you don't want to check for the correct spelling of "InnerSource", comment this in
; ISC.InnerSource = NO
```

3. Synchronize your vale packages:

```shell
$ vale sync
```

4. Run vale on your files:

```shell
$ vale .
```

## Adding vale assets to your project's .gitignore

As you are downloading these styles via `vale sync` to your local repository, you want to make sure that you don't commit them to your repository. Therefore add this entry to your `.gitignore`:

```txt
# We want to ignore the vale StylesPath
.github/vale/*
```

If you want to add a custom Vocab for your repo (e.g. in `.github/vale/Vocab/Base`), we recommend to use `git add -f` to bypass the .gitignore entry. The vale documentation about [Packages and VCS](https://vale.sh/docs/topics/packages/#packages-and-vcs) does mention a way to add an exception to the  `.gitignore` on a folder level, however we have not been able to get that to work.

## Using vale in a GitHub Action

When you starting using vale, you likely want to do a one time run as explained above to highlight all spelling/styles issues, and to fix them accordingly.

Besides that, we recommend to integrate vale into the regular CI runs of your project, to identify issues as they happen.

To do that, copy this [vale.yml](.github/workflows/vale.yml) GitHub Action and configure it according to your needs.

Further information about this topic:

- https://redhat-documentation.github.io/vale-at-red-hat/docs/main/user-guide/using-vale-github-action/
- https://github.com/errata-ai/vale-action

## What if I am in doubt about spelling?

We use a custom dictionary for American English (provided by [Libre Office](https://cgit.freedesktop.org/libreoffice/dictionaries/tree/en)).

However it can still happen that a word that you consider correct, is flagged by vale as incorrect. This happen especially when you are using domain-specific words like `hackathon` or similar that might be common in the software development domain but still not a proper word in the dicitonary sense :)

If in doubt, please check the spelling of a word against the [Meriam Webster](https://www.merriam-webster.com/) dictionary.

## References

- We should try learn how others have used vale, and what of that we want to adopt for our purposes. For an example of another org see https://github.com/aiven/devportal/blob/main/.github/vale/README.rst
