This is a list of bugs I found (so far) in the documentation of TeX and METAFONT. All of them were found in 2020 and reported to karl or tex-k, but of course I do not claim to be the first finder of them. In the page numbers, "A" stands for _The TeXbook_ and "C" stands for _The METAFONTbook_.

## Technical errors

Page | Line | Typo | Correction
-----|------|------|-----------
A305|-1|`-\wd0}`|`-\wd0 }`
A375|6–7|`\ht0}`|`\ht0 }`
A407|-5|`\penalty5000}`|`\penalty5000 }`
A420|11|`-.1ex }`|`-.1ex\relax}`
A423|16|`width0pt }`|`width0pt\relax}`
C68|9|`-36.16279`|[that value can't be printed]
C68|-13|`(x+0.16667y,y)`|`(0.16667y+x,y)`
C83|16|`-0.5b-c+1.5`|`-c-0.5b+1.5`
C83|19|0.75*b* + 0.5*c* + 0.75|0.5*c* + 0.75*b* + 0.75
C180|-3|‘=’|‘=’ or ‘:=’
C187|-11|\<pair primary\>|\<pair expression\>
C214|-6|\<pair primary\>|\<pair expression\>
C224|9|<code>&lt;insert&gt;&nbsp;&nbsp;mode_setup</code>|<code>&lt;insert&gt;&nbsp;&nbsp;&nbsp;mode_setup</code>
C230|8|*tracingcommands* = 3|*tracingcommands* ≥ 3
C241|2|`\mode="cheapo"`|`\mode=cheapo`
C243|16|**begingroup**|**begingroup** **save** *region*;
C243|25|**beginchar**(*M*, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);|**beginchar**(`"M"`, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);
C247|5|*hheight*<sup>#</sup>|*h_height*<sup>#</sup>
C250|1|\<statement list\>|\<statements\>
C250|13|a nonnegative even integer|an even integer
C254|-10|`?`|[smallskip] `?`
C257|7|`yoffset`|`boundarychar`
C260|4|`headerbytes`|`headerbyte`
C261|10|`makegrid(`\<pairs\>`)(`\<pairs\>`)`|`makegrid(`\<numerics\>`)(`\<numerics\>`)`
C291|18|`setu_ u`|`save u_; setu_ u`
C305|14|`serif_fit`|`serif_fit#`
C305|15|`letter_fit`|`letter_fit#`
C318|-16–-15|\<label\>|\<label ending with `:`\>
C323|27|**proofrule**|**proofrule**(*z*<sub>1</sub>, *z*<sub>2</sub>)
C341|-14|`text`|`\text`
mf.web|§632, §720|control sequence|macro

Proposed changes to the syntax rules in *The METAFONTbook*:
<ul>
<li>Change the definition of &lt;numeric primary&gt; to
<pre><code>&lt;numeric primary&gt; ::= &lt;numeric atom&gt; [ &lt;numeric expression&gt; , &lt;numeric expression&gt; ]
    | &lt;numeric atom not followed by `[ &lt;numeric expression&gt; , &lt;numeric expression&gt; ]'&gt;
</code></pre>
and move the alternatives that begin with an operator to the definition of &lt;numeric atom&gt;. (This recursive approach ensures that expressions like <code>3sqrt3(9)[1,2][3,4][5,6][7,8]</code> are properly handled.)</li>
<li>Add &lt;future pen argument&gt; as an alternative in the definition of &lt;future pen primary&gt;.</li>
</ul>

Exercise 15.7 in *The METAFONTbook*: To make the program on page C144 work with nonsquare pixels, simply changing line 10 is not enough. Line 11 should also take *aspect_ratio* into account, either by using a plain METAFONT command (like line 10), or by doing the *aspect_ratio* adjustment manually, e.g. **addto** *currentpicture* **also** *currentpicture* rotatedaround((.5*w*,.5*h*) yscaled *aspect_ratio*, −180).

The program on page C299 has three problems: (1) It doesn't work with *flex* due to naming conflict of the private variable *n_*. (2) It doesn't work with *flex* even with (1) solved, due to ‘[…]’ evaluating its arguments twice when *n_* < 3, and due to *flex* saying ‘*z_*[incr *n_*]’ in its definition. (3) It doesn't work with **show** when *n_* ≥ 3, since it calculates the Bernstein polynomial from a list of dependencies across the private array *u_*[]. For example, **show** .5[2*a*, 2*b*, 2*c*, 2*d*] prints the result as 0.75*b* + 0.25*a* + 0.75*u_*<sub>3</sub> − 0.25*u_*<sub>4</sub>, which is implicit even if it is correct:
> `*`**showdependencies**;<br>
> *u_*<sub>1</sub> = 0.75*b* + 0.25*a* + 0.75*u_*<sub>3</sub> − 0.25*u_*<sub>4</sub><br>
> *u_*<sub>2</sub> = 0.5*b* + *u_*<sub>3</sub> − 0.25*u_*<sub>4</sub><br>
> *d* = 0.5*u_*<sub>4</sub><br>
> *c* = *u_*<sub>3</sub> − 0.5*u_*<sub>4</sub>

The second problem can be solved by changing ‘**if** *n_* < 3: [[[*t*]]]’ to ‘**if** *n_* = 0: [[[]]] **elseif** *n_* = 1: [[[*u_*[[[1]]] ]]] **elseif** *n_* = 2: [[[*u_*[[[1]]], *u_*[[[2]]] ]]]’ on line 6 of the program. To solve the third problem, you can change *u_* from an array to a list macro:
> **def** *lbrack* = *hide*(**delimiters** []) *lookahead* [ **enddef**;<br>
> **let** [[[ = [; **let** ]]] = ]; **let** [ = *lbrack*;<br>
> **def** *lookahead*(**text** *t*) =<br>
> &nbsp;*hide*(**let** [ = *lbrack*;<br>
> &nbsp;&nbsp;**for** *u* = *t*, *hide*(*nn_* := 0; **let** *uu_* = \\): **if** incr *nn_* = 1: **def** *uu_* = *u* **enddef**<br>
> &nbsp;&nbsp;&nbsp;**else**: **expandafter** **def** **expandafter** *uu_* **expandafter** = *uu_*, *u* **enddef**<br>
> &nbsp;&nbsp;**fi**; **endfor**)<br>
> &nbsp;**if** *nn_* \< 3: [[[*uu_*]]] **else**: Bernshtein *nn_* **fi** **enddef**;<br>
> **primarydef** *t* Bernshtein *nn* = **begingroup** *c_*[[[1]]] := 1;<br>
> &nbsp;**for** *n* = 1 **upto** *nn* - 1: *c_*[[[*n* + 1]]] := *t* \* *c_*[[[*n*]]];<br>
> &nbsp;&nbsp;**for** *k* = *n* **downto** 2: *c_*[[[*k*]]] := *t*[[[*c_*[[[*k*]]], *c_*[[[*k* - 1]]] ]]];<br>
> &nbsp;&nbsp;**endfor** *c_*[[[1]]] := (1 - *t*) \* *c_*[[[1]]]; **endfor**<br>
> &nbsp;*nn_* := 0; **for** *u* = *uu_*: + *c_*[[[incr *nn_*]]] \* *u* **endfor** **endgroup** **enddef**;

Henceforth **show** .5[2*a*, 2*b*, 2*c*, 2*d*] prints 0.25*d* + 0.75*c* + 0.75*b* + 0.25*a*, and everyone will be happy. (The alternative definition of ‘Bernshtein’,
> **primarydef** *t* Bernshtein *nn* = **begingroup** *nn_* := 0; *f_* := *t*/(1 - *t*);<br>
> &nbsp;**def** *next_* = *co_* := takepower *nn* - 1 of (1 - *t*);<br>
> &nbsp;&nbsp;**def** *next_* = *co_* := *co_* \* *f_* \* (*nn* - incr *nn_*) / *nn_* **enddef** **enddef**;<br>
> &nbsp;**for** *u* = *uu_*: + **begingroup** *next_*; *co_* **endgroup** \* *u* **endfor** **endgroup** **enddef**;

also works whenever *t* ≠ 1, and that case isn't hard to patch.)

## Typographical errors

Page | Line | Typo | Correction
-----|------|------|-----------
A51|19|<code>``</code> yields“|<code>``</code> yields “
A164|-14|Exercise 17.20|exercise 17.20
A368|8|'*40*=`SP`|'*40* = `SP`
Cx|-4|More about Macros|More About Macros
C23|-9, -7|*ss* [math italic]|*ss* [text italic]
C28|12|*down* [math italic]|*down* [text italic]
C69|11|cosd 90°|cos 90°
C80|14|**penpos**|*penpos*
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
C172|-11|‘ **for** *x* = 1 **step** 2 **until** 0’ .|‘ **for** *x* = 1 **step** 2 **until** 0 ’.
C176|18|`(x3r, y3r)`|`(x3r,y3r)`
C176|-7|**if** `@#`(*x_*) : *tx_* **else** :|**if** `@#`(*x_*): *tx_* **else**:
C178|19|primarydef|**primarydef**
C178|21|secondarydef|**secondarydef**
C178|23|tertiarydef|**tertiarydef**
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
C242|-4–-2|**of**|of
C242|-1|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|7–8|**of**|of
C243|10|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|28–29|(*origin* .. *z*1 .. *z*2 .. *z*3 .. *z*4 .. *z*5 .. *z*6 .. *z*7 ..<br>*origin* .. −*z*7 .. −*z*6 .. −*z*5 .. −*z*4 .. −*z*3 .. −*z*2 .. −*z*1 .. cycle)|(*origin* .. *z*<sub>1</sub> .. *z*<sub>2</sub> .. *z*<sub>3</sub> .. *z*<sub>4</sub> .. *z*<sub>5</sub> .. *z*<sub>6</sub> .. *z*<sub>7</sub> ..<br>*origin* .. −*z*<sub>7</sub> .. −*z*<sub>6</sub> .. −*z*<sub>5</sub> .. −*z*<sub>4</sub> .. −*z*<sub>3</sub> .. −*z*<sub>2</sub> .. −*z*<sub>1</sub> .. cycle)
C244|-10|*region*=**nullpicture**;|*region* = **nullpicture**;
C247|-7–-6|?|*?*
C248|1|?|*?*
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
C298|18–20|**tensepath**|*tensepath*
C307|-2|ad-hoc dimension|ad hoc dimension
C319|25|“spacefactor”|“space factor”
C324|2–3|≠|\<\>
C324|16|`[`*c.x*`]`|`[`*c*`.`*x*`]`
C324|7|[65.3]|`[65.3]`
C339|3|‘ß’, ‘æ’, ‘œ’, and &nbsp;ø’|‘ß’, ‘æ’, ‘œ’, and ‘ø’
mf.web|§107|((2<sup>29</sup>\**p*+*q*) **div** (2\**q*)|(2<sup>29</sup>\**p*+*q*) **div** (2\**q*)
mf.web|§757|he|they [or rewrite the sentence]
mf.web|§798|a the|the

Bugs in Appendix I of *The METAFONTbook* are too numerous to list exhausively, but here are the serious ones. (Since GitHub Markdown doesn't support underlining, I'm using bold font instead.)
Entry | Correction
------|-----------
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
\*`unknown`, 79–82, ….|\*`unknown`, ….
\<with clause\>, …, 120.|\<with clause\>, …, 220.

General issues:
- inconsistent use of text italic and math italic for single-letter variables (e.g. page C245 line 5)
- inconsistent use of roman `%` and typewriter `%` in prettyprinted METAFONT programs
- inconsistent use of `\ldots` and `\cdots` contradicting *The TeXbook*'s advice (e.g. page C176, line 20; page C307, lines 12–13)
- inconsistent use of *z*[*k*] and *z*<sub><i>k</i></sub> inside loops like **for** *k* = 1 **upto** 4: … **endfor** ([details](https://tug.org/pipermail/tex-k/2020-July/003269.html))
- space factor not turned off after code fragments (e.g. “gives ‘?’&nbsp; a fresh meaning” on page C247, lines -7–-6)
- *The TeXbook* uses thrice "his or her", and *TeX: The Program* uses twice "he or she", which are no longer gender-inclusive

## Other people's bug reports I'm aware of

Page | Line | Typo | Correction
-----|------|------|------------
C224|-10–-7|`259.0005`|`259.00049` [also reverse the order of the four lines]
C250|11|**endfor**|**fi**
[C333](https://tug.org/pipermail/tex-k/2019-October/003055.html)|-14|`fi"`|`fi "`
mf.web|§323|the the log *n* factor|the log *n* factor
mf.web|§534|to to vertex *r*|to vertex *r*
