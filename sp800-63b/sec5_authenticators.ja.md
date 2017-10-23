<a name="sec5"></a>

## 5 <a name="AAL_SEC5"></a>Authenticator及びVerifier要件
<!--
## 5 <a name="AAL_SEC5"></a>Authenticator and Verifier Requirements
-->

_本セクションは標準である．_
<!--
_This section is normative._
-->

本セクションでは，各Authenticatorタイプごとの要件詳細について記載する．[Section 4](#AAL_SEC4)で指定されたReauthentication要件及び[Section 5.2.5]に記載があるAAL3におけるVerifierなりすまし耐性の例外を除いて，各Authenticatorタイプ毎の技術要件はAuthenticatorが利用されるAALに関わらず同様である．

<!--
This section provides the detailed requirements specific to each type of authenticator. With the exception of reauthentication requirements specified in [Section 4](#AAL_SEC4) and the requirement for verifier impersonation resistance at AAL3 described in [Section 5.2.5](#verifimpers), the technical requirements for each of the authenticator types are the same regardless of the AAL at which the authenticator is used.
-->

### <a name="reqauthtype"></a> 5.1 Authenticatorタイプ毎の要件
<!--
### <a name="reqauthtype"></a> 5.1 Requirements by Authenticator Type
-->

#### <a name="memsecret"></a> 5.1.1 記憶シークレット
<!--
#### <a name="memsecret"></a> 5.1.1 Memorized Secrets
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Memorized-secret.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>記憶シークレットAuthenticator — 一般的には<i>パスワード</i>や，数字ならば<i>PIN</i>として表現されているもの — は，ユーザによって選択され，記憶されるシークレットである．記憶シークレットは攻撃者が正しい値を推測したり秘密の値を特定できないように，十分に複雑かつ秘密にしておく必要がある． 記憶シークレットは <i>something you know</i> である．</td>
    <!--
    <td>A Memorized Secret authenticator — commonly referred to as a <i>password</i> or, if numeric, a <i>PIN</i> — is a secret value intended to be chosen and memorized by the user. Memorized secrets need to be of sufficient complexity and secrecy that it would be impractical for an attacker to guess or otherwise discover the correct secret value. A memorized secret is <i>something you know</i>.</td>
    -->
  </tr>
  </table>
  </div>

#### 5.1.1.1 記憶シークレットAuthenticators
<!--
#### 5.1.1.1 Memorized Secret Authenticators
-->

記憶シークレットは，Subscriberにより選択されば場合少なくとも8文字とするものとする(SHALL)．記憶シークレットがCSPまたはVerifierによってランダムに選択されたものである場合は，少なくとも6文字であるものとし(SHALL)，全て数字でもよい(MAY)．
CSPやVerifierが指定された記憶シークレットがセキュリティ侵害を受けたブラックリストに出現するかどうかに基づいて拒否した場合，Subscriberは別の記憶シークレット値を選ぶよう要求されるものとする(SHALL)．記憶シークレットの複雑さに関する他の要件を課すべきではない(SHOULD)．本件についての論拠は[Appendix A](#appA)の _Strength of Memorized Secrets_ に記載されている．
<!--
Memorized secrets SHALL be at least 8 characters in length if chosen by the subscriber. Memorized secrets chosen randomly by the CSP or verifier SHALL be at least 6 characters in length and MAY be entirely numeric. If the CSP or verifier disallows a chosen memorized secret based on its appearance on a blacklist of compromised values, the subscriber SHALL be required to choose a different memorized secret. No other complexity requirements for memorized secrets SHOULD be imposed. A rationale for this is presented in [Appendix A](#appA) _Strength of Memorized Secrets_.
-->

#### <a name="memsecretver"></a> 5.1.1.2 記憶シークレットVerifiers
<!--
#### <a name="memsecretver"></a> 5.1.1.2 Memorized Secret Verifiers
-->

Verifierは，Subscriberが選択した記憶シークレットに対して最低8文字であることを要求するものとする(SHALL)．Verifierは，Subscriberが選択した記憶シークレットに対して最低64文字を許可すべきである(SHOULD)．すべての印字可能なASCII [[RFC 20]](#RFC20) 文字(スペースも同様)は記憶シークレットとして許容されるべきである(SHOULD)．Unicode[[ISO/ISC 10646]](#ISOIEC10646)文字も同様に許容されるべきである(SHOULD)．Verifierは，8文字以上であることの検証を行う前に，タイピングミスの類を考慮して連続した複数のスペースまたは全てのスペースを除去してもよい(MAY)．シークレットの切り詰めについては実施しないものとする(SHALL NOT)．前述の記憶シークレットの長さ要件を満たすために，それぞれのUnicodeの符号位置は一文字としてカウントされるものとする(SHALL)．

<!--
Verifiers SHALL require subscriber-chosen memorized secrets to be at least 8 characters in length. Verifiers SHOULD permit subscriber-chosen memorized secrets at least 64 characters in length. All printing ASCII [[RFC 20]](#RFC20) characters as well as the space character SHOULD be acceptable in memorized secrets. Unicode [[ISO/ISC 10646]](#ISOIEC10646) characters SHOULD be accepted as well. To make allowances for likely mistyping, verifiers MAY replace multiple consecutive space characters with a single space character prior to verification, provided that the result is at least 8 characters in length. Truncation of the secret SHALL NOT be performed. For purposes of the above length requirements, each Unicode code point SHALL be counted as a single character.
-->

もしUnicode文字が記憶シークレットとして許容されるならば，Verifierは，Unicode Standard Annex 15 [[UAX 15]](#UAX15) の Section 12.1で定義されている"Stablized Strings"のためのNFKCまたはNFKD正規化のいずれかを用いた正規化処理を適用すべきである(SHOULD)．この処理は記憶シークレットのバイト文字表現のハッシュ化の前に適用される．Unicode文字を含む記憶シークレットを選択したSubscriberは，いくつかのエンドポイントでは異なる表現になるかもしれない文字があり，それが彼らが正しくAuthenticationを行う能力に影響する可能性があるということをことを通知されるべきである(SHOULD)．

<!--
If Unicode characters are accepted in memorized secrets, the verifier SHOULD apply the Normalization Process for Stabilized Strings using either the NFKC or NFKD normalization defined in Section 12.1 of Unicode Standard Annex 15 [[UAX 15]](#UAX15). This process is applied before hashing the byte string representing the memorized secret. Subscribers choosing memorized secrets containing Unicode characters SHOULD be advised that some characters may be represented differently by some endpoints, which can affect their ability to authenticate successfully.
-->

記憶シークレットは，CSP(例えばEnrollment時など)やVerifier(ユーザが新しいPINを要求した時など)によりランダムに選択されるもので，最低6文字であるものとし(SHALL)，Approve済み乱数生成器 [[SP 800-90Ar1]](#SP800-90Ar1) を利用して生成されるものとする(SHALL)．

<!--
Memorized secrets that are randomly chosen by the CSP (e.g., at enrollment) or by the verifier (e.g., when a user requests a new PIN) SHALL be at least 6 characters in length and SHALL be generated using an approved random bit generator [[SP 800-90Ar1]](#SP800-90Ar1).
-->

記憶シークレットVerifierは，Subscriberに対して，UnauthenticatedでないClaimantでも到達可能な「ヒント」を記録することを許可しないものとする(SHALL NOT)．
記憶シークレットを選択する際，VerifierはSubscriberに対して特定のタイプの情報（例えば，「あなたが飼った最初のペットの名前はなんですか？」といったもの）の入力を求めないものとする(SHALL NOT)．

<!--
Memorized secret verifiers SHALL NOT permit the subscriber to store a "hint" that is accessible to an unauthenticated claimant. Verifiers SHALL NOT prompt subscribers to use specific types of information (e.g., "What was the name of your first pet?") when choosing memorized secrets.
-->

記憶シークレットの設定，変更の要求を処理する際，Verifierは候補となっているシークレットの値を，一般的に利用されている値，予想されうる値，セキュリティ侵害を受けた値として知られている値を含むリストに対し，比較するものとする(SHALL)．例えば，以下のリストが含んでいるものでよい(MAY)が，限定するものではない:

* 過去に漏洩した語彙集から得られるパスワード
* 辞書に含まれる言葉
* 繰り返しまたはシーケンシャルな文字 (例： 'aaaaaa'，'1234abcd')
* サービス名や，ユーザ名，そこから派生するようなものなど，文脈で特定可能な単語

<!--
When processing requests to establish and change memorized secrets, verifiers SHALL compare the prospective secrets against a list that contains values known to be commonly-used, expected, or compromised. For example, the list MAY include, but is not limited to:

* Passwords obtained from previous breach corpuses.
* Dictionary words.
* Repetitive or sequential characters (e.g. 'aaaaaa', '1234abcd').
* Context-specific words, such as the name of the service, the username, and derivatives thereof.
-->

もし選択したシークレットがリスト中に存在したら，CSPまたはVerifierはSubscriberに対して異なるシークレット値を選ぶ必要があるということを知らせるものとし(SHALL)，その理由を提供するものとし(SHALL)，そしてSubscriberに異なる値を選択するよう求められるものとする(SHALL)．

<!--
If the chosen secret is found in the list, the CSP or verifier SHALL advise the subscriber that they need to select a different secret, SHALL provide the reason for rejection, and SHALL require the subscriber to choose a different value.
-->

VerifierはSubscriberに対して，ユーザが強力な記憶シークレットを選択するのを支援するために，パスワード強度メーター [[Meters]](#meters) のようなガイダンスを行うべきである(SHOULD)．上記におリストに載っている記憶シークレットを拒否したのち，[[Blacklists]](#blacklists)化されている(そしておそらく非常に弱い)記憶シークレットからのささいな変更を思いとどまらせることは特に重要である．

<!--
Verifiers SHOULD offer guidance to the subscriber, such as a password-strength meter [[Meters]](#meters), to assist the user in choosing a strong memorized secret. This is particularly important following the rejection of a memorized secret on the above list as it discourages trivial modification of listed (and likely very weak) memorized secrets [[Blacklists]](#blacklists).
-->

Verifierは，[Section 5.2.2](#throttle)に記載されているように，SubscriberのアカウントにおけるAuthentication失敗回数を効果的に制限するレート制限の仕組みを実装するものとする(SHALL)．

<!--
Verifiers SHALL implement a rate-limiting mechanism that effectively limits the number of failed authentication attempts that can be made on the subscriber's account as described in [Section 5.2.2](#throttle).
-->

Verifierは他の構成ルール(例えば，異なる文字種の組み合わせ，一定の文字の繰り返し)を記憶シークレットに課すべきではない(SHOULD NOT)．Verifierは，記憶シークレットを任意で(例えば，定期的に)変更するよう要求すべきではない(SHOULD NOT)．しかしながらAuthenticatorが侵害されている証拠がある場合は，変更を強制するものとする(SHALL)．

<!--
Verifiers SHOULD NOT impose other composition rules (e.g., requiring mixtures of different character types or prohibiting consecutively repeated characters) for memorized secrets. Verifiers SHOULD NOT require memorized secrets to be changed arbitrarily (e.g., periodically). However, verifiers SHALL force a change if there is evidence of compromise of the authenticator.
-->

VerifierはClaimantによる記憶シークレットを入力時に"ペースト"機能を利用することを許可すべきである(SHOULD)．これはパスワードマネージャの利用を促進し，広く利用されるようになることで多くの場合ユーザがより強力な記憶シークレットを選択する可能性を増加させる．．
<!--
Verifiers SHOULD permit claimants to use "paste" functionality when entering a memorized secret. This facilitates the use of password managers, which are widely used and in many cases increase the likelihood that users will choose stronger memorized secrets.
-->

Claimantが記憶シークレットを正しく入力することを支援するために，Verifierは，ドットやアスタリスク表示ではなく，入力され終わるまでシークレットを表示するオプションを提供すべき(SHOULD)である．こうすることで，Claimantは彼らのスクリーンが盗み見られる可能性が低い場所にいる場合に，入力内容を検証することができる．Verifierは更に，ユーザのデバイスに対して，入力が正しいことを確認する目的で個々の文字を入力後に短期間表示することを許可してもよい(MAY)．これは特にモバイルデバイスに当てはまる．
<!--
In order to assist the claimant in successfully entering a memorized secret, the verifier SHOULD offer an option to display the secret — rather than a series of dots or asterisks — until it is entered. This allows the claimant to verify their entry if they are in a location where their screen is unlikely to be observed. The verifier MAY also permit the user's device to display individual entered characters for a short time after each character is typed to verify correct entry. This is particularly applicable on mobile devices.
-->

VerifierはApprove済み暗号化を利用するものとし(SHALL)，記憶シークレットを要求する際には，盗聴や中間者攻撃を防止するためにAuthenticateされた保護チャネルを用いるものとする(SHALL)．
<!--
The verifier SHALL use approved encryption and an authenticated protected channel when requesting memorized secrets in order to provide resistance to eavesdropping and MitM attacks.
-->

Verifierは，オフライン攻撃に対して耐性をもった形式で記憶シークレットを保存するものとする(SHALL)．シークレットは， ソルトを追加したうえで適切な一方向の鍵導出関数を利用してハッシュされるものとする(SHALL)，鍵導出関数は，パスワード，ソルト，コストファクタを入力して，パスワードハッシュを生成する．例えば[[SP800-132]](#SP800-132)で記載されているPBKDF2のようなApprove済みハッシュを用いてハッシュ化されるものとする(SHALL)．ソルト値は32ビット以上のランダム値で，承認済み(approved)の乱数生成器を用いて生成され，ハッシュ結果とともに記録される．少なくとも繰り返し10000回のハッシュ関数を適用すべきである(SHOULD)．ハッシュAuthenticatorから分離されて記録される鍵(例:ハードウェアセキュリティモジュール中)を用いる鍵付ハッシュ関数(例:HMAC)は，記録済みハッシュ化Authenticatorに対する辞書攻撃に対する更なる対抗方法として利用されるべきである(SHOULD)．パスワードハッシュのファイルを入手した攻撃者によってパスワード推測の試行に費用がかかるようにする．そのためパスワード推測攻撃のコストは高い，もしくは非常に法外なものになる．適切な鍵導出関数の例としてPassword-based Key Derivation Function 2 (PBKDF2) [[SP 800-132]](#SP800-132)及びBalloon [[BALLOON]](#balloon)がある．攻撃コストを増加させることができるため，memory-hardな関数が利用されるべきである(SHOULD)．鍵導出関数はApprove済み一方向関数が用いられるべき(SHOULD)であり，例えば，Keyed Hash Message Authentication Code (HMAC) [[FIPS 198-1]](#FIPS198-1)，[SP 800-107](#SP800-107)のApprove済みハッシュ関数の何れか，Secure Hash Algorithm 3 (SHA-3) [[FIPS 202]](#FIPS202)，CMAC [[SP 800-38B]](#SP800-38B)，Keccak Message Authentication Code (KMAC)，Customizable SHAKE (cSHAKE)，ParallelHash [[SP 800-185]](#SP800-185)などがある．鍵導出関数からの出力を選択する際，根拠となる一方向関数の出力と長さが同じであるべきである(SHOULD)．

<!--
Verifiers SHALL store memorized secrets in a form that is resistant to offline attacks. Memorized secrets SHALL be salted and hashed using a suitable one-way key derivation function. Key derivation functions take a password, a salt, and a cost factor as inputs then generate a password hash. Their purpose is to make each password guessing trial by an attacker who has obtained a password hash file expensive and therefore the cost of a guessing attack high or prohibitive. Examples of suitable key derivation functions include Password-based Key Derivation Function 2 (PBKDF2) [[SP 800-132]](#SP800-132) and Balloon [[BALLOON]](#balloon). A memory-hard function SHOULD be used because it increases the cost of an attack. The key derivation function SHALL use an approved one-way function such as Keyed Hash Message Authentication Code (HMAC) [[FIPS 198-1]](#FIPS198-1), any approved hash function in [SP 800-107](#SP800-107), Secure Hash Algorithm 3 (SHA-3) [[FIPS 202]](#FIPS202), CMAC [[SP 800-38B]](#SP800-38B) or Keccak Message Authentication Code (KMAC), Customizable SHAKE (cSHAKE), or ParallelHash [[SP 800-185]](#SP800-185). The chosen output length of the key derivation function SHOULD be the same as the length of the underlying one-way function output.
-->

ソルトは少なくとも32ビットの長さで，保存されたハッシュ間でソルト値の衝突が最小化されるように任意に選択されたものとする(SHALL)．ソルト値及び結果のハッシュはいずれも記憶シークレットAuthenticatorを利用してSubscriber毎に保存されるものとする(SHALL)．
<!--
The salt SHALL be at least 32 bits in length and be chosen arbitrarily so as to minimize salt value collisions among stored hashes. Both the salt value and the resulting hash SHALL be stored for each subscriber using a memorized secret authenticator.
-->

PBKDF2において，コストファクタは繰り返し回数である: PBKDF2関数が繰り返し適用される回数が増加すれば，パスワードハッシュの計算時間が必要となる．すなわち，繰り返し回数は検証サーバのパフォーマンスが許す限り大きくするべきであり(SHOULD)，概ね10,000以上とすべきである．
<!--
For PBKDF2, the cost factor is an iteration count: the more times the PBKDF2 function is iterated, the longer it takes to compute the password hash. Therefore, the iteration count SHOULD be as large as verification server performance will allow, typically at least 10,000 iterations.
-->

加えて，Verifierは，自身だけが知っているシークレットをソルト値として用いた鍵導出関数の適用を追加で実施すべきである(SHOULD)．もし可能ならばソルト値はApprove済み乱数生成器 [[SP 800-90Ar1]](#SP800-90Ar1)を利用して生成されるべき(SHOULD)であり，[SP 800-131A](#SP800-131A)の最新版で指定されている最小のセキュリティ強度(本書の公開日時点では112ビット)を少なくとも備えるべき(SHOULD)である．このシークレットソルト値は，ハッシュ化された記憶シークレットとは別に(例えば，ハードウェアセキュリティモジュールなどの特別なデバイスの中に)保存されるものとする(SHALL)．この追加の適用により，シークレットソルト値が秘密である限り，記憶シークレットのハッシュに対するブルートフォース攻撃は非現実的である．
<!--
In addition, verifiers SHOULD perform an additional iteration of a key derivation function using a salt value that is secret and known only to the verifier. This salt value, if used, SHALL be generated by an approved random bit generator [[SP 800-90Ar1]](#SP800-90Ar1) and provide at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication). The secret salt value SHALL be stored separately from the hashed memorized secrets (e.g., in a specialized device like a hardware security module). With this additional iteration, brute-force attacks on the hashed memorized secrets are impractical as long as the secret salt value remains secret.
-->

#### <a name="lookupsecrets"></a> 5.1.2 ルックアップシークレット
<!--
#### <a name="lookupsecrets"></a> 5.1.2 Look-Up Secrets
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Look-up-secrets.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>ルックアップシークレットAuthenticatorは物理的または電子的なレコードであり，ClaimantとCSPとの間で共有されているシークレット一式を記録するものである．Claimantは，Verifierからの入力要求に答えるために必要とされる適切なシークレットを検索するためにAuthenticatorを利用する．例えば，VerifierはClaimantに対して，カード上に印字された表形式の数字または文字列のうち特定の一部を提示するよう求められるかもしれない．ルックアップシークレットの一般的な適用としては，Subscriberによって保存され，別のAuthenticatorが紛失したり機能しなくなった際に用いる"リカバリキー"の利用がある．ルックアップシークレットは<i>something you have</i>である．</td>
    <!--
    <td>A look-up secret authenticator is a physical or electronic record that stores a set of secrets shared between the claimant and the CSP. The claimant uses the authenticator to look up the appropriate secret(s) needed to respond to a prompt from the verifier. For example, the verifier may ask a claimant to provide a specific subset of the numeric or character strings printed on a card in table format. A common application of look-up secrets is the use of "recovery keys" stored by the subscriber for use in the event another authenticator is lost or malfunctions. A look-up secret is <i>something you have</i>.</td>
    -->
  </tr>
  </table>
  </div>

#### <a name="lusa"></a>5.1.2.1 ルックアップシークレットAuthenticator
<!--
#### <a name="lusa"></a>5.1.2.1 Look-Up Secret Authenticators
-->

CSPがルックアップシークレットAuthenticatorを生成する際，Approve済み乱数生成器 [[SP 800-90Ar1]](#SP800-90Ar1) を用いてシークレットのリストを生成するものとし(SHALL)，Subscriberに対してAuthenticatorを安全に届けるものとする(SHALL)．ルックアップシークレットは最低20ビットのエントロピーを持つものとする(SHALL)．
<!--
CSPs creating look-up secret authenticators SHALL use an approved random bit generator [[SP 800-90Ar1]](#SP800-90Ar1) to generate the list of secrets and SHALL deliver the authenticator securely to the subscriber. Look-up secrets SHALL have at least 20 bits of entropy.
-->

ルックアップシークレットは，CSPの人間の手での配布，Subscriberの住所宛への配送，またはオンラインでの配布が行われてもよい(MAY)，もし配布がオンラインで行われるならば，ルックアップシークレットはpost-enrollment binding要件[Section 6.1.2](#post-enroll-bind)を満たすセキュアチャネル上で配布されるものとする(SHALL)．
<!--
Look-up secrets MAY be distributed by the CSP in person, by postal mail to the subscriber's address of record, or by online distribution. If distributed online, look-up secrets SHALL be distributed over a secure channel in accordance with the post-enrollment binding requirements in [Section 6.1.2](#post-enroll-bind).
-->

もしAuthenticatorがルックアップシークレットを連続してリストから利用する場合，Subscriberは一度Authenticationに成功した場合に限ってシークレットを破棄してもよい(MAY)．
<!--
If the authenticator uses look-up secrets sequentially from a list, the subscriber MAY dispose of used secrets, but only after a successful authentication.
-->

#### 5.1.2.2 Look-Up Secret Verifiers

ルックアップシークレットのVerifierはClaimantに対して，彼らのAuthenticatorから得られる次のシークレット，または特定の(例:付番された)シークレットの入力を促すものとする(SHALL)．Authenticatorから得られたシークレットは1度しか正常に利用できないものとする(SHALL)．もしルックアップシークレットが格子状のカードから得られる場合，格子の各セルは1度だけ利用するものとする(SHALL)．
<!--
Verifiers of look-up secrets SHALL prompt the claimant for the next secret from their authenticator or for a specific (e.g., numbered) secret. A given secret from an authenticator SHALL be used successfully only once. If the look-up secret is derived from a grid card, each cell of the grid SHALL be used only once.
-->

Verifierは，オフライン攻撃へ対策する形式でルックアップシークレットを保存するものとする(SHALL)．112ビット以上のエントロピーを持ったルックアップシークレットは，[Section 5.1.1.2](#memsecretver)に記載されているようにApprove済み一方向関数でハッシュ化されるものとする(SHALL)．112ビット未満のエントロピーを持ったルックアップシークレットは[Section 5.1.1.2](#memsecretver)に記載されているように，ソルトを追加したうえで適切な一方向の鍵導出関数を用いてハッシュされるものとする．ソルト値は32ビット以上の長さで，保存されたハッシュ間でソルト値の衝突が最小化されるように任意に選択されるものとする(SHALL)．ソルト値及び結果のハッシュはいずれもルックアップシークレット毎に保存されるものとする(SHALL)．
<!--
Verifiers SHALL store look-up secrets in a form that is resistant to offline attacks. Look-up secrets having at least 112 bits of entropy SHALL be hashed with an approved one-way function as described in [Section 5.1.1.2](#memsecretver). Look-up secrets with fewer than 112 bits of entropy SHALL be salted and hashed using a suitable one-way key derivation function, also described in [Section 5.1.1.2](#memsecretver). The salt value SHALL be at least 32 in bits in length and arbitrarily chosen so as to minimize salt value collisions among stored hashes. Both the salt value and the resulting hash SHALL be stored for each look-up secret.
-->

64ビット未満のエントロピーを持つルックアップシークレットに対して，Verifierは，[Section 5.2.2](#throttle)に記載されているように，SubscriberのアカウントにおけるAuthentication失敗回数を効果的に制限するレート制限の仕組みを実装するものとする(SHALL)．
<!--
For look-up secrets that have less than 64 bits of entropy, the verifier SHALL implement a rate-limiting mechanism that effectively limits the number of failed authentication attempts that can be made on the subscriber's account as described in [Section 5.2.2](#throttle).
-->

VerifierはApprove済み暗号化を利用するものとし(SHALL)，ルックアップシークレットを要求する際には，盗聴や中間者攻撃を防止する目的で，Authenticateされた保護チャネルを利用するものとする(SHALL)．
<!--
The verifier SHALL use approved encryption and an authenticated protected channel when requesting look-up secrets in order to provide resistance to eavesdropping and MitM attacks.
-->

#### <a name="out-of-band"></a> 5.1.3 アウトオブバンドデバイス
<!--
#### <a name="out-of-band"></a> 5.1.3 Out-of-Band Devices
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Out-of-band-OOB.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>アウトオブバンドAuthenticatorは，一意にアドレス可能，かつセカンダリチャネルと呼ばれる異なる通信チャネルを介してVerifierと安全に通信することができる物理デバイスである．デバイスはClaimantによって所有及び制御されており，E-Authenticationのためのプライマリチャネルと分離されたセカンダリチャネルを介したプライベートな通信をサポートしている．アウトオブバンドAuthenticatorは<i>something you have</i>である．<br><br>

アウトオブバンドAuthenticatorは以下の方法の1つで動作する: <br><br>

- Claimantはアウトオブバンドデバイスによってセカンダリチャネルを介して受け取ったシークレットを，プライマリチャネルを使ってVerifierに送信する．例えば，Claimantは自身のモバイルデバイス上でシークレットを受信し，それ(一般的には数字6桁のコード)を自身のAuthenticationセッションに対して入力してもよい．<br><br>

- Claimantはプライマリチャネルを介して受け取ったシークレットを，アウトオブバンドデバイスに対して送信し，セカンダリチャネルを介してVerifierに対して送信する．例えば，Claimantは自身のAuthenticationセッション上で確認したシークレットを，モバイルデバイス上のアプリケーション対して入力したり，バーコード・QRコードといった技術を利用して送信を行ってもよい．<br><br>

- Claimantはプライマリチャネルとセカンダリチャネルから得たシークレットを比較し，セカンダリチャネルを介したAuthenticationを確認する．<br><br>

シークレットの目的は安全にAuthentication操作をプライマリとセカンダリのチャネルに結びつけることである．プライマリ通信チャネルを介してレスポンスをする場合，シークレットはアウトオブバンドデバイスをClaimantが制御していることもまた証明していることになる．</td> 
    <!--
    <td>An out-of-band authenticator is a physical device that is uniquely addressable and can communicate securely with the verifier over a distinct communications channel, referred to as the secondary channel. The device is possessed and controlled by the claimant and supports private communication over this secondary channel, separate from the primary channel for e-authentication. An out-of-band authenticator is <i>something you have</i>.<br><br>

The out-of-band authenticator can operate in one of the following ways: <br><br>

- The claimant transfers a secret received by the out-of-band device via the secondary channel to the verifier using the primary channel. For example, the claimant may receive the secret on their mobile device and type it (typically a 6-digit code) into their authentication session.<br><br>

- The claimant transfers a secret received via the primary channel to the out-of-band device for transmission to the verifier via the secondary channel. For example, the claimant may view the secret on their authentication session and either type it into an app on their mobile device or use a technology such as a barcode or QR code to effect the transfer.<br><br>

- The claimant compares secrets received from the primary channel and the secondary channel and confirms the authentication via the secondary channel.<br><br>

The secret's purpose is to securely bind the authentication operation on the primary and secondary channel. When the response is via the primary communication channel, the secret also establishes the claimant's control of the out-of-band device.</td>
-->
  </tr>
  </table>
  </div>

#### <a name="ooba"></a> 5.1.3.1 アウトオブバンドAuthenticator
<!--
#### <a name="ooba"></a> 5.1.3.1 Out-of-Band Authenticators
-->

アウトオブバンドAuthenticatorはアウトオブバンドシークレットやAuthenticationリクエストを取得するためにVerifierとの分離された通信チャネルを確立するものとする(SHALL)．このチャネルはプライマリ通信チャネルとの関係においてアウトオブバンドであるとし，(同じデバイス上で終端されている場合でさえも)，Claimantの認可なしに一方から他方に対して情報が漏洩することがないようなデイバイスであることを前提とする．
<!--
The out-of-band authenticator SHALL establish a separate channel with the verifier in order to retrieve the out-of-band secret or authentication request. This channel is considered to be out-of-band with respect to the primary communication channel (even if it terminates on the same device) provided the device does not leak information from one channel to the other without the authorization of the claimant.
-->

アウトオブバンドデバイスは一意にアドレス可能であるべきであり(SHOULD)，セカンダリチャネルを介した通信は，公衆交換電話網(PSTN)を介して送信されない場合は暗号化されているものとする(SHALL)．PSTNに固有な追加のAuthenticator要件に対しては，[Section 5.1.3.3](#pstnOOB)を参照すること．Voice-over-IP(VoIP)やEmailなど，特定デバイスの所有を証明を行わない方式は，アウトオブバンドAuthenticationを行う目的では利用しないものとする(SHALL)．
<!--
The out-of-band device SHOULD be uniquely addressable and communication over the secondary channel SHALL be encrypted unless sent via the public switched telephone network (PSTN). For additional authenticator requirements specific to the PSTN, see [Section 5.1.3.3](#pstnOOB). Methods that do not prove possession of a specific device, such as voice-over-IP (VOIP) or email, SHALL NOT be used for out-of-band authentication.
-->

アウトオブバンドAuthenticatorは，Verifierとの通信において以下に記載する方法の1つを用いて，一意に自身の真正性を証明するものとする(SHALL):
<!--
The out-of-band authenticator SHALL uniquely authenticate itself in one of the following ways when communicating with the verifier:
-->

- Approve済み暗号理論を利用してVerifierに対するAuthenticateされた保護チャネルを確立すること．鍵はAuthenticatorアプリケーションが利用可能なデバイス上で適切にセキュアであるストレージ(例:キーチェーンストレージ，TPM，TEE，セキュアエレメント)に記録されるものとする(SHALL)．
<!--
- Establish an authenticated protected channel to the verifier using approved cryptography. The key used SHALL be stored in suitably secure storage available to the authenticator application (e.g., keychain storage, TPM, TEE, secure element).
-->

- SIMカードまたはデバイスを一意に識別する等価な方法を用いて公衆携帯電話網に対してAuthenticateする．この方法はPSTN(SMSまたは音声)を介してアウトオブバンドデバイスに対してVerifierからシークレットが送信される場合に限り用いるものとする(SHALL)．
<!--
- Authenticate to a public mobile telephone network using a SIM card or equivalent that uniquely identifies the device. This method SHALL only be used if a secret is being sent from the verifier to the out-of-band device via the PSTN (SMS or voice).
-->

もしVerifierからアウトオブバンドデバイスに対してシークレットが送信されるならば，デバイスは所有者によってデバイスがロックされている(例:表示するために，PINやパスコード入力，またはバイオメトリックの入力が必要とされる)間はAuthenticationシークレットを表示すべきではない(SHOULD NOT)．しかしながらAuthenticatorはロックされたデバイス上でAuthenticationシークレットを受信したことを表示すべきである(SHOULD)．
<!--
If a secret is sent by the verifier to the out-of-band device, the device SHOULD NOT display the authentication secret while it is locked by the owner (i.e., requires an entry of a PIN, passcode, or biometric to view). However, authenticators SHOULD indicate the receipt of an authentication secret on a locked device.
-->

もしアウトオブバンドAuthenticatorがセカンダリ通信チャネルを介して承認メッセージを送信するならば(Claimantがプライマリ通信チャネルに対して受け取ったシークレットを送信するよりもむしろ)，次のうち1つを実施するものとする(SHALL):
<!--
If the out-of-band authenticator sends an approval message over the secondary communication channel — rather than by the claimant transferring a received secret to the primary communication channel — it SHALL do one of the following:
-->

* Authenticatorはプライマリチャネルから得たシークレットを転送することを許容するものとし(SHALL)，Authenticationトランザクションに対する承認と関連付けるために，セカンダリチャネルを介してVerifierに対して送信するものとする(SHALL)．Claimantは送信を手動で実施，またはバーコード・QRコードといった技術を利用して送信を行ってもよい(MAY)．
<!--
* The authenticator SHALL accept transfer of the secret from the primary channel which it SHALL send to the verifier over the secondary channel to associate the approval with the authentication transaction. The claimant MAY perform the transfer manually or use a technology such as a barcode or QR code to effect the transfer.
-->

* Authenticatorはセカンダリチャネルを介してVerifierから受け取ったシークレットを提示し，Claimantに対してプライマリチャネルのシークレットとの一貫性を検証するよう促した上で，Claimantから「はい/いいえ」の応答を受け入れるものとする(SHALL)．
<!--
* The authenticator SHALL present a secret received via the secondary channel from the verifier and prompt the claimant to verify the consistency of that secret with the primary channel, prior to accepting a yes/no response from the claimant. It SHALL then send that response to the verifier.
-->

#### 5.1.3.2 アウトオブバンドVerifier
<!--
#### 5.1.3.2 Out-of-Band Verifiers
-->

PSTNに特有の追加の検証要件は，[Section 5.1.3.3](#pstnOOB)を参照すること．
<!--
For additional verification requirements specific to the PSTN, see [Section 5.1.3.3](#pstnOOB).
-->

アウトオブバンド検証がセキュアなアプリケーション(例:スマートフォン上)を利用して行われる場合，Verifierはデバイスに対してPush通知を行ってもよい(MAY)．VerifierはAuthenticateされた保護チャネルの確立を待ち，Authenticatorの識別キーを検証する．Authenticatorは識別キー自身を記録しないものとする(SHALL NOT)が，Authenticatorを一意に識別するためにハッシュのような検証方法(例えばApprove済みのハッシュ関数や，識別キーの所持証明)を用いるものとする(SHALL)．Authenticateされると，VerifierはAuthenticationシークレットをAuthenticatorに対して送信する．
<!--
If out-of-band verification is to be made using a secure application, such as on a smart phone, the verifier MAY send a push notification to that device. The verifier then waits for the establishment of an authenticated protected channel and verifies the authenticator's identifying key. The verifier SHALL NOT store the identifying key itself, but SHALL use a verification method (e.g., an approved hash function or proof of possession of the identifying key) to uniquely identify the authenticator. Once authenticated, the verifier transmits the authentication secret to the authenticator.
-->

アウトオブバンドAuthenticatorの種別に応じて，以下のうち1つを行うものとする(SHALL):
<!--
Depending on the type of out-of-band authenticator, one of the following SHALL take place:
-->

* シークレットをプライマリチャネルに送出: VerifierはSubscriberのAuthenticatorを持つデバイスに対してAuthenticationの準備を示すシグナルを送信してもよい(MAY)．そのうえで，アウトオブバンドAuthenticatorに対してランダムなシークレットを送信するものとする(SHALL)．Verifierはプライマリ通信チャネル上でシークレットが返却されるのを待つものとする(SHALL)．

<!--
* Transfer of secret to primary channel: The verifier MAY signal the device containing the subscriber's authenticator to indicate readiness to authenticate. It SHALL then transmit a random secret to the out-of-band authenticator. The verifier SHALL then wait for the secret to be returned on the primary communication channel.
-->

* シークレットをセカンダリチャネルに送出: VerifierはランダムなAuthenticationシークレットをプライマリチャネル経由でClaimantに対して表示するものとする(SHALL)．そのうえで，セカンダリチャネル上でClaimantのアウトオブバンドAuthenticatorからシークレットが返却されるのを待つものとする(SHALL)．

<!--
* Transfer of secret to secondary channel: The verifier SHALL display a random authentication secret to the claimant via the primary channel. It SHALL then wait for the secret to be returned on the secondary channel from the claimant's out-of-band authenticator.
-->

* ClaimantによるシークレットのVerifier: VerifierはランダムなAuthenticationシークレットをプライマリチャネル経由でClaimantに対して表示するものとし(SHALL)，セカンダリチャネルを介してアウトオブバンドAuthenticatorに対して同じシークレットを送信しClaimantに提示するものとする(SHALL)．そのうえで，セカンダリチャネルを介した承認(非承認)メッセージを待つものとする(SHALL)．

<!--
* Verification of secrets by claimant: The verifier SHALL display a random authentication secret to the claimant via the primary channel, and SHALL send the same secret to the out-of-band authenticator via the secondary channel for presentation to the claimant. It SHALL then wait for an approval (or disapproval) message via the secondary channel.
-->

全てのケースにおいて，10分以内に完了しないAuthenticationは不正とみなすものとする(SHALL)．[Section 5.2.8](#replay)に記載されているリプレイ耐性を備えるために，Verifierは特定のAuthenticationシークレットを確認期間の間で一度だけ受け付けるものとする(SHALL)．

<!--
In all cases, the authentication SHALL be considered invalid if not completed within 10 minutes. In order to provide replay resistance as described in [Section 5.2.8](#replay), verifiers SHALL accept a given authentication secret only once during the validity period.
-->

Verifierは，Approve済み乱数生成器 [[SP 800-90Ar1]](#SP800-90Ar1) を用いて少なくとも20ビットのエントロピーでランダムなAuthenticationシークレットを生成するものとする(SHALL)．もし認証シークレットが64ビット未満のエントロピーを持つ場合は，ルックアップシークレットに対して，Verifierは，[Section 5.2.2](#throttle)に記載されているように，SubscriberのアカウントにおけるAuthentication失敗回数を効果的に制限するレート制限の仕組みを実装するものとする(SHALL)．

<!--
The verifier SHALL generate random authentication secrets with at least 20 bits of entropy using an approved random bit generator [[SP 800-90Ar1]](#SP800-90Ar1). If the authentication secret has less than 64 bits of entropy, the verifier SHALL implement a rate-limiting mechanism that effectively limits the number of failed authentication attempts that can be made on the subscriber's account as described in [Section 5.2.2](#throttle).
-->


#### <a name="pstnOOB"></a> 5.1.3.3 公衆交換電話網を利用するAuthenticator
<!--
#### <a name="pstnOOB"></a> 5.1.3.3 Authentication using the Public Switched Telephone Network
-->

アウトオブバンドでの検証を目的としたPSTNの利用は，本セクション及び [Section 5.2.10](#restricted) に記載されているように制限されている(RESTRICTED)．もしアウトオブバンドでの検証がPSTNを用いて実施される場合は，Verifierは利用されている事前登録済みの電話番号が，特定の物理デバイスに紐付けられていることを検証するものとする(SHALL)．事前登録済みの電話番号の変更は，新しいAuthenticatorを結びつける行為とみなされ，[Section 6.1.2](#post-enroll-bind) に記載されている場合のみ発生するものとする(SHALL)．

<!--
Use of the PSTN for out-of-band verification is RESTRICTED as described in this section and in [Section 5.2.10](#restricted). If out-of-band verification is to be made using the PSTN, the verifier SHALL verify that the pre-registered telephone number being used is associated with a specific physical device. Changing the pre-registered telephone number is considered to be the binding of a new authenticator and SHALL only occur as described in [Section 6.1.2](#post-enroll-bind).
-->

Verifierは，デバイス入れ替え，SIM変更，番号ポーティング，あるいはその他にアウトオブバンドAuthenticationシークレットの配送にPSTNを利用する以前の異常な振る舞いのようなリスク指標を考慮すべきである(SHOULD)．
<!--
Verifiers SHOULD consider risk indicators such as device swap, SIM change, number porting, or other abnormal behavior before using the PSTN to deliver an out-of-band authentication secret.
-->


> 注記: [Section 5.2.10](#restricted)におけるAuthenticatorの制限に従い，NISTは脅威状況及びPSTNの技術的な運用の発展に基づき，PSTNの制限(RESTRICTED)状態を時間の経過とともに調整するかもしれない．
<!--
> NOTE: Consistent with the restriction of authenticators in [Section 5.2.10](#restricted), NIST may adjust the RESTRICTED status of the PSTN over time based on the evolution of the threat landscape and the technical operation of the PSTN.
-->

#### <a name="singlefactorOTP"></a> 5.1.4 単一要素OTPVerifier
<!--
#### <a name="singlefactorOTP"></a> 5.1.4 Single-Factor OTP Device
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>単一要素OTPデバイスはOTPの生成をサポートするデバイスである．単一要素OTPデバイスは，携帯電話のようなデバイスにインストールされたソフトウェアのOTP生成器及びハードウェアデバイスが含まれる．これらのデバイスは，OTPの生成のシードとして利用される組み込みのシークレットを保持しており，二要素目によるアクティベーションを必要としない．OTPはデバイス上で表示，手動でVerifierに対して入力され，そのことによりデバイスの所持と制御を証明する．OTPデバイスは例えば一度に6文字の表示を行うことがある．単一要素OTPデバイスは<i>something you have</i>である．<br><br>

単一要素OTPデバイスはルックアップシークレットAuthenticatorと同様，暗号理論に基づいてAuthenticatorとVerifierがシークレットを生成し，Verifierによって比較されるという例外を除いて同様である．シークレットは，時間ベースのノンスまたはAuthenticatorとVerifierのカウンタに基づいて計算される.</td> 
    <!--
    <td>A single-factor OTP device generates OTPs. This category includes hardware devices and software-based OTP generators installed on devices such as mobile phones. These devices have an embedded secret that is used as the seed for generation of OTPs and does not require activation through a second factor. The OTP is displayed on the device and manually input for transmission to the verifier, thereby proving possession and control of the device. An OTP device may, for example, display 6 characters at a time. A single-factor OTP device is <i>something you have</i>.<br><br>

Single-factor OTP devices are similar to look-up secret authenticators with the exception that the secrets are cryptographically and independently generated by the authenticator and verifier and compared by the verifier. The secret is computed based on a nonce that may be time-based or from a counter on the authenticator and verifier.</td>
-->
  </tr>
  </table>
  </div>

#### <a name="sfotpa"></a>5.1.4.1 Single-Factor OTP Authenticators

単一要素OTPAuthenticatorは2つの永続的な値を保持する.1つ目はデバイスの生存期間の間保持し続ける対象鍵である.2つ目は認証機が使われる都度変化する，またはリアルタイムクロックに基づいているノンスである.
<!--
Single-factor OTP authenticators contain two persistent values. The first is a symmetric key that persists for the device's lifetime. The second is a nonce that is either changed each time the authenticator is used or is based on a real-time clock.
-->

秘密鍵とそのアルゴリズムは少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)であるものとする(SHALL)．ノンスは，デバイスの生存期間に渡りデバイスが操作される都度一意な値であることを確実にするために十分長いこととする(SHALL). OTP Authenticatorは - 特にソフトウェアベースのOTP生成器の場合 - 複数デバイスに対して秘密鍵を複製する行為を思いとどまらせるべきであり(SHOULD)，助長しないものとする(SHALL NOT)．
<!--
The secret key and its algorithm SHALL provide at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication). The nonce SHALL be of sufficient length to ensure that it is unique for each operation of the device over its lifetime. OTP authenticators — particularly software-based OTP generators — SHOULD discourage and SHALL NOT facilitate the cloning of the secret key onto multiple devices.
-->

Authenticator出力は，鍵とノンスとを安全な方法で組み合わせ，Approveされたブロック暗号またはハッシュ関数を用いることで得られる．Authenticator出力は少なくとも(約20ビットのエントロピーの)6桁の数字になるよう切り詰めてもよい(MAY).
<!--
The authenticator output is obtained by using an approved block cipher or hash function to combine the key and nonce in a secure manner. The authenticator output MAY be truncated to as few as 6 decimal digits (approximately 20 bits of entropy).
-->

もしAuthenticator出力を生成するために利用されるノンスがリアルタイムクロックをベースとしている場合，ノンスは少なくとも2分毎に変化するものとする(SHALL).与えられたノンスと関連するOTP値は一度だけ受け入れられるものとする(SHALL).
<!--
If the nonce used to generate the authenticator output is based on a real-time clock, the nonce SHALL be changed at least once every 2 minutes. The OTP value associated with a given nonce SHALL be accepted only once.
-->

#### 5.1.4.2 単一要素OTP Verifier
<!--
#### 5.1.4.2 Single-Factor OTP Verifiers
-->

単一要素OTP Verifierは，AuthenticatorによるOTPの生成プロセスを実質的に再現する．Verifierは，Authenticatorが使う対称鍵を所持しており，セキュリティ侵害に対する強力な防御が行われているものとする(SHALL)．
<!--
Single-factor OTP verifiers effectively duplicate the process of generating the OTP used by the authenticator. As such, the symmetric keys used by authenticators are also present in the verifier, and SHALL be strongly protected against compromise.
-->

単一要素OTP AuthenticatorがSubscriberアカウントに紐付けられている時，Verifierまたは関連するCSPは，Authenticatorの出力を再現するために必要なシークレットを生成，交換または取得するためにApproveされた暗号理論を利用するものとする(SHALL)．．
<!--
When a single-factor OTP authenticator is being associated with a subscriber account, the verifier or associated CSP SHALL use approved cryptography to either generate and exchange or to obtain the secrets required to duplicate the authenticator output.
-->

Verifierは，OTPを収集する際の盗聴や中間者攻撃に対抗するために，Approveされた暗号化を利用し，Authenticateされた保護チャネルを利用するものとする(SHALL)．時間ベースのOTP[[RFC 6238]](#RFC6238)は，有効期間を定義するものとし(SHALL)，Authenticator自体の寿命までに予想される（何れの方向に対する）時刻ずれにネットワーク遅延とユーザによるOTP入力の許容時間を加えて決定される．[Section 5.2.8](#replay)に記載されているリプレイ耐性を備えるために，Verifierは指定された時間ベースのOTPを有効期間で一度だけ受け付けるものとする(SHALL)．
<!--
The verifier SHALL use approved encryption and an authenticated protected channel when collecting the OTP in order to provide resistance to eavesdropping and MitM attacks. Time-based OTPs [[RFC 6238]](#RFC6238) SHALL have a defined lifetime that is determined by the expected clock drift — in either direction — of the authenticator over its lifetime, plus allowance for network delay and user entry of the OTP. In order to provide replay resistance as described in [Section 5.2.8](#replay), verifiers SHALL accept a given time-based OTP only once during the validity period.
-->

もしAuthenticator出力が64ビット未満のエントロピーを持つ場合は，Verifierは，[Section 5.2.2](#throttle)に記載されているように，SubscriberのアカウントにおけるAuthentication失敗回数を効果的に制限するレート制限の仕組みを実装するものとする(SHALL)．
<!--
If the authenticator output has less than 64 bits of entropy, the verifier SHALL implement a rate-limiting mechanism that effectively limits the number of failed authentication attempts that can be made on the subscriber's account as described in [Section 5.2.2](#throttle).
-->

#### <a name="multifactorOTP"></a> 5.1.5 Multi-Factor OTP Devices

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>多要素OTPデバイスは，追加の認証要素によりアクティベートされた後にAuthenticationで使われるワンタイムパスワードを生成する．多要素OTPデバイスは，ハードウェアデバイス及び携帯電話のようなデバイスにインストールされたソフトウェアのOTP生成器が含まれる．Authenticationの2要素目は組み込みの入力パッド，組み込みのバイオメトリック(例：指紋)リーダ，USBポートなどのコンピュータに対するダイレクトなインタフェースを介して実現される．ワンタイムパスワードはデバイス上で表示，手動でVerifierに対して入力され，そのことによりデバイスの所持と制御を証明する．ワンタイムパスワードデバイスは例えば一度に6文字の表示を行うことがある．多要素OTPデバイスは<i>something you have</i>である．また，<i>something you know</i>または<i>something you are</i>のどちらかによってアクティベートされるものとする(SHALL)．</td>
<!--
    <td>A multi-factor OTP device generates OTPs for use in authentication after activation through an additional authentication factor. This includes hardware devices and software-based OTP generators installed on devices such as mobile phones. The second factor of authentication may be achieved through some kind of integral entry pad, an integral biometric (e.g., fingerprint) reader, or a direct computer interface (e.g., USB port). The OTP is displayed on the device and manually input for transmission to the verifier. For example, an OTP device may display 6 characters at a time, thereby proving possession and control of the device. The multi-factor OTP device is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td>
    -->
  </tr>
  </table>
  </div>


#### 5.1.5.1 <a name="mfotpa"></a>多要素OTP Authenticator
<!--
#### 5.1.5.1 <a name="mfotpa"></a>Multi-Factor OTP Authenticators
-->

多要素OTP Authenticatorは，Authenticatorからパスワードを得るために記憶シークレットの入力またはバイオメトリクスの利用を要求する点を除いて，単一要素OTP Authenticator([Section 5.1.4.1](#sfotpa)参照)と同じ方法で動作する．いずれの場合でも追加要素の入力が必要であるものとする(SHALL)．
<!--
Multi-factor OTP authenticators operate in a similar manner to single-factor OTP authenticators (see [Section 5.1.4.1](#sfotpa)), except that they require the entry of either a memorized secret or the use of a biometric to obtain the OTP from the authenticator. Each use of the authenticator SHALL require the input of the additional factor.
-->

アクティベーション情報に加えて，多要素OTP Authenticatorは2つの永続的な値を含んでいる．1つ目はデバイスの有効期間の間永続する対称鍵である．2つ目は，Authenticator利用の都度変化する，またはリアルタイムクロックに基づいているノンスである．
<!--
In addition to activation information, multi-factor OTP authenticators contain two persistent values. The first is a symmetric key that persists for the device's lifetime. The second is a nonce that is either changed each time the authenticator is used or is based on a real-time clock.
-->

秘密鍵とそのアルゴリズムは少なくとも[[SP 800-131A]](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)であるものとする(SHALL)．ノンスは，デバイスの生存期間に渡りデバイスが操作される都度一意な値であることを確実にするために十分長いこととする(SHALL). OTP Authenticatorは - 特にソフトウェアベースのOTP生成器の場合 - 複数デバイスに対して秘密鍵を複製する行為を思いとどまらせるべきであり(SHOULD)，助長しないものとする(SHALL NOT)．
<!--
The secret key and its algorithm SHALL provide at least the minimum security strength specified in the latest revision of [[SP 800-131A]](#SP800-131A) (112 bits as of the date of this publication). The nonce SHALL be of sufficient length to ensure that it is unique for each operation of the device over its lifetime. OTP authenticators — particularly software-based OTP generators — SHOULD discourage and SHALL NOT facilitate the cloning of the secret key onto multiple devices.
-->

Authenticator出力は，鍵とノンスとを安全な方法で組み合わせ，Approveされたブロック暗号またはハッシュ関数を用いることで得られる．Authenticator出力は少なくとも(約20ビットのエントロピーの)6桁の数字になるよう切り詰めてもよい(MAY)．
<!--
The authenticator output is obtained by using an approved block cipher or hash function to combine the key and nonce in a secure manner. The authenticator output MAY be truncated to as few as 6 decimal digits (approximately 20 bits of entropy).
-->

もしAuthenticator出力を生成するために利用されるノンスがリアルタイムクロックをベースとしている場合，ノンスは少なくとも2分毎に変化するものとする(SHALL)．与えられたノンスと関連するOTP値は一度だけ受け入れられるものとする(SHALL)．
<!--
If the nonce used to generate the authenticator output is based on a real-time clock, the nonce SHALL be changed at least once every 2 minutes. The OTP value associated with a given nonce SHALL be accepted only once.
-->

Authenticatorのアクティベーションのために利用される記憶シークレットは，ランダムに選ばれた最低6文字の数字または[Section 5.1.1.2](#memsecretver)に記載されているものと同等な複雑さを備えた他の記憶シークレットであるものとし(SHALL)，[Section 5.2.2](#throttle)に記載されているようにレート制限が行われるものとする(SHALL)．バイオメトリックのアクティベーション要素は，[Section 5.2.3](#biometric_use)の要件を満たすものとし(SHALL)，連続するAuthentication失敗回数に制限がある．
<!--
A memorized secret used by the authenticator for activation SHALL be a randomly-chosen numeric secret at least 6 decimal digits in length or other memorized secret of comparable complexity as described in [Section 5.1.1.2](#memsecretver) and SHALL be rate limited as specified in [Section 5.2.2](#throttle). A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on the number of consecutive authentication failures.
-->

暗号化されていない秘密鍵とアクティベーションシークレット，またはバイオメトリック標本（及び信号処理により生成されたプローブのようなバイオメトリック標本に由来する任意のバイオメトリックデータ）は，パスワード生成が終わると直ちにゼロ埋めされるものとする(SHALL)．
<!--
The unencrypted secret key and activation secret or biometric sample (and any biometric data derived from the biometric sample such as a probe produced through signal processing) SHALL be zeroized immediately after a password has been generated.
-->

#### 5.1.5.2 多要素OTP Verifier
<!--
#### 5.1.5.2 Multi-Factor OTP Verifiers
-->

多要素OTP Verifierは，AuthenticatorによるOTPの生成プロセスを実質的に再現するが，2要素目の要求は行わない．例えば，Authenticatorが用いる対象鍵は，セキュリティ侵害に対して強力な防御が行われているものとする(SHALL)．
<!--
Multi-factor OTP verifiers effectively duplicate the process of generating the OTP used by the authenticator, but without the requirement that a second factor be provided. As such, the symmetric keys used by authenticators SHALL be strongly protected against compromise.
-->

多要素OTP AuthenticatorがSubscriberアカウントに紐付けられている時，Verifierまたは関連するCSPは，Authenticatorの出力を再現するために必要なシークレットを生成，交換または取得するためにApproveされた暗号理論を利用するものとする(SHALL)．VerifierまたはCSPは，Authenticatorの出所によって，Authenticatorが多要素デバイスであることを証明するものとする(SHALL)．それが多要素Authenticatorであるという信頼できる報告がない場合、Verifierは[Section 5.1.4](#singlefactorOTP)に従いAuthenticatorを単一要素として扱うものとする(SHALL)．
<!--
When a multi-factor OTP authenticator is being associated with a subscriber account, the verifier or associated CSP SHALL use approved cryptography to either generate and exchange or to obtain the secrets required to duplicate the authenticator output. The verifier or CSP SHALL also establish, via the authenticator source, that the authenticator is a multi-factor device. In the absence of a trusted statement that it is a multi-factor device, the verifier SHALL treat the authenticator as single-factor, in accordance with [Section 5.1.4](#singlefactorOTP).
-->

Verifierは，OTPを収集する際の盗聴や中間者攻撃に対抗するために，Approveされた暗号化を利用し，Authenticateされた保護チャネルを利用するものとする(SHALL)．時間ベースのOTP[[RFC 6238]](#RFC6238)は，有効期間を定義するものとし(SHALL)，Authenticator自体の寿命までに予想される（何れの方向に対する）時刻ずれにネットワーク遅延とユーザによるOTP入力の許容時間を加えて決定される．[Section 5.2.8](#replay)に記載されているリプレイ耐性を備えるために，Verifierは指定された時間ベースのOTPを有効期間で一度だけ受け付けるものとする(SHALL)．あるOTPの使い回しによりClaimantのAuthenticationが拒否されるような場合には，VerifierはClaimantに対して，攻撃者が先回りしてAuthenticationを行うことができる可能性があることを警告してもよい(MAY)．Verifierは，あるOTPの使い回しが試みられた既存セッションのSubscriberに対して同様に警告してもよい(MAY)．
<!--
The verifier SHALL use approved encryption and an authenticated protected channel when collecting the OTP in order to provide resistance to eavesdropping and MitM attacks. Time-based OTPs [[RFC 6238]](#RFC6238) SHALL have a defined lifetime that is determined by the expected clock drift — in either direction — of the authenticator over its lifetime, plus allowance for network delay and user entry of the OTP. In order to provide replay resistance as described in [Section 5.2.8](#replay), verifiers SHALL accept a given time-based OTP only once during the validity period. In the event a claimant's authentication is denied due to duplicate use of an OTP, verifiers MAY warn the claimant in case an attacker has been able to authenticate in advance. Verifiers MAY also warn a subscriber in an existing session of the attempted duplicate use of an OTP.
-->

もしAuthenticator出力またはアクティベーションシークレットが64ビット未満のエントロピーを持つ場合は，Verifierは，[Section 5.2.2](#throttle)に記載されているように，SubscriberのアカウントにおけるAuthentication失敗回数を効果的に制限するレート制限の仕組みを実装するものとする(SHALL)．バイオメトリックのアクティベーション要素は，[Section 5.2.3](#biometric_use)の要件を満たすものとし(SHALL)，連続するAuthentication失敗回数に制限がある．
<!--
If the authenticator output or activation secret has less than 64 bits of entropy, the verifier SHALL implement a rate-limiting mechanism that effectively limits the number of failed authentication attempts that can be made on the subscriber's account as described in [Section 5.2.2](#throttle). A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on the number of consecutive authentication failures.
-->

#### <a name="sfcs"></a> 5.1.6 単一要素暗号ソフトウェア
<!--
#### <a name="sfcs"></a> 5.1.6 Single-Factor Cryptographic Software
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-software-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>単一要素ソフトウェア暗号Authenticatorは、ディスクあるいは"ソフト"媒体に記録された暗号鍵である．Authenticationは鍵の所有と制御を証明することで行われる．Authenticator出力は特定の暗号プロトコルに強く依存し、一般的にはある種の署名付メッセージになっている．単一要素ソフトウェア暗号Authenticatorは<i>something you have</i>である．</td>
    <!--
    <td>A single-factor software cryptographic authenticator is a cryptographic key stored on disk or some other "soft" media. Authentication is accomplished by proving possession and control of the key. The authenticator output is highly dependent on the specific cryptographic protocol, but it is generally some type of signed message. The single-factor software cryptographic authenticator is <i>something you have</i>.</td>
    -->
  </tr>
  </table>
  </div>


#### <a name="sfcsa"></a>5.1.6.1 単一要素暗号ソフトウェアAuthenticator
#### <a name="sfcsa"></a>5.1.6.1 Single-Factor Cryptographic Software Authenticators

単一要素暗号ソフトウェアAuthenticatorは、Authenticatorで一意な秘密鍵を保持している．鍵はAuthenticatorアプリケーションが利用可能なデバイス上で適切にセキュアであるストレージ(例:キーチェーンストレージ，TPMまたは可能であればTEE)に記録されるものとする(SHALL)．デバイス上のソフトウェアコンポーネントがアクセス要求を行ったときのみ鍵にアクセスできるよう制限するアクセス制御を用いて、鍵は許可のない暴露から強力に保護されているものとする(SHALL)．単一要素暗号ソフトウェアAuthenticatorは，複数デバイスに対して秘密鍵を複製する行為を思いとどまらせるべきであり(SHOULD)，助長しないものとする(SHALL NOT)．
<!--
Single-factor software cryptographic authenticators encapsulate a secret key that is unique to the authenticator. The key SHALL be stored in suitably secure storage available to the authenticator application (e.g., keychain storage, TPM, or TEE if available). The key SHALL be strongly protected against unauthorized disclosure by the use of access controls that limit access to the key to only those software components on the device requiring access. Single-factor cryptographic software authenticators SHOULD discourage and SHALL NOT facilitate the cloning of the secret key onto multiple devices.
-->

#### 5.1.6.2 単一要素暗号ソフトウェアVerifier
<!--
#### 5.1.6.2 Single-Factor Cryptographic Software Verifiers
-->

単一要素暗号ソフトウェアVerifierに対する要件は，[Section 5.1.7.2](#sfcdv) に記載されている単一要素暗号デバイスVerifierに対する要件と同一である．
<!--
The requirements for a single-factor cryptographic software verifier are identical to those for a single-factor cryptographic device verifier, described in [Section 5.1.7.2](#sfcdv).
-->

#### <a name="sfcd"></a> 5.1.7 単一要素暗号デバイス
<!--
#### <a name="sfcd"></a> 5.1.7 Single-Factor Cryptographic Devices
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>単一要素暗号デバイスは，保護された暗号鍵を用いた暗号操作，及びユーザエンドポイントに対する直接コネクションを介してAuthenticator出力を提供するハードウェアデバイスである．デバイスは組み込みの対象暗号鍵，非対称暗号鍵を利用し，Authenticationの2要素目を用いたアクティベーションを要求しない．AuthenticationはAuthenticationプロトコルを介してデバイスの所持証明を行うことにより達成される．Authenticator出力はユーザエンドポイントに対する直接接続により提供され，特定の暗号デバイスとプロトコルに強く依存し，典型的にはある種の署名付メッセージになっている．単一要素暗号デバイスは<i>something you have</i>である．</td>
<!--
    <td>A single-factor cryptographic device is a hardware device that performs cryptographic operations using protected cryptographic key(s) and provides the authenticator output via direct connection to the user endpoint. The device uses embedded symmetric or asymmetric cryptographic keys, and does not require activation through a second factor of authentication. Authentication is accomplished by proving possession of the device via the authentication protocol. The authenticator output is provided by direct connection to the user endpoint and is highly dependent on the specific cryptographic device and protocol, but it is typically some type of signed message. A single-factor cryptographic device is <i>something you have</i>.</td>
    -->
  </tr>
  </table>
  </div>

#### 5.1.7.1 <a name="sfcda"></a>単一要素暗号デバイスAuthenticator
<!--
#### 5.1.7.1 <a name="sfcda"></a>Single-Factor Cryptographic Device Authenticators
-->

単一要素暗号デバイスAuthenticatorは秘密鍵を格納しており，その鍵はデバイスで一意かつエクスポートされない(つまりデバイスから除去することができない)ものとする(SHALL NOT)．Authenticatorは，通常はUSBポートなどのコンピュータに対するダイレクトなインタフェースを介して提供されるチャレンジノンスに署名することで動作する．暗号デバイスはソフトウェアを含んでいるが，全ての組み込みソフトウェアがCSP(または発行者)の制御下にあるという点，及びAuthenticator全体でAuthentication時のAALにおけるFIPS 140要件に適合する必要がある点において，暗号ソフトウェアAuthenticatorとは異なる．
<!--
Single-factor cryptographic device authenticators encapsulate a secret key that is unique to the device and SHALL NOT be exportable (i.e., it cannot be removed from the device). The authenticator operates by signing a challenge nonce presented through a direct computer interface (e.g., a USB port). Although cryptographic devices contain software, they differ from cryptographic software authenticators in that all embedded software is under control of the CSP or issuer and that the entire authenticator is subject to all applicable FIPS 140 requirements at the AAL being authenticated.
-->

秘密鍵とそのアルゴリズムは少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)であるものとする(SHALL)．チャレンジノンスは少なくとも64ビット長であるものとする(SHALL)．Approveされた暗号理論が利用されるものとする(SHALL)．
<!--
The secret key and its algorithm SHALL provide at least the minimum security length specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication). The challenge nonce SHALL be at least 64 bits in length. Approved cryptography SHALL be used.
-->

単一要素暗号デバイスAuthenticatorは動作するために(ボタンを押すなどの)物理的な入力を必要とすべきである(SHOULD)．これにより，デバイスが接続している先がセキュリティ侵害をうけているような場合に起こりうる，デバイスの意図しない動作を防止することができる．
<!--
Single-factor cryptographic device authenticators SHOULD require a physical input (e.g., the pressing of a button) in order to operate. This provides defense against unintended operation of the device, which might occur if the endpoint to which it is connected is compromised.
-->

#### 5.1.7.2 <a name="sfcdv"></a>単一要素暗号デバイスVerifier
<!--
#### 5.1.7.2 <a name="sfcdv"></a>Single-Factor Cryptographic Device Verifiers
-->

単一要素暗号デバイスVerifierはチャレンジノンスを生成して，対応するAuthenticatorに送信する．また，Authenticator出力をデバイスの所有を検証するために用いる．Authenticator出力は特定の暗号デバイスとプロトコルに強く依存し，典型的にはある種の署名付メッセージになっている．
<!--
Single-factor cryptographic device verifiers generate a challenge nonce, send it to the corresponding authenticator, and use the authenticator output to verify possession of the device. The authenticator output is highly dependent on the specific cryptographic device and protocol, but it is generally some type of signed message.
-->

Verifierは，各Authenticatorに対応する対象鍵または非対称暗号鍵を保持している．どちらのタイプの鍵も改変に対して保護されているものとし(SHALL)，対象鍵については追加で許可のない暴露に対して保護されているものとする(SHALL)．
<!--
The verifier has either symmetric or asymmetric cryptographic keys corresponding to each authenticator. While both types of keys SHALL be protected against modification, symmetric keys SHALL additionally be protected against unauthorized disclosure.
-->

チャレンジノンスは少なくとも64ビット長であるとし(SHALL)，Authenticatorの有効期間を通じて一意，または統計上一意(したがって，Approveされた乱数生成器[[SP 800-90Ar1]](#SP800-90Ar1)を用いて生成されたもの)であるとする(SHALL)．
<!--
The challenge nonce SHALL be at least 64 bits in length, and SHALL either be unique over the authenticator's lifetime or statistically unique (i.e., generated using an approved random bit generator [[SP 800-90Ar1]](#SP800-90Ar1)). The verification operation SHALL use approved cryptography.
-->

#### <a name="mfcs"></a> 5.1.8 多要素暗号ソフトウェア
<!--
#### <a name="mfcs"></a> 5.1.8 Multi-Factor Cryptographic Software
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-software-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>多要素ソフトウェア暗号Authenticatorは，ディスクあるいは"ソフト"媒体に記録された暗号鍵であり，Authenticationの2要素目を用いたアクティベーションを必要とする．Authenticationは鍵の所有と制御を証明することで行われる．Authenticator出力は特定の暗号プロトコルに強く依存し，一般的にはある種の署名付メッセージになっている．多要素ソフトウェア暗号Authenticatorは<i>something you have</i>であり，<i>something you know</i>または<i>something you are</i>のどちらかによってアクティベートされるものとする(SHALL)．</td>
    <!--
    <td>A multi-factor software cryptographic authenticator is a cryptographic key stored on disk or some other "soft" media that requires activation through a second factor of authentication. Authentication is accomplished by proving possession and control of the key. The authenticator output is highly dependent on the specific cryptographic protocol, but it is generally some type of signed message. The multi-factor software cryptographic authenticator is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td>
    -->
  </tr>
  </table>
  </div>

#### <a name="mfcsa"></a>5.1.8.1 多要素暗号ソフトウェアAuthenticators
<!--
#### <a name="mfcsa"></a>5.1.8.1 Multi-Factor Cryptographic Software Authenticators
-->

多要素暗号ソフトウェアAuthenticatorは秘密鍵を格納しており，その鍵はデバイスで一意であり記憶シークレットやバイオメトリックなどの追加の要素の入力を経たときだけアクセスできる．鍵はAuthenticatorアプリケーションが利用可能なデバイス上で適切にセキュアであるストレージ(例:キーチェーンストレージ，TPM，TEE)に記録されるべきである(SHOULD)．デバイス上のソフトウェアコンポーネントがアクセス要求を行ったときのみ鍵にアクセスできるよう制限するアクセス制御を用いて、鍵は許可のない暴露から強力に保護されているものとする(SHALL)．多要素暗号ソフトウェアAuthenticatorは，複数デバイスに対して秘密鍵を複製する行為を思いとどまらせるべきであり(SHOULD)，助長しないものとする(SHALL NOT)．

<!--
Multi-factor software cryptographic authenticators encapsulate a secret key that is unique to the authenticator and is accessible only through the input of an additional factor, either a memorized secret or a biometric. The key SHOULD be stored in suitably secure storage available to the authenticator application (e.g., keychain storage, TPM, TEE). The key SHALL be strongly protected against unauthorized disclosure by the use of access controls that limit access to the key to only those software components on the device requiring access. Multi-factor cryptographic software authenticators SHOULD discourage and SHALL NOT facilitate the cloning of the secret key onto multiple devices.
-->

Authenticatorを用いた各Authentication操作には両方の要素の入力を必要とするものとする(SHALL)．
<!--
Each authentication operation using the authenticator SHALL require the input of both factors.
-->

Authenticatorのアクティベーションのために利用される記憶シークレットは，最低6文字の数字または同等な複雑さを備えたものとし(SHALL)，[Section 5.2.2](#throttle)に記載されているようにレート制限が行われるものとする(SHALL)．バイオメトリックのアクティベーション要素は，[Section 5.2.3](#biometric_use)の要件を満たすものとし(SHALL)，連続するAuthentication失敗回数に対する制限を含むものとする．
<!--
Any memorized secret used by the authenticator for activation SHALL be at least 6 decimal digits in length, or equivalent complexity, and SHALL be rate limited as specified in [Section 5.2.2](#throttle). A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), and SHALL include limits on the allowable number of consecutive authentication failures.
-->

暗号化されていない秘密鍵とアクティベーションシークレット，またはバイオメトリック標本（及び信号処理により生成されたプローブのようなバイオメトリック標本に由来する任意のバイオメトリックデータ）は，Authenticationトランザクションが行われたら直ちにゼロ埋めされるものとする(SHALL)．
<!--
The unencrypted key and activation secret or biometric sample — and any biometric data derived from the biometric sample such as a probe produced through signal processing — SHALL be zeroized immediately after an authentication transaction has taken place.
-->

#### 5.1.8.2 多要素暗号ソフトウェアVerifier
<!--
#### 5.1.8.2 Multi-Factor Cryptographic Software Verifiers
-->

多要素暗号ソフトウェアVerifierに対する要件は，[Section 5.1.7.2](#sfcdv) に記載されている単一要素暗号デバイスVerifierに対する要件と同一である．
多要素暗号ソフトウェアAuthenticator出力を検証することで，アクティベーション要素の使用の証明となる．
<!--
The requirements for a multi-factor cryptographic software verifier are identical to those for a single-factor cryptographic device verifier, described in [Section 5.1.7.2](#sfcdv). Verification of the output from a multi-factor cryptographic software authenticator proves use of the activation factor.
-->

#### 5.1.9 <a name="mfcd"></a> 多要素暗号デバイス
<!--
#### 5.1.9 <a name="mfcd"></a> Multi-Factor Cryptographic Devices
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-crypto-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;"/></td>
    <td>多要素暗号デバイスは，1つ以上の保護された暗号鍵を用いた暗号操作を行うハードウェアデバイスであり，2要素目を用いたアクティベーションを要求する．Authenticationはデバイスの所持と鍵の制御を証明することで実現される．Authenticator出力はユーザエンドポイントに対する直接接続を介して提供され，特定の暗号デバイスとプロトコルに強く依存し，典型的にはある種の署名付メッセージになっている．多要素暗号デバイスは<i>something you have</i>であり，<i>something you know</i>または<i>something you are</i>のどちらかによってアクティベートされるものとする(SHALL)．</td>
<!--
    <td>A multi-factor cryptographic device is a hardware device that performs cryptographic operations using one or more protected cryptographic keys and requires activation through a second authentication factor. Authentication is accomplished by proving possession of the device and control of the key. The authenticator output is provided by direct connection to the user endpoint and is highly dependent on the specific cryptographic device and protocol, but it is typically some type of signed message. The multi-factor cryptographic device is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td>
    -->
  </tr>
  </table>
  </div>

#### 5.1.9.1 多要素暗号デバイスAuthenticator
<!--
#### 5.1.9.1 Multi-Factor Cryptographic Device Authenticators
-->

多要素暗号デバイスAuthenticatorは耐タンパ性を有するハードウェアを用いて秘密鍵を格納しており，その鍵はデバイスで一意であり記憶シークレットやバイオメトリックなどの追加の要素の入力を経たときだけアクセスできる．鍵はAuthenticatorアプリケーションが利用可能なデバイス上で適切にセキュアであるストレージ(例:キーチェーンストレージ，TPM，TEE)に記録されるべきである(SHOULD)．デバイス上のソフトウェアコンポーネントがアクセス要求を行ったときのみ鍵にアクセスできるよう制限するアクセス制御を用いて、鍵は許可のない暴露から強力に保護されているものとする(SHALL)．多要素暗号ソフトウェアAuthenticatorは，複数デバイスに対して秘密鍵を複製する行為を思いとどまらせるべきであり(SHOULD)，助長しないものとする(SHALL NOT)．
<!--
Multi-factor cryptographic device authenticators use tamper-resistant hardware to encapsulate a secret key that is unique to the authenticator and accessible only through the input of an additional factor, either a memorized secret or a biometric. The authenticator operates by signing a challenge nonce presented through a direct computer interface (e.g., a USB port). Although cryptographic devices contain software, they differ from cryptographic software authenticators in that all embedded software is under control of the CSP or issuer, and that the entire authenticator is subject to any applicable FIPS 140 requirements at the selected AAL.
-->

秘密鍵とそのアルゴリズムは少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)であるものとする(SHALL)．チャレンジノンスは少なくとも64ビット長であるものとする(SHALL)．Approveされた暗号理論が利用されるものとする(SHALL)．
<!--
The secret key and its algorithm SHALL provide at least the minimum security length specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication). The challenge nonce SHALL be at least 64 bits in length. Approved cryptography SHALL be used.

Authenticatorを用いた各Authentication操作には追加の要素の入力を必要とすべきである(SOULD)．追加要素の入力は，デバイスへの直接入力かハードウェア接続(例：USB，スマートカード)を介して実施されてもよい(MAY)．
<!--
Each authentication operation using the authenticator SHOULD require the input of the additional factor. Input of the additional factor MAY be accomplished via either direct input on the device or via a hardware connection (e.g., USB, smartcard).
-->

Authenticatorのアクティベーションのために利用される記憶シークレットは，最低6文字の数字または同等な複雑さを備えたものとし(SHALL)，[Section 5.2.2](#throttle)に記載されているようにレート制限が行われるものとする(SHALL)．バイオメトリックのアクティベーション要素は，[Section 5.2.3](#biometric_use)の要件を満たすものとし(SHALL)，連続するAuthentication失敗回数に対する制限を含むものとする．
<!--
Any memorized secret used by the authenticator for activation SHALL be at least 6 decimal digits in length, or equivalent complexity, and SHALL be rate limited as specified in [Section 5.2.2](#throttle). A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), and SHALL include limits on the number of consecutive authentication failures.
-->

暗号化されていない秘密鍵とアクティベーションシークレット，またはバイオメトリック標本（及び信号処理により生成されたプローブのようなバイオメトリック標本に由来する任意のバイオメトリックデータ）は，Authenticationトランザクションが行われたら直ちにメモリが上書きされるものとする(SHALL)．
<!--
The unencrypted key and activation secret or biometric sample — and any biometric data derived from the biometric sample such as a probe produced through signal processing — SHALL be overwritten in memory immediately after an authentication transaction has taken place.
-->

#### <a name="mfcdv"></a>5.1.9.2多要素暗号デバイスVerifier
<!--
#### <a name="mfcdv"></a>5.1.9.2 Multi-Factor Cryptographic Device Verifiers
-->

多要素暗号デバイスVerifierに対する要件は，[Section 5.1.7.2](#sfcdv) に記載されている単一要素暗号デバイスVerifierに対する要件と同一である．
多要素暗号デバイスAuthenticator出力を検証することで，アクティベーション要素の使用の証明となる．
<!--
The requirements for a multi-factor cryptographic device verifier are identical to those for a single-factor cryptographic device verifier, described in [Section 5.1.7.2](#sfcdv). Verification of the authenticator output from a multi-factor cryptographic device proves use of the activation factor.
-->

#### 5.2. 一般Authenticator要件
<!--
#### 5.2 General Authenticator Requirements
-->

#### 5.2.1 Physical Authenticators

CSPはSubscriberに対して，Authenticatorの盗難や紛失を正しく防止する方法について指示するものとする(SHALL)．CSPはSubscriberから認証機の盗難や紛失の疑いがある旨の通知に対し，直ちにAuthenticatorを無効化，停止するメカニズムを備えるものとする(SHALL)．
<!--
CSPs SHALL provide subscriber instructions on how to appropriately protect the authenticator against theft or loss. The CSP SHALL provide a mechanism to revoke or suspend the authenticator immediately upon notification from subscriber that loss or theft of the authenticator is suspected.
-->

#### <a name="throttle"></a>5.2.2 レート制限 (スロットリング)
<!--
#### <a name="throttle"></a>5.2.2 Rate Limiting (Throttling)
-->

[Section 5.1](#reqauthtype)のAuthenticatorタイプの説明で要求される場合，Verifierはオンライン推測攻撃に対抗するための制御を実装するものとする(SHALL)．指定されたAuthenticatorの説明に記載がなければ，Verifierはオンライン攻撃者に対し，同一アカウントで100回以上の連続した認証失敗試行を制限をするものとする(SHALL)．
<!--
When required by the authenticator type descriptions in [Section 5.1](#reqauthtype), the verifier SHALL implement controls to protect against online guessing attacks. Unless otherwise specified in the description of a given authenticator, the verifier SHALL limit consecutive failed authentication attempts on a single account to no more than 100.
-->

レート制限の結果として攻撃者が正しいclaimantをロックアウトさせる頻度を減少させるために用いられる追加のテクニックを用いてもよい(MAY)．追加テクニックは以下を含む:
<!--
Additional techniques MAY be used to reduce the likelihood that an attacker will lock the legitimate claimant out as a result of rate limiting. These include:
-->

- Claimantに対して，Authentication試行前にCAPTCHAの入力を要求する．

<!--
- Requiring the claimant to complete a CAPTCHA before attempting authentication.
-->

- Claimantに対して認証失敗後に一定期間待つように要求し，連続する認証失敗の最大回数に近づくにつれてその時間を(例えば30秒から1時間まで)増加させる．

<!--
- Requiring the claimant to wait following a failed attempt for a period of time that increases as the account approaches its maximum allowance for consecutive failed attempts (e.g., 30 seconds up to an hour).
-->

- Subscriberが以前Authenticationに成功したことがあるIPアドレスのホワイトリストからのみ行われるAuthentication要求だけを受理する．

<!--
- Accepting only authentication requests that come from a white list of IP addresses from which the subscriber has been successfully authenticated before.
-->

- ユーザの振る舞いが通常の範疇にあるかないかを特定するリスクベースまたは適応型Authenticationの手法を活用する．

<!--
- Leveraging other risk-based or adaptive authentication techniques to identify user behavior that falls within, or out of, typical norms.
-->

SubscriberがAuthenticationに成功した場合，Verifierは同一IPアドレスからの以前の失敗したAuthenticationの試行を無視すべきである(SHOULD)．

<!--
When the subscriber successfully authenticates, the verifier SHOULD disregard any previous failed attempts for that user from the same IP address.
-->

#### <a name="biometric_use"></a>5.2.3 バイオメトリクスの利用
<!--
#### <a name="biometric_use"></a>5.2.3 Use of Biometrics
-->

Authenticationにおけるバイオメトリクス(*something you are*)の利用は，物理的な特性(例：指紋，虹彩，顔の特徴)及び振る舞い特性(例：タイピングのリズム)の両方を測定法を含んでいる．[Section 5.2.9](#intent)に記載されているAuthentication意図を確認する範囲とは差があるかもしれないが，両方の分類ともに，異なるバイオメトリック計測手段とみなされる．
<!--
The use of biometrics (*something you are*) in authentication includes both measurement of physical characteristics (e.g., fingerprint, iris, facial characteristics) and behavioral characteristics (e.g., typing cadence). Both classes are considered biometric modalities, although different modalities may differ in the extent to which they establish authentication intent as described in [Section 5.2.9](#intent).
-->

様々な理由で，本書はAuthenticationにおけるバイオメトリクスの利用を限定的にサポートする．それらは以下のとおりである:
<!--
For a variety of reasons, this document supports only limited use of biometrics for authentication. These reasons include:
-->

- バイオメトリックのFalse Match Rate(FMR)は，それ自身ではSubscriberのAuthenticationにおける確実性を与えるものではない．更に，FMRはスプーフィング攻撃を考慮したものではない．

<!--
- The biometric False Match Rate (FMR) does not provide confidence in the authentication of the subscriber by itself. In addition, FMR does not account for spoofing attacks.
-->

- バイオメトリックの比較は確率的なものであるが，他のAuthentication要素は決定的なものである．

<!--
- Biometric comparison is probabilistic, whereas the other authentication factors are deterministic.
-->

- バイオメトリックのテンプレート保護スキームは，他のAuthentication要素(例: PKI証明書やパスワード)に相当するバイオメトリッククレデンシャルを無効化するための手段を提供する．しかしながら，そのようなソリューションの可用性は制限されており，これらの手段を試験するための標準も策定中の段階である．

<!--
- Biometric template protection schemes provide a method for revoking biometric credentials that is comparable to other authentication factors (e.g., PKI certificates and passwords). However, the availability of such solutions is limited, and standards for testing these methods are under development.
-->

- バイオメトリック特性はシークレットにはならない．それらはオンラインで取得したり，知識のあるなしに関わらず誰かが携帯電話のカメラで(例えば顔の)写真を取ることができ，誰かが触った物から(例えば潜在的に指紋を)採取することができ，高精細な画像から(例えば虹彩パターンを)キャプチャすることができる．生体検知のようなPresentation attack detaction(PAD)技術は，これらの種別の攻撃リスクを緩和することができるが，センサーやバイオメトリック処理はCSPとSubscriberのニーズに合うようにPADを適切に実施していることを保証する必要がある．

<!--
- Biometric characteristics do not constitute secrets. They can be obtained online or by taking a picture of someone with a camera phone (e.g., facial images) with or without their knowledge, lifted from objects someone touches (e.g., latent fingerprints), or captured with high resolution images (e.g., iris patterns). While presentation attack detection (PAD) technologies (e.g., liveness detection) can mitigate the risk of these types of attacks, additional trust in the sensor or biometric processing is required to ensure that PAD is operating in accordance with the needs of the CSP and the subscriber.
-->

したがって，Authenticationにおける制限されたバイオメトリクスの利用は，以下の要件とガイドラインの下でサポートされる:
<!--
Therefore, the limited use of biometrics for authentication is supported with the following requirements and guidelines:
-->

バイオメトリクスは物理的なAuthenticatorを用いた多要素Authentication(*something you have*)の一部としてのみ利用されるものとする(SHALL)．
<!--
Biometrics SHALL be used only as part of multi-factor authentication with a physical authenticator (*something you have*).
-->

センサ(またはセンサ置き換え耐性のあるセンサーを持ったエンドポイント)とVerifier間のAuthenticateされた保護チャネルが確立され(SHALL)，センサーまたはエンドポイントが設置され(SHALL)，Claimantからバイオメトリック標本を取得するのに先立ってセンサーまたはエンドポイントがAuthenticateされているものとする(SHALL)．
<!--
An authenticated protected channel between sensor (or an endpoint containing a sensor that resists sensor replacement) and verifier SHALL be established and the sensor or endpoint SHALL be established and the sensor or endpoint authenticated prior to capturing the biometric sample from the claimant.
-->

バイオメトリックシステムは，FMR [[ISO/IEC 2382-37]](#ISOIEC2382-37)は1000分の1より優れたレートで運用されるものとする．このFMRは[[ISO/IEC 30107-1]](#ISOIEC30107-1)で定義されているConformant attack(すなわちZero-effort imporster attempt)の条件下で達成されるものとする(SHALL)．
<!--
The biometric system SHALL operate with an FMR [[ISO/IEC 2382-37]](#ISOIEC2382-37) of 1 in 1000 or better. This FMR SHALL be achieved under conditions of a conformant attack (i.e., zero-effort impostor attempt) as defined in [[ISO/IEC 30107-1]](#ISOIEC30107-1).
-->

バイオメトリックシステムは，PADを実装すべきである(SHOULD)．バイオメトリックシステムを配備を目的として実施するテストでは，各関連攻撃タイプ(すなわち種類)に対して少なくとも90%の耐性があることを示すべきである(SHOULD)．ここでの耐性はプレゼンテーション攻撃の失敗回数をプレゼンテーション攻撃の試行回数で割ったものとして定義される．プレゼンテーション攻撃耐性のテストは，[[ISO/IEC 30107-3]](#ISOIEC30107-3)の12条に従い行われるものとする(SHALL)．PADはClaimantのデバイス上でローカルに実施されても，または中央のVerifierによって実施されてもよい(MAY)．
<!--
The biometric system SHOULD implement PAD. Testing of the biometric system to be deployed SHOULD demonstrate at least 90% resistance to presentation attacks for each relevant attack type (i.e., species), where resistance is defined as the number of thwarted presentation attacks divided by the number of trial presentation attacks. Testing of presentation attack resistance SHALL be in accordance with Clause 12 of [[ISO/IEC 30107-3]](#ISOIEC30107-3). The PAD decision MAY be made either locally on the claimant's device or by a central verifier.
-->

>注釈: PADはガイドラインの将来の版では必須要件としてみなされる．
<!--
>Note: PAD is being considered as a mandatory requirement in future editions of this guideline.
-->

バイオメトリックシステム5回の連続したAuthentication試行の失敗を許容するものとする(SHALL)．もしPADが上記の要件を満たして実装されている場合は，10回の連続したAuthentication試行の失敗を許容するものとする(SHALL)．一度上限に達すると，バイオメトリックAuthenticatorは以下の何れかであるものとする(SHALL): 
<!--
The biometric system SHALL allow no more than 5 consecutive failed authentication attempts or 10 consecutive failed attempts if PAD meeting the above requirements is implemented. Once that limit has been reached, the biometric authenticator SHALL either:
-->

- 次回の試行までに少なくとも30秒の遅延を課し，試行回数が増える毎に指数関数的に遅延を増加させる(例えば，後続の失敗する試行の前に1分，その次の試行では2分)か，

<!--
- Impose a delay of at least 30 seconds before the next attempt, increasing exponentially with each successive attempt (e.g., 1 minute before the following failed attempt, 2 minutes before the second following attempt), or
-->

- もし既に利用可能な代替手段があるのであれば，バイオメトリックユーザAuthenticationを無効化し，もう一つの要素(例えば，異なるバイオメトリック計測手段や，まだ要求されていない要素であればPIN/パスコード)の利用を試みる．

<!--
- Disable the biometric user authentication and offer another factor (e.g., a different biometric modality or a PIN/Passcode if it is not already a required factor) if such an alternative method is already available.
-->

Verifierはセンサー及びポイントのパフォーマンス，一貫性，真正性について決定するものとする(SHALL)．この決定を行うために容認できる方法として以下があるが，限定はされていない:
<!--
The verifier SHALL make a determination of sensor and endpoint performance, integrity, and authenticity. Acceptable methods for making this determination include, but are not limited to:
-->

* センサー及びエンドポイントのAuthentication．
* 承認済みの適格性認定機関による認定．
* [Section 5.2.4](#attestation)に記載されている署名済みメタデータの実効時照会(例: アテステーション)

<!--
* Authentication of the sensor or endpoint.
* Certification by an approved accreditation authority.
* Runtime interrogation of signed metadata (e.g., attestation) as described in [Section 5.2.4](#attestation).
-->

バイオメトリックの比較はClaimantのデバイス上でローカルに実施されるか，中央のVerifierで実施される．中央のVerifierでの大規模な攻撃の可能性が増加しつつあるため，ローカルでの比較が好ましい．
<!--
Biometric comparison can be performed locally on claimant's device or at a central verifier. Since the potential for attacks on a larger scale is greater at central verifiers, local comparison is preferred.
-->

もし比較が中央で実施される場合:
<!--
If comparison is performed centrally:
-->

* Authenticationとしてのバイオメトリック利用はApproveされた暗号理論を用いて特定される一つ以上の特定デバイスに限定されるものとする(SHALL)．バイオメトリックがまだメインのAuthentication鍵をアンロックしていないのであれば，分離している鍵がデバイスの特定のために利用されるものとする(SHALL)．
* バイオメトリックの破棄は，[ISO/IEC 24745](#ISO24745)中のバイオメトリックテンプレート保護と呼ばれており，実装するものとする(SHALL)．
* 全てのバイオメトリクスの送信はAuthenticateされた保護チャネルを介して行われる．．

<!--
* Use of the biometric as an authentication factor SHALL be limited to one or more specific devices that are identified using approved cryptography. Since the biometric has not yet unlocked the main authentication key, a separate key SHALL be used for identifying the device.
* Biometric revocation, referred to as biometric template protection in [ISO/IEC 24745](#ISO24745), SHALL be implemented.
* All transmission of biometrics SHALL be over the authenticated protected channel.
-->

Authenticationプロセス中で収集されたバイオメトリック標本は，ユーザの同意の下で，研究目的で比較アルゴリズムの学習に利用してもよい(MAY)．バイオメトリック標本及び信号処理により生成されたプローブのようなバイオメトリック標本に由来する任意のバイオメトリックデータは，学習や派生した研究データが得られた後は直ちにゼロ埋めされるものとする(SHALL)．

<!--
Biometric samples collected in the authentication process MAY be used to train comparison algorithms or — with user consent — for other research purposes. Biometric samples and any biometric data derived from the biometric sample such as a probe produced through signal processing SHALL be zeroized immediately after any training or research data has been derived.
-->

バイオメトリクスは，[SP 800-63A](sp800-63a.html)で記載されている全てのEnrollmentプロセスフェーズにおいて，Enrollmentの否認を防ぐため，また関与する同一個人であることを検証するために利用される．
<!--
Biometrics are also used in some cases to prevent repudiation of enrollment and to verify that the same individual participates in all phases of the enrollment process as described in [SP 800-63A](sp800-63a.html).
-->

#### <a name="attestation"></a>5.2.4 アテステーション
<!--
#### <a name="attestation"></a>5.2.4 Attestation
-->

アテステーションは，直接接続されているAuthenticatorやAuthentication操作に参加するエンドポイントに関してVerifierに対して伝達される情報のことである．アテステーションにより伝達される情報は次を含んでもよい(MAY)が，限定はされていない:

<!--
An attestation is information conveyed to the verifier regarding a directly-connected authenticator or the endpoint involved in an authentication operation. Information conveyed by attestation MAY include, but is not limited to:
-->

* Authenticatorやエンドポイントの出所(例えば，製造元やサプライヤ認定など)，健康および一貫性．
* Authenticatorのセキュリティ機能
* バイオメトリックセンサーのセキュリティや性能特性
* センサー計測手段

<!--
* The provenance (e.g., manufacturer or supplier certification), health, and integrity of the authenticator and endpoint.
* Security features of the authenticator.
* Security and performance characteristics of biometric sensor(s).
* Sensor modality.
-->

このアテステーションが署名される場合，少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)を備えるデジタル署名を用いて署名されるものとする(SHALL)．
<!--
If this attestation is signed, it SHALL be signed using a digital signature that provides at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication).
-->

アテステーション情報は，VerifierのリスクベースAuthenticationの判断の一部に利用してもよい(MAY)．
<!--
Attestation information MAY be used as part of a verifier's risk-based authentication decision.
-->

#### <a name="verifimpers"></a>5.2.5 Verifierなりすまし耐性
<!--
#### <a name="verifimpers"></a>5.2.5 Verifier Impersonation Resistance
-->

Verifierなりすまし攻撃は，しばしばフィッシング攻撃と呼ばれ，VerifierやRPになりすまして不用心なClaimantを騙して詐欺サイトに対してAuthenticateさせる試みである．SP 800-63の以前の版では，Verifierなりすまし攻撃に対するプロトコル耐性は，中間者攻撃への強い耐性と呼ばれていた．
<!--
Verifier impersonation attacks, sometimes referred to as "phishing attacks," are attempts by fraudulent verifiers and RPs to fool an unwary claimant into authenticating to an impostor website. In prior versions of SP 800-63, protocols resistant to verifier-impersonation attacks were also referred to as "strongly MitM resistant."
-->

Verifierなりすまし耐性のあるAuthenticationプロトコルは，Authenticateされた保護チャネルをVerifierとの間に確立するものとする(SHALL)．Authenticateされた保護チャネルを確立する際にネゴシエートされたチャネル識別子は強く，変更できない形で(例えば，Verifierが知っている公開鍵に対する，Claimantが制御している秘密鍵を用いて2つの値を署名することにより)Authenticator出力に結び付けられるものとする(SHALL)．Verifierは署名またはVerifierなりすまし耐性を確認するための情報を確認するものとする(SHALL)．このようにすることで，不正なVerifierが，実際のVerifierを表す証明書を得た場合でさえも，異なるAuthenticateされた保護チャネルでAuthenticationを再生することを防止できる．
<!--
A verifier impersonation-resistant authentication protocol SHALL establish an authenticated protected channel with the verifier. It SHALL then strongly and irreversibly bind a channel identifier that was negotiated in establishing the authenticated protected channel to the authenticator output (e.g., by signing the two values together using a private key controlled by the claimant for which the public key is known to the verifier). The verifier SHALL validate the signature or other information used to prove verifier impersonation resistance. This prevents an impostor verifier, even one that has obtained a certificate representing the actual verifier, from replaying that authentication on a different authenticated protected channel.
-->

Verifierなりすまし耐性が要求された場合に，それを確立するためにApproveされた暗号アルゴリズムが利用されるものとする(SHALL)．この目的で利用される鍵は，少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)を備えるものとする(SHALL)．
<!--
Approved cryptographic algorithms SHALL be used to establish verifier impersonation resistance where it is required. Keys used for this purpose SHALL provide at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication).
-->

Verifierなりすまし耐性のあるAuthenticationプロトコルの例としては，Client-authenticated TLSがある．クライアントは，ネゴシエーション済みの特定TLSコネクション対して一意なプロトコルから予めメッセージを受取り，そのメッセージと共にAuthenticator出力に対して署名を行う．
<!--
One example of a verifier impersonation-resistant authentication protocol is client-authenticated TLS, because the client signs the authenticator output along with earlier messages from the protocol that are unique to the particular TLS connection being negotiated.
-->

アウトオブバンドAuthenticatorやOTP Authenticatorのような，Authenticator出力を手動入力するようなAuthenticatorでは，手動入力ではAuthenticator出力を特定のAuthenticateされたセッションに結びつけていないため，Verifierなりすまし耐性があるとは考えないものとする(SHALL NOT)．中間者攻撃の場合には，不正なVerifierはOTP Authenticator出力をVerifierに対して再生し，Authenticationが成功してしまう．
<!--
Authenticators that involve the manual entry of an authenticator output, such as out-of-band and OTP authenticators, SHALL NOT be considered verifier impersonation-resistant because the manual entry does not bind the authenticator output to the specific session being authenticated. In a MitM attack, an impostor verifier could replay the OTP authenticator output to the verifier and successfully authenticate.
-->

#### <a name="csp-verifier"></a>5.2.6 Verifier-CSP通信
<!--
#### <a name="csp-verifier"></a>5.2.6 Verifier-CSP Communications
-->

VerifierとCSPが個別のエンティティである場合([SP 800-63-3 Figure 4-1](sp800-63-3.html#63Sec4-Figure1)の点線で示されているように)，VerifierとCSPの間の通信は，(Client-authenticated TLS接続のような)Approveされた暗号理論を利用する相互にAuthenticateされたセキュアチャネルを介して行われるものとする(SHALL)．
<!--
In situations where the verifier and CSP are separate entities (as shown by the dotted line in [SP 800-63-3 Figure 4-1](sp800-63-3.html#63Sec4-Figure1)), communications between the verifier and CSP SHALL occur through a mutually-authenticated secure channel (such as a client-authenticated TLS connection) using approved cryptography.
-->

#### <a name="verifier-secrets"></a>5.2.7 Verifier侵害耐性
<!--
#### <a name="verifier-secrets"></a>5.2.7 Verifier-Compromise Resistance
-->

いくつかのAuthenticatorタイプを利用に際しては，VerifierがAuthenticatorシークレットのコピーを記録する必要がある．例えば，OTP Authenticator([Section 5.1.4](#singlefactorOTP)で記載)では，VerifierがClaimantから送信された値と比較するために，個別にAuthenticator出力を生成する必要がある．Verifierが侵害され，記録されているシークレットが窃取される可能性があるため，Verifierが永続的にAuthenticationに利用するシークレットを記録する必要のないAuthenticationプロトコルは，より強力であるとみなされ，ここでは*Verifier侵害耐性*があるものとして記載されている．そのようなVerifierが，全ての攻撃に耐性があるのではないことに注意すること．Verifierは，特定のAuthenticator出力を常に受け付けるように操作されるなど，異なる方法で侵害される可能性がある．
<!--
Use of some types of authenticators requires that the verifier store a copy of the authenticator secret. For example, an OTP authenticator (described in [Section 5.1.4](#singlefactorOTP)) requires that the verifier independently generate the authenticator output for comparison against the value sent by the claimant. Because of the potential for the verifier to be compromised and stored secrets stolen, authentication protocols that do not require the verifier to persistently store secrets that could be used for authentication are considered stronger, and are described herein as being *verifier compromise resistant*. Note that such verifiers are not resistant to all attacks. A verifier could be compromised in a different way, such as being manipulated into always accepting a particular authenticator output.
-->

Verifier侵害耐性は異なる方法で実現することができる．例えば:
<!--
Verifier compromise resistance can be achieved in different ways, for example:
-->

- 暗号Authenticatorを利用して，Authenticatorが保持する秘密鍵に対応する公開鍵をVerifierに記録する．

<!--
- Use a cryptographic authenticator that requires the verifier store a public key corresponding to a private key held by the authenticator.
-->

- 期待するAuthenticator出力をハッシュ形式で記録する．この方式は，例えばルックアップシークレット([Section 5.1.2](#lookupsecrets)に記載)で用いることができる．

<!--
- Store the expected authenticator output in hashed form. This method can be used with some look-up secret authenticators (described in [Section 5.1.2](#lookupsecrets)), for example.
-->

Verifier侵害耐性を考慮し，Verifierによって記録される公開鍵は，Approveされた暗号アルゴリズムの利用と関連付けられているものとし(SHALL)，少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)を備えるものとする(SHALL)．
<!--
To be considered verifier compromise resistant, public keys stored by the verifier SHALL be associated with the use of approved cryptographic algorithms and SHALL provide at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication).
-->

他のVerifier侵害耐性のあるシークレットは，Approveされた暗号アルゴリズムを利用するものとし(SHALL)，基礎となるシークレットは少なくとも[SP 800-131A](#SP800-131A)の最新版で定義された最低のセキュリティ強度(本書の刊行現在では112ビット)を備えるものとする(SHALL)．より複雑性の低いシークレット(例えば記憶シークレット)は，辞書の探索や全探索などを通してハッシュ処理を攻略できる可能性があるため，ハッシュされていてもVerifier侵害耐性を持つものと満たさないものとする(SHALL NOT)．
<!--
Other verifier compromise resistant secrets SHALL use approved hash algorithms and the underlying secrets SHALL have at least the minimum security strength specified in the latest revision of [SP 800-131A](#SP800-131A) (112 bits as of the date of this publication). Secrets (e.g., memorized secrets) having lower complexity SHALL NOT be considered verifier compromise resistant when hashed because of the potential to defeat the hashing process through dictionary lookup or exhaustive search.
-->

#### <a name="replay"></a>5.2.8 リプレイ耐性
<!--
#### <a name="replay"></a>5.2.8 Replay Resistance
-->

Authenticationプロセスは，以前のAuthenticationメッセージを記録し再生することでAuthenticationを成功させることが困難であるならば，リプレイアタックに耐性を持つ．リプレイ耐性は，Authenticator出力が保護チャネルに入力されるまえに窃取される可能性があるため，Authenticateされた保護チャネルのリプレイ耐性に加えて施されるものである．ノンスやチャレンジをトランザクションの"新鮮さ"を示すために用いるプロトコルは，再生されるメッセージが適切なノンスや時系列データを含んでおらず，Verifierが容易に過去のプロトコルメッセージが再生されたことを検知しうるため，リプレイ耐性があるといえる．
<!--
An authentication process resists replay attacks if it is impractical to achieve a successful authentication by recording and replaying a previous authentication message. Replay resistance is in addition to the replay-resistant nature of authenticated protected channel protocols, since the output could be stolen prior to entry into the protected channel. Protocols that use nonces or challenges to prove the "freshness" of the transaction are resistant to replay attacks since the verifier will easily detect when old protocol messages are replayed since they will not contain the appropriate nonces or timeliness data.
-->

リプレイ耐性のあるAuthenticatorの例として，OTPデバイス，暗号Authenticatorおよびルックアップシークレットがある．
<!--
Examples of replay-resistant authenticators are OTP devices, cryptographic authenticators, and look-up secrets.
-->

反対に記憶シークレットはAuthenticator出力がシークレットそのものであり，各Authenticationで入力されるため，リプレイ耐性があるものとはみなさない．
<!--
In contrast, memorized secrets are not considered replay resistant because the authenticator output — the secret itself — is provided for each authentication.
-->

#### <a name="intent"></a>5.2.9 Authentication意図
<!--
#### <a name="intent"></a>5.2.9 Authentication Intent
-->

Authenticationプロセスは，Subjectが明示的に各AuthenticationやReauthenticationの要求に応じる必要がある場合，意図を明らかにする．Authentication意図の目的は，直接接続された物理的なAuthenticator(例えば，多要素暗号デイバス)が，エンドポイント上でマルウェアなどによりSubjectが知らないうちに利用されることをより困難にすることである．Authentication意図はそのAuthenticatorそのものにより立証するものとする(SHALL)が，多要素暗号デバイスがそのAuthenticatorが利用されるエンドポイント上で，他のAuthentication要素を再入力することにより立証してもよい(MAY)．
<!--
An authentication process demonstrates intent if it requires the subject to explicitly respond to each authentication or reauthentication request. The goal of authentication intent is to make it more difficult for directly-connected physical authenticators (e.g., multi-factor cryptographic devices) to be used without the subject's knowledge, such as by malware on the endpoint. Authentication intent SHALL be established by the authenticator itself, although multi-factor cryptographic devices MAY establish intent by reentry of the other authentication factor on the endpoint with which the authenticator is used.
-->

Authentication意図は，いくつかの方法で立証してもよい(MAY)．Subjectの介入(例えばOTPデバイスから得たAuthenticator出力をClaimantが入力すること)を必要とするAuthenticationプロセスは意図を立証している．各AuthenticationやReauthentication操作に対して(例えばボタン押下や再挿入のような)ユーザアクションを必要とする暗号デバイスもまた意図を立証している．
<!--
Authentication intent MAY be established in a number of ways. Authentication processes that require the subject's intervention (e.g., a claimant entering an authenticator output from an OTP device) establish intent. Cryptographic devices that require user action (e.g., pushing a button or reinsertion) for each authentication or reauthentication operation are also establish intent.
-->

バイオメトリクスのプレゼンテーションは，計測手段に応じてAuthentication意図を立証したりしなかったりする．指紋のプレゼンテーションは通常は意図を立証するが，一方カメラを用いたClaimantの顔の観測は，一般的にはそうならない．行動バイオメトリクスは，Claimant側で特定のアクションを常に要求されるわけではないので，同様にAuthentication意図を立証する可能性は低い．
<!--
Depending on the modality, presentation of a biometric may or may not establish authentication intent. Presentation of a fingerprint would normally establish intent, while observation of the claimant's face using a camera normally would not by itself. Behavioral biometrics similarly are less likely to establish authentication intent because they do not always require a specific action on the claimant's part.
-->

#### <a name="restricted"></a> 5.2.10 制限された(RESTRICTED) Authenticator
<!--
#### <a name="restricted"></a> 5.2.10 Restricted Authenticators
-->

脅威の進化につれて，Authenticatorが攻撃に対抗する能力は一般的には減少する．一方で，いくつかのAuthenticatorの性能は改善するかもしれない &mdash; 例えば，根拠となる標準が改定されることで特定の攻撃に対抗する能力が増加する．
<!--
As threats evolve, authenticators' capability to resist attacks typically degrades. Conversely, some authenticators' performance may improve &mdash; for example, when changes to their underlying standards increases their ability to resist particular attacks.
-->

Authenticatorの性能におけるこれらの変更を考慮するために，NISTは追加の制限を，Authenticatorタイプや特定のクラスまたはAuthenticatorタイプのインスタンスに対して設けた．
<!--
To account for these changes in authenticator performance, NIST places additional restrictions on authenticator types or specific classes or instantiations of an authenticator type.
-->

制限された(RESTRICTED) Authenticatorを利用するには，実装した組織が，制限された(RESTRICTED) Authenticatorに関連するリスクを評価，理解，許容し，時間の経過とともにリスクが増加しうるということを認識する必要がある．組織の責任は，彼らのシステムおよび関連データにおけるリスクを許容できるレベルを決定し，過度なリスクを緩和する方法を定義することである．何れかの当事者に対するリスクが許容できないと組織が判断した時点で，Authenticatorは利用されないものとする(SHALL NOT)．
<!--
The use of a RESTRICTED authenticator requires that the implementing organization assess, understand, and accept the risks associated with that RESTRICTED authenticator and acknowledge that risk will likely increase over time. It is the responsibility of the organization to determine the level of acceptable risk for their system(s) and associated data and to define any methods for mitigating excessive risks. If at any time the organization determines that the risk to any party is unacceptable, then that authenticator SHALL NOT be used.
-->

更に，Authenticationエラーのリスクは一般的には，実装した組織，Authentication結果に依存する組織，Subscriberを含む複数の当事者が負うものである．組織が制限された(RESTRICTED) Authenticatorを採用すると，Subscriberがそのリスクを十分に理解していない，またリスクを統制する能力が制限されている可能性があり，Subscriberは追加のリスクにさらされることになる．その為，CSPは次のことを実施することとする(SHALL)．
<!--
Further, the risk of an authentication error is typically borne by multiple parties, including the implementing organization, organizations that rely on the authentication decision, and the subscriber. Because the subscriber may be exposed to additional risk when an organization accepts a RESTRICTED authenticator and that the subscriber may have a limited understanding of and ability to control that risk, the CSP SHALL:
-->

1. Subscriberに対して少なくとも1つの制限されていない代替Authenticatorを提示し，要求されるAALでAuthenticateできるようにする．

2. Subscriberが理解しやすいように，制限されているAuthenticatorのセキュリティリスクと，制限されていない代替Authenticatorが利用可能であることを通知する．

3. リスクアセスメントにおけるSubscriberに対する追加のリスクに対処する．

4. 将来的にある地点で制限された(RESTRICTED) Authenticatorが許容可能でなくなる可能性を踏まえて移行プランを立て，[digital identity acceptance statement](sp800-63-3.html#daps)の内容ににこの移行プランを含めておく．

<!--
1. Offer subscribers at least one alternate authenticator that is not RESTRICTED and can be used to authenticate at the required AAL.

2. Provide meaningful notice to subscribers regarding the security risks of the RESTRICTED authenticator and availability of alternative(s) that are not RESTRICTED.

3. Address any additional risk to subscribers in its risk assessment.

4. Develop a migration plan for the possibility that the RESTRICTED authenticator is no longer acceptable at some point in the future and include this migration plan in its [digital identity acceptance statement](sp800-63-3.html#daps).
-->
