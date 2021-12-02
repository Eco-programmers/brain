---
title: Howto Code reviews
date created: 2021-12-02T00:00:00.000Z
date updated: '2021-12-02'
---

# Code reviews

Code reviews are essential for high quality code. Also they are a great opportunity to share knowledge, all participants. Good code reviews can be lots of effort, but they take your code to the next level, not only because of the outside view and fresh ideas but also because you write just better code when you know that others will review it later. Code reviews should always go over manageable parts, i.e. individual program features. Avoid code reviews of thousands of lines of code from several program parts. This is frustrating for both the reviewer and the reviewee.

Code reviews can be done either in writing or, especially for shorter reviews or when there is still a lot of explanation needed, directly together on the screen. This howto is specifically about written code reviews.

Code reviews are often done within a merge request on GitHub or GitLab, where code reviews are built into the merge request. Otherwise, you must first decide how to perform the code review.

For example, you can write your annotations directly as comments in the code. Then you should use unique markers so that the reviewee can find your comments quickly with the search function. I use, e.g., simply my initials, in C++ `// SH: ...`. Of course, it is important to stay consistent and not suddenly write `//SH ...`, otherwise comments might get lost.

Another option is to use an external text document. I prefer Markdown here because it is effortless to insert code sections. I then divide the text document into sections: the first section contains general comments, the second section includes comments on the user interface. After that, each file I review gets its own section. Finally, I write the corresponding line number in the code before each comment. But of course, you can't add comments in the code itself because this would change the line numbers. So you have to decide on one option.

Code reviews are not trivial and can contain some pitfalls. The perhaps most important to be aware of: it can be [challenging to communicate emotion and intention online](https://thoughtbot.com/blog/empathy-online).

It is helpful to understand that there are three perspectives to a code review: (i) of the person who wrote the code, (ii) of the reviewer, and (iii) of the team. During a code review, you should keep all three perspectives in mind, whether you are the reviewer or the reviewee. Here are some hints and ideas to consider for each of the perspectives:

(the following part is mostly copied from [guides/code-review at main · thoughtbot/guides](https://github.com/thoughtbot/guides/tree/main/code-review))

## Everyone

- Accept that many programming decisions are opinions. Discuss tradeoffs, which you prefer, and reach a resolution quickly.
- Ask good questions; don't make demands. ("What do you think about naming this `:user_id`?")
- Good questions avoid judgment and avoid assumptions about the author's perspective.
- Ask for clarification. ("I didn't understand. Can you clarify?")
- Avoid selective ownership of code. ("mine", "not mine", "yours")
- Assume everyone is intelligent and well-meaning. Avoid using terms that could be seen as referring to personal traits. ("dumb", "stupid").
- Be explicit. Remember people don't always understand your intentions online.
- Be humble. ("I'm not sure - let's look it up.")
- Don't use hyperbole. ("always", "never", "endlessly", "nothing")
- Don't use sarcasm.
- Keep it real. If emoji, animated gifs, or humor aren't you, don't force them. If they are, use them with aplomb.
- Talk synchronously (e.g. chat, screen-sharing, in person) if there are too many "I didn't understand" or "Alternative solution:" comments. Post a follow-up comment summarizing the discussion.

## Having Your Code Reviewed

- Be grateful for the reviewer's suggestions. ("Good call. I'll make that change.")
- Be aware that it can be [challenging to convey emotion and intention online](https://thoughtbot.com/blog/empathy-online)
- Have only "finished" code reviewed. Finished means that you are not able or have no idea on how to further improve the code.
- Delete all commented code and unused before the review.  
- Comments make it easier for the reviewer to understand your code. Comments give context and explain why the code exists, they are not a description of what the code itself does. ("It's like that because of these reasons. Would it be more clear if I rename this class/file/method/variable?")
- Seek to understand the reviewer's perspective.
- Try to respond to every comment.

## Reviewing Code

Understand why the change is necessary (fixes a bug, improves the user experience, refactors the existing code). Then:

- Communicate which ideas you feel strongly about and those you don't ("I think this is important, because ...", "I'd prefer it to ...,  but I think that is personal preference").
- Identify ways to simplify the code while still solving the problem.
- If discussions turn too philosophical or academic, move the discussion offline to a regular Friday afternoon technique discussion. In the meantime, let the author make the final decision on alternative implementations.
- Offer alternative implementations, but assume the author already considered them. ("What do you think about using ... here?")
- Seek to understand the author's perspective.

---

References:
Related:
