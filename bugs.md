This is a list of bugs I found (so far) in the documentation of TeX and METAFONT. All of them are found in 2020 and reported to karl or tex-k, but of course I do not claim to be the first finder of them. In the page numbers, "A" stands for _The TeXbook_ and "C" stands for _The METAFONTbook_.

Page | line | Typo | Correction
-----|------|------|------------
A51|19|`‘‘` yields‘‘|`‘‘` yields ‘‘
A368|8|'*40*=`SP`|'*40* = `SP`
A457|right column|`[1]`, 23, <sub>119</sub>|`[1]` (progress report), 23, <sub>119</sub>
A475|left column|programs, for computers, 38, 165, 234|programs, for computers, 38, 165, *234*
Cx|-4|More about Macros|More About Macros
C80|14|**penpos**|*penpos*
C114|23|**of**|of
C115|19|*currentpicture*:=**nullpicture**|*currentpicture* := **nullpicture**
C116|8|**hide**|*hide*
C134|-4|*heart* [math italic]|*heart* [text italic]
C143|1|‘hide’|“hide”
C150|21|\| sin *θ*\|, \| cos *θ*\||\|sin *θ*\|, \|cos *θ*\|
C167|11|\<expression\> of \<primary\>|‘\<expression\> of \<primary\>’
C172|-11|‘ **for** *x* = 1 **step** 2 **until** 0’ .|‘ **for** *x* = 1 **step** 2 **until** 0 ’.
C183|25|**incr**|incr
C189|14|`"! "` and followed by `"."`|‘`! `’ and followed by ‘`.`’
C200|18|*autorounding*=*smoothing*=0|*autorounding* = *smoothing* = 0
C202|8|*max*|max
C202|26|penpos|*penpos*
C203|14|(*stem*,*curve*)|(*stem*, *curve*)
C203|21|*d*<sub>*n*</sub> := …*d*<sub>2</sub> := *d*<sub>1</sub>|*d*<sub>*n*</sub> := … := *d*<sub>2</sub> := *d*<sub>1</sub>
C218|-12|**let** [[= (; **let** ]] =)|**let** [[ = (; **let** ]] = )
C219|25|subscripts and attributes|["attribute" is an unexplained concept]
C230|8|*tracingcommands* = 3|*tracingcommands* ≥ 3
C235|8–17|*theta* [math italic]|*theta* [text italic]
C237|18–20|**or**|or
C242|-4–-2|**of**|of
C242|-1|**labels**(0,1,2,3,4);|**labels**(0, 1, 2, 3, 4);
C243|7–8|**of**|of
C243|25|**beginchar**(*M*, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);|**beginchar**(`"M"`, 1.25*in*<sup>#</sup>, .5*in*<sup>#</sup>, 0);
C243|28–29|(*origin* .. *z*1 .. *z*2 .. *z*3 .. *z*4 .. *z*5 .. *z*6 .. *z*7 ..<br>*origin* .. −*z*7 .. −*z*6 .. −*z*5 .. −*z*4 .. −*z*3 .. −*z*2 .. −*z*1 .. cycle)|(*origin* .. *z*<sub>1</sub> .. *z*<sub>2</sub> .. *z*<sub>3</sub> .. *z*<sub>4</sub> .. *z*<sub>5</sub> .. *z*<sub>6</sub> .. *z*<sub>7</sub> ..<br>*origin* .. −*z*<sub>7</sub> .. −*z*<sub>6</sub> .. −*z*<sub>5</sub> .. −*z*<sub>4</sub> .. −*z*<sub>3</sub> .. −*z*<sub>2</sub> .. −*z*<sub>1</sub> .. cycle)
C244|-10|*region*=**nullpicture**;|*region* = **nullpicture**;
C247|5|*hheight*<sup>#</sup>|*h_height*<sup>#</sup>
C257|7|`yoffset`|`boundarychar`
C259|13|\<modename\>|\<mode name\>
C260|4|`headerbytes`|`headerbyte`
C261|10|`makegrid(`\<pairs\>`)(`\<pairs\>`)`|`makegrid(`\<numerics\>`)(`\<numerics\>`)`
C262|-8|**hide**|*hide*
C267|8|‘superellipse’|‘*superellipse*’
C267|15|‘interpath’|‘*interpath*’
C298|18–20|**tensepath**|*tensepath*
C319|25|“spacefactor”|“space factor”
C324|16|`[`*c.x*`]`|`[`*c*`.`*x*`]`
C324|7|[65.3]|`[65.3]`
C339|3|‘ß’, ‘æ’, ‘œ’, and &nbsp;ø’|‘ß’, ‘æ’, ‘œ’, and ‘ø’
mf.web|§107|((2<sup>29</sup>\*p+q) **div** (2\*q)|(2<sup>29</sup>\*p+q) **div** (2\*q)
mf.web|§323|the the log *n* factor|the log *n* factor
mf.web|§534|to to vertex *r*|to vertex *r*

General issues:
- inconsistent use of text italic and math italic for single-letter variables (cf. page C245 line 5)
- inconsistent use of roman `%` and typewriter `%` in prettyprinted METAFONT programs
- space factor not turned off after code fragments (e.g. “gives ‘?’&nbsp; a fresh meaning” on page C247, lines -7–-6)