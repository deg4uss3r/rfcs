- Feature Name: Rust_Language_Analysis
- Start Date:   2017-03-05
- RFC PR:       
- Rust Issue:   

# Summary
[summary]: #summary

As the [Rust](https://www.rust-lang.org) language evolves, it's important to continue to implement new features and use them benefit the entire community of Rust-lang programmers. This means we need to understand:
* _how_ developers are using the language
* _what_ they normally struggle with
* _what_ can give the Rust community the biggest benefits either as a future RFC or just an additional chapter to the [Rust book](https://doc.rust-lang.org/book/) or [Rust By Example](http://rustbyexample.com/).

# Motivation
[motivation]: #motivation

The motivation for this RFC was Rust's [blog post on Ergonomics](https://blog.rust-lang.org/2017/03/02/lang-ergonomics.html) and several comments in the [Hacker News comment chain](https://news.ycombinator.com/item?id=13785277) specifically comments made by [modeless](https://news.ycombinator.com/user?id=modeless), [d33](https://news.ycombinator.com/user?id=d33), and of course [shepmaster](https://news.ycombinator.com/user?id=shepmaster). Rust appears to be at an impasse with what to formally implement and how to make the language better for both new and old users; therefore, a formal verification on how users _use_ Rust is necessary to make informed decisions.

# Detailed design
[design]: #detailed-design

As [d33](https://news.ycombinator.com/user?id=d33) first mentioned, I am in favor of adding this to the [Rust Playground](https://play.rust-lang.org). This should be in opt-in feature since it will track users keystrokes while on the site. The questions I would intend to answer are:

1. How do users solve common (and difficult) programming challenges?
    - Doing this will allow the Rust community to see what users are using feature-wise (e.g. are people actually using `?`?) and also how long a user takes for challenges like fizz-buzz.
    - In addition to the added benefit to Rust, we can also build a community that has beginner challenges/speed tests for users, by users, and reviewed by users and experts. Including this into our culture would be a huge benefit. Already the Rust community is amazing with IRC, the [Rust By Example](http://rustbyexample.com/) book, and the friendly nature of Rust programmers. Including challenges like these would introduce more opportunities for code review (on both the reviewer and the reviewee sides), which would be beneficial for community involvement. For this to be successful, feedback is required, which can be difficult and require additional community engagement.
    - This will require a variety of challenges--short/easy ones that could be reviewed quickly by experts, and more difficult ones that beginners can look at and _learn something from_.
2. Track anonymous programming occurring in the [Rust Playground](https://play.rust-lang.org).
    - My background is in python programming. I frequently use the Python IDLE as a quick sanity check/verification that my idea isn't totally wrong. This is also how I (and I expect many others) use the [Rust Playground](https://play.rust-lang.org). Allowing the Rust community to have data on what people are putting into the Playground will allow us to see the following:
      * common mistakes people make (e.g. a missing semi-colon)
      * the most common compiler errors, what errors are most often repeated by a user(s)
      * what does the scenario look like when a user is defeated (e.g. gets multiple errors in a row and closes the session without a successful build)
      * how users overcome an error. 
    - A corollary to this would be the possible inclusion of user accounts. Perhaps we can link queries in the Rust Docs to what a user is working on in the Playground.
    - Obviously, any data collected should be appropriately anonymized, and it should be an "opt-in" program with a single-click opt-out.

3. We should then open-source the data by publishing results/having an API to explore them. This way, the community can analyze the results themselves. This will allow RFCs and discussions to be more data-driven. It's important to avoid biases that occur when only a small subset of people review [data][1].

## Collecting the Data

This is largely determinisitc on what the community would decide is the optimial boundry between the validity of the collected data and the privacy of the users. This RFC would propose the data is collected in two majro ways: 

1. Using the [Rust Playground]((https://play.rust-lang.org).
 - This would hypotechically be done by running a keylogger on the input to the website, or a snapshot tool that takes a snapshot of the input area in a pre-definied period of time. We could ,ake this time period relative to the user's activity (e.g. if a user is idle for a long period of time do not keep snapping at 5 second intervals).  
2. Built into the Rust Package Manager [Cargo](http://doc.crates.io/guide.html).
 - Here we can add a --send-diagnostics feature to `Cargo` and create an option in `~/.cargo/config` to automatically send information to a respoitiory server on each `cargo build`.  



## Data Collected

Inital thoughts on data collection are: 

- any time a user runs Play record the code submitted
- any time a complication is made record the result (especially any compiler error messages)
 - record or give the user any options to submit and resources used
  - Possibly record the way the user interacts with docs.rust-lang using cookies, but this might be a little too privacy invasive
- record session time (e.g. how long as the window been open without the text input cleared)
- record lines that have changed (plus timing information)


# How We Teach This
[how-we-teach-this]: #how-we-teach-this

Using GitHub to submit solutions (via PRs) and conduct reviews will allow users to become familiar with Git simultaneously. We can further lower this barrier to entry by including resources in the Rust Book and potentially interface with the Rust Playground (possibly have a "submit for review" button that walks you through making a PR).

I'm the first in my company to really use Rust, and all of my code is proprietary, so there's no one who can/will review my code. It would be a _huge_ benefit to me to have challenges where I can learn from others' examples and get feedback on my own code. The Rust community is already active on GitHub, so this extends interactions beyond IRC without adding yet another tool to monitor. Popping into IRC can be a bit overwhelming, especially as a beginner (even #rust-beginners), and it's easier to refer back to comments on a PR than sift through enormous amounts of IRC backlog.

Having expert programmers review PRs by beginner and advanced users will be necessary for this to work and benefit the community. Thus, keeping the challenges short and familiar will be beneficial to start with as finding the time to review code is always difficult. 

This proposal could be a useful complement to the Rust Book by allowing new programmers to try samples out and get feedback on them. While I love reading about code, I learn a lot more by writing it. Getting advice like "return an `Option` instead of a -1!" would have been useful when I first started using Rust. This would allow users to begin with writing idiomatic Rust code, rather than writing in the style of the language they're used to, just in Rust. Since certain elements of safe rust code are idiomatic (e.g. iterators), this would result in safer, better code from the beginning, rather than being acquired over a longer period of time.

We can host these challenges under the Rust Project and link directly to them from [Rust By Example](http://rustbyexample.com/) in the relevant places. As opposed to the examples there, the challenges should be more complex--focused solving a problem rather than teaching syntax, and they should build on concepts as users work through the book. There could also be a suggestion process by which users pick examples they'd like challenges for.

# Drawbacks
[drawbacks]: #drawbacks

This will be a lot of work. It will take a lot of time developing the tracking, the Git repo, adding in the challenges, developing an API of the results, etc. --this would be the initial spin up. It will also take a lot of time from community members to review the PRs and submitted solutions. This could distract developers from submitting actual work to the Rust back-end. The worst case scenario would be that a system like this would be set up, and users wouldn't use it--that would be a huge waste of effort.

Privacy is another concern. If enough users don't opt-in to the anonymized tracking or disagree with snapshots of their code in the Playground, the results won't be useful.

# Alternatives
[alternatives]: #alternatives

Alternatives to be considered are to have more IRC or Git issue involvement on what you're having issues with. Possibly voting on the Rust-lang website on RFCs and issues. Alternatives to this RFC would be more simplistic in nature and require less work from developers to spin up. Of course, more and more documentation thrown at the problem is an alternative as well. 

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

