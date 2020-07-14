This is a list of bugs I found (so far) in the documentation of TeX and METAFONT. All of them were found in 2020 and reported to karl or tex-k, but of course I do not claim to be the first finder of them. In the page numbers, "A" stands for _The TeXbook_ and "C" stands for _The METAFONTbook_. "\*" stands for errors already reported by others (according to karl).

Page | Line | Typo | Correction
-----|------|------|------------
A51|19|<code>``</code> yields“|<code>``</code> yields “
A164|-14|Exercise 17.20|exercise 17.20
A305|-1|`-\wd0}`|`-\wd0 }`
A368|8|'*40*=`SP`|'*40* = `SP`
A375|6–7|`\ht0}`|`\ht0 }`
A407|-5|`\penalty5000}`|`\penalty5000 }`
A420|11|`-.1ex }`|`-.1ex\relax}`
A423|16|`width0pt }`|`width0pt\relax}`
A457|right column|`[1]`, 23, <u>119</u>|`[1]` (progress report), 23, <u>119</u>
A475|left column|programs, for computers, 38, 165, 234|programs, for computers, 38, 165, *234*
Cx|-4|More about Macros|More About Macros
C23|-9, -7|*ss* [math italic]|*ss* [text italic]
C28|12|*down* [math italic]|*down* [text italic]
C68|9|`-36.16279`|[that value can't be printed]
C69|11|cosd 90°|[drop either the ‘d’ or the ‘°’]
C80|14|**penpos**|*penpos*
C83|16|`-0.5b-c+1.5`|`-c-0.5b+1.5`
C97|10|E [logo10]|E [logo9]
C114|23|**of**|of
C115|19|*currentpicture*:=**nullpicture**|*currentpicture* := **nullpicture**
C116|8|**hide**|*hide*
C134|-4|*heart* [math italic]|*heart* [text italic]
C143|1|‘hide’|“hide”
C145|-5|*METAFONT* [logosl10]|*METAFONT* [logosl9]
C150|21|\| sin *θ*\|, \| cos *θ*\||\|sin *θ*\|, \|cos *θ*\|
C151|11|‘T’ [cmr9]|‘T’ [logo9]
C157|6|`begingroup`\<statement list\>\<expression\> `endgroup`|`begingroup`\<statement list\>\<expression\>`endgroup`
C157|25–27|?|*?*
C160|8–9|[break in the midst of `shifted`]|[break after `->`]
C163|1, 21|*ht* [math italic]|*ht* [text italic]
C163|-11–-10|*jut* [math italic]|*jut* [text italic]
C167|11|\<expression\> of \<primary\>|‘\<expression\> of \<primary\>’
C171|4|round(*n*)|round *n*
C172|-11|‘ **for** *x* = 1 **step** 2 **until** 0’ .|‘ **for** *x* = 1 **step** 2 **until** 0 ’.
C176|18|`(x3r, y3r)`|`(x3r,y3r)`
C176|-7|**if** `@#`(*x_*) : *tx_* **else** :|**if** `@#`(*x_*): *tx_* **else**:
C178|19|primarydef|**primarydef**
C178|21|secondarydef|**secondarydef**
C178|23|tertiarydef|**tertiarydef**
C180|-3|‘=’|‘=’ or ‘:=’
C183|25|**incr**|incr
C187|-11|\<pair primary\>|\<pair expression\>
C189|14|`"! "` and followed by `"."`|‘`! `’ and followed by ‘`.`’
C200|18|*autorounding*=*smoothing*=0|*autorounding* = *smoothing* = 0
C202|8|*max*|max
C202|26|penpos|*penpos*
C203|14|(*stem*,*curve*)|(*stem*, *curve*)
C203|21|*d*<sub>*n*</sub> := …*d*<sub>2</sub> := *d*<sub>1</sub>|*d*<sub>*n*</sub> := … := *d*<sub>2</sub> := *d*<sub>1</sub>
C206|14|*METAFONT* [logosl10]|*METAFONT* [logosl9]
C210|-1|‘`/`\<numeric token\>’\>|‘`/` \<numeric token\>’ \>
C214|-6|\<pair primary\>|\<pair expression\>
C218|-12|**let** [[= (; **let** ]] =)|**let** [[ = (; **let** ]] = )
C219|25|subscripts and attributes|["attribute" is an unexplained concept]
C224|9|<code>&lt;insert&gt;&nbsp;&nbsp;mode_setup</code>|<code>&lt;insert&gt;&nbsp;&nbsp;&nbsp;mode_setup</code>
\*C224|-10–-7|`259.0005`|`259.00049` [also reverse the order of the four lines]
C228|-9|`p.4,l.94`|`l.94`
C230|8|*tracingcommands* = 3|*tracingcommands* ≥ 3
C230|11|*tracingedges* = 1|*tracingedges* := 1
C235|8–17|*theta* [math italic]|*theta* [text italic]
C236|13|`bc`\_`d`|`bc_d`
C237|18–20|**or**|or
C237|22|false|**false**
C238|26|whatevers|`whatever`s
C241|2|`\mode="cheapo"`|`\mode=cheapo`
C242|-4–-2|**of**|of
C242|-1|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|7–8|**of**|of
C243|10|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|16|**begingroup**|**begingroup** **save** *region*;
C243|25|**beginchar**(*M*, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);|**beginchar**(`"M"`, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);
C243|28–29|(*origin* .. *z*1 .. *z*2 .. *z*3 .. *z*4 .. *z*5 .. *z*6 .. *z*7 ..<br>*origin* .. −*z*7 .. −*z*6 .. −*z*5 .. −*z*4 .. −*z*3 .. −*z*2 .. −*z*1 .. cycle)|(*origin* .. *z*<sub>1</sub> .. *z*<sub>2</sub> .. *z*<sub>3</sub> .. *z*<sub>4</sub> .. *z*<sub>5</sub> .. *z*<sub>6</sub> .. *z*<sub>7</sub> ..<br>*origin* .. −*z*<sub>7</sub> .. −*z*<sub>6</sub> .. −*z*<sub>5</sub> .. −*z*<sub>4</sub> .. −*z*<sub>3</sub> .. −*z*<sub>2</sub> .. −*z*<sub>1</sub> .. cycle)
C244|-10|*region*=**nullpicture**;|*region* = **nullpicture**;
C247|5|*hheight*<sup>#</sup>|*h_height*<sup>#</sup>
C247|-7–-6|?|*?*
C248|1|?|*?*
\*C250|11|**endfor**|**fi**
C250|13|a nonnegative even integer|an even integer
C251|-3|Iff|If and only if
C254|-10|`?`|[smallskip] `?`
C257|7|`yoffset`|`boundarychar`
C258|5|\<numeric\>`*`\<pair\>|\<numeric\> `*` \<pair\>
C259|13|\<modename\>|\<mode name\>
C260|4|`headerbytes`|`headerbyte`
C261|10|`makegrid(`\<pairs\>`)(`\<pairs\>`)`|`makegrid(`\<numerics\>`)(`\<numerics\>`)`
C261|11|`proofrulethickness` \<numeric\>|`proofrulethickness` \<numeric<sup>#</sup>\>
C262|-8|**hide**|*hide*
C267|8|‘superellipse’|‘*superellipse*’
C267|15|‘interpath’|‘*interpath*’
C287|-3|expandafters|**expandafter**s
C290|8|*dx* [math italic]|*dx* [text italic]
C293|24|solve|*solve*
C298|18–20|**tensepath**|*tensepath*
C305|14|`serif_fit`|`serif_fit#`
C305|15|`letter_fit`|`letter_fit#`
C318|-16–-15|\<label\>|\<label ending with `:`\>
C319|25|“spacefactor”|“space factor”
C323|27|**proofrule**|**proofrule**(*z*<sub>1</sub>, *z*<sub>2</sub>)
C324|2–3|≠|\<\>
C324|16|`[`*c.x*`]`|`[`*c*`.`*x*`]`
C324|7|[65.3]|`[65.3]`
C339|3|‘ß’, ‘æ’, ‘œ’, and &nbsp;ø’|‘ß’, ‘æ’, ‘œ’, and ‘ø’
C341|-14|`text`|`\text`
C358|left column|\*`turningnumber`, 111, 211, 257, *264*|\*`turningnumber`, 211, 257, *264*
mf.web|§107|((2<sup>29</sup>\**p*+*q*) **div** (2\**q*)|(2<sup>29</sup>\**p*+*q*) **div** (2\**q*)
\*mf.web|§323|the the log *n* factor|the log *n* factor
\*mf.web|§534|to to vertex *r*|to vertex *r*
mf.web|§632, §720|control sequence|macro
mf.web|§757|he|they [or rewrite the sentence]
mf.web|§798|a the|the

Syntax:
```
<numeric atom> ::= <numeric variable> | <numeric argument>
    | <numeric token primary>
    | <internal quantity>
    | normaldeviate
    | ( <numeric expression> )
    | begingroup <statement list> <numeric expression> endgroup
    | length <numeric primary> | length <pair primary>
    | length <path primary> | length <string primary>
    | ASCII <string primary> | oct <string primary> | hex <string primary>
    | <pair part> <pair primary> | <transform part> <transform primary>
    | angle <pair primary>
    | turningnumber <path primary> | totalweight <picture primary>
    | <numeric operator> <numeric primary>
    | directiontime <pair expression> of <path primary>
<numeric primary> ::= <numeric atom> [ <numeric expr> , <numeric expr> ]
    | <numeric atom not followed by `[ <numeric expr> , <numeric expr> ]'>
```

Bugs in Appendix I are too numerous to mention here.

General issues:
- inconsistent use of text italic and math italic for single-letter variables (e.g. page C245 line 5)
- inconsistent use of roman `%` and typewriter `%` in prettyprinted METAFONT programs
- inconsistent use of `\ldots` and `\cdots` contradicting *The TeXbook*'s advice (e.g. page C176, line 20; page C307, lines 12–13)
- space factor not turned off after code fragments (e.g. “gives ‘?’&nbsp; a fresh meaning” on page C247, lines -7–-6)
- *The TeXbook* uses thrice "his or her", and *TeX: The Program* uses twice "he or she", which are no longer gender-inclusive
