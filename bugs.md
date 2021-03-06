This is a list of bugs I found (so far) in the documentation of TeX and METAFONT. In the page numbers, "A" stands for _The TeXbook_ and "C" stands for _The METAFONTbook_.

## Bugs for the 2029 tuneup

Page | Line | Bug | Fix
-----|------|-----|----
A158|-12|˝28|˝29
A213|-13|character tokens|non-active character tokens
A274|4|overfull boxes|overfull hboxes
C72/C211|17/9|\<numeric atom not followed by `[` \<expression\> `,` \>|\<numeric atom not followed by ‘`[` \<expression\> `,`’ \>
C210|-13, -12|**expr** argument to a macro|argument to a macro, loop, etc. [any capsule, actually] 
C296|14|`fill`|`addto currentpicture contour` ([details](https://tug.org/pipermail/tex-k/2021-April/003541.html))

File | Section | Bug | Fix
-----|---------|-----|----
mf.web|101|0.250000|0.25000
mf.web|107|(2<sup>29</sup>\*_p_+_q_ ) **div**(2\*_q_)|(2<sup>29</sup>\*_p_+_q_)**div**(2\*_q_)
mf.web|289|, [in the denominator]|, [after the fraction]
gftodvi.web|160|`"/"` .. .`"8"`|`"/"` .. `"8"`

In addition to the typos listed above, _The TeXbook_ and _The METAFONTbook_ [use the terms “eye”, “mouth”, and “gullet” inconsistently](https://tug.org/pipermail/tex-k/2021-April/003531.html). Also, the description of `\if` and `\ifcat` on page A209 [is not very correct](https://tug.org/pipermail/tex-k/2021-March/003470.html). The truth is that after two unexpandable tokens are found, TeX replaces them by their current *meaning*. Then control sequences have (character code, category code) = (256, 0), except that `\relax` produced by `\noexpand`\<active character\> are reverted to the active character itself, which has category code 13.

## Bugs for the 2021 tuneup

### Technical errors

Page | Line | Bug | Fix
-----|------|-----|----
A215|26|`$`<sub>3</sub>|math shift
A252|6|redefining the control sequences|changing [the token lists]
A305|-1|`-\wd0}`|`-\wd0 }`
A341|-2|`\parindent`. Turn|`\parindent`.&nbsp;&nbsp;Turn
A342|12|three|five [`\␣` and `\char`]
A375|6–7|`\ht0}`|`\ht0 }`
A407|-5|`\penalty5000}`|`\penalty5000 }`
A420|11|`-.1ex }`|`-.1ex\relax}`
A423|16|`width0pt }`|`width0pt\relax}`
C68|9|`-36.16279`|[that value can't be printed]
C83|16|`-0.5b-c+1.5`|`-c-0.5b+1.5`
C83|19|0.75*b* + 0.5*c* + 0.75|0.5*c* + 0.75*b* + 0.75
C180|-3|‘=’|‘=’ or ‘:=’
C187|-11|\<pair primary\>|\<pair expression\>
C214|6|\<future pen primary\> → `pencircle`|\<future pen primary\> → \<future pen argument\><br>&nbsp;&nbsp;&nbsp;&nbsp;\| `pencircle`
C214|-6|\<pair primary\>|\<pair expression\>
C224|9|<code>&lt;insert&gt;&nbsp;&nbsp;mode_setup</code>|<code>&lt;insert&gt;&nbsp;&nbsp;&nbsp;mode_setup</code>
C243|16|**begingroup**|**begingroup** **save** *region*;
C243|25|**beginchar**(*M*, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);|**beginchar**(`"M"`, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);
C246|17|expands into|is equivalent to
C247|5|*hheight*<sup>#</sup>|*h_height*<sup>#</sup>
C249|17|**beginchar**(`"H"`, 13*u*<sup>#</sup>, *ht*<sup>#</sup>, 0);|**beginchar**(`"H"`, 13*u*<sup>#</sup>, *ht*<sup>#</sup>, 0);<br>**pickup** *broad_pen*;
C249|27|**fill** *bot_serif_edge*<sub>4</sub>|**filldraw** *bot_serif_edge*<sub>4</sub>
C250|13|a nonnegative even integer|an even integer
C254|-10|`?`|[smallskip] `?`
C257|7|`yoffset`|`boundarychar`
C260|4|`headerbytes`|`headerbyte`
C261|10|`makegrid(`\<pairs\>`)(`\<pairs\>`)`|`makegrid(`\<numerics\>`)(`\<numerics\>`)`
C289|20|`{{pair x cand x>(0,0)}}`|`{{(pair x) cand x>(0,0)}}`
C291|18|`setu_ u;`|`save u_; setu_ u;`
C292|-10|known *p* - *q*|known (*p* - *q*)
C293|-14–-13|When *c* → 0, the quantity *a*<sup>3</sup> + *b*<sup>3</sup> approaches −∞ when *c* is negative, +∞ when *c* is positive.|When *c* → 0, the quantity *a*<sup>3</sup> + *b*<sup>3</sup> approaches +∞ when *c* is negative, −∞ when *c* is positive.
C305|14|`serif_fit`|`serif_fit#`
C305|15|`letter_fit`|`letter_fit#`

File | Section | Bug | Fix
-----|---------|-----|----
mf.web|§632, §720|control sequence|macro
mf.web|§1096|**fontinfo**|**fontdimen**
mf.web|§1106|`fontinfo`|`fontdimen`

Change the definition of \<numeric primary\> on pages C72 and C211 to
> \<numeric primary\> → \<numeric atom\> `[` \<numeric expression\> `,` \<numeric expression\> `]`<br>
> &nbsp;&nbsp;&nbsp;&nbsp;| \<numeric atom not followed by ‘`[` \<numeric expression\> `,` \<numeric expression\> `]`’\>

and move the alternatives that begin with an operator to the definition of \<numeric atom\>. (This recursive approach ensures that expressions like 3 sqrt 3(9)[1, 2][3, 4][5, 6][7, 8] are properly handled.)

Exercise 8.1 of *The METAFONTbook* assumes that the ‘..’ operator is left-associative. In fact (*p* .. *q*) .. *r* is usually different from *p* .. *q* .. *r*. But I think this is a white lie.

Exercise 15.7 in *The METAFONTbook*: To make the program on page C144 work with nonsquare pixels, simply changing line 10 is not enough. Line 11 should also take *aspect_ratio* into account, either by using a plain METAFONT command (like line 10), or by doing the *aspect_ratio* adjustment manually, e.g. ‘**addto** *currentpicture* **also** *currentpicture* rotatedaround((.5*w*,.5*h*) yscaled *aspect_ratio*, -180)’.

The program on page C299 has three problems: (1) It doesn't work with *flex* due to naming conflict of the private variable *n_*. Solution: rename it to *N_*. (2) It doesn't work with *flex* even with (1) solved, due to ‘[…]’ evaluating its arguments twice when *N_* < 3, and due to *flex* saying ‘*z_*[incr *n_*]’ in its definition. Solution: change ‘**if** *N_* < 3: [[[*t*]]]’ to ‘**if** *N_* = 0: [[[]]] **elseif** *N_* = 1: [[[*u_*[[[1]]] ]]] **elseif** *N_* = 2: [[[*u_*[[[1]]], *u_*[[[2]]] ]]]’ on line 6 of the program. (3) See my article “Improvements to the generalized mediation macros in _The METAFONTbook_”, to appear in TUGboat 42:1.

### Typographical errors

Page | Line | Bug | Fix
-----|------|-----|----
A51|19|<code>``</code> yields“|<code>``</code> yields “
A164|-14|Exercise 17.20|exercise 17.20
A226|-7|filename|file name
A248|2|36em|36 em
A280|3, 6, 21|\<filename\>|\<file name\>
A350|30|he really wants|they really want
A368|8|'*40*=`SP`|'*40* = `SP`
A373|22|Chapter 24|Chapters 24–26
Cx|-4|More about Macros|More About Macros
C23|-9, -7|*ss* [math italic]|*ss* [text italic]
C28|12|*down* [math italic]|*down* [text italic]
C46|15|`\mode=smoke`; `input badio`|`\mode=smoke; input badio`
C50|27|`10000`?|`10000`.
C80|14|**penpos**|*penpos*
C97|10|E [logo10]|E [logo9]
C115|19|*currentpicture*:=**nullpicture**|*currentpicture* := **nullpicture**
C116|8|**hide**|*hide*
C130|26|*z*<sub>0</sub> .. *z*<sub>1</sub>{curl 1}&{curl 1}*z*<sub>1</sub> .. *z*<sub>2</sub> .. cycle|*z*<sub>0</sub> .. *z*<sub>1</sub>{curl 1} & {curl 1}*z*<sub>1</sub> .. *z*<sub>2</sub> .. cycle
C134|-4|*heart* [math italic]|*heart* [text italic]
C143|1|‘hide’|“hide”
C145|-5|*METAFONT* [logosl10]|*METAFONT* [logosl9]
C150|21|\| sin *θ*\|, \| cos *θ*\||\|sin *θ*\|, \|cos *θ*\|
C151|11|‘T’ [cmr9]|‘T’ [logo9]
C157|6|`begingroup`\<statement list\>\<expression\> `endgroup`|`begingroup`\<statement list\>\<expression\>`endgroup`
C160|8–9|[break in the midst of `shifted`]|[break after `->`]
C163|1, 21|*ht* [math italic]|*ht* [text italic]
C163|-11–-10|*jut* [math italic]|*jut* [text italic]
C167|11|\<expression\> of \<primary\>|‘\<expression\> of \<primary\>’
C172|-11|‘ **for** *x* = 1 **step** 2 **until** 0’ .|‘ **for** *x* = 1 **step** 2 **until** 0 ’.
C176|-7|**if** `@#`(*x_*) : *tx_* **else** : *fx_* **fi** := *x_*; **enddef**;|**if** `@#`(*x_*): *tx_* **else**: *fx_* **fi** := *x_*; **enddef**
C183|25|**incr**|incr
C189|14|`"! "` and followed by `"."`|‘`! `’ and followed by ‘`.`’
C200|18|*autorounding*=*smoothing*=0|*autorounding* = *smoothing* = 0
C202|8|*max*|max
C202|26|penpos|*penpos*
C203|14|(*stem*,*curve*)|(*stem*, *curve*)
C203|21|*d*<sub>*n*</sub> := …*d*<sub>2</sub> := *d*<sub>1</sub>|*d*<sub>*n*</sub> := … := *d*<sub>2</sub> := *d*<sub>1</sub>
C206|14|*METAFONT* [logosl10]|*METAFONT* [logosl9]
C210|-1|‘`/`\<numeric token\>’\>|‘`/` \<numeric token\>’ \>
C218|-12|**let** [[= (; **let** ]] =)|**let** [[ = (; **let** ]] = )
C219|25|subscripts and attributes|["attribute" is an unexplained concept]
C228|-3|proofmode|proof mode
C230|11|*tracingedges* = 1|*tracingedges* := 1
C235|8–17|*theta* [math italic]|*theta* [text italic]
C236|13|`bc`\_`d`|`bc_d`
C237|18–20|**or**|or
C237|22|false|**false**
C238|26|whatevers|`whatever`s
C242|-1|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|7–8|**of**|of
C243|10|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|28–29|(*origin* .. *z*1 .. *z*2 .. *z*3 .. *z*4 .. *z*5 .. *z*6 .. *z*7 ..<br>*origin* .. −*z*7 .. −*z*6 .. −*z*5 .. −*z*4 .. −*z*3 .. −*z*2 .. −*z*1 .. cycle)|(*origin* .. *z*<sub>1</sub> .. *z*<sub>2</sub> .. *z*<sub>3</sub> .. *z*<sub>4</sub> .. *z*<sub>5</sub> .. *z*<sub>6</sub> .. *z*<sub>7</sub> ..<br>*origin* .. −*z*<sub>7</sub> .. −*z*<sub>6</sub> .. −*z*<sub>5</sub> .. −*z*<sub>4</sub> .. −*z*<sub>3</sub> .. −*z*<sub>2</sub> .. −*z*<sub>1</sub> .. cycle)
C251|-3|Iff|If and only if
C258|5|\<numeric\>`*`\<pair\>|\<numeric\> `*` \<pair\>
C259|13|\<modename\>|\<mode name\>
C261|11|`proofrulethickness` \<numeric\>|`proofrulethickness` \<numeric<sup>#</sup>\>
C262|-8|**hide**|*hide*
C267|8|‘superellipse’|‘*superellipse*’
C267|15|‘interpath’|‘*interpath*’
C287|-3|expandafters|**expandafter**s
C288|-13, -6|Boolean|boolean
C290|8|*dx* [math italic]|*dx* [text italic]
C293|24|solve|*solve*
C298|13, -10|`--subpath(t,T) of r shifted .5up -- cycle`|`-- subpath(t,T) of r shifted .5up -- cycle`
C298|18–20|**tensepath**|*tensepath*
C307|-2|ad-hoc dimension|ad hoc dimension
C319|25|“spacefactor”|“space factor”
C324|16|`[`*c.x*`]`|`[`*c*`.`*x*`]`
C324|7|[65.3]|`[65.3]`
C339|3|‘ß’, ‘æ’, ‘œ’, and &nbsp;ø’|‘ß’, ‘æ’, ‘œ’, and ‘ø’

File | Section | Bug | Fix
-----|---------|-----|----
tex.web|§208|( `\kern`)|( `\kern` )
tex.web|§307|‘to be read again’.|‘to be read again’;
tex.web|§764|a 8 × 8 table|an 8 × 8 table
tex.web|§1062|\<`hlist`\>|\<hlist\>
mf.web|§107|((2<sup>29</sup> \* *p* + *q*) **div** (2 \* *q*)|(2<sup>29</sup> \* *p* + *q*) **div** (2 \* *q*)
mf.web|§632|‘to be read again’.|‘to be read again’;
mf.web|§757|he|they [or rewrite the sentence]
mf.web|§798|a the|the
mf.web|§798|node .|node.

Bugs in Appendix I of *The METAFONTbook* are too numerous to list exhausively, but here are the serious ones.

Entry | Fix
------|----
Boolean expressions, ….|boolean expressions, ….
\<declaration\>, 56, **171**.|\<declaration\>, **56**, 171.
\*`directiontime`, …, *295*.|\*`directiontime`, …, *298*.
\*`from` 191, ….|\*`from`, 191, ….
greatest integer function, *see* floor.|greatest integer function, *see* `floor`.
\<internal quantity\>, …, 265.|\<internal quantity\>, ….
Journal of Algorithms, ….|*Journal of Algorithms*, ….
\<keep or drop\>, …, 120.|\<keep or drop\>, …, 220.
labels on *proofmode* output, ….|labels on *proof* mode output, ….
least integer function, *see* ceiling.|least integer function, *see* `ceiling`.
\*`ligtable`, …, *305*, ….|\*`ligtable`, …, *305*–*306*, ….
`offset`, …, 379.|`offset`, …, 329.
pens, 21–39, ….|pens, 21–29, ….
\*`rotated`, …, 212, ….|\*`rotated`, …, 213, ….
`rule`, 234, ….|`rule`, ….
\*`scaled`, …, 212, ….|\*`scaled`, …, 213, ….
\*`turningnumber`, 111, ….|\*`turningnumber`, ….
undelimited suffix parameters, …, 265, ….|undelimited suffix parameters, …, 266, ….
\*`unknown`, 79–82, 143, ….|\*`unknown`, ….
\<with clause\>, …, 120.|\<with clause\>, …, 220.

General issues:
- inconsistent use of text italic vs math italic for single-letter variables (e.g. page C245 line 5)
- inconsistent use of roman ‘%’ vs typewriter ‘`%`’ in prettyprinted METAFONT programs
- inconsistent use of `\ldots` vs `\cdots` contradicting *The TeXbook*'s advice (e.g. page C176, line 20; page C307, lines 12–13)
- inconsistent use of *z*[*k*] vs *z*<sub><i>k</i></sub> inside loops like **for** *k* = 1 **upto** 4: … **endfor** ([details](https://tug.org/pipermail/tex-k/2020-July/003269.html))
- inconsistent use of ‘;’ vs ‘.’ at the end of programs (e.g. page C249)
- inconsistent use of ‘<>, <=, >=’ vs ‘≠, ≤, ≥’ in prettyprinted METAFONT programs ([details](https://tug.org/pipermail/tex-k/2020-August/003276.html))
- space factor not turned off after code fragments (e.g. “and ‘?’&nbsp;&nbsp;is restored” on page C247, lines -6)
- *The TeXbook* uses thrice "his or her", and *TeX: The Program* uses twice "he or she", which are no longer gender-inclusive

### Other people's bug reports I'm aware of

Page | Line | Bug | Fix
-----|------|-----|-----
C22|10|**draw** *z*<sub>1</sub>; **draw** *z*<sub>2</sub>|**draw** *z*<sub>1</sub>;&nbsp;&nbsp;**draw** *z*<sub>2</sub>
C68|-13|`(x+0.16667y,y)`|`(0.16667y+x,y)`
C114|23|**of**|of
[C224](https://tug.org/pipermail/tex-k/2018-December/002972.html)|-10–-7|`259.0005`|`259.00049` [also reverse the order of the four lines]
C241|2|`\mode="cheapo"`|`\mode=cheapo`
C242|-4–-2|**of**|of
C244|-10|*region*=**nullpicture**;|*region* = **nullpicture**;
C250|11|**endfor**|**fi**
C279|1|`blacker:=.2`|`blacker:=.1`
C318|-16–-15|\<label\>|\<label ending with `:`\>
[C333](https://tug.org/pipermail/tex-k/2019-October/003055.html)|-14|`fi"`|`fi "`
C341|-14|`text`|`\text`

File | Section | Bug | Fix
-----|---------|-----|----
mf.web|§323|the the log *n* factor|the log *n* factor
mf.web|§534|to to vertex *r*|to vertex *r*

### Bug that won't be fixed

Page A415, lines 24–25: change
```
\def\ninebig#1{{\hbox{$\textfont0=\tenrm\textfont2=\tensy
  \left#1\vbox to7.25pt{}\right.\n@space$}}}
```
to
```
\def\ninebig#1{{\vcenter{\hbox{$\textfont0=\tenrm\textfont2=\tensy
  \left#1\vbox to7.25pt{}\right.\n@space$}}}}
```
otherwise `\big` delimiters in nine-point formulas won't be vertically centered. (See page C298, line -1, or run the input `\input manmac \ninepoint $\bigl[ [] \bigr]$ \end`, for an example of this vertical asymmetry.)
