---
title: Latex Guide
description: 
published: true
date: 2023-05-24T07:08:41.095Z
tags: wikijs, latex, edit
editor: markdown
dateCreated: 2023-05-24T07:08:41.095Z
---

# 특수 문자

## 구별 부호

```
\dot{a}, \ddot{a}, \acute{a}, \grave{a} 
```
$$
\dot{a}, \ddot{a}, \acute{a}, \grave{a} \!
$$

```
\check{a}, \breve{a}, \tilde{a}, \bar{a} 
```
$$
\check{a}, \breve{a}, \tilde{a}, \bar{a} \!
$$

```
\hat{a}, \widehat{a}, \vec{a} 
```
$$
\hat{a}, \widehat{a}, \vec{a} \!
$$



## 산술함수

```latex
\exp_a b = a^b, \exp b = e^b, 10^m 
```
$$
\exp_a b = a^b, \exp b = e^b, 10^m \!
$$

```latex
\ln c, \lg d = \log e, \log_{10} f 
```
$$
\ln c, \lg d = \log e, \log_{10} f \!
$$

```latex
\sin a, \cos b, \tan c, \cot d, \sec e, \csc f
```
$$
\sin a, \cos b, \tan c, \cot d, \sec e, \csc f\!
$$

```latex
\arcsin h, \arccos i, \arctan j 
```
$$
\arcsin h, \arccos i, \arctan j \!
$$

```latex
\sinh k, \cosh l, \tanh m, \coth n 
```
$$
\sinh k, \cosh l, \tanh m, \coth n \!
$$

```
\operatorname{sh}\,k, \operatorname{ch}\,l, \operatorname{th}\,m, \operatorname{coth}\,n 
```
$$
\operatorname{sh}\,k, \operatorname{ch}\,l, \operatorname{th}\,m, \operatorname{coth}\,n \!
$$

```
\operatorname{argsh}\,o, \operatorname{argch}\,p, \operatorname{argth}\,q 
```
$$
\operatorname{argsh}\,o, \operatorname{argch}\,p, \operatorname{argth}\,q \!
$$

```latex
\sgn r, \left\vert s \right\vert 
```
$$
\sgn r, \left\vert s \right\vert \!
$$





## 상한과 하한

```latex
\min x, \max y, \inf s, \sup t 
```
$$
\min x, \max y, \inf s, \sup t \!
$$

```latex
\lim u, \liminf v, \limsup w 
```
$$
\lim u, \liminf v, \limsup w \!
$$

```latex
\dim p, \deg q, \det m, \ker\phi 
```
$$
\dim p, \deg q, \det m, \ker\phi \!
$$



## 투영

```latex
\Pr j, \hom l, \lVert z \rVert, \arg z 
```
$$
\Pr j, \hom l, \lVert z \rVert, \arg z \!
$$



## 미분

```latex
dt, \operatorname{d}\!t, \partial t, \nabla\psi
```
$$
dt, \operatorname{d}\!t, \partial t, \nabla\psi\!
$$

```latex
dy/dx, \operatorname{d}\!y/\operatorname{d}\!x, {dy \over dx}, {\operatorname{d}\!y\over\operatorname{d}\!x}, {\partial^2\over\partial x_1\partial x_2}y 
```
$$
dy/dx, \operatorname{d}\!y/\operatorname{d}\!x, {dy \over dx}, {\operatorname{d}\!y\over\operatorname{d}\!x}, {\partial^2\over\partial x_1\partial x_2}y \!
$$

```latex
\prime, \backprime, f^\prime, f', f'', f^{(3)}, \dot y, \ddot y 
```
$$
\prime, \backprime, f^\prime, f', f'', f^{(3)} \!, \dot y, \ddot y
$$



## 유사 문자 기호

```latex
\infty, \aleph, \complement, \backepsilon, \eth, \Finv, \hbar 
```
$$
\infty, \aleph, \complement, \backepsilon, \eth, \Finv, \hbar \!
$$

```latex
\Im, \imath, \jmath, \Bbbk, \ell, \mho, \wp, \Re, \circledS 
```
$$
\Im, \imath, \jmath, \Bbbk, \ell, \mho, \wp, \Re, \circledS \!
$$



## 모듈러 연산

```latex
s_k \equiv 0 \pmod{m} 
```
$$
s_k \equiv 0 \pmod{m} \!
$$

```latex
a\,\bmod\,b 
```
$$
a\,\bmod\,b \!
$$

```latex
\gcd(m, n), \operatorname{lcm}(m, n)
```
$$
\gcd(m, n), \operatorname{lcm}(m, n)
$$

```latex
\mid, \nmid, \shortmid, \nshortmid 
```
$$
\mid, \nmid, \shortmid, \nshortmid \!
$$



## 근호

```latex
\surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{x^3+y^3 \over 2} 
```
$$
\surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{x^3+y^3 \over 2} \!
$$




## 조합론

```latex
_{n}\mathrm{P}_{k} , _{n}\mathrm{C}_{k} , _{n}\mathrm{\Pi}_{k}, _{n}\mathrm{H}_{k}, P(n,k), S(n,k), \mathrm{P}_{k}^{n} 
```
$$
{}_n\mathrm{P}_{k}\;,\;_{n}\mathrm{C}_{k}\;, \;_{n}\mathrm{\Pi}_{k}\;, \;_{n}\mathrm{H}_{k}\;, \; P(n,k)\;, \; S(n,k)\;, \mathrm{P}_{k}^{n} 
$$



## 연산자

```latex
+, -, \pm, \mp, \dotplus 
```
$$
+, -, \pm, \mp, \dotplus \!
$$

```latex
\times, \div, \divideontimes, /, \backslash 
```
$$
\times, \div, \divideontimes, /, \backslash \!
$$

```latex
\cdot, * \ast, \star, \circ, \bullet 
```
$$
\cdot, * \ast, \star, \circ, \bullet \!
$$

```latex
\boxplus, \boxminus, \boxtimes, \boxdot 
```
$$
\boxplus, \boxminus, \boxtimes, \boxdot \!
$$

```latex
\oplus, \ominus, \otimes, \oslash, \odot
```
$$
\oplus, \ominus, \otimes, \oslash, \odot\!
$$

```latex
\circleddash, \circledcirc, \circledast 
```
$$
\circleddash, \circledcirc, \circledast \!
$$

```latex
\bigoplus, \bigotimes, \bigodot 
```
$$
\bigoplus, \bigotimes, \bigodot \!
$$



## 집합

```
\{ \}, \O \empty \emptyset, \varnothing 
```
$$
\{ \}, \O \empty \emptyset, \varnothing \!
$$

```latex
\in, \notin \not\in, \ni, \not\ni 
```
$$
\in, \notin \not\in, \ni, \not\ni \!
$$

```latex
\cap, \Cap, \sqcap, \bigcap 
```
$$
\cap, \Cap, \sqcap, \bigcap \!
$$

```latex
\cup, \Cup, \sqcup, \bigcup, \bigsqcup, \uplus, \biguplus 
```
$$
\cup, \Cup, \sqcup, \bigcup, \bigsqcup, \uplus, \biguplus \!
$$

```latex
\setminus, \smallsetminus, \times 
```
$$
\setminus, \smallsetminus, \times \!
$$

```latex
\subset, \not\subset, \Subset, \sqsubset 
```
$$
\subset, \not\subset, \Subset, \sqsubset \!
$$

```latex
\supset, \not\supset, \Supset, \sqsupset 
```
$$
\supset, \not\supset, \Supset, \sqsupset \!
$$

```latex
\subseteq, \nsubseteq, \subsetneq, \varsubsetneq, \sqsubseteq 
```
$$
\subseteq, \nsubseteq, \subsetneq, \varsubsetneq, \sqsubseteq \!
$$

```latex
\supseteq, \nsupseteq, \supsetneq, \varsupsetneq, \sqsupseteq 
```
$$
\supseteq, \nsupseteq, \supsetneq, \varsupsetneq, \sqsupseteq \!
$$

```latex
\subseteqq, \nsubseteqq, \subsetneqq, \varsubsetneqq 
```
$$
\subseteqq, \nsubseteqq, \subsetneqq, \varsubsetneqq \!
$$

```latex
\supseteqq, \nsupseteqq, \supsetneqq, \varsupsetneqq 
```
$$
\supseteqq, \nsupseteqq, \supsetneqq, \varsupsetneqq \!
$$



## 관계

```latex
=, \ne, \neq, \equiv, \not\equiv 
```
$$
=, \ne, \neq, \equiv, \not\equiv \!
$$

```latex
\doteq, \doteqdot,
``` ```latex
\overset{\underset{\mathrm{def}}{}}{=},
``` ```latex
:=
```
$$
\doteq, \doteqdot, \overset{\underset{\mathrm{def}}{}}{=}, := \!
$$

```latex
\sim, \nsim, \backsim, \thicksim, \simeq, \backsimeq, \eqsim, \cong, \ncong 
```
$$
\sim, \nsim, \backsim, \thicksim, \simeq, \backsimeq, \eqsim, \cong, \ncong \!
$$

```latex
\approx, \thickapprox, \approxeq, \asymp, \propto, \varpropto 
```
$$
\approx, \thickapprox, \approxeq, \asymp, \propto, \varpropto \!
$$

```latex
<, \nless, \ll, \not\ll, \lll, \not\lll, \lessdot 
```
$$
<, \nless, \ll, \not\ll, \lll, \not\lll, \lessdot \!
$$

```latex
>, \ngtr, \gg, \not\gg, \ggg, \not\ggg, \gtrdot 
```
$$
>, \ngtr, \gg, \not\gg, \ggg, \not\ggg, \gtrdot \!
$$

```latex
\le, \leq, \lneq, \leqq, \nleq, \nleqq, \lneqq, \lvertneqq 
```
$$
\le, \leq, \lneq, \leqq, \nleq, \nleqq, \lneqq, \lvertneqq \!
$$

```latex
\ge, \geq, \gneq, \geqq, \ngeq, \ngeqq, \gneqq, \gvertneqq 
```
$$
\ge, \geq, \gneq, \geqq, \ngeq, \ngeqq, \gneqq, \gvertneqq \!
$$

```latex
\lessgtr, \lesseqgtr, \lesseqqgtr, \gtrless, \gtreqless, \gtreqqless 
```
$$
\lessgtr, \lesseqgtr, \lesseqqgtr, \gtrless, \gtreqless, \gtreqqless \!
$$

```latex
\leqslant, \nleqslant, \eqslantless 
```
$$
\leqslant, \nleqslant, \eqslantless \!
$$

```latex
\geqslant, \ngeqslant, \eqslantgtr 
```
$$
\geqslant, \ngeqslant, \eqslantgtr \!
$$

```latex
\lesssim, \lnsim, \lessapprox, \lnapprox 
```
$$
\lesssim, \lnsim, \lessapprox, \lnapprox \!
$$

```latex
\gtrsim, \gnsim, \gtrapprox, \gnapprox 
```
$$
\gtrsim, \gnsim, \gtrapprox, \gnapprox \,
$$

```latex
\prec, \nprec, \preceq, \npreceq, \precneqq 
```
$$
\prec, \nprec, \preceq, \npreceq, \precneqq \!
$$

```latex
\succ, \nsucc, \succeq, \nsucceq, \succneqq 
```
$$
\succ, \nsucc, \succeq, \nsucceq, \succneqq \!
$$

```latex
\preccurlyeq, \curlyeqprec 
```
$$
\preccurlyeq, \curlyeqprec \,
$$

```latex
\succcurlyeq, \curlyeqsucc 
```
$$
\succcurlyeq, \curlyeqsucc \,
$$

```latex
\precsim, \precnsim, \precapprox, \precnapprox 
```
$$
\precsim, \precnsim, \precapprox, \precnapprox \,
$$

```latex
\succsim, \succnsim, \succapprox, \succnapprox 
```
$$
\succsim, \succnsim, \succapprox, \succnapprox \,
$$



## 기하

```latex
\parallel, \nparallel, \shortparallel, \nshortparallel 
```
$$
\parallel, \nparallel, \shortparallel, \nshortparallel \!
$$

```latex
\perp, \angle, \sphericalangle, \measuredangle, 45^\circ 
```
$$
\perp, \angle, \sphericalangle, \measuredangle, 45^\circ \!
$$

```latex
\Box, \blacksquare, \diamond, \Diamond \lozenge, \blacklozenge, \bigstar 
```
$$
\Box, \blacksquare, \diamond, \Diamond \lozenge, \blacklozenge, \bigstar \!
$$

```latex
\bigcirc, \triangle \bigtriangleup, \bigtriangledown 
```
$$
\bigcirc, \triangle \bigtriangleup, \bigtriangledown \!
$$

```latex
\vartriangle, \triangledown 
```
$$
\vartriangle, \triangledown\!
$$

```latex
\blacktriangle, \blacktriangledown, \blacktriangleleft, \blacktriangleright 
```
$$
\blacktriangle, \blacktriangledown, \blacktriangleleft, \blacktriangleright \!
$$

```latex
\bar{q}, \bar{abc}, \overline{q}, \overline{abc}, \stackrel\frown{AB}
```
$$
\bar{q}, \bar{abc}, \overline{q}, \overline{abc}, \! \stackrel\frown{AB}
$$



## 논리

```latex
\forall, \exists, \nexists 
```
$$
\forall, \exists, \nexists \!
$$

```latex
\therefore, \because, \And 
```
$$
\therefore \;, \because \;, \And \!
$$

```latex
\or \lor \vee, \curlyvee, \bigvee 
```
$$
\or \lor \vee, \curlyvee, \bigvee \!
$$

```latex
\and \land \wedge, \curlywedge, \bigwedge 
```
$$
\and \land \wedge, \curlywedge, \bigwedge \!
$$

```latex
\lnot \neg, \not\operatorname{R}, \bot, \top
```
$$
\lnot \neg, \not\operatorname{R}, \bot, \top \!
$$

```latex
\vdash \dashv, \vDash, \Vdash, \models 
```
$$
\vdash \dashv, \vDash, \Vdash, \models \!
$$

```latex
\Vvdash \nvdash \nVdash \nvDash \nVDash 
```
$$
\Vvdash \nvdash \nVdash \nvDash \nVDash \!
$$

```latex
\ulcorner \urcorner \llcorner \lrcorner 
```
$$
\ulcorner \urcorner \llcorner \lrcorner \,
$$



## 화살표

```latex
\Rrightarrow, \Lleftarrow 
```
$$
\Rrightarrow, \Lleftarrow \!
$$

```latex
\Rightarrow, \nRightarrow, \Longrightarrow \implies 
```
$$
\Rightarrow, \nRightarrow, \Longrightarrow \implies\!
$$

```latex
\Leftarrow, \nLeftarrow, \Longleftarrow 
```
$$
\Leftarrow, \nLeftarrow, \Longleftarrow \!
$$

```latex
\Leftrightarrow, \nLeftrightarrow, \Longleftrightarrow \iff 
```
$$
\Leftrightarrow, \nLeftrightarrow, \Longleftrightarrow \iff \!
$$

```latex
\Uparrow, \Downarrow, \Updownarrow 
```
$$
\Uparrow, \Downarrow, \Updownarrow \!
$$

```latex
\rightarrow \to, \nrightarrow, \longrightarrow 
```
$$
\rightarrow \to, \nrightarrow, \longrightarrow\!
$$

```latex
\leftarrow \gets, \nleftarrow, \longleftarrow 
```
$$
\leftarrow \gets, \nleftarrow, \longleftarrow\!
$$

```latex
\leftrightarrow, \nleftrightarrow, \longleftrightarrow 
```
$$
\leftrightarrow, \nleftrightarrow, \longleftrightarrow \!
$$

```latex
\uparrow, \downarrow, \updownarrow 
```
$$
\uparrow, \downarrow, \updownarrow \!
$$

```latex
\nearrow, \swarrow, \nwarrow, \searrow 
```
$$
\nearrow, \swarrow, \nwarrow, \searrow \!
$$

```latex
\mapsto, \longmapsto 
```
$$
\mapsto, \longmapsto \!
$$

```latex
\rightharpoonup \rightharpoondown \leftharpoonup \leftharpoondown \upharpoonleft \upharpoonright \downharpoonleft \downharpoonright \rightleftharpoons \leftrightharpoons
```
$$
\rightharpoonup \rightharpoondown \leftharpoonup \leftharpoondown \upharpoonleft \upharpoonright \downharpoonleft \downharpoonright \rightleftharpoons \leftrightharpoons \,\!
$$

```latex
\curvearrowleft \circlearrowleft \Lsh \upuparrows \rightrightarrows \rightleftarrows \rightarrowtail \looparrowright
```
$$
\curvearrowleft \circlearrowleft \Lsh \upuparrows \rightrightarrows \rightleftarrows \rightarrowtail \looparrowright \,\!
$$

```latex
\curvearrowright \circlearrowright \Rsh \downdownarrows \leftleftarrows \leftrightarrows \leftarrowtail \looparrowleft
```
$$
\curvearrowright \circlearrowright \Rsh \downdownarrows \leftleftarrows \leftrightarrows \leftarrowtail \looparrowleft \,\!
$$

```latex
\hookrightarrow \hookleftarrow \multimap \leftrightsquigarrow \rightsquigarrow \twoheadrightarrow \twoheadleftarrow 
```
$$
\hookrightarrow \hookleftarrow \multimap \leftrightsquigarrow \rightsquigarrow \twoheadrightarrow \twoheadleftarrow \!
$$



## 특수

```latex
\amalg \P \S \% \dagger \ddagger \ldots \cdots 
```
$$
\amalg \P \S \% \dagger \ddagger \ldots \cdots \!
$$

```latex
\smile \frown \wr \triangleleft \triangleright
```
$$
\smile \frown \wr \triangleleft \triangleright\!
$$

```latex
\diamondsuit, \heartsuit, \clubsuit, \spadesuit, \Game, \flat, \natural, \sharp 
```
$$
\diamondsuit, \heartsuit, \clubsuit, \spadesuit, \Game, \flat, \natural, \sharp \!
$$



## 삭제표시

```latex
\cancel{1} 
```
$$
\cancel{1}\;
$$




## 색깔

```latex
{\color{Blue}x^2}+{\color{Red}2x}-{\color{Green}1}
```
$$
{\color{Blue}x^2}+{\color{Red}2x}-{\color{Green}1}
$$



## 기타

```latex
\diagup \diagdown \centerdot \ltimes \rtimes \leftthreetimes \rightthreetimes 
```
$$
\diagup \diagdown \centerdot \ltimes \rtimes \leftthreetimes \rightthreetimes \!
$$

```latex
\eqcirc \circeq \triangleq \bumpeq \Bumpeq \doteqdot \risingdotseq \fallingdotseq 
```
$$
\eqcirc \circeq \triangleq \bumpeq \Bumpeq \doteqdot \risingdotseq \fallingdotseq \!
$$

```latex
\intercal \barwedge \veebar \doublebarwedge \between \pitchfork 
```
$$
\intercal \barwedge \veebar \doublebarwedge \between \pitchfork \!
$$

```latex
\vartriangleleft \ntriangleleft \vartriangleright \ntriangleright 
```
$$
\vartriangleleft \ntriangleleft \vartriangleright \ntriangleright \!
$$

```latex
\trianglelefteq \ntrianglelefteq \trianglerighteq \ntrianglerighteq 
```
$$
\trianglelefteq \ntrianglelefteq \trianglerighteq \ntrianglerighteq \!
$$

