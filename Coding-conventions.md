Database:\
database tables -> underscore_case\
database columns -> CapitalCamelCase\
SQL keywords -> CAPITAL\
file numbering is different per database, but all are usually NUMBER_name_of_change.sql

Anything C++:\
http://astyle.sourceforge.net/astyle.html \
Old code in C++ utilized https://en.wikipedia.org/wiki/Hungarian_notation for variables however new code is slowly being converted to simple camelCase and
m_memberVariable.

Examples of old style code:\
Class members:\
type _memberVariable;\
type memberVariable;\
type i_memberVariable;\
type* m_pMemberVariable;\
Correct:\
type m_memberVariable;

Not using m_ is fine for local script structs, to avoid unnecessary typing.

Large scale codestyle changes that do not alter behaviour are generally discouraged (like making a PR for) due to it altering git history without much benefit. However, when altering a codebase, lets say reworking battlegrounds, fixing codestyle is encouraged. Renaming global frequently used functions should be done after communication, since it creates many merge errors, however it is also encouraged, but should be done last.



