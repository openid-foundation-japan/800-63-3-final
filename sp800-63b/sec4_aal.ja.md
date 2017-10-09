<a name="sec4"></a>

## <a name="AAL_SEC4"></a>4 Authenticator Assurance Levels

_本セクションは標準及び参考情報の題材両方を含む._
<!--
_This section contains both normative and informative material._
-->

指定されたAALの要件を満たすために，Claimantは少なくとも自身がSubscriberとして認識される強度のレベルでAuthenticateされるものとする(SHALL)．Authenticationプロセスの結果は識別子であり，SubscriberがRPに対してAuthenticateするたびに使われるものとする(SHALL)．それは仮名でもよい(MAY)，Subscriberの識別子は異なる目的で再利用すべきではない(SHOULD NOT)が，CSPによって過去に登録済みのSubjectが再登録される場合には再利用すべきである(SHOULD)．Subscriberをを一意なSubjectであると識別する他の属性もまた提供されてもよい(MAY)．

<!--
To satisfy the requirements of a given AAL, a claimant SHALL be authenticated with at least a given level of strength to be recognized as a subscriber. The result of an authentication process is an identifier that SHALL be used each time that subscriber authenticates to that RP. The identifier MAY be pseudonymous. Subscriber identifiers SHOULD NOT be reused for a different subject but SHOULD be reused when a previously-enrolled subject is re-enrolled by the CSP. Other attributes that identify the subscriber as a unique subject MAY also be provided.
-->

各AALにおけるAuthenticator及びVerifierに対する標準要件の詳細についてはセクション5に示されている．
<!--
Detailed normative requirements for authenticators and verifiers at each AAL are provided in Section 5.
-->

最も適切なAALの選択方法の詳細については [SP 800-63](sp800-63-3.html) セクション6.2参照．
<!--
See [SP 800-63](sp800-63-3.html) Section 6.2 for details on how to choose the most appropriate AAL.
-->

FIPS 140 要件は，[FIPS 140-2](#FIPS140-2)またはより新しい版によって充足される．
<!--
FIPS 140 requirements are satisfied by [FIPS 140-2](#FIPS140-2) or newer revisions.
-->

IAL1では，属性はDigital Identityサービスによって収集され，利用可能となる．任意のPIIまたは他の個人情報は - self-assertedまたは確認されたもののどちらでも - 多要素Authenticationを必要とする．従って，連邦政府機関はself-assertedであるPIIや他の個人情報がオンラインで利用可能である場合，最低でもAAL2を選択するものとする(SHALL)．
<!--
At IAL1, it is possible that attributes are collected and made available by the digital identity service. Any PII or other personal information — whether self-asserted or validated — requires multi-factor authentication. Therefore, agencies SHALL select a minimum of AAL2 when self-asserted PII or other personal information is made available online.
-->

### 4.1 Authenticator Assurance Level 1

*本セクションは標準である．*
<!--
*This section is normative.*
-->


AAL 1はSubscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという，ある程度の保証を提供する．AAL 1では幅広く利用可能なAuthentication技術を利用した，単一要素または多要素のAuthenticationを必要とする．Authenticationが成功するには，そのClaimantが，セキュアなAuthenticationプロトコルを介して，自身がそのAuthenticatorを所有・制御していることを証明する必要がある．
<!--
AAL1 provides some assurance that the claimant controls an authenticator bound to the subscriber's account. AAL1 requires either single-factor or multi-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove possession and control of the authenticator through a secure authentication protocol.
-->

#### 4.1.1 許可されているAuthenticatorタイプ
<!--
#### 4.1.1 Permitted Authenticator Types
-->

AAL1のAuthenticationでは，[Section 5](#sec5) で定義されている次のAuthenticatorタイプの何れかを利用するものとする(SHALL):
<!--
AAL1 authentication SHALL occur by the use of any of the following authenticator types, which are defined in [Section 5](#sec5):
-->

* 記憶シークレット ([Section 5.1.1](#memsecret))
* ルックアップシークレット ([Section 5.1.2](#lookupsecrets))
* アウトオブバンドデバイス  ([Section 5.1.3](#out-of-band))
* 単一要素ワンタイムパスワード (OTP) デバイス ([Section 5.1.4](#singlefactorOTP))
* 多要素 OTP デバイス ([Section 5.1.5](#multifactorOTP))
* 単一要素暗号ソフトウェア ([Section 5.1.6](#sfcs))
* 単一要素暗号デバイス ([Section 5.1.7](#sfcd))
* 多要素暗号ソフトウェア ([Section 5.1.8](#mfcs))
* 多要素暗号デバイス ([Section 5.1.9](#mfcd))

<!--
* Memorized Secret ([Section 5.1.1](#memsecret))
* Look-Up Secret ([Section 5.1.2](#lookupsecrets))
* Out-of-Band Devices ([Section 5.1.3](#out-of-band))
* Single-Factor One-Time Password (OTP) Device ([Section 5.1.4](#singlefactorOTP))
* Multi-Factor OTP Device ([Section 5.1.5](#multifactorOTP))
* Single-Factor Cryptographic Software ([Section 5.1.6](#sfcs))
* Single-Factor Cryptographic Device ([Section 5.1.7](#sfcd))
* Multi-Factor Cryptographic Software ([Section 5.1.8](#mfcs))
* Multi-Factor Cryptographic Device ([Section 5.1.9](#mfcd))
-->

#### <a name="aal1req"></a>4.1.2 Authenticator及びVerifierの要件
<!--
#### <a name="aal1req"></a>4.1.2 Authenticator and Verifier Requirements
-->

AAL 1で用いられる暗号Authenticatorは，Approved Cryptographyを利用するものとする(SHALL)．オペレーティング・システム環境で動作するソフトウェアベースのAuthenticatorは，該当する場合(例，マルウェアによって)それ自身が動作している利用者のエンドポイントの改竄検出を試みてもよく(MAY)，そのような改竄が検出された場合には操作を完了すべきでではない(SHOULD NOT)．

<!--
Cryptographic authenticators used at AAL1 SHALL use approved cryptography. Software-based authenticators that operate within the context of an operating system MAY, where applicable, attempt to detect compromise (e.g., by malware) of the user endpoint in which they are running and SHOULD NOT complete the operation when such a compromise is detected.
-->

ClaimantとVerifierとの間の通信(アウトオブバンドAuthenticatorの場合はプライマリチャネル)は，Authenticator出力の秘匿性と中間者攻撃に対する耐性を提供する保護されたAuthenticatedチャネルを介して行われるものとする(SHALL)．

<!--
Communication between the claimant and verifier (using the primary channel in the case of an out-of-band authenticator) SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to man-in-the-middle (MitM) attacks.
-->

政府機関が運用するVerifierは，AAL 1において，[FIPS 140](#FIPS140-2) Level 1 の要件に適合していることが確認されるものとする(SHALL)．

<!--
Verifiers operated by government agencies at AAL1 SHALL be validated to meet the requirements of [FIPS 140](#FIPS140-2) Level 1.
-->

#### <a name="aal1reauth"></a>4.1.3 Reauthentication

[Section 7.2](#sessionreauthn)に記載があるように，Subscriberのセッションの定期的なReauthenticationが行われるものとする(SHALL)．AAL 1では，ユーザの活動に関わらず，SubscriberのReauthenticationは少なくとも30日に1回は繰り返し実施すべきである(SHOULD)．セッションはこの時間制限に到達したら終了される(すなわちログアウトされる)べき(SHOULD)である

<!--
Periodic reauthentication of subscriber sessions SHALL be performed as described in [Section 7.2](#sessionreauthn). At AAL1, reauthentication of the subscriber SHOULD be repeated at least once per 30 days during an extended usage session, regardless of user activity. The session SHOULD be terminated (i.e., logged out) when this time limit is reached.
-->

#### 4.1.4 セキュリティ統制

<!--
#### 4.1.4 Security Controls
-->

CSPは，[SP 800-53](#SP800-53) または等価な連邦政府機関(例えば [FEDRAMP](#FEDRAMP)) あるいは業界標準で定義されているセキュリティ統制の*低度な*基準から適切に調整されているセキュリティ統制を採用することとする(SHALL)．CSPは*影響が低度な*システム，またはそれに相当するものに対する最低限の保証関連の統制を果たしていることを保証することとする(SHALL)．

<!--
The CSP SHALL employ appropriately-tailored security controls from the *low* baseline of security controls defined in [SP 800-53](#SP800-53) or equivalent federal (e.g. [FEDRAMP](#FEDRAMP)) or industry standard. The CSP SHALL ensure that the minimum assurance-related controls for *low-impact* systems, or equivalent, are satisfied.
-->

#### <a name="aal1records"></a> 4.1.5 レコード保持ポリシ

<!--
#### <a name="aal1records"></a> 4.1.5 Records Retention Policy
-->

CSPは，準拠法，規則，及び任意のNational Archives and Records Administration (NARA)のレコード保持スケジュールを含むポリシに合致するそれぞれのレコード保持ポリシに従う．もしCSPがいずれの必須要件なくレコードを保持することを選択する場合，CSPはレコードの保持期間を決定するためのプライバシ及びセキュリティリスクのアセスメントを含むリスク管理プロセスを実施するものとし(SHALL)，Subscriberに対して当該保持ポリシについて通知するものとする(SHALL)．

<!--
The CSP shall comply with its respective records retention policies in accordance with applicable laws, regulations, and policies, including any National Archives and Records Administration (NARA) records retention schedules that may apply. If the CSP opts to retain records in the absence of any mandatory requirements, the CSP SHALL conduct a risk management process, including assessments of privacy and security risks, to determine how long records should be retained and SHALL inform the subscriber of that retention policy.
-->

### 4.2 Authenticator Assurance Level 2

*本セクションは標準である．*
<!--
*This section is normative.*
-->

AAL 2は，Subscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという，高い確実性を提供する．セキュアなAuthenticationプロトコルを介して，2つの異なるAuthentication要素の所有と制御の証明を必要とする．Approved Cryptographic技術がAAL2及びそれ以上では必要である．

<!--
AAL2 provides high confidence that the claimant controls authenticator(s) bound to the subscriber's account. Proof of possession and control of two distinct authentication factors is required through secure authentication protocol(s). Approved cryptographic techniques are required at AAL2 and above.
-->

#### <a name="aal2types"></a>4.2.1 許可されているAuthenticatorタイプ
<!--
#### <a name="aal2types"></a>4.2.1 Permitted Authenticator Types
-->

AAL2のAuthenticationでは， 一つの多要素Authenticatorまたは2つの単一要素Authenticatorの組み合わせのどちらかを利用するものとする(SHALL)．一つの多要素Authenticatorは，デバイスをアクティベートするために統合されたバイオメトリックセンサを備え，暗号的にセキュアであるようなデバイスのように，1回のAuthenticationイベントで二つの要素を必要とする．Authenticatorの要件は[Section 5](#sec5)で指定されている．

<!--
At AAL2, authentication SHALL occur by the use of either a multi-factor authenticator or a combination of two single-factor authenticators. A multi-factor authenticator requires two factors to execute a single authentication event, such as a cryptographically-secure device with an integrated biometric sensor that is required to activate the device. Authenticator requirements are specified in [Section 5](#sec5).
-->

多要素Authenticatorを利用する際，以下の任意のものを利用してよい(MAY): 
<!--
When a multi-factor authenticator is used, any of the following MAY be used:
-->

* 多要素 OTP デバイス ([Section 5.1.5](#multifactorOTP))
* 多要素暗号ソフトウェア ([Section 5.1.8](#mfcs))
* 多要素暗号デバイス ([Section 5.1.9](#mfcd))
<!--
* Multi-Factor OTP Device ([Section 5.1.5](#multifactorOTP))
* Multi-Factor Cryptographic Software ([Section 5.1.8](#mfcs))
* Multi-Factor Cryptographic Device ([Section 5.1.9](#mfcd))
-->

2つの単一要素Authenticatorを組み合わせる際には，記憶シークレットAuthentiactor ([Section 5.1.1](#memsecret)) と以下のリストから1つの所有ベース("something you have")のAuthenticatorを含むこととする(SHALL):
<!--
When a combination of two single-factor authenticators is used, it SHALL include a Memorized Secret authenticator ([Section 5.1.1](#memsecret)) and one possession-based (i.e., "something you have") authenticator from the following list:
-->

* ルックアップシークレット ([Section 5.1.2](#lookupsecrets))
* アウトオブバンドデバイス  ([Section 5.1.3](#out-of-band))
* 単一要素 OTP デバイス ([Section 5.1.4](#singlefactorOTP))
* 単一要素暗号ソフトウェア ([Section 5.1.6](#sfcs))
* 単一要素暗号デバイス ([Section 5.1.7](#sfcd))

<!--
* Look-Up Secret ([Section 5.1.2](#lookupsecrets))
* Out-of-Band Device ([Section 5.1.3](#out-of-band))
* Single-Factor OTP Device ([Section 5.1.4](#singlefactorOTP))
* Single-Factor Cryptographic Software ([Section 5.1.6](#sfcs))
* Single-Factor Cryptographic Device ([Section 5.1.7](#sfcd))
-->

> 注記: [Section 5.2.3](#biometric_use)でのバイオメトリックAuthenticationの要件を満たすために，デバイスはバイオメトリックに加えて，デバイスをAuthenticateされる必要がある &mdash バイオメトリックは1つの要素としてみなせるが，それ自体をAuthenticatorとしてみなしてはいない．従って，バイオメトリックを用いたAuthenticationを実施する時，2つのAuthenticatorを使う必要はない．なぜならば，関連付けられたデバイスは"something you have"として機能し，バイオメトリックは"something you are"として機能するからである．

<!--
> Note: When biometric authentication meets the requirements in [Section 5.2.3](#biometric_use), the device has to be authenticated in addition to the biometric &mdash; a biometric is recognized as a factor, but not recognized as an authenticator by itself. Therefore, when conducting authentication with a biometric, it is unnecessary to use two authenticators because the associated device serves as "something you have," while the biometric serves as "something you are."
-->

#### <a name="aal2req"></a>4.2.2 Authenticator及びVerifierの要件

<!--
#### <a name="aal2req"></a>4.2.2 Authenticator and Verifier Requirements
-->

AAL 2で用いられる暗号Authenticatorは，Approved Cryptographyを使うものとする(SHALL)．政府機関によって調達されたAuthenticatorは，[FIPS 140](#FIPS140-2) Level 1の要件に適合していることを確認されるものとする(SHALL)．オペレーティング・システム環境で動作するソフトウェアベースのAuthenticatorは，該当する場合(例，マルウェアによって)それ自身が動作しているプラットフォームの改竄検知を試みてもよく(MAY)，そのような改竄が検出されると操作を拒否すべき(SHOULD)である．AAL2では少なくとも1つのAuthenticatorは[Section 5.2.8](#replay)に記載されているように，リプレイ耐性があるものとする(SHALL)．AAL2のAuthenticatorは[Section 5.2.9](#intent)に記載されているように，少なくとも1つのAuthenticatorからAuthenticationの意図を明示するべきである(SHOULD)．

<!--
Cryptographic authenticators used at AAL2 SHALL use approved cryptography. Authenticators procured by government agencies SHALL be validated to meet the requirements of [FIPS 140](#FIPS140-2) Level 1. Software-based authenticators that operate within the context of an operating system MAY, where applicable, attempt to detect compromise of the platform in which they are running (e.g., by malware) and SHOULD NOT complete the operation when such a compromise is detected. At least one authenticator used at AAL2 SHALL be replay resistant as described in [Section 5.2.8](#replay). Authentication at AAL2 SHOULD demonstrate authentication intent from at least one authenticator as discussed in [Section 5.2.9](#intent).
-->

ClaimantとVerifierとの間の通信(アウトオブバンドAuthenticatorの場合はプライマリチャネル)は，Authenticator出力の秘匿性と中間者攻撃に対する耐性を提供する保護されたAuthenticatedチャネルを介して行われるものとする(SHALL)．

<!--
Communication between the claimant and verifier (the primary channel in the case of an out-of-band authenticator) SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to MitM attacks.
-->

政府機関が運用するVerifierは，AAL 2において，[FIPS 140](#FIPS140-2) Level 1 の要件に適合していることが確認されるものとする(SHALL)．

<!--
Verifiers operated by government agencies at AAL2 SHALL be validated to meet the requirements of [FIPS 140](#FIPS140-2) Level 1.
-->

Authenticationプロセスでスマートフォンなどのデバイスが利用される際に，（典型的にはPINやバイオメトリックを利用して）デバイスをアンロックする行為はAuthentication要素の一つとしてみなされないものとする(SHALL NOT)．一般的には，Verifierがそのデバイスがロックされていたのか，あるいはアンロックプロセスが関連するAuthenticatorタイプの要件に合致していたのかを把握することができない．

<!--
When a device such a smartphone is used in the authentication process, the unlocking of that device (typically done using a PIN or biometric) SHALL NOT be considered one of the authentication factors. Generally, it is not possible for a verifier to know that the device had been locked or if the unlock process met the requirements for the relevant authenticator type.
-->

バイオメトリック要素がAAL 2で利用される場合，[Section 5.2.3](#biometric_use)に規定されたパフォーマンス要件を満たすものとし(SHALL)，Verifierはバイオメトリックセンサー及び後続処理がこれらの要件に合致していることを明確にしなければならない(SHOULD)．
<!--
When a biometric factor is used in authentication at AAL2, the performance requirements stated in [Section 5.2.3](#biometric_use) SHALL be met, and the verifier SHOULD make a determination that the biometric sensor and subsequent processing meet these requirements.
-->

#### <a name="aal2reauth"></a>4.2.3 Reauthentication

[Section 7.2](#sessionreauthn)に記載があるように，Subscriberのセッションの定期的なReauthenticationが行われるものとする(SHALL)．AAL 2では，ユーザの活動に関わらず，SubscriberのReauthenticationはセッションの利用が延長されている間は少なくとも12時間に1回は繰り返されるものとする(SHALL)．
30分以上継続している非活動期間の後は，SubscriberのReauthenticationは繰り返されるものとする(SHALL)．
セッションはこの時間制限に到達したら終了される(すなわちログアウトされる)ものとする(SHALL)．

<!--
Periodic reauthentication of subscriber sessions SHALL be performed as described in [Section 7.2](#sessionreauthn). At AAL2, authentication of the subscriber SHALL be repeated at least once per 12 hours during an extended usage session, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following any period of inactivity lasting 30 minutes or longer. The session SHALL be terminated (i.e., logged out) when either of these time limits is reached.
-->

まだ時間制限に到達していないセッションのReauthenticationは，記憶シークレットだけ，あるいはまだ有効なセッションシークレットと連動しているバイオメトリックを要求してもよい(MAY)．Verifierは非活動によるタイムアウトの直前に，ユーザに対して活動を促してもよい(MAY)．
<!--
Reauthentication of a session that has not yet reached its time limit MAY require only a memorized secret or a biometric in conjunction with the still-valid session secret. The verifier MAY prompt the user to cause activity just before the inactivity timeout.
-->

#### 4.2.4 セキュリティ統制
<!--
#### 4.2.4 Security Controls
-->

CSPは，[SP 800-53](#SP800-53) または等価な連邦政府機関(例えば [FEDRAMP](#FEDRAMP)) あるいは業界標準で定義されているセキュリティ統制の*中度な*基準から適切に調整されているセキュリティ統制を採用することとする(SHALL)．CSPは*影響が中度な*システム，またはそれに相当するものに対する最低限の保証関連の統制を果たしていることを保証することとする(SHALL)．

<!--
The CSP SHALL employ appropriately-tailored security controls from the *moderate* baseline of security controls defined in [SP 800-53](#SP800-53) or equivalent federal (e.g., [FEDRAMP](#FEDRAMP)) or industry standard. The CSP SHALL ensure that the minimum assurance-related controls for *moderate-impact* systems or equivalent are satisfied.
-->

#### <a name="aal2records"></a> 4.2.5 レコード保持ポリシ

<!--
#### <a name="aal2records"></a> 4.2.5 Records Retention Policy
-->

CSPは，準拠法，規則，及び任意のNational Archives and Records Administration (NARA)のレコード保持スケジュールを含むポリシに合致するそれぞれのレコード保持ポリシに従う．もしCSPがいずれの必須要件なくレコードを保持することを選択する場合，CSPはレコードの保持期間を決定するためのプライバシ及びセキュリティリスクのアセスメントを含むリスク管理プロセスを実施するものとし(SHALL)，Subscriberに対して当該保持ポリシについて通知するものとする(SHALL)．

<!--
The CSP shall comply with its respective records retention policies in accordance with applicable laws, regulations, and policies, including any NARA records retention schedules that may apply. If the CSP opts to retain records in the absence of any mandatory requirements, the CSP SHALL conduct a risk management process, including assessments of privacy and security risks to determine how long records should be retained and SHALL inform the subscriber of that retention policy.
-->

### 4.3 Authenticator Assurance Level 3

*本セクションは標準である．*
<!--
*This section is normative.*
-->

AAL 3は，Subscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという，極めて高い確実性を提供する．AAL3におけるAuthenticationは，暗号プロトコルを介した，鍵の所有の証明に基づいている．．AAL3 Authenticationは，1つのハードウェアベースのAuthenticatorと，1つのVerifierなりすまし耐性を備えるAuthenticatorを利用するものとする(SHALL)．同じデバイスが両方の要件を満たしても良い(MAY)．AAL3でAuthenticateするために，claimantはセキュアなAuthenticationプロトコルを介して，2つの異なるAuthentication要素の所有と制御を証明するものとする(SHALL)．Approved Cryptographic技術が必要である．

<!--
AAL3 provides very high confidence that the claimant controls authenticator(s) bound to the subscriber's account. Authentication at AAL3 is based on proof of possession of a key through a cryptographic protocol. AAL3 authentication SHALL use a hardware-based authenticator and an authenticator that provides verifier impersonation resistance — the same device MAY fulfill both these requirements. In order to authenticate at AAL3, claimants SHALL prove possession and control of two distinct authentication factors through secure authentication protocol(s). Approved cryptographic techniques are required.
-->

#### <a name="aal3types"></a>4.3.1 許可されているAuthenticatorタイプ
<!--
#### <a name="aal3types"></a>4.3.1 Permitted Authenticator Types
-->

AAL3のAuthenticationでは， セクション4.3の要件を満たすAuthenticatorの組み合わせの1つを利用するものとする(SHALL)．有効な組み合わせは次の通り:．

<!--
AAL3 authentication SHALL occur by the use of one of a combination of authenticators satisfying the requirements in Section 4.3. Possible combinations are:
-->

* 多要素暗号デバイス ([Section 5.1.9](#mfcd))
* 単一要素暗号デバイス ([Section 5.1.7](#sfcd))を記憶シークレット ([Section 5.1.1](#memsecret))と併用
* 多要素 OTP デバイス(ソフトウェアまたはハードウェア) ([Section 5.1.5](#multifactorOTP))を単一要素暗号デバイス ([Section 5.1.7](#sfcd))と併用
* 多要素 OTP デバイス(ハードウェアのみ) ([Section 5.1.5](#multifactorOTP))を単一要素暗号ソフトウェア ([Section 5.1.6](#sfcs))と併用
* 単一要素 OTP デバイス(ハードウェアのみ) ([Section 5.1.4](#singlefactorOTP)) を多要素暗号ソフトウェア ([Section 5.1.8](#mfcs))と併用
* 単一要素 OTP デバイス(ハードウェアのみ) ([Section 5.1.4](#singlefactorOTP)) を単一要素暗号ソフトウェア ([Section 5.1.6](#sfcs))及び記憶シークレット([Section 5.1.1](#memsecret))と併用

<!--
* Multi-Factor Cryptographic Device ([Section 5.1.9](#mfcd))
* Single-Factor Cryptographic Device ([Section 5.1.7](#sfcd)) used in conjunction with Memorized Secret ([Section 5.1.1](#memsecret))
* Multi-Factor OTP device (software or hardware) ([Section 5.1.5](#multifactorOTP)) used in conjunction with a Single-Factor Cryptographic Device ([Section 5.1.7](#sfcd))
* Multi-Factor OTP device (hardware only) ([Section 5.1.5](#multifactorOTP)) used in conjunction with a Single-Factor Cryptographic Software ([Section 5.1.6](#sfcs))
* Single-Factor OTP device (hardware only) ([Section 5.1.4](#singlefactorOTP)) used in conjunction with a Multi-Factor Cryptographic Software Authenticator ([Section 5.1.8](#mfcs))
* Single-Factor OTP device (hardware only) ([Section 5.1.4](#singlefactorOTP)) used in conjunction with a Single-Factor Cryptographic Software Authenticator ([Section 5.1.6](#sfcs)) and a Memorized Secret ([Section 5.1.1](#memsecret))
-->

#### <a name="aal3req"></a>4.3.2 Authenticator及びVerifierの要件
<!--
#### <a name="aal3req"></a>4.3.2 Authenticator and Verifier Requirements
-->

ClaimantとVerifierとの間の通信は，Authenticator出力の秘匿性と中間者攻撃に対する耐性を提供する保護されたAuthenticatedチャネルを介して行われるものとする(SHALL)．AAL3 Authenticationで利用される全ての暗号デバイスAuthenticatorは，[Section 5.2.5](#verifimpers)に記載されているVerifierなりすまし耐性を備えているものとし(SHALL)，[Section 5.2.8](#replay)に記載されているように，リプレイ耐性があるものとする(SHALL)．AAL3のAuthenticatorは[Section 5.2.9](#intent)に記載されているように，少なくとも1つのAuthenticatorからAuthentication及びReauthenticationの意図を明示するべきである(SHOULD)．

<!--
Communication between the claimant and verifier SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to MitM attacks. All cryptographic device authenticators used at AAL3 SHALL be verifier impersonation resistant as described in Section [5.2.5](#verifimpers) and SHALL be replay resistant as described in Section [5.2.8](#replay). All authentication and reauthentication processes at AAL3 SHALL demonstrate authentication intent from at least one authenticator as described in [Section 5.2.9](#intent).
-->

AAL 3で利用される多要素Authenticatorは，少なくとも[FIPS 140](#FIPS140-2) Level 3物理セキュリティを伴っており，総合的に[FIPS 140](#FIPS140-2) Level 2またはそれ以上で確認されたハードウェア暗号モジュールであるものとする(SHALL)．AAL3で利用される単一要素暗号デバイスは，少なくとも[FIPS 140](#FIPS140-2) Level 3物理セキュリティを伴っており，総合的に[FIPS 140](#FIPS140-2) Level 1またはそれ以上で確認されたハードウェア暗号モジュールであるものとする(SHALL)．

<!--
Multi-factor authenticators used at AAL3 SHALL be hardware cryptographic modules validated at [FIPS 140](#FIPS140-2) Level 2 or higher overall with at least [FIPS 140](#FIPS140-2) Level 3 physical security. Single-factor cryptographic devices used at AAL3 SHALL be validated at [FIPS 140](#FIPS140-2) Level 1 or higher overall with at least [FIPS 140](#FIPS140-2) Level 3 physical security.
-->

AAL3におけるVerifierは，[FIPS 140](#FIPS140-2) Level 1またはそれ以上の基準で確認されるものとする(SHALL)．
<!--
Verifiers at AAL3 SHALL be validated at [FIPS 140](#FIPS140-2) Level 1 or higher.
-->

AAL3におけるVerifierは，[Section 5.2.7](#verifier-secrets)に記載のあるように，少なくとも１つのAuthenticator要素においてVerifier改竄耐性があるものとする(SHALL)．

<!--
Verifiers at AAL3 SHALL be verifier compromise resistant as described in [Section 5.2.7](#verifier-secrets) with respect to at least one authentication factor.
-->

AAL3におけるハードウェアベースのAuthenticatorとVerifierは，関連するサイドチャネル(例，タイミング及び消費電力分析)攻撃への耐性があるべきである(SHOULD)．関連するサイドチャネル攻撃は，CSPによって実施されるリスクアセスメントにより，明確にされるものとする(SHALL)．
<!--
Hardware-based authenticators and verifiers at AAL3 SHOULD resist relevant side-channel (e.g., timing and power-consumption analysis) attacks. Relevant side-channel attacks SHALL be determined by a risk assessment performed by the CSP.
-->

Authenticationプロセスでスマートフォンなどのデバイスが利用される際に，デバイスが上記の要件に合致している可能性が推測される場合でも，デバイスをアンロックする行為はAuthentication要素の一つとしてみなされないものとする(SHALL NOT)．これは，一般的には，Verifierがそのデバイスがロックされていたのか，あるいはアンロックプロセスが関連するAuthenticatorタイプの要件に合致していたのかを把握することができないからである．

<!--
When a device such a smartphone is used in the authentication process — presuming that the device is able to meet the requirements above — the unlocking of that device SHALL NOT be considered to satisfy one of the authentication factors. This is because it is generally not possible for verifier to know that the device had been locked nor whether the unlock process met the requirements for the relevant authenticator type.
-->

バイオメトリック要素がAAL3で利用される場合，Verifierはバイオメトリックセンサー及び後続処理が，[Section 5.2.3](#biometric_use)に規定されたパフォーマンス要件に合致していることを明確にしなければならない(SHALL)．

<!--
When a biometric factor is used in authentication at AAL3, the verifier SHALL make a determination that the biometric sensor and subsequent processing meet the performance requirements stated in [Section 5.2.3](#biometric_use).
-->

#### <a name="aal3reauth"></a>4.3.3 Reauthentication

[Section 7.2](#sessionreauthn)に記載があるように，Subscriberのセッションの定期的なReauthenticationが行われるものとする(SHALL)．AAL3では，[Section 7.2](#sessionreauthn)に記載があるように，ユーザの活動に関わらず，SubscriberのReauthenticationはセッションの利用が延長されている間は少なくとも12時間に1回は繰り返されるものとする(SHALL)．15分以上継続している非活動期間の後は，SubscriberのReauthenticationは繰り返されるものとする(SHALL)．Reauthenticationには両方のAuthenticator要素を用いるものとする(SHALL)．セッションはこれらの時間制限に到達したら終了される(すなわちログアウトされる)ものとする(SHALL)．Verifierは非活動によるタイムアウトの直前に，ユーザに対して活動を促してもよい(MAY)．

<!--
Periodic reauthentication of subscriber sessions SHALL be performed as described in [Section 7.2](#sessionreauthn). At AAL3, authentication of the subscriber SHALL be repeated at least once per 12 hours during an extended usage session, regardless of user activity, as described in [Section 7.2](#sessionreauthn). Reauthentication of the subscriber SHALL be repeated following any period of inactivity lasting 15 minutes or longer. Reauthentication SHALL use both authentication factors. The session SHALL be terminated (i.e., logged out) when either of these time limits is reached. The verifier MAY prompt the user to cause activity just before the inactivity timeout.
-->

#### 4.3.4 セキュリティ統制
<!--
#### 4.3.4 Security Controls
-->

CSPは，[SP 800-53](#SP800-53) または等価な連邦政府機関(例えば [FEDRAMP](#FEDRAMP)) あるいは業界標準で定義されているセキュリティ統制の*高度な*基準から適切に調整されているセキュリティ統制を採用することとする(SHALL)．CSPは*影響が高度な*システム，またはそれに相当するものに対する最低限の保証関連の統制を果たしていることを保証することとする(SHALL)．
<!--
e CSP SHALL employ appropriately-tailored security controls from the *high* baseline of security controls defined in [SP 800-53](#SP800-53) or an equivalent federal (e.g., [FEDRAMP](#FEDRAMP)) or industry standard. The CSP SHALL ensure that the minimum assurance-related controls for *high-impact* systems or equivalent are satisfied.
-->

#### <a name="aal3records"></a> 4.3.5 レコード保持ポリシ
<!--
#### <a name="aal3records"></a> 4.3.5 Records Retention Policy
-->

CSPは，準拠法，規則，及び任意のNational Archives and Records Administration (NARA)のレコード保持スケジュールを含むポリシに合致するそれぞれのレコード保持ポリシに従う．もしCSPがいずれの必須要件なくレコードを保持することを選択する場合，CSPはレコードの保持期間を決定するためのプライバシ及びセキュリティリスクのアセスメントを含むリスク管理プロセスを実施するものとし(SHALL)，Subscriberに対して当該保持ポリシについて通知するものとする(SHALL)．
<!--
The CSP shall comply with its respective records retention policies in accordance with applicable laws, regulations, and policies, including any NARA records retention schedules that may apply. If the CSP opts to retain records in the absence of any mandatory requirements, the CSP SHALL conduct a risk management process, including assessments of privacy and security risks, to determine how long records should be retained and SHALL inform the subscriber of that retention policy.
-->

### <a name="aal_privacy"></a>4.4 プライバシ要件
<!--
### <a name="aal_privacy"></a>4.4 Privacy Requirements
-->

CSPは[SP 800-53](#SP800-53)で定義された適切に調整されたプライバシコントロール、または他の等価な業界標準を採用するものとする(SHALL)。
<!--
The CSP SHALL employ appropriately-tailored privacy controls defined in [SP 800-53](#SP800-53) or equivalent industry standard.
-->

CSPは、追加の用途のために明確な通知を行い加入者から承諾を得なければ、Authentication実施、詐欺緩和、または法令遵守や法的手続き以外のいかなる目的でもSubscriberの情報を利用・開示しないものとする(SHALL NOT)。CSPは、同意をサービスの条件としてはならない(SHALL NOT)。情報を収集した際の元々の目的に利用が限定されていることを保証するための対策が講じられるものとする(SHALL)。このような情報の利用が、Authenticationや法令遵守、法的手続きに関連する用途に該当しないのであれば、CSPは通知を行い、Subscriberから同意を得るものとする(SHALL)。この通知は、[SP 800-63A](sp800-63a.html) Section 8.2の*Notice and Consent*に記載されているのと同じ原則に従うべき(SHOULD)であり、法律に固執し過ぎたプライバシポリシや一般的な利用規約に丸め込むべきではない(SHOULD NOT)。明示的な目的外の用途がある場合は、むしろSubscriberが追加の利用目的を理解するための意味のある方法、及び承諾または辞退する機会が提供されるべきである(SHOULD)。

<!--
CSPs SHALL NOT use or disclose information about subscribers for any purpose other than conducting authentication, related fraud mitigation, or to comply with law or legal process, unless the CSP provides clear notice and obtains consent from the subscriber for additional uses. CSPs SHALL NOT make consent a condition of the service. Care SHALL be taken to ensure that use of such information is limited to its original purpose for collection. If the use of such information does not fall within uses related to authentication or to comply with law or legal process, the CSP SHALL provide notice and obtain consent from the subscriber. This notice SHOULD follow the same principles as described in *Notice and Consent* in [SP 800-63A](sp800-63a.html) Section 8.2 and SHOULD NOT be rolled up into a legalistic privacy policy or general terms and conditions. Rather, if there are uses outside the bounds of these explicit purposes, the subscriber SHOULD be provided with a meaningful way to understand the purpose for additional uses, and the opportunity to accept or decline.
-->

CSPが政府機関または民間のプロバイダであるかどうかにかかわらず、次の要件がAuthenticationサービスを提供・利用する政府機関に対して適用される:
<!--
Regardless of whether the CSP is an agency or private sector provider, the following requirements apply to an agency offering or using the authentication service:
-->

* 政府機関は、Authenticatorの発行・維持を目的としたPIIの収集が*Privacy Act of 1974* [[Privacy Act]](#PrivacyAct) ([Section 9.4](#agency-privacy)参照)の要件をもたらすかどうか明確にするため、各機関のSenior Agency Official for Privacy (SAOP)と協議するものとする(SHALL)。
* 政府機関は、必要に応じてそのような収集活動を対象とするSystem of Records Notice (SORN)を公開するものとする(SHALL)。
* 政府機関は、Authenticatorの発行・維持を目的としたPIIの収集が*E-Government Act of 2002* [[E-Gov]](#E-Gov)の要件をもたらすかどうか明確にするため、各機関のSAOPと協議するものとする(SHALL)。
* 政府機関は、必要に応じてそのような収集活動を対象とするPrivacy Impact Assement(PIA)を公開するものとする(SHALL)。

<!--
1. The agency SHALL consult with their Senior Agency Official for Privacy (SAOP) and conduct an analysis to determine whether the collection of PII to issue or maintain authenticators triggers the requirements of the *Privacy Act of 1974* [[Privacy Act]](#PrivacyAct) (see [Section 9.4](#agency-privacy)).
* The agency SHALL publish a System of Records Notice (SORN) to cover such collections, as applicable.
* The agency SHALL consult with their SAOP and conduct an analysis to determine whether the collection of PII to issue or maintain authenticators triggers the requirements of the *E-Government Act of 2002* [[E-Gov]](#E-Gov).
* The agency SHALL publish a Privacy Impact Assessment (PIA) to cover such collection, as applicable.
-->

### 4.5 要件サマリ
<!--
### 4.5 Summary of Requirements
-->

*本セクションは参考情報である*
<!--
*This section is informative.*
-->

[Table 4-1](#63bSec4-Table1) にて各AAL毎の要件のサマリを述べる:
<!--
[Table 4-1](#63bSec4-Table1) summarizes the requirements for each of the AALs:
-->

<a name="63bSec4-Table1"></a>

<div class="text-center" markdown="1">

**Table 4-1 各AAL毎の要件サマリ**
<!--
**Table 4-1 AAL Summary of Requirements**
-->

</div>

要件 | AAL1 | AAL2 | AAL3
------------|-------|-------|-------
**許可されているAuthenticatorタイプ** | 記憶シークレット;<br />ルックアップシークレット;<br />アウトオブバンド;<br />単一要素OTPデバイス;<br />多要素OTPデバイス;<br />単一要素暗号ソフトウェア;<br />単一要素暗号デバイス;<br />多要素暗号ソフトウェア;<br />多要素暗号デバイス<br /> | 多要素OTPデバイス;<br />多要素暗号ソフトウェア;<br />単一要素暗号デバイス;<br />または 記憶シークレット及び:<br />&nbsp;&bull;&nbsp;ルックアップシークレット<br />&nbsp;&bull;&nbsp;アウトオブバンド<br />&nbsp;&bull;&nbsp;単一要素OTPデバイス<br />&nbsp;&bull;&nbsp;単一要素暗号ソフトウェア<br />&nbsp;&bull;&nbsp;単一要素暗号デバイス<br /> | 多要素暗号デバイス;<br />単一要素暗号デバイス及び &nbsp;&nbsp;記憶シークレット;<br />単一要素OTPデバイス及び多要素暗号デバイスまたはソフトウェア;<br />単一要素OTPデバイス及び単一要素暗号ソフトウェア及び記憶シークレット
**FIPS 140 確認** | Level 1 (政府機関のVerifier) | Level 1 (政府機関のAuthenticator及びVerifier) | Level 2 総合 (多要素Authenticator)<br />Level 1 総合 (Verifier及び単一要素暗号デバイス)<br />Level 3 物理セキュリティ (全てのAuthenticator)
**Reauthentication** | 30 日 | 12 時間 または 30 分 の非活動; 1つのAuthentication要素でもよい(MAY) | 12 時間 または 15 分 の非活動; 両方のAuthentication要素をつかうものとする(SHALL)
**セキュリティ統制**|[SP 800-53](#SP800-53) 低度のベースライン(または等価)|[SP 800-53](#SP800-53) 中度のベースライン(または等価)|[SP 800-53](#SP800-53) 高度のベースライン(または等価)
**中間者攻撃耐性** | 必須 | 必須 | 必須 |
**Verifierなりすまし耐性** | 不要 | 不要 | 必須 |
**Verifier改竄耐性** | 不要 | 不要 | 必須 |
**リプレイ耐性** | 不要 | 必須 | 必須 |
**Authentication意図** | 不要 | 推奨 | 必須 |
**レコード保持ポリシ** | 必須 | 必須 | 必須 |
**プライバシ統制** | 必須 | 必須 | 必須 |

<!--
Requirement | AAL1 | AAL2 | AAL3
------------|-------|-------|-------
**Permitted authenticator types** | Memorized Secret;<br />Look-up Secret;<br />Out-of-Band;<br />SF OTP Device;<br />MF OTP Device;<br />SF Crypto Software;<br />SF Crypto Device;<br />MF Crypto Software;<br />MF Crypto Device<br /> | MF OTP Device;<br />MF Crypto Software;<br />MF Crypto Device;<br />or Memorized Secret plus:<br />&nbsp;&bull;&nbsp;Look-up Secret<br />&nbsp;&bull;&nbsp;Out-of-Band<br />&nbsp;&bull;&nbsp;SF OTP Device<br />&nbsp;&bull;&nbsp;SF Crypto Software<br />&nbsp;&bull;&nbsp;SF Crypto Device<br /> | MF Crypto Device;<br />SF Crypto Device plus &nbsp;&nbsp;Memorized Secret;<br />SF OTP Device plus MF Crypto Device or Software;<br />SF OTP Device plus SF Crypto Software plus Memorized Secret
**FIPS 140 verification** | Level 1 (Government agency verifiers) | Level 1 (Government agency authenticators and verifiers) | Level 2 overall (MF authenticators)<br />Level 1 overall (verifiers and SF Crypto Devices)<br />Level 3 physical security (all authenticators)
**Reauthentication** | 30 days | 12 hours or 30 minutes inactivity; MAY use one authentication factor | 12 hours or 15 minutes inactivity; SHALL use both authentication factors
**Security controls**|[SP 800-53](#SP800-53) Low Baseline (or equivalent)|[SP 800-53](#SP800-53) Moderate Baseline (or equivalent)|[SP 800-53](#SP800-53) High Baseline (or equivalent)
**MitM resistance** | Required | Required | Required |
**Verifier-impersonation resistance** | Not required | Not required | Required |
**Verifier-compromise resistance** | Not required | Not required | Required |
**Replay resistance** | Not required | Required | Required |
**Authentication intent** | Not required | Recommended | Required |
**Records Retention Policy** | Required | Required | Required |
**Privacy Controls** | Required | Required | Required |
-->