---
title: How to Make Your Code Reviewer Fall in Love with You
tags:
- code review
- culture
- code style
description: TODO
date: '2020-11-15'
hero_image: cover.png
images:
- code-review-love/og-cover.jpg
hide_affiliate_warning: true # No affiliate links in this post
---
When people talk about code reviews, they often focus on rules the reviewer should follow. What about the author? The person who writes the code is just as important as the reader in achieving a successful review. Sadly, there's scant guidance for developers on preparing their code for review. As a result, authors often sabotage their own reviews simply because they don't know any better.

This article describes best practices for participating in a code review when you're the author. In fact, by the end of this post, you're going to be so good at sending your code out for review that **your reviewer will literally fall in love with you**.

## But I don't want my reviewer to fall in love with me

They're going to fall in love with you. Deal with it.

Nobody ever complained on their deathbed that too many people fell in love with them.

## Why improve your code reviews?

Improving code review technique helps your reviewer, your team, and, most importantly, you.

* Learn faster
  * If you properly prepare changelists for review, it directs your reviewer's attention to areas where you can grow as a developer rather than boring issues like style violations.
  * Your reviewer provides better feedback when you demonstrate that you value constructive criticism.
* Make others better
  * The way you participate in code reviews as an author sets an example for others. If you follow good practices, it will rub off on your teammates. This makes your job easier when you're reviewing their code.
* Minimize team conflicts
  * Code reviews are sensitive and are a common source of friction. Approaching code reviews deliberately and conscientiously minimizes arguments.

## The golden rule: value your reviewer's time

Reviewing code is difficult &mdash; harder than writing the code in the first place.

Your teammate arrives at work each day with a finite supply of focus. If they allocate some of it to reviewing your code, that's time they can't spend on their own work. It's only fair that you maximize the value of their time.

This advice sounds obvious, but I often see authors treat reviewers like personal quality assurance technicians. They ignore opportunities to catch their own careless errors, and they make minimal effort to organize their changelist for reviewability.

Reviews improve drastically when participants trust each another. When your reviewer has confidence that you respect their time and take their feedback seriously, they'll put more effort into helping you. If you treat your review as a box you have to check before merging in your code, you miss out on expertise that your reviewer can offer you.

## Techniques

TODO(mtlynch): Add links for all of these and match the wording in the headings.

1. Review your own code first
1. Write a clear changelist description
1. Automate the easy stuff
1. Answer questions with the code itself
1. Keep changes narrowly scoped
1. Separate functional and non-functional changes
1. Break up large changelists
1. Respond graciously to critiques
1. Be patient when your reviewer is wrong
1. Communicate your responses explicitly
1. Artfully solicit missing information
1. Award all ties to your reviewer
1. Minimize lag between rounds of review

## Review your own code first

Before sending code to your teammate, read it yourself. Don't just check for mistakes &mdash; imagine reading the code for the first time. What would be confusing?

I find it helpful to take a break between writing my code and reviewing it. People often they fire off their changes at the end of the day, but that's when you're least likely to spot your own mistakes. Wait until morning, and take a second look with fresh eyes before handing it over to your teammate.

{{<img src="what-idiot.jpg">}}

Adopt your reviewer's environment as much as possible. Use the same diff view that they'll see. It's easier to catch careless errors in a diff than simply reading code in your normal editor.

Don't expect yourself to be perfect. Inevitably, you'll send out a changelist with debugging code that you forgot to delete or with an extra file you meant to exclude. These mistakes aren't the end of the world, but they're also not nothing. Pay attention to the categories of mistakes you make and think about systems you can put in place to prevent them. If they happen too frequently, it signals to your reviewer that you don't value their time.

## Write a clear changelist description

At my last job, I met regularly with a senior engineer as part of my company's developer mentorship program. Before our first meeting, he asked me to bring a design doc I'd written. As I handed it to him, I explained what the project was and how my design doc fit in with my team's goals. My mentor frowned. "Everything you just told me should be on the first page of your design doc," he said, bluntly.

He was right. I wrote the design document imagining how my teammates would read it, but I failed to consider other readers. Partner teams might want to understand it. I definitely wanted Google's [promotion committee](#TODO) to understand it, as they decided my career trajectory.

Ever since that discussion, I always think about how to package my work to make the context discoverable to readers, especially while writing my changelist descriptions. The changelist description should describe the full context needed for your reviewer to understand it and anyone else who might need to read this changelist in the future.

You might have a code reviewer in mind when you write your code, but they don't necessarily have the context that you assume they do. Besides, other developers on your team should understand the change, and developers in the future should be able to understand it if they ever need to review the change history.

A good changelist description explains:

* **what** the change achieves, at a high level
* **why** you're making this change

For an example of an excellent changelist description, see David Thompson's article, ["My favourite Git commit."](https://dhwthompson.com/2019/my-favourite-git-commit)

## Automate the easy stuff

If you rely on your reviewer to tell you that you put the curly braces on the wrong line or that your change broke the automated test suite, you're egregiously wasting their time.

{{<img src="verify-syntax.jpg">}}

Automated checks should be part of your team's normal workflow. The review begins only after [all automated checks pass in a continuous integration environment](/human-code-reviews-1/#let-computers-do-the-boring-parts).

If your team is woefully misguided and refuses to invest in continuous integration, automate these checks yourself by adding [git pre-commit hooks](https://www.atlassian.com/git/tutorials/git-hooks), linters, and formatters to your development environment. This ensures that your code doesn't go out for review until it matches your team's style and passes your automated checks.

## Answer questions with the code itself

What's wrong with this picture?

TODO: Make this a screenshot

>`function verifyInput(frombobulator) {`
>
>**Me, reviewer**: I'm having trouble understanding the purpose of this function.
>
>**Author**: Oh, it's in case the caller passes a Frombobulator that's missing a frombobulate implementation.

The author helped me understand the function, but what about the next person who reads it? Should they dive into the change history and read every code review discussion ever? Worse is when the author comes over to my desk to give me an in-person explanation, which both interrupts my focus and ensures that nobody else ever has access to the explanation.

When your reviewer expresses confusion about how the code works, the solution isn't to explain it to that one person. You need to explain it to *everyone*.

{{<img src="late-night-question.jpg" maxWidth="600px">}}

The best way to answer someone's question is to refactor the code to eliminate the confusion. Can you rename things or restructure logic to make it more clear? Code comments are an acceptable solution, but they're strictly inferior to code that documents itself naturally.

## Narrowly scope changes

Scope creep is a common anti-pattern in code reviews. A developer starts with the goal of fixing a logic bug, but they notice a UI blemish in the process. "While I'm here," they think to themselves, "I'll just fix this other thing." But now they've muddled things. Their reviewer has to figure out which changes serve goal A and which serve goal B 

The best changelists just [Do One Thing](https://blog.codinghorror.com/curlys-law-do-one-thing/). The smaller and simpler the change, the easier it is for the reviewer to keep all the context in their head. Decoupling unrelated changes also allows you to parallelize your reviews across separate reviewers, reducing turnaround time for your changes.

## Separate functional and non-functional changes

The corollary to tightly scoping your changes is to separate functional and non-functional changes.

Developers inexperienced with code reviews often violate this rule. They'll make two lines of actual code changes, and then their code editor automatically reformats the entire file. They either don't realize what they did or decide their formatting is better, so they send out the two-line functional change buried in hundreds of lines of non-functional whitespace changes.

This is a huge insult to your reviewer. Whitespace-only changes are easy to review. Two-line changes are easy to review. Two-line functional changes lost in a sea of whitespace changes are tedious and maddening.

TODO: Show screenshot of buried change

When refactoring, developers also tend to inapproriately mix changes. I love it when my teammates refactor code to make it easier to understand and maintain. But I don't like it when they refactor code *while* changing its behavior.

TODO: Screenshot of a function changing behavior and being refactored at the same time. First screenshot shows everything changing at once, second screenshot shows refactoring in one step followed by behavior change in second.

If a piece of code requires refactoring *and* behavioral changes, this should happen in two to three changelists:

1. Add tests to exercise the existing behavior (if they're not already there).
1. Refactor the production code while holding the test code constant.
1. Change behavior in the production code and update the tests to match.

By leaving the automated tests untouched in step 2, you prove to your reviewer that your refactoring preserves behavior. When you reach step 3, your reviewer doesn't have to suss out what's a refactoring change and what's a behavioral change because you've decoupled them properly ahead of time.

## Break up large changelists

Overly large changelists are the ugly cousins of scope creep. A developer finds that to add feature A, they need modify a parameter to functions B and C. If it's a small set of changes, that's fine, but it can also make a change enormous.

A changelist's complexity grows exponentially with its size. There's no exact limit, but when my changes exceed 500 lines of production code, I look for opportunities to break it up before requesting a review.

 Instead of changing everything at once, can you change the dependencies first and add the new feature in a subsequent changelist? Can you preserve the sanity of the codebase if you add half of the feature now and the other half in the next changelist?

It's tedious to break up your code to find a subset that makes a working, intelligible change, but it yields better feedback and puts less strain on your reviewer.

## Respond graciously to critiques

The fastest way to ruin a code review is to take feedback personally. This is challenging, as many developers take pride in their work and see it as an extension of themselves. If your reviewer frames their feedback [to focus on you instead of your work](/human-code-reviews-1/#never-say-you), it's even harder.

As the author, [you ultimately control your reaction to feedback](/book-reports/7-habits-of-highly-effective-people/#habit-1-be-proactive). Treat your reviewer's notes as an objective discussion about the code, not your personal worth as a human. Responding defensively will only make things worse.

I find it helpful to interpret all notes as helpful lessons. When a reviewer catches an embarrassing bug in my code, my instinct is to make excuses for myself. Instead, I praise my reviewer for their scrupulousness.

>`ConvertExcelDateToBasicDate(int32 timestamp) {`
>
>A: This actually won't work for January and February, 1900.
>
>B: Wow, nice catch!

Surprisingly, it's a **good** sign when your reviewer spots subtle flaws in your code. It indicates that you're packaging your changelists well. When you clear out all the obvious issues like bad formatting and confusing names, your reviewer can focus deeply on logic and design, yielding more interesting feedback.

## Be patient when your reviewer is wrong

From time time time, reviewers are just plain wrong. Just as you can accidentally write buggy code, your reviewer can misunderstand correct code. (TODO: don't use just twice)

Many developers react to reviewer mistakes with defensiveness. They take it as an affront that someone would insult their code with criticisms that *aren't even true*.

Even when your reviewer mistakenly sees a flaw in your code, that's still a red flag. If they read it incorrectly, will others make the same mistake? Do readers require unusual scrutiny to reassure themselves that a particular bug *isn't* there?

TODO: Screenshot of two people arguing in a code review.

>A: There's a buffer overflow vulnerability here since we never verify that `sourceLength <= destinationLength`.
>
>B: In **my** code? Impossible! The constructor calls `PurchaseHats`, which calls `CheckWeather`, which would have returned an error if the buffer length was incorrect. Try actually **reading** the entire 200k line codebase before you even **begin** to entertain the notion that I'm capable of a mistake.

Look for ways to refactor the code or add comments that make the code's correctness obvious. If their confusion stems from obscure language features, rewrite your code using mechanisms that are intelligible to non-experts.

## Communicate your responses explicitly

I frequently run into a scenario where I give someone notes, they update their code to address *some* of my feedback, but they don't write any replies. Now we're in an ambiguous state. Did they miss my other notes? Or are they still working? If I begin a new round of review, I'm potentially wasting my time on a half-finished changelist. If I wait, I might create a deadlock where both of us are waiting on the other to make the next move.

Establish conventions on your team that make it clear who's "holding the baton" at any point during a review. Either the author is working on edits or the reviewer is writing feedback. There should never be a situation where the review is stalled because nobody knows who's working on the changelist. You can accomplish this easily with a changelist-level comment that says you're passing the code back to the reviewer.

TODO: Screenshot of someone saying, "Updated! Please take a look."

For every note that requires action, respond explicitly to confirm that you've addressed the note. If your code review tool supports it, mark comments as "resolved." If not, follow a simple convention, like, "Fixed," for each note. If you disagree with the note, explain politely why you didn't take action.

TODO: Screenshot of Reviewable mark as resolved.

Adjust your response based on your reviewer's effort. If they write you a detailed note to help you learn something new, don't just mark it done. Respond thoughtfully to show gratitude for their effort.


## Artfully solicit missing information

Sometimes code review notes leave too much to interpretation. When you receive a note like, "This function is confusing," you probably wonder what "confusing" means, exactly. Is the function too long? Is the name unclear? Does it require more documentation?

For a long time, I struggled with notes like these because it was hard to clarify them without sounding defensive. My instinct was to ask, "what's confusing about it?" but that could come across as grouchy.

Once, I unintentionally sent a vague note to my teammate, and he responded in a way that I found fantastically disarming:

>What changes would be helpful?

I love this response because it lacks defensiveness and signals openness to feedback. Whenever a reviewer gives me unclear feedback, I always respond with some variation on the "helpful" question.

Another useful technique is to guess your reviewer's intent and proactively edit your code based on that assumption. For a note like, "this is confusing," give your code a second look. Usually there's *something* you can do to improve clarity. A revision communicates to your reviewer that you're open to change, even if it's not the one they had in mind.

## Award all ties to your reviewer

In tennis, when you're unsure if your opponent's serve landed out of bounds, you give them the benefit of the doubt. There should be a similar expectation for code reviews.

>A player in attempting to be scrupulously honest on line calls frequently will keep a ball in play
that might have been out or that the player discovers too late was out. Even so, the game is
much better played this way.
>
>-[*THE CODE: The Players' Guide to Fair Play and the Unwritten Rules of Tennis*](https://www.usta.com/content/dam/usta/pdfs/2015_Code.pdfhttps://www.usta.com/content/dam/usta/pdfs/2015_Code.pdf) by the US Tennis Association

Some decisions about code are a matter of personal taste. If your reviewer thinks your 8-line function would be better as two 5-line functions, neither of you is objectively "right." It's a matter of opinion which version is better.

When your reviewer makes a suggestion, and you each have roughly equal evidence to support your position, defer to your reviewer. Between the two of you, they have better perspective on what it's like to read this code fresh.

## Minimize lag between rounds of review

A few months ago, a reviewer contributed a small change to an open source project I maintain. I gave them feedback within hours, but they promptly disappeared. I checked again a few days later, but there was still no response from the author.

Six weeks later, the mysterious developer popped up again to submit their revisions. While I appreciated their effort, the lag between rounds of review had doubled my workload. Not only did I have to re-read their code, I had to re-read my feedback to recall the state of the discussion. Had they followed up within a day or two, I wouldn't have had to do all the extra work of restoring context.

{{<img src="effort-graph.jpg">}}

A six-week pause is extreme, but I frequently see unnecessary pauses on full-time teams. Someone sends out a changelist for review, receives feedback, then puts it on the backburner for a week because another task distracted them.

In addition to the time lost in restoring context, half-finished changelists increase complexity. It's harder for everyone to keep track of what's already merged and what's in flight. With more partially-complete changelists, there are more merge conflicts, and nobody likes fixing those.

Once you send your code out for review, driving the review to completion should be your highest priority. Delays on your end waste time for your reviewer and increase complexity for your whole team.

## Conclusion

When preparing your changelists for review, remember the golden rule: value your reviewer's time. If you demonstrate that you care about their experience as a reviewer, they'll return the favor. A reviewer who can focus on the interesting parts of your code generates quality feedback. If they have to spend time untangling your code or policing simple mistakes you could have caught yourself, you both suffer.

Congratulations! You've read to this point and integrated these ideas, which means you're now an expert reviewee. Your reviewer is likely in love with you, so treat them well.

TODO: Add alt text

TODO: Put in plug for *The Software Developer's Guide to Writing*.

## Further Reading

* [How to do Code Reviews Like a Human](/human-code-reviews-1/): Now that you're an expert reviewee, learn to make your code reviews more effective when you're the reviewer.

---

*Illustrations by [Loraine Yow](https://www.linkedin.com/in/lolo-ology/). Edited by [Samantha Mason](https://www.samanthamasonfreelancer.com).*