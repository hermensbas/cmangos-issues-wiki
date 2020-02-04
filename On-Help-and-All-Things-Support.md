> TL;DR: **Provide us with data!**

While it's certainly faster to ask us in `#general`,
the most preferred way is to [file an issue][1] in a repository, created specifically for that very purpose.

That being said, if you can't (or won't) -- there are multiple things we would _require_ to know about the issue in order to handle it efficiently, __or at all__.

Don't forget that we are volunteers and donating our spare time to the project, so be prepared before you ask.


#### In particular:
- **Search** Disocrd chat logs for relevant messages, **explore** the Web -- maybe someone else has already found the solution? It happens a lot.

- **Provide us with data!** We _need_ that stuff to efficiently help you.

  - `mangosd -v` will give you a lot of information that is useful right away. That is, if you've built and can run the thing at all.

  - `git rev-parse HEAD`: **commit hash** is much better than saying "latest release from github" (the meaning you think it has is lost a few hours after you've built the core)

  - Versions of **CMake** and **Boost** used (check compatibility table [here][3])

  - In what **mode** the core was built? `DEBUG`? `RELEASE`? `RelWithDebugInfo` or maybe something else?
  
  - What **cmake flags** were used? These are things like `PCH=1` or `BUILD_PLAYERBOT=1`
  
  - Any additional tools you've used, such as `ccache`?

  - **Compiler name and version**, kind / flavor of **OS**, name / version of **DB server** (e.g MariaDB?) you're running?

  - Any **related details** you can dig up yourself, like spell / creature IDs, crash- and execution- **logs**, in-game **messages** and **screenshots**.

  - Is it a crash? [**Run a debugger**][4], check **state of threads**, look for **stack traces**. Use Debug builds of the core.


**P.S.** Use Discord's [**formatting**][2] facilities! That way you can make all this data _readable_ to most of us~

**P.P.S.** If you can spare an hour of your time: [READ THIS][0]. Helping others help you helps.


[0]: http://www.catb.org/~esr/faqs/smart-questions.html
[1]: https://github.com/cmangos/issues/issues/new/choose
[2]: https://support.discordapp.com/hc/en-us/articles/210298617-Markdown-Text-101-Chat-Formatting-Bold-Italic-Underline-
[3]: https://gist.github.com/Levitanious/d3756fd1634c7be58c51add9466bbe2e
[4]: https://duckduckgo.com/?q=how+to+use+gdb&t=ffab&ia=web