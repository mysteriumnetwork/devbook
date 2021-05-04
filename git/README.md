# Git

## Workflow

0. Plan/estimate release date of a NON RC release and notify marketing. Marketing needs time to prepare and plan announcements.
   Ideally they would need at least 1-week notice.

1. Create a feature branch  

    - Prefix branch name with `feature/` or `fix/` when applicable; otherwise, prefix with your initials, e.g. `tk/`
    - Use kebabcase
    - Include the issue number when applicable
    - Briefly describe the change  

    Examples: `feature/610-seelog-wrapper`, `fix/tequilapi-startup`, `tk/polish-tequilapi`

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

## Commit messages

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

## Releases process

In order to release new version of a software: 
 1) Decide if a release branch is required. (i.e. you should create release branch if there are commits in master branch you don't want to release)
    - If required: create branch reflecting release version. If release version is `0.21` then branch name must be `release/0.21`.
    - If not: continue release from master
 2) Create a **pre-release** in GitHub and tag appropriate branch (see 1.) with tag named `0.21.0-rc1`.
 3) After pipeline completes and publishes release artifacts make an internal announcement in slack to start testing pre-release.   
 4) When team finishes testing, release should be made from appropriate branch (see 1.) with a tag `0.21.0`.
 5) In case branched release all future critical bugs affecting network operation should be back-ported to `release/0.21` branch for 30 days since its initial release.

#### Motivation for such release process
 - Improve on timely releases with a bit more confidence in quality.
 - Ability to backport critical fixes for stable already released versions. (Currently we aim to support releases for last 30 days)
 - Make release cycle more mainnet-like.
 - After freezing ability to start testing without affecting natural development flow.
 - Gain more confidence while auto-updating mysterium network of nodes.

#### Tagging convention
For go projects, release tags follow this convention: `[major].[minor].[patch]`
