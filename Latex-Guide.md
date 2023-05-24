---
title: Latex Guide
description: 
published: true
date: 2023-05-24T08:16:08.949Z
tags: wikijs, latex, edit
editor: markdown
dateCreated: 2023-05-24T07:08:41.095Z
---

# 개요
본 가이드는 [latex wiki](https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:TeX_%EB%AC%B8%EB%B2%95)의 내용을 정리하였으며, 일반 텍스트로 노출되는 구문은 본 wikijs에서 지원하지 않는 것으로 보인다.

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
단, wikijs에서 \sgn 사용 불가
```

$$
\left\vert s \right\vert
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
\{ \}, \empty \emptyset, \varnothing 
```
$$
\{ \}, \empty \emptyset, \varnothing \!
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
\overset{\underset{\mathrm{def}}{}}{=},
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

단, wikijs 에서 \or 사용불가
```
$$
\lor \vee, \curlyvee, \bigvee \!
$$

```latex
\and \land \wedge, \curlywedge, \bigwedge 

단, wikijs 에서 \and 사용불가
```
$$
\land \wedge, \curlywedge, \bigwedge \!
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

## 위, 아래, 전치, 후치 첨자

```latex
a^2
``` 
$$
a^2
$$


```latex
y_m
```

$$
y_m
$$



```latex
x_s-x_D
```

$$
x_s-x_D
$$


```latex
a^{2+2}
``` 
$$
a^{2+2}
$$

```latex
a_{i,j}
``` 
$$
a_{i,j}
$$

### 위 아래 첨자 동시에 
```latex
x_2^3
``` 
$$
x_2^3
$$

### 위 가운데 첨자 
```latex
\overset{x}{P}
``` 
$$
\overset{x}{P}
$$

### 전치 위,아래 첨자 동시에 
```latex
{}_{b}^{a}X
``` 
$$
{}_{b}^{a}X
$$

### 전치,후치,위,아래 첨자 동시에 
```latex
_{c}^{a}Z_{d}^{b}
``` 
$$
_{c}^{a}Z_{d}^{b}
$$

### 전,후치,가운데,위,아래 첨자 동시에 
```latex
\underset{y}{\overset{x}{_{c}^{a}Z_{d}^{b}}}
``` 
$$
\underset{y}{\overset{x}{_{c}^{a}Z_{d}^{b}}}
$$

### 미분 (옳음) 
```latex
x'
``` 
$$
x'
$$

### 미분 (HTML의 경우 틀림) 
```latex
x^\prime
``` 
$$
x^\prime
$$

### 미분 (PNG의 경우 틀림) 
```latex
x\prime
``` 
$$
x\prime
$$

### 시그마
```latex
\sum_{k=1}^N k^2
``` 
$$
\sum_{k=1}^N k^2
$$

### 곱집합|곱기호
```latex
\prod_{i=1}^N x_i
``` 
$$
\prod_{i=1}^N x_i
$$

### 극한
```latex
\lim_{n \to \infty}x_n
``` 
$$
\lim_{n \to \infty}x_n
$$

### 적분
```latex
\int_{-N}^{N} e^x\, dx
``` 
$$
\int_{-N}^{N} e^x\, dx
$$

### 선적분
```latex
\oint_{C} x^3\, dx + 4y^2\, dy
```
$$
\oint_{C} x^3\, dx + 4y^2\, dy
$$


##  분수, 행렬, 여러행 


### 분수 
```latex
\frac{2}{4}
``` or ```latex
{2 \over 4}
``` 
$$
\frac{2}{4}
$$

### 이항 계수 
```latex
{n \choose k}
``` 
$$
{n \choose k}
$$

### 행렬
```latex
\begin{pmatrix} x & y \\ z & v \end{pmatrix}
```
$$
\begin{pmatrix} x & y \\ z & v \end{pmatrix}
$$

```latex
 \begin{bmatrix}
 0 & \cdots & 0 \\
 \vdots & \ddots & \vdots \\
 0 & \cdots & 0
 \end{bmatrix}
```
$$
 \begin{bmatrix}
 0 & \cdots & 0 \\
 \vdots & \ddots & \vdots \\
 0 & \cdots & 0
 \end{bmatrix}
$$

```latex
\begin{Bmatrix} x & y \\ z & v \end{Bmatrix}
```
$$
\begin{Bmatrix} x & y \\ z & v \end{Bmatrix}
$$

```latex
\begin{vmatrix} x & y \\ z & v \end{vmatrix}
```
$$
\begin{vmatrix} x & y \\ z & v \end{vmatrix}
$$

```latex
\begin{Vmatrix} x & y \\ z & v \end{Vmatrix}
```
$$
\begin{Vmatrix} x & y \\ z & v \end{Vmatrix}
$$

```latex
\begin{matrix} x & y \\ z & v \end{matrix}
```
$$
\begin{matrix} x & y \\ z & v \end{matrix}
$$

### 경우 나누기

```latex
 f(n)=
 \begin{cases}
 n/2, & \mbox{if }n\mbox{ is even} \\
 3n+1, & \mbox{if }n\mbox{ is odd}
 \end{cases}
 
 단, \mbox 가 wikijs에 적용되지 않아 다음 수식으로 대체
 f(n)=
 \begin{cases}
 n/2 & \mathrm{if\ }\ n\ \mathrm{ is\ even} \\
 3n+1, & \mathrm{if\ }\ n\ \mathrm{ is\ odd}
 \end{cases}
```
$$
 f(n)=
 \begin{cases}
 n/2 & \mathrm{if\ }\ n\ \mathrm{ is\ even} \\
 3n+1, & \mathrm{if\ }\ n\ \mathrm{ is\ odd}
 \end{cases}
$$

### 두줄 이상의 방정식
```latex
 \begin{matrix}
 f(n+1) &=& (n+1)^2 \\
        &=& n^2 + 2n + 1
 \end{matrix}
```
$$
\begin{matrix}f(n+1)&=& (n+1)^2 \\ \ & =& n^2 + 2n + 1\end{matrix}
$$


##  글꼴 


### 그리스어

```latex
\Alpha \Beta \Gamma \Delta \Epsilon \Zeta \Eta \Theta 
\Iota \Kappa \Lambda \Mu \Nu \Xi \Pi \Rho 
\Sigma \Tau \Upsilon \Phi \Chi \Psi \Omega 
\alpha \beta \gamma \delta \epsilon \zeta \eta \theta 
\iota \kappa \lambda \mu \nu \xi \pi \rho 
\sigma \tau \upsilon \phi \chi \psi \omega 
\varepsilon \digamma \varkappa \varpi 
```
$$
\Alpha \Beta \Gamma \Delta \Epsilon \Zeta \Eta \Theta \!
$$

$$
\Iota \Kappa \Lambda \Mu \Nu \Xi \Pi \Rho \!
$$

$$
\Sigma \Tau \Upsilon \Phi \Chi \Psi \Omega \!
$$

$$
\alpha \beta \gamma \delta \epsilon \zeta \eta \theta \!
$$

$$
\iota \kappa \lambda \mu \nu \xi \pi \rho \!
$$

$$
\sigma \tau \upsilon \phi \chi \psi \omega \!
$$

$$
\varepsilon \digamma \varkappa \varpi \!
$$

$$
\varrho \varsigma \vartheta \varphi \!
$$

### 히브리어

```latex
\aleph \beth \gimel \daleth 
```
$$
\aleph \beth \gimel \daleth \!
$$

### 칠판체 로마자

```latex
\mathbb{ABCDEFGHI} 
\mathbb{JKLMNOPQR} 
\mathbb{STUVWXYZ} 
```
$$
\mathbb{ABCDEFGHI} \!
$$

$$
\mathbb{JKLMNOPQR} \!
$$

$$
\mathbb{STUVWXYZ} \!
$$

### 볼드체 로마자

```latex
\mathbf{ABCDEFGHI} 
\mathbf{JKLMNOPQR} 
\mathbf{STUVWXYZ} 
\mathbf{abcdefghijklm} 
\mathbf{nopqrstuvwxyz} 
\mathbf{0123456789} 
```
$$
\mathbf{ABCDEFGHI} \!
$$

$$
\mathbf{JKLMNOPQR} \!
$$

$$
\mathbf{STUVWXYZ} \!
$$

$$
\mathbf{abcdefghijklm} \!
$$

$$
\mathbf{nopqrstuvwxyz} \!
$$

$$
\mathbf{0123456789} \!
$$

### 볼드체 그리스어

```latex
\boldsymbol{\Alpha\Beta\Gamma\Delta\Epsilon\Zeta\Eta\Theta} 
\boldsymbol{\Iota\Kappa\Lambda\Mu\Nu\Xi\Pi\Rho} 
\boldsymbol{\Sigma\Tau\Upsilon\Phi\Chi\Psi\Omega} 
\boldsymbol{\alpha\beta\gamma\delta\epsilon\zeta\eta\theta} 
\boldsymbol{\iota\kappa\lambda\mu\nu\xi\pi\rho} 
\boldsymbol{\sigma\tau\upsilon\phi\chi\psi\omega} 
\boldsymbol{\varepsilon\digamma\varkappa\varpi} 
\boldsymbol{\varrho\varsigma\vartheta\varphi} 
```
$$
\boldsymbol{\Alpha\Beta\Gamma\Delta\Epsilon\Zeta\Eta\Theta} \!
$$

$$
\boldsymbol{\Iota\Kappa\Lambda\Mu\Nu\Xi\Pi\Rho} \!
$$

$$
\boldsymbol{\Sigma\Tau\Upsilon\Phi\Chi\Psi\Omega} \!
$$

$$
\boldsymbol{\alpha\beta\gamma\delta\epsilon\zeta\eta\theta} \!
$$

$$
\boldsymbol{\iota\kappa\lambda\mu\nu\xi\pi\rho} \!
$$

$$
\boldsymbol{\sigma\tau\upsilon\phi\chi\psi\omega} \!
$$

$$
\boldsymbol{\varepsilon\digamma\varkappa\varpi} \!
$$

$$
\boldsymbol{\varrho\varsigma\vartheta\varphi} \!
$$

### 기울임체 로마자

```latex
\mathit{0123456789} 
```
$$
\mathit{0123456789} \!
$$

### 기울임체 그리스어

```latex
\mathit{\Alpha\Beta\Gamma\Delta\Epsilon\Zeta\Eta\Theta} 
\mathit{\Iota\Kappa\Lambda\Mu\Nu\Xi\Pi\Rho} 
\mathit{\Sigma\Tau\Upsilon\Phi\Chi\Psi\Omega} 
```
$$
\mathit{\Alpha\Beta\Gamma\Delta\Epsilon\Zeta\Eta\Theta} \!
$$

$$
\mathit{\Iota\Kappa\Lambda\Mu\Nu\Xi\Pi\Rho} \!
$$

$$
\mathit{\Sigma\Tau\Upsilon\Phi\Chi\Psi\Omega} \!
$$

### 로만체

```latex
\mathrm{ABCDEFGHI} 
\mathrm{JKLMNOPQR} 
\mathrm{STUVWXYZ} 
\mathrm{abcdefghijklm} 
\mathrm{nopqrstuvwxyz} 
\mathrm{0123456789} 
```
$$
\mathrm{ABCDEFGHI} \!
$$

$$
\mathrm{JKLMNOPQR} \!
$$

$$
\mathrm{STUVWXYZ} \!
$$

$$
\mathrm{abcdefghijklm} \!
$$

$$
\mathrm{nopqrstuvwxyz} \!
$$

$$
\mathrm{0123456789} \!
$$

### 산세리프체

```latex
\mathsf{ABCDEFGHI} 
\mathsf{JKLMNOPQR} 
\mathsf{STUVWXYZ} 
\mathsf{abcdefghijklm} 
\mathsf{nopqrstuvwxyz} 
\mathsf{0123456789} 
```
$$
\mathsf{ABCDEFGHI} \!
$$

$$
\mathsf{JKLMNOPQR} \!
$$

$$
\mathsf{STUVWXYZ} \!
$$

$$
\mathsf{abcdefghijklm} \!
$$

$$
\mathsf{nopqrstuvwxyz} \!
$$

$$
\mathsf{0123456789} \!
$$

### 산세리프체 그리스어

```latex
\mathsf{\Alpha \Beta \Gamma \Delta \Epsilon \Zeta \Eta \Theta} 
\mathsf{\Iota \Kappa \Lambda \Mu \Nu \Xi \Pi \Rho} 
\mathsf{\Sigma \Tau \Upsilon \Phi \Chi \Psi \Omega}
```
$$
\mathsf{\Alpha \Beta \Gamma \Delta \Epsilon \Zeta \Eta \Theta} \!
$$

$$
\mathsf{\Iota \Kappa \Lambda \Mu \Nu \Xi \Pi \Rho} \!
$$

$$
\mathsf{\Sigma \Tau \Upsilon \Phi \Chi \Psi \Omega}\!
$$

### 흘림체

```latex
\mathcal{ABCDEFGHI} 
\mathcal{JKLMNOPQR} 
\mathcal{STUVWXYZ} 
```
$$
\mathcal{ABCDEFGHI} \!
$$

$$
\mathcal{JKLMNOPQR} \!
$$

$$
\mathcal{STUVWXYZ} \!
$$

### 흑자체

```latex
\mathfrak{ABCDEFGHI} 
\mathfrak{JKLMNOPQR} 
\mathfrak{STUVWXYZ} 
\mathfrak{abcdefghijklm} 
\mathfrak{nopqrstuvwxyz} 
\mathfrak{0123456789} 
```
$$
\mathfrak{ABCDEFGHI} \!
$$
$$
\mathfrak{JKLMNOPQR} \!
$$
$$
\mathfrak{STUVWXYZ} \!
$$
$$
\mathfrak{abcdefghijklm} \!
$$
$$
\mathfrak{nopqrstuvwxyz} \!
$$
$$
\mathfrak{0123456789} \!
$$


### 작은 글자

```latex
{\scriptstyle\text{abcdefghijklm}}
```
$$
{\scriptstyle\text{abcdefghijklm}}
$$


##  괄호 쓰기 
```latex
\left ( \frac{1}{2} \right )
```
$$
\left ( \frac{1}{2} \right )
$$

> `\left` 와 `\right` 를 사용하여, 여러가지 괄호를 사용할 수 있습니다. 


### 괄호
```latex
\left( A \right)
``` 
$$
\left( A \right)
$$

### 사각 괄호 
```latex
\left[ A \right]
``` 
$$
\left[ A \right]
$$

### 집합괄호
```latex
\left\{ A \right\}
```
$$
\left\{ A \right\}
$$

### 부등호 괄호 
```latex
\left\langle A \right\rangle
```
$$
\left\langle A \right\rangle
$$

### 바 
```latex
\left| A \right|
```
$$
\left| A \right|
$$

### `\left.` 혹은 `\right.` 라고 쓰면, 그 쪽 괄호는 나타나지 않습니다.
```latex
\left. {A \over B} \right\} \to X
```
$$
\left. {A \over B} \right\} \to X
$$

### 내림수와 올림수 기호
```latex
\lfloor\sqrt{n}\rfloor  \lceil\sqrt{n}\rceil
```
$$
\lfloor\sqrt{n}\rfloor \quad \lceil\sqrt{n}\rceil
$$


##  빈칸 조정 
TeX은 빈칸의 크기를 자동으로 조정합니다. 특별히 조정이 필요한 경우는 다음을 사용하면 됩니다.

### double quad space 
```latex
a \qquad b
``` 
$$
a \qquad b
$$

### quad space 
```latex
a \quad b
``` 
$$
a \quad b
$$

### text space 
```latex
a\ b
``` 
$$
a\ b
$$

### large space 
```latex
a\;b
``` 
$$
a\;b
$$

### small space 
```latex
a\,b
``` 
$$
a\,b
$$

### no space 
```latex
ab
``` 
$$
ab\,
$$

### negative space 
```latex
a\!b
``` 
$$
a\!b
$$

