---
layout: post
title: "Regular expressions tutorial"

date: 2021-09-14
---

I like regular expressions. Constructing a regular expression is like solving a puzzle, and they are a powerful tool for lots of situations. In my work on Chess software for MediaWiki, we use regular expressions to validate chess game files before commiting to the full parser in order to save resources. These game files are complex, but as a file format highly regular and well defined. You can see in [patch set 719449](https://gerrit.wikimedia.org/r/c/mediawiki/extensions/ChessBrowser/+/719449/3/includes/ChessBrowser.php) the kinds of regular expression we use for validation alongside detailed documentation of how it works. The old version was one massive expression, and while it worked most of the time, the false positives and complexity made it hard to maintain. In the newer patch, it gets broken up into multiple expressions that act like filters, and overall the regular expressions are easier to understand and maintain. While the reasons for the change are related to that specific software, the difference between the old and new version exemplifies some useful insights that are helpful for those new to regular expressions, and I thought it would be useful to write up some similar advice I gave to another graduate student.

Their regular expressions were effective for the most part, and despite a couple missed matches, the main problem turned out to be a python coding error. Since I was asked for more general advice on regular expressions, I wrote them the following tutorial to help improve their expressions and better understand how to approach these kinds of coding problems in the future.

They had the following text from the Corpus of Contemporary American English, and wanted to parse it to remove all the names. 

> @@4123272 @!MITT-ROMNEY- ( R ) , PRESIDENTIAL CANDIDATE : This is time for America to choose whether they want more of the same , whether unemployment above 8 percent month after month after month is satisfactory or not . @!BARACK-OBAMA# The choice in this election could not be clearer and it could not be bigger , the stakes could not be bigger . @!UNIDENTIFIED-MALE# You can do it ! @!OBAMA# I know . @(END-VIDEO-CLIP) @!SCHIEFFER# Or can he ? We will talk about it with Republican John McCain , who found out in 2008 what it is like to run for president when the economy turns bad . We will talk politics with Haley Barbour , the former chairman of the Republican Party , and the Senate 's number two Democrat , Dick Durbin . And what is the fallout from the bombshell leak about Chief Justice John Roberts reversing his position to ensure that the court upheld the president 's health care plan ? Will it affect the court 's future deliberations ? CBS News Jan Crawford , the reporter who broke the story , has a follow-up @ @ @ @ @ @ @ @ @ @ House correspondent Norah O'Donnell will also join us for analysis on that and more . And at baseball 's All-Star Break , we will talk about America 's game with historian Doris Kearns Goodwin , Sports Illustrated 's Frank Deford , former all-star Harold Reynolds , and ESPN 's Jayson Stark .


There are two important insights for regular expressions. First is to think in groups rather than words or characters. Consider the examples you gave below of inconsistent speaker identification. Think of it as two groups: a name and (optionally) a title. Using some pseudo code we can conceptualize all of your examples as: "(NAME), (TITLE)". Now, within those groups, what are the regularities? Well, we know that names are pretty regular, and titles can be just about anything, so it's probably best to focus on the name group and just match whatever is left over using the non-greedy wildcard (i.e., `.*?`).

Anyway, this gets us to the second insight: think of regular expressions as filters on a text. You want to start by matching the largest chunks of text and then match slightly more specific text, and so on until you are left with what you want. Part of your problem, I think, is that you started by matching specific text first, namely, the "@". What you'll notice in the example is that all speakers begin with "@!" and this is incredibly useful for matching!

With these in mind, we can look at the example source to try and make sense of it a little more. What is the most general group that we can start filtering by? We see the "@" repetition, so that's likely to be helpful, then we notice the "name title" pattern. Looking closer we see that "name title" group is always preceded by "@!" and always terminated by either "#" or ":". So our most general filter is:

(1) `r"@!.*?[#:]"`

This works, but it is way too general and opens us up to a lot of false matches. It also doesn't match bare "@" or "@" followed by digits but we'll get to that in a later filter. so we have this group, how can we break it down further? Well, we already have the "name title" pattern, so let's use that:

(2) `r"@!.*?,.*?[#:]"`

We can improve on this further by limiting what gets matched in these groups and how we define them. They got to about here it seems, using `r"[A-Z1-9\-\s\'\(\),]+"` but we can not only make this more elegant, we can do it with more precision. They were trying to work around the problem of "...ROMNEY- (R), ..." since that breaks our pattern, but the buggy-expression collapses the groups and just tries to match the whole thing. Instead, what if we redefined our groups? As written, our groups are NAME and TITLE delimited by ", " and being surrounded by some symbols. Since we have a pretty good idea of name patterns, what if we defined the groups as NAME and NOTNAME? We take the chunk from (1), match the name using a stringent expression, and then match the rest so that we don't need to worry about the "- (R), " problem. This gets us:

(3) `r"@![A-Z0-9\-]+.*?[#:]"`

But we can clean this up a bit more. Names are composed of alphanumeric symbols, "word characters", and regex has a short-hand notation for that: `\w`. We know that these sequences of word characters (some people call them names) are delimited by a hyphen, and that this pattern repeats for as many names as someone has. So we can simplify the above to:

(4) `r"@!((\w+)-?)+.*?[#:]"`

Now, it may not look "simple" but it has the advantage of conveying all the insights we compiled above. The string we are looking for is composed of one or more word characters, `\w+`, followed by 0 or 1 hyphen, `(\w+)-?`, with one or more such sequences in a row, `((\w+)-?)+`; that regular string is initiated by "@!" and precedes some unknown sequence of characters terminated by either "#" or ":".

So why go through all that, and why prefer (4) over (3) which is roughly equivalent? The reason is that (4) is easier to debug and extend. If you run into names that are separated by a space instead of a hyphen, you know exactly what to fix, use `[\-\s]?` instead of `-?`. If you find that these speaker codes are terminated by something other than `[#:]`, you just add it to the list. If you find a pattern within the NOTNAME group, you replace `.*?` with something more specific. Etc, etc. You can even run similar patterns multiple times if you find that just adding to the list matches the wrong things.

Now that we've got that big chunk out of the way, we're left with "@@13352534 ... @ @ @ @ @ ..." (I made the number up, it won't matter). Now that we've removed everything else, these are simple to catch because we don't have to worry about false positives now that the "@!..." speaker tags are gone. We see that an "@" can be followed by nothing, or it can be followed by some number of digits. Regular expressions has a symbol for digits,`\d`, so we can just do:

(5) `r"@(\d+)?"`

And that gets all of them. Importantly, (5) will match all the "@" symbols that start speaker tags, and if you run it before (4) then (4) will not work. This is why they're like filters. By handling the bulky stuff first, we can use simple expressions for the truly simple stuff. If the big filters can get the fine stuff too, then that's just a bonus. By thinking about patterns in terms of groups, we are able to complement this filtering by capturing chunks, refining those chunks into more chunks, and so on and so forth until we get an expression that not only works but has a semantic relationship to the thing it is matching.
