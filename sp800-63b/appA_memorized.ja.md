<a name="appA"></a>

## 付録 A&mdash;記憶シークレットの強度
<!--
## Appendix A&mdash;Strength of Memorized Secrets
-->

*本付録は参考情報である.*
<!--
*This appendix is informative.*
-->

本付録を通じて，ディスカッションを容易にするため"パスワード"という単語を用いる．使用箇所では，パスワード同様にパスフレーズおよびPINを含むものとして解釈すべきである．
<!--
Throughout this appendix, the word "password" is used for ease of discussion. Where used, it should be interpreted to include passphrases and PINs as well as passwords.
-->

### A.1 Introduction

ユーザビリティとセキュリティの立場の両面からパスワードの利用は大きな不満を伴うにも関わらず，Authenticationの形式 [[Persistance]](#persistence) として極めて広く利用され続けている．人間は，しかしながら，複雑で任意のシークレットを記憶する能力が限られているため，しばしば容易に推測できるパスワードを選ぶことがある．その結果発生するセキュリティ上の問題に対処するため，オンラインサービスでは，これらの記憶シークレットの複雑さを増加させる努力として，ルールが導入されてきた．最も注目すべき形式としては，ユーザがパスワードを選択する際に，少なくとも1文字以上の数字，大文字，記号のような文字種を組み合わせて作成するよう求める構成ルールがある．しかし，漏洩したパスワードデータベースの分析により，そのようなルールでは，ユーザビリティと記憶難易度へ与える影響はあれど，当初 [[ポリシー]](#policies) で考えられていたほど得られる利益が大きくないことが明らかになった．
<!--
Despite widespread frustration with the use of passwords from both a usability and security standpoint, they remain a very widely used form of authentication [[Persistence]](#persistence). Humans, however, have only a limited ability to memorize complex, arbitrary secrets, so they often choose passwords that can be easily guessed. To address the resultant security concerns, online services have introduced rules in an effort to increase the complexity of these memorized secrets. The most notable form of these is composition rules, which require the user to choose passwords constructed using a mix of character types, such as at least one digit, uppercase letter, and symbol. However, analyses of breached password databases reveal that the benefit of such rules is not nearly as significant as initially thought [[Policies]](#policies), although the impact on usability and memorability is severe.
-->

ユーザが選択したパスワードの複雑さは，エントロピー [[Shannon]](#shannon) という情報理論の概念を用いて特徴づけられることが多い．確定的分布関数に従うデータに対するエントロピーを計算することは容易だが，ユーザが選択したパスワードのエントロピーを推測することは難しく，それを行うための過去の努力は特に正確ではない．このため，主にパスワードの長さの観点で差があり少しシンプルになっているアプローチがここに示されている．
<!--
Complexity of user-chosen passwords has often been characterized using the information theory concept of entropy [[Shannon]](#shannon). While entropy can be readily calculated for data having deterministic distribution functions, estimating the entropy for user-chosen passwords is difficult and past efforts to do so have not been particularly accurate. For this reason, a different and somewhat simpler approach, based primarily on password length, is presented herein.
-->

パスワードの利用に関連する多くの攻撃はパスワードの複雑さと長さに影響をうけない．キー入力ロギング，フィッシング，ソーシャルエンジニアリング攻撃は，複雑で長いパスワードに対しても，それがシンプルなものであるのと同様に作用する．これらの攻撃は本付録の対象外である．
<!--
Many attacks associated with the use of passwords are not affected by password complexity and length. Keystroke logging, phishing, and social engineering attacks are equally effective on lengthy, complex passwords as simple ones. These attacks are outside the scope of this Appendix.
-->

### A.2 長さ
<!--
### A.2 Length
-->

パスワードの長さは，パスワードの強度 [[Strength]](#strength) [[Composition]](#composition) を特徴付ける主要因であることがわかっている．短すぎるパスワードは単語や一般的に選択されたパスワードを利用する辞書攻撃と同様にブルートフォース攻撃をももたらす．
<!--
Password length has been found to be a primary factor in characterizing password strength [[Strength]](#strength) [[Composition]](#composition). Passwords that are too short yield to brute force attacks as well as to dictionary attacks using words and commonly chosen passwords.
-->

最低でもどの程度の長さのパスワードが必要となるかは，想定する脅威モデルによって大きく左右される．攻撃者がパスワードを推測してログインを試みるオンライン攻撃では，許容するログイン試行回数に対してレート制限をかけることで緩和することができる．攻撃者(またはしつこくタイプミスを繰り返すClaimant)が大量の誤ったパスワード推測を行いSubscriberに対するDoS攻撃を容易に行えないようにするためには，そこまで誤った試行回数が多くはないのであればレート制限を発生させなくても済むほど十分複雑である必要がある．とはいえ，推測が成功する確率が大きくなる前にレート制限は発生する．
<!--
The minimum password length that should be required depends to a large extent on the threat model being addressed. Online attacks where the attacker attempts to log in by guessing the password can be mitigated by limiting the rate of login attempts permitted. In order to prevent an attacker (or a persistent claimant with poor typing skills) from easily inflicting a denial-of-service attack on the subscriber by making many incorrect guesses, passwords need to be complex enough that rate limiting does not occur after a modest number of erroneous attempts, but does occur before there is a significant chance of a successful guess.
-->

オフライン攻撃は，攻撃者がデータベース侵害を通じて1つ以上のハッシュされたパスワードを得た場合に発生する可能性がある．攻撃者が1人以上のユーザのパスワードを決定する能力は，パスワードの記録方法によって異なる．一般的には，パスワードはランダム値を用いてソルトを追加したうえでハッシュ化され，そのために計算コストが高いアルゴリズムを用いることが望ましい．そのような基準でさえも，レート制限なしで毎秒何十億もの計算を行うことができる現在の攻撃者の能力に対抗するためには，パスワードはオンライン攻撃だけに対抗することを想定するよりも複雑で大きなオーダーである必要がある．
<!--
Offline attacks are sometimes possible when one or more hashed passwords is obtained by the attacker through a database breach. The ability of the attacker to determine one or more users' passwords depends on the way in which the password is stored. Commonly, passwords are salted with a random value and hashed, preferably using a computationally expensive algorithm. Even with such measures, the current ability of attackers to compute many billions of hashes per second with no rate limiting requires passwords intended to resist such attacks to be orders of magnitude more complex than those that are expected to resist only online attacks.
-->

ユーザは，こういった理由もあり，望みどおり長いパスワードが使えるよう促進されるべきである．ハッシュされたパスワードの長さはパスワードそのものの長さと無関係であるため，長いパスワード(またはパスフレーズ)の利用を許可しない理由はない．極端に長いパスワード(おそらくはメガバイト)はハッシュ処理に極端に時間を要すると考えられるため，何らかの制限を行うのは適切なことである．
<!--
Users should be encouraged to make their passwords as lengthy as they want, within reason. Since the size of a hashed password is independent of its length, there is no reason not to permit the use of lengthy passwords (or pass phrases) if the user wishes. Extremely long passwords (perhaps megabytes in length) could conceivably require excessive processing time to hash, so it is reasonable to have some limit.
-->

### A.3 複雑さ
<!--
### A.3 Complexity
-->

上記のように，構成ルールはユーザが選択したパスワードの推測難易度を上げる目的で一般的に利用される．しかしながら，研究者はユーザが構成ルール [[Policies]](#policies) で課せられた要件に対してかなり予測可能な方法で応答することを示した．例えば，パスワードとして"password"を選択したユーザは，大文字と数字を含む要件を与えると，比較的高い確率で"Password1"を選択し，記号を要件に追加すると"Password1!"を選択する．
<!--
As noted above, composition rules are commonly used in an attempt to increase the difficulty of guessing user-chosen passwords. Research has shown, however, that users respond in very predictable ways to the requirements imposed by composition rules [[Policies]](#policies). For example, a user that might have chosen "password" as their password would be relatively likely to choose "Password1" if required to include an uppercase letter and a number, or "Password1!" if a symbol is also required.
-->

複雑なパスワードを作成しようとしてオンラインサービスにそれを拒否されるとユーザも不満を抱く．多くのサービスではスペースや様々な特殊文字を含むパスワードを拒否する．場合により，特殊文字が受け入れられないことがあるが，それは特殊文字を用いるSQLインジェクションのような攻撃を回避するためである．しかし，適切にハッシュ化されたパスワードはいかなる場合でもそのままデータベースに送信されることはないので，そのような予防策は不要である．ユーザはフレーズの利用を許容するためにスペースを使ってもよい．しかし，スペースはそれ自体ではパスワードの複雑さを僅かに増加させるにすぎず，ユーザビリティの問題(例えば，1つの場合に比べて2つのスペースを利用したことが検出されないなど)を招く可能性があるため，検証時は事前に入力されたパスワードから連続するスペースを削除すると効果的である．
<!--
Users also express frustration when attempts to create complex passwords are rejected by online services. Many services reject passwords with spaces and various special characters. In some cases, the special characters that are not accepted might be an effort to avoid attacks like SQL injection that depend on those characters. But a properly hashed password would not be sent intact to a database in any case, so such precautions are unnecessary. Users should also be able to include space characters to allow the use of phrases. Spaces themselves, however, add little to the complexity of passwords and may introduce usability issues (e.g., the undetected use of two spaces rather than one), so it may be beneficial to remove repeated spaces in typed passwords prior to verification.
-->

ユーザのパスワードの選択は非常に予想可能であり，攻撃者は過去に成功した正しいパスワードを推測する可能性がある．これらのパスワードには，辞書の単語や上記例の"Password1!"のような過去に漏洩したパスワード，このような状況から，ユーザが選択したパスワードは許容できないパスワードのブラックリストと比較することが望ましい．このブラックリストは，ユーザが選択する可能性が高い，過去に漏洩したパスワード，語彙集，辞書の単語および特定の用語(サービス自体の名前など)を含むべきである．ユーザのパスワードの選択は最低文字の要件が適用されるため，この辞書は要件に合致したものだけを含んでいる必要がある．
<!--
Users' password choices are very predictable, so attackers are likely to guess passwords that have been successful in the past. These include dictionary words and passwords from previous breaches, such as the "Password1!" example above. For this reason, it is recommended that passwords chosen by users be compared against a "black list" of unacceptable passwords. This list should include passwords from previous breach corpuses, dictionary words, and specific words (such as the name of the service itself) that users are likely to choose. Since user choice of passwords will also be governed by a minimum length requirement, this dictionary need only include entries meeting that requirement.
-->

極端に複雑な記憶シークレットは新たな潜在的な脆弱性を生み出す: シークレットを記憶できる可能性が減り，書き留めたり安全でない方法で電子的に記録する可能性が高まる．これらの慣例は必ずしも脆弱であるわけではないが，統計的にそのようなシークレットの記録方法のなかには脆弱なものがある．これは，極端に長い、または極端に複雑な記憶シークレットを要求しないということの追加の動機付けになる．
<!--
Highly complex memorized secrets introduce a new potential vulnerability: they are less likely to be memorable, and it is more likely that they will be written down or stored electronically in an unsafe manner. While these practices are not necessarily vulnerable, statistically some methods of recording such secrets will be. This is an additional motivation not to require excessively long or complex memorized secrets.
-->

### A.4 ランダムに選択されたシークレット
<!--
### A.4 Randomly-Chosen Secrets
-->

記憶シークレットの強度を決定するもう一つの要素が，それが生成されるプロセスである．(VerifierやCSPでは殆どの場合)分布が一様でランダムなシークレットでは、同じ長さと複雑さ要件に対してユーザが選択するシークレットに比べてパスワード推測やブルートフォース攻撃の難易度が高くなるだろう．従って，SP 800-63-2のLOA2ではランダムに選択された6桁の数字のPINが許容されるのに対し，ユーザが選択したシークレットの場合は最低8文字という要件になっている．
<!--
Another factor that determines the strength of memorized secrets is the process by which they are generated. Secrets that are randomly chosen (in most cases by the verifier or CSP) and are uniformly distributed will be more difficult to guess or brute-force attack than user-chosen secrets meeting the same length and complexity requirements. Accordingly, at LOA2, SP 800-63-2 permitted the use of randomly generated PINs with 6 or more digits while requiring user-chosen memorized secrets to be a minimum of 8 characters long.
-->

上で論じたように，記憶シークレットの長さ要件に考慮された脅威モデルには，オンライン攻撃に対するレート制限が含まれているが，オフライン攻撃は含まれていない．この制約があるものの，6桁のランダムに生成されたPINは記憶シークレットに対しては引き続き適切であるとみなされる．
<!--
As discussed above, the threat model being addressed with memorized secret length requirements includes rate-limited online attacks, but not offline attacks. With this limitation, 6 digit randomly-generated PINs are still considered adequate for memorized secrets.
-->

### A.5 サマリ
<!--
### A.5 Summary
-->

ここで推奨されている内容を超えた長さと複雑さの要件は，記憶シークレットの難易度を大幅に増加させ，ユーザの不満を増加させる．結果としてユーザはしばしばこれらの制限を回避してしまうため，逆効果である． 更に，ブラックリスト，安全なハッシュストレージ，レート制限などの他の緩和策は，のブルートフォース攻撃をためにより効果的です．したがって，複雑さについて追加の要件が課されることはない．
<!--
Length and complexity requirements beyond those recommended here significantly increase the difficulty of memorized secrets and increase user frustration. As a result, users often work around these restrictions in a way that is counterproductive. Furthermore, other mitigations such as blacklists, secure hashed storage, and rate limiting are more effective at preventing modern brute-force attacks. Therefore, no additional complexity requirements are imposed.
-->
