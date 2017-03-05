- Feature Name: Rust_Language_Analysis
- Start Date:   2017-03-05
- RFC PR:       
- Rust Issue:   

# Summary
[summary]: #summary

As the [Rust](https://www.rust-lang.org) language evolves it is becoming paramount to implement new features and uses that benefit the community of Rust-lang programmers as a whole. This means we need to understand; _how_ developers are using the language, _what_ they normally struggle with, and _what_ can give the Rust community the biggest benefits either as a future RFC or even just an additional chapter to the Rust book [Rust By Example](http://rustbyexample.com/).

# Motivation
[motivation]: #motivation

The motivation for this RFC was Rust's [blog post on Ergonomics](https://blog.rust-lang.org/2017/03/02/lang-ergonomics.html) and several comments in the [Hacker News comment chain](https://news.ycombinator.com/item?id=13785277) specifically comments made by [modeless](https://news.ycombinator.com/user?id=modeless), [d33](https://news.ycombinator.com/user?id=d33), and of course [shepmaster](https://news.ycombinator.com/user?id=shepmaster). Seeing how Rust is at an impasse with what to formally implement and how to make the language better for new and old users alike a formal verification on how users _use_ Rust is necessary to make informed decisions.

# Detailed design
[design]: #detailed-design

As [d33](https://news.ycombinator.com/user?id=d33) first mentioned I am in favor of adding this to the [Rust Playground](https://play.rust-lang.org). This should be in opt-in feature since it will track users keystrokes while on the site. My initial thoughts on this are three fold: 

1. Have users solve common (and difficult) programming channels and submit them.
    - Doing this will allow the Rust community to not only see what users are using feature-wise (e.g. are people actually using `?`?) but also how long a user takes for challenges like fizz-buzz.
    - In addition to the added benefit to Rust, we can also build a community that has beginner challenges/speed tests for users, by users, and reviewed by users and experts. Including this into our culture would be a huge benefit. Already the Rust community is amazing with IRC, the [Rust By Example](http://rustbyexample.com/) book, and the friendly nature of Rust programmers. Adding in these challenges with not only formal language analysis done by Rust developers for the benefit of the language but also to the benefit of the direct user would increase community involvement. Though, it is _absolutely necessary_ that feedback happens for this to work. Feedback is difficult to do and will require even more community engagement.
2. Track anonymous programming occurring in the [Rust Playground](https://play.rust-lang.org).
    - A lot of users use the [Rust Playground](https://play.rust-lang.org) just as I do almost like the Python IDLE. As a quick sanity check and a "can I even do this?" test. Allowing the Rust community to have data on what people are putting into the Playground will allow us to see what are the common mistakes people make (e.g. a missing semi-colon), the most common compiler errors, what errors are most often repeated by a user(s), what does the scenario look like when a user is defeated (e.g. gets multiple errors in a row and closes the session without a successful build), and how users overcome an error. 
    - In addition if user accounts are necessary for this to work or if user accounts are a good idea to implement for other reasons we can also look at what did the user look up in the [Rust Documentation](https://doc.rust-lang.org/std/) whilst programming on the playground. As useful as this would be anonymously it would not be appropriate; however, to inspect the user's session or cookies to track what they are browsing without explicit permission. I am not suggesting any tracking data _without_ complete agreement from the user.

3. We Must then publish results or have an API to explore the results so that the community can analyze results for themselves. I believe this will allow more direct RFCs with formal analysis and statistical evidence _to support_ their claims. Without opening the data to the community we can fall to the same biases that are made when only a small subset of people review [data][1]. 

# How We Teach This
[how-we-teach-this]: #how-we-teach-this

Allowing users to submit solutions to a Git repository via PRs and reviews will allow the Rust programmers to not only get familiar with Rust but also Git. Including resources on the Rust Book and possibly an interface with the Rust Playground will allow this barrier to be lower to start with the possibility of a "submit for review" button be a walkthrough of your first PR and only accepting subsequent PRs through the Git account. 

I, for one, would welcome both completing challenges to have others review my work (since in my formal job I write Rust but no one can or will review my code), and help review PRs or challenge solutions. Utilizing the Rust community in more than IRC would be very beneficial to budding users who may be afraid to pop into chat and get overwhelmed. Comments on a PR are easier to look at later or over long periods of time without worrying ring that anyone is not at their computer at the moment. I am not suggesting getting rid of IRC or using it less, but this as a supplement for help with the option to chat live if schedules can sync up. 

Having expert programmers review PRs by beginner and advanced users will be necessary for this to work and benefit the community. Thus, keeping the challenges short and familiar will be beneficial to start with as finding the time to review code is always difficult. 

Accepting this proposal will drastically change the way that Rust is taught. Not only will we have the great Rust Book, but we will also have a way to have your code looked at by Rust programmers who can give good advice (e.g. return a `Some(T)` or `None` type with an `.unwrap()` in your code instead of a negative `i32` when your break early out of loop, etc.). Things that you acquire over time by reading code from established projects can be much easier learned by doing. This process will not only teach the Rust language but can teach users the Rustacean way of doing things.

We can host these challenges under the Rust Project and link directly to them from [Rust By Example](http://rustbyexample.com/) in their relevant places. We should *not* have the challenge be too simple (e.g. implementing a small change to a `impl fmt` as opposed to creating a `impl fmt` to a complex or custom `struct` from scratch). Allowing users to learn more as they work through the book. As well as allowing other users to pick specific examples they want to be challenged on.

# Drawbacks
[drawbacks]: #drawbacks

This will be a lot of work. It will take a lot of time developing the tracking, the Git repo, adding in the challenges, developing an API of the results, and so on. This is just the initial spin up, it will also take a lot of time from community members to review the PRs and submitted solutions. This will distract developers from submitting actual work to the Rust back-end. The worst part is, when all the time has been taken to set this up, what if users do **not** use it? That's a lot of effort wasted on something that is not needed or necessary. 

Another major what-if is what if the users do not opt-in to tracking or have a fundamental disagreement with keystroke logging while they code. The results then will be useless to core developers and the community and what changes are needed/necessary.

# Alternatives
[alternatives]: #alternatives

Alternatives to be considered are to have more IRC or Git issue involvement on what you're having issues with. Possibly voting on the Rust-lang website on RFCs and issues. Alternatives to this RFC would be more simplistic in nature and require less work from developers to spin up. 

# Unresolved questions
[unresolved]: #unresolved-questions

- How do we track users without violating privacy or the core values of the open source community?
- How do we make the relevant results from this analysis make sense to our core developers (i.e the decision makers of features)?
- Do we enable a user-account type design so we can see what the user looked up in the [Docs](https://doc.rust-lang.org/std/)?
- What challenges are necessary and appropriate?
- Does having a Git repo à la [Year of Programming Challenges](https://github.com/YearOfProgramming/2017Challenges) make sense for the Rust community?
- Will this fizzle out?
- Can we get experts, advanced, intermediate, and beginner users alike to use this system?
- FEEDBACK!


[1]: http://www.psych.purdue.edu/~willia55/392F-'06/HewstoneRubinWillis.pdf "In-Group Bias"
