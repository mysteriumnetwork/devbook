# Mysterium developer's handbook

The goal of the devbook is to improve development efficiency. It serves 2 purposes: 

1. align developers on development/collaboration practices
2. smoothen onboarding for the newcomers

All practices in the devbook are meant to serve as guidelines, rather than rules.  
There will always be exceptions to the guidelines. 
However, if exceptions occur frequently, consider adjusting guidelines (by creating a PR) to keep them up-to-date.

## Table of contents

- [Git](#git)
  - [Workflow](#workflow)
  - [Commit messages](#commit-messages)

## [Git](#git)

### [Workflow](#workflow)

1. Create a feature branch  

    - Prefix branch name with `feature/` or `fix/` when applicable; otherwise, prefix with your initials, e.g. `tk/`
    - Use kebabcase
    - Include the issue number when applicable
    - Briefly describe the change  

    Examples: `feature/610-seelog-wrapper`, `fix/tequilapi-startup`, `tk/polish`

2. Implement the changes (series of commits)
    - It's best when commmits are clearly separated, i.e. each fix, change, refactoring, extra tests go into their own commits
    - When fixing up a commit that already exists on your feature branch, try your best to squash the fix to the related commit so that we can avoid noise in git history
      - If it's the last commit:

        ```
        $ git commit --amend
        ```

      - Otherwise, do [an interactive rebase](https://help.github.com/en/articles/about-git-rebase) to squash them into cohesive commits with good messages:

        ```
        $ git fetch origin
        $ git rebase -i origin/master
        ```
3. Rebase frequently to incorporate upstream changes

    ```
    $ git pull --rebase origin master
    ```

4. Push your branch and create a pull request (PR)
    - Request reviews as suggested and anyone else you see fit
    - Wait for approvals and CI checks to pass

5. Merge PR and remove the branch (or ask someone with push rights to do it)

General tips:

- Try to integrate with master branch ASAP. Prefer delivering feature in smaller working chunks rather than one huge PR.
- Avoid merging `origin/master` into feature branch. Rebase instead to keep git history as linear as possible.

### [Commit messages](#commit-messages)

We use widely established conventions for idiomatic Git commit messages:

- Use imperative mood in the subject line.  

  A properly formed Git commit subject line should always be able to complete the following sentence:  
  If applied, this commit will _**your subject line here**_
- Separate subject from body with a blank line
- Limit the subject line to a single, short sentence
- Capitalize the subject line
- Do not end the subject line with a period
- Use the body to explain _what_ and _why_ vs. _how_.  
- Wrap the body at 72 characters

[Read more &#x2197;](https://chris.beams.io/posts/git-commit/)

### Credits

Inspired by:
- [Thoughtbot guides](https://github.com/thoughtbot/guides) by thoughtbot, inc. It is distributed under the [Creative Commons Attribution License](http://creativecommons.org/licenses/by/3.0/).
