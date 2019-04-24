# Mysterium developer's handbook

The goal of the devbook is to improve development efficiency. It serves 2 purposes: 

1. align developers on development/collaboration practices
2. smoothen onboarding for the newcomers

All practices in the devbook are meant to serve as guidelines, rather than rules.  
There will always be exceptions to the guidelines. 
However, if exceptions occur frequently, consider adjusting guidelines (by creating a PR) to keep them up-to-date.

## Table of contents

- [Code review](#code-review)
- [Git](#git)
  - [Workflow](#workflow)
  - [Commit messages](#commit-messages)

## [Code review](#code-review)

A guide for reviewing code and having your code reviewed. Watch a presentation
that covers this material from [Derek Prior at RailsConf 2015](https://www.youtube.com/watch?v=PJjmw9TRB7s).

### Everyone

* Accept that many programming decisions are opinions. Discuss tradeoffs, which
  you prefer, and reach a resolution quickly.
* Ask good questions; don't make demands. ("What do you think about naming this
  `:user_id`?")
* Good questions avoid judgment and avoid assumptions about the author's
  perspective.
* Ask for clarification. ("I didn't understand. Can you clarify?")
* Avoid selective ownership of code. ("mine", "not mine", "yours")
* Avoid using terms that could be seen as referring to personal traits. ("dumb",
  "stupid"). Assume everyone is intelligent and well-meaning.
* Be explicit. Remember people don't always understand your intentions online.
* Be humble. ("I'm not sure - let's look it up.")
* Don't use hyperbole. ("always", "never", "endlessly", "nothing")
* Don't use sarcasm.
* Keep it real. If emoji, animated gifs, or humor aren't you, don't force them.
  If they are, use them with aplomb.
* Talk synchronously (e.g. chat, screensharing, in person) if there are too many
  "I didn't understand" or "Alternative solution:" comments. Post a follow-up
  comment summarizing the discussion.

### Having Your Code Reviewed

* Be grateful for the reviewer's suggestions. ("Good call. I'll make that
  change.")
* A common axiom is "Don't take it personally. The review is of the code, not you." We used to include this, but now prefer to say what we mean: Be aware of [how hard it is to convey emotion online] and how easy it is to misinterpret feedback. If a review seems aggressive or angry or otherwise personal, consider if it is intended to be read that way and ask the person for clarification of intent, in person if possible.
* Keeping the previous point in mind: assume the best intention from the reviewer's comments.
* Explain why the code exists. ("It's like that because of these reasons. Would
  it be more clear if I rename this class/file/method/variable?")
* Extract some changes and refactorings into future tickets/stories.
* Link to the code review from the ticket/story. ("Ready for review:
  https://github.com/organization/project/pull/1")
* Push commits based on earlier rounds of feedback as isolated commits to the
  branch. Do not squash until the branch is ready to merge. Reviewers should be
  able to read individual updates based on their earlier feedback.
* Seek to understand the reviewer's perspective.
* Try to respond to every comment.
* Wait to merge the branch until continuous integration tells you the test suite is green in the branch.
* Merge once you feel confident in the code and its impact on the project.
* Final editorial control rests with the pull request author.

[how hard it is to convey emotion online]: https://www.fastcodesign.com/3036748/why-its-so-hard-to-detect-emotion-in-emails-and-texts

### Reviewing Code

Understand why the change is necessary (fixes a bug, improves the user
experience, refactors the existing code). Then:

* Communicate which ideas you feel strongly about and those you don't.
* Identify ways to simplify the code while still solving the problem.
* If discussions turn too philosophical or academic, move the discussion offline
  to a regular Friday afternoon technique discussion. In the meantime, let the
  author make the final decision on alternative implementations.
* Offer alternative implementations, but assume the author already considered
  them. ("What do you think about using a custom validator here?")
* Seek to understand the author's perspective.
* Sign off on the pull request with a :thumbsup: or "Ready to merge" comment.
* Remember that you are here to provide feedback, not to be a gatekeeper.

### Style Comments

Reviewers should comment on missed style guidelines. Example comment:

    > Order resourceful routes alphabetically by name.

An example response to style comments:

    Whoops. Good catch, thanks. Fixed in a4994ec.

If you disagree with a guideline, open an issue on the guides repo rather than
debating it within the code review. In the meantime, apply the guideline.

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
    - Request [reviews](#code-review) as suggested and anyone else you see fit
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
