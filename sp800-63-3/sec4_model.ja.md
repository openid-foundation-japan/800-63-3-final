<a name="sec4"></a>

<div class="breaker"></div>

## 4 Digital Identity Model

*This section is informative.*

### <a name="4-1"></a>4.1 Overview

本ガイドライン群における Digital Identity モデルは, 現時点で市場で調達可能なテクノロジーやアーキテクチャーを反映したものとなっている. 多数の主体に渡って Credential 発行機能と Attribute 発行機能を分離するといったようなより複雑なモデルも, 実現可能かつある種のアプリケーションでは有用かもしれない. 本ドキュメントではよりシンプルなモデルを採用するが, これは各機関が上記の機能分割などを行うことを妨げるものではない. さらには, CSP が実行する Enrollment, Identity Proofing および発行プロセスの中には, しばしば Registration Authority (RA) や Identity Manager (IM) と呼ばれるような主体に移譲されるものもある. こういったタイプの関係性や要件は本ドキュメントの扱うところではない. また CSP といった場合には RA と IM の機能も含むものとする. また CSP が Digital Identity サービス以外のサービスを提供することもありうる. そういったシチュエーションでは, 本ガイドライン群の要件は CSP としての機能にのみ該当し, その他のサービスには影響を与えないものとする.

<!-- The digital identity model used in these guidelines reflects technologies and architectures currently available in the market. More complex models that separate functions &mdash; such as issuing credentials and providing attributes &mdash; among a larger number of parties are also available and may have advantages in some application classes. While a simpler model is used in this document, it does not preclude agencies from separating these functions. Additionally, certain enrollment, identity proofing, and issuance processes performed by the CSP are sometimes delegated to an entity known as either the registration authority (RA) or identity manager (IM). A close relationship between the RA and CSP is typical, and the nature of this relationship may differ among RAs, IMs, and CSPs. The type of relationship and its requirements is outside of the scope of this document. Accordingly, the term CSP will be inclusive of RA and IM functions. Finally, a CSP may provide other services in addition to digital identity services. In these situations, the requirements specified throughout these guidelines only apply to the CSP function(s), not the additional services. -->

Digital Identity はオンライン Transaction に関与する Subject を一意に表現するものである. Subject と現実世界の Identity との紐付けを検証するプロセスは, *Identity Proofing* と呼ばれる. 本ガイドラインでは, Proof される主体を *Applicant* と呼び, Proofing プロセスを完了した Applicant のことを *Subscriber* と呼ぶ.

<!-- Digital identity is the unique representation of a subject engaged in an online transaction. The process used to verify a subject's association with their real world identity is called *identity proofing*. In these guidelines, the party to be proofed is called an *applicant*. When the applicant successfully completes the proofing process, they are referred to as a *subscriber*. -->

Identity Proofing の強度は IAL と呼ばれる序数的指標で表される. IAL1 では Identity Proofing は不要で, Applicant から提供された Attribute 情報はすべて (それが CSP / RP から提供されたものだとしても) Self-asserted であるか, 未検証の Self-asserted 相当として扱われる. IAL2 と IAL3 では Identity Proofing が必須となり, RP が CSP に対して, 検証済 Attribute Value, 検証済 Attribute Reference, ないしは Pseudonymous Identifier などといった Subscriber に関する情報を Assert するよう要求することもある. これらの情報は RP が Authorization 判定を行う際の材料となる. RP は IAL2 ないしは IAL3 を必要としつつ, 特定の Attribute のみを必須とすることもでき, そうすることで Subject に対してある一定レベルの Pseudonymity を確保することができる. このプライバシー強化アプローチは, Proofing プロセスの強度を Authentication プロセスの強度から分離したことにより可能となっている. さらに RP は Federated Identity アプローチを採用することもでき, その場合 RP は Identity Proofing, Attribute 収集および保管をすべて CSP にアウトソースすることとなる.

<!-- The strength of identity proofing is described by an ordinal measurement called the IAL. At IAL1, identity proofing is not required, therefore any attribute information provided by the applicant is self-asserted, or should be treated as self-asserted and not verified (even if provided by a CSP to an RP). IAL2 and IAL3 require identity proofing, and the RP may request the CSP assert information about the subscriber, such as verified attribute values, verified attribute references, or pseudonymous identifiers. This information assists the RP in making authorization decisions. An RP may decide that it requires IAL2 or IAL3, but may only need specific attributes, resulting in the subject retaining some degree of pseudonymity. This privacy-enhancing approach is a benefit of separating the strength of the proofing process from that of the authentication process. An RP may also employ a federated identity approach where the RP outsources all identity proofing, attribute collection, and attribute storage to a CSP. -->

本ガイドライン群では Authenticate される主体を *Claimant* と呼び, 当該 Identity を検証する主体を *Verifier* と呼ぶ. Authentication Protocol を通じ, Claimant が Verifier に対して1つ以上の Authenticator を保持・管理していることを立証すると, Verifier は Claimant が正規の Subscriber であると検証できる. その後 Verifier は Subscriber に関する Assertion を RP に送る. この時 Subscriber は Pseudonymous なこともあればそうでないこともある. Assertion には識別子が含まれ, 場合によっては氏名や Enrollment プロセスにおいて収集されたその他の Attribute などの Subscriber に関する Identity 情報も含まれる. どういった情報を含むかは CSP のポリシーや RP のニーズ, Subject による Attribute 提供に関する同意内容などに依存する) Verifier 自身が RP である場合, Assertion は暗黙的なものとなる. RP は Verifier から提供された Authenticated な情報を元に, Authorization 判定を行う.

<!-- In these guidelines, the party to be authenticated is called a *claimant* and the party verifying that identity is called a *verifier*. When a claimant successfully demonstrates possession and control of one or more authenticators to a verifier through an authentication protocol, the verifier can verify that the claimant is a valid subscriber. The verifier passes on an assertion about the subscriber, who may be either pseudonymous or non-pseudonymous, to the RP. That assertion includes an identifier, and may include identity information about the subscriber, such as the name, or other attributes that were collected in the enrollment process (subject to the CSP's policies, the RP's needs, and consent for disclosure of attributes given by the subject). Where the verifier is also the RP, the assertion may be implicit. The RP can use the authenticated information provided by the verifier to make authorization decisions. -->

Authentication により, Claimant が Credential に紐づく Authenticator を管理下に置いていることが確かめられ, 場合によっては Subscriber の Attribute Value (e.g., Subscriber が U.S. 市民, 特定の大学の生徒であること, ある機関や組織から特定の番号やコードを割り当てられていること) についても確認できる. Authentication は Claimant の Authorization や Access 権限の決定を行うものではなく, これらは別の意思決定であり, 本ガイドライン群の扱うところではない. RP は Subscriber の Authenticated Identity および Attribute を他の要素と組み合わせ, Authorization の決定を行う. 本ドキュメントスイートは RP が Subscriber に対して Authenticate を成功させるために追加情報を要求することを妨げるものではない.

<!-- Authentication establishes confidence that the claimant has possession of an authenticator(s) bound to the credential, and in some cases in the attribute values of the subscriber (e.g., if the subscriber is a U.S. citizen, is a student at a particular university, or is assigned a particular number or code by an agency or organization). Authentication does not determine the claimant's authorizations or access privileges; this is a separate decision, and is out of these guidelines' scope. RPs can use a subscriber's authenticated identity and attributes with other factors to make authorization decisions. Nothing in this document suite precludes RPs from requesting additional information from a subscriber that has successfully authenticated. -->

Authentication プロセスの強度は AAL と呼ばれる序数的指標で表される. AAL1 では Single-factor Authentication が求められ, 幅広い種類の Authenticator Type が利用可能である. AAL2 ではより強固なセキュリティーの為に2つの Authentication Factor が要求される. 最高レベルの Authentication である AAL3 では, さらにハードウェアベースの Authenticator と Verifier なりすまし対策が要求される.

<!-- The strength of the authentication process is described by an ordinal measurement called the AAL. AAL1 requires single-factor authentication and is permitted with a variety of different authenticator types. At AAL2, authentication requires two authentication factors for additional security. Authentication at the highest level, AAL3, additionally requires the use of a hardware-based authenticator and verifier impersonation resistance. -->

ここで扱われる Digital Identity モデルを構成する多様な主体とインタラクションを [Figure 4-1](#63Sec4-Figure1) に示す.

<!-- The various entities and interactions that comprise the digital identity model used here are illustrated in [Figure 4-1](#63Sec4-Figure1). -->

<a name="63Sec4-Figure1"></a>
<div class="text-center" markdown="1">
<img src="sp800-63-3/media/model.png" alt="Digital Identity Model" style="width:1000px;height:528px;;min-width: 1000px;min-height: 528px;"/>

**Figure 4-1 Digital Identity Model**
</div>

このダイアグラム左側は Enrollment, Credential 発行, ライフサイクル管理, および Identity Proofing と Authentication プロセスにおけるさまざまなステータスを示している. 通常は以下のようなシーケンスでインタラクションが行われる.

<!-- The left side of the diagram shows the enrollment, credential issuance, lifecycle management activities, and various states of an identity proofing and authentication process. The usual sequence of interactions is as follows: -->

1. Applicant が Enrollment プロセスを通じて CSP に申請を行う.
2. CSP は Applicant に対して Identity Proofing を行い, Proofing が成功すると Applicant は Subscriber になる.
3. Authenticator とそれに対応する Credential が CSP と Subscriber の間で確立される.
4. CSP は Credential とそのステータスを管理, Credential のライフタイム期間内に収集された Enrollment データを管理し, Subscriber は自身の Authenticator を管理する.

<!-- 1.	An applicant applies to a CSP through an enrollment process.
2.	The CSP identity proofs that applicant. Upon successful proofing, the applicant becomes a subscriber.
3.	Authenticator(s) and a corresponding credential are established between the CSP and the subscriber.
4.	The CSP maintains the credential, its status, and the enrollment data collected for the lifetime of the credential (at a minimum). The subscriber maintains his or her authenticator(s). -->

上記のシーケンスほど一般的ではなくても, 同様の機能要件を満たすその他のシーケンスもありうる.

<!-- Other sequences are less common, but could also achieve the same functional requirements. -->

[Figure 4-1](#63Sec4-Figure1) 右側は Authenticator を利用して Digital Authentication を行う主体およびインタラクションを示している. Subscriber は Verifier に対して Authenticate する必要がある時は Claimant と呼ばれる. ここでのインタラクションは以下の通りである.

<!-- The right side of [Figure 4-1](#63Sec4-Figure1) shows the entities and interactions involved in using an authenticator to perform digital authentication. A subscriber is referred to as a claimant when he or she needs to authenticate to a verifier. The interactions are as follows: -->

1. Claimant が Authentication Protocol を通じて, Verifier に対し Authenticator を保持・管理していることを証明する.
2. Verifier は CSP とインタラクションを行い, Subscriber の Identity と Authenticator を紐づける Credential を検証し, 任意で Claimant の Attribute を取得する.
3. CSP ないし Verifier は Subscriber に関する Assertion を RP に提供する. RP は Assertion に含まれる情報を利用して Authorization の決定を行う.
4. Subscriber と RP の間で Authenticated Session が確立される.

<!-- 1.	The claimant proves possession and control of the authenticator(s) to the verifier through an authentication protocol.
2.	The verifier interacts with the CSP to validate the credential that binds the subscriber's identity to their authenticator and to optionally obtain claimant attributes.
3.	The CSP or verifier provides an assertion about the subscriber to the RP, which may use the information in the assertion to make an authorization decision.
4.	An authenticated session is established between the subscriber and the RP. -->

いかなる場合でも, RP は Claimant を Authenticate する前に CSP に対して必要な Attribute を要求しべきである. さらに Claimant は Assertion の生成および送信前に Attribute 送信についての同意を求められるべきである.

<!-- In all cases, the RP should request the attributes it requires from a CSP before authenticating the claimant. In addition, the claimant should be requested to consent to the release of those attributes prior to generation and release of an assertion. -->

場合によっては, Verifier は Authentication を完了させる為に CSP とリアルタイムでコミュニケーションする必要はない (e.g., デジタル証明書を利用する場合). したがって, Verifier と CSP の間の点線は当該2主体の論理的なリンクを示している. 実装によっては, Verifier, RP, CSP の各機能は [Figure 4-1](#63Sec4-Figure1) のように分離されているが, これらの機能が同じプラットフォーム上に存在する場合, 各構成要素間のインタラクションは, 共有の信頼できない Network 越しのプロトコルではなく, 同一システム上で動作するアプリケーション間のローカルメッセージであることもある.

<!-- In some cases, the verifier does not need to communicate in real time with the CSP to complete the authentication activity (e.g., some uses of digital certificates). Therefore, the dashed line between the verifier and the CSP represents a logical link between the two entities. In some implementations, the verifier, RP, and CSP functions may be distributed and separated as shown in [Figure 4-1](#63Sec4-Figure1). However, if these functions reside on the same platform, the interactions between the components are local messages between applications running on the same system rather than protocols over shared, untrusted networks. -->

上述の通り, CSP は自身が発行した Credential に関するステータス情報を管理する. CSP は通常 Credential 発行時に管理期間を制限するため有限のライフタイムを設定する. ステータス変更時や Credential の期限切れに近づいた時は, Credential は更新されたり再発行されるか, 無効化され破棄される. 典型的には, Subscriber が自身の現存の期限切れしていない Authenticator および Credential を使って CSP に対して Authenticate した上で新規の Authenticator および Credential の発行を依頼する. Subscriber が有効期限切れや無効化処理が行われる前に Authenticator および Credential の再発行を行えなかった場合は, 再度 Enrollment プロセスを経て新規の Authenticator および Credential を取得することになるであろう. その代わりに CSP が有効期限切れ後一定期間は再発行リクエストを受け付ける, というようなことも考えられる.

<!-- As noted above, a CSP maintains status information about the credentials it issues. CSPs will generally assign a finite lifetime when issuing credentials to limit the maintenance period. When the status changes, or when the credentials near expiration, credentials may be renewed or re-issued; or, the credential may be revoked and destroyed. Typically, the subscriber authenticates to the CSP using their existing, unexpired authenticator and credential in order to request issuance of a new authenticator and credential. If the subscriber fails to request authenticator and credential re-issuance prior to their expiration or revocation, they may be required to repeat the enrollment process to obtain a new authenticator and credential. Alternatively, the CSP may choose to accept a request during a grace period after expiration. -->

### 4.2 Enrollment and Identity Proofing

Normative 要件は [SP 800-63A](sp800-63a.html) *Enrollment and Identity Proofing* に従うこと.

<!-- Normative requirements can be found in [SP 800-63A](sp800-63a.html), *Enrollment and Identity Proofing*. -->

前セクションでは Digital Identity 概念モデルにおける参加者を紹介した. 本セクションでは, 上記参加者の関係性と Enrollment および Identity Proofing における責任について詳説する.

<!-- The previous section introduced the  participants in the conceptual digital identity model. This section provides additional details regarding the participants' relationships and responsibilities in enrollment and identity proofing. -->

このステージで *Applicant* と呼ばれている個人は, CSP に Identity Proofing を要求する. Applicant が Proofing に成功すると, 当該個人は当該 CSP の Subscriber と呼ばれることになる.

<!-- An individual, referred to as an *applicant* at this stage, opts to be identity proofed by a CSP. If the applicant is successfully proofed, the individual is then termed a subscriber of that CSP. -->

CSP は個々の Subscriber をユニークに識別する方法を確立し, Subscriber の Credential を登録し, Subscriber に発行された Authenticator をトラックする. Subscriber が Enrollment 時に Authenticator を渡されることもあれば, CSP が Subscriber のすでに所有している Authenticator に Subscriber を紐付けることもあれば, それ以降の必要となった段階で Authenticator が生成されることもある. Subscriber は Authenticator を管理し, Authenticator をアクティブに保つため CSP のポリシーにしたがう責務がある. CSP は各 Subscriber の Enrollment レコードを管理し, Authenticator の紛失・盗難時等のリカバリーに対応する責務がある.

<!-- The CSP establishes a mechanism to uniquely identify each subscriber, register the subscriber's credentials, and track the authenticators issued to that subscriber. The subscriber may be given authenticators at the time of enrollment, the CSP may bind authenticators the subscriber already has, or they may be generated later as needed. Subscribers have a duty to maintain control of their authenticators and comply with CSP policies in order to maintain active authenticators. The CSP maintains enrollment records for each subscriber to allow recovery of authenticators, for example, when they are lost or stolen. -->

### 4.3 Authentication and Lifecycle Management

Normative 要件は [SP 800-63B](sp800-63b.html), *Authentication and Lifecycle Management* に従うこと.

<!-- Normative requirements can be found in [SP 800-63B](sp800-63b.html), *Authentication and Lifecycle Management*. -->

#### 4.3.1 Authenticators

Authentication システムの古典的パラダイムでは, 3つの要素を Authentication の要とする.

<!-- The classic paradigm for authentication systems identifies three factors as the cornerstones of authentication: -->

* Something you know (e.g., a password).
* Something you have (e.g., an ID badge or a cryptographic key).
* Something you are (e.g., a fingerprint or other biometric data).

MFA は上記のうち2つ以上の要素を使うことを意味する. Authentication システムの強度は, そのシステムに組み込まれた上記の要素数に大きく依存する. より多くの要素を用いれば, システムはより堅固になる. 本ガイドライン群の目的においては, Authentication システムが最高のセキュリティー要件を満たすには, 2つの要素を利用するのが適切である. [Section 5.1](#5-1) で述べるように, RP や Verifier は Claimed Identity に対するリスク評価のために, 位置データや Device Identity など, 上記3要素以外のタイプの情報を利用することもありうるが, それらは Authentication Factor とは見なされない.

<!-- MFA refers to the use of more than one of the above factors. The strength of authentication systems is largely determined by the number of factors incorporated by the system &mdash; the more factors employed, the more robust the authentication system. For the purposes of these guidelines, using two factors is adequate to meet the highest security requirements. As discussed in [Section 5.1](#5-1), other types of information, such as location data or device identity, may be used by an RP or verifier to evaluate the risk in a claimed identity, but they are not considered authentication factors. -->

Digital Authentication では, Claimant は CSP に登録された Authenticator を保持・管理し, 当該 Authenticator は Claimant Identity の証明に使われる. Authenticator は Claimant が正規の Subscriber であることを証明するためのシークレットを内包し, Claimant は Authenticator を保持・管理していることをネットワーク越しに証明することで, システムやアプリケーションに対して Authenticate する.

<!-- In digital authentication the claimant possesses and controls one or more authenticators that have been registered with the CSP and are used to prove the claimant's identity. The authenticator(s) contains secrets the claimant can use to prove that he or she is a valid subscriber, the claimant authenticates to a system or application over a network by proving that he or she has possession and control of one or more authenticators. -->

Authenticator に含まれるシークレットは, Public Key ペア (Asymmetric Keys) ないしは Shared Secret (Symmetric Key) に基づいている. Public Key と Private Key の対が Public Key ペアとなる. Private Key は Authenticator 上に保存され, Claimant が Authenticator を保持・管理していることを証明するために利用される. Verifier は何らかの Credential (典型的には Public Key Certificate) を通じて Claimant の Public Key を知っており, Authentication Protocol を通じて Claimant が対応する Private Key を含んだ Authenticator を保持・管理していることを証明することで, Claimant の Identity を検証できる.

<!-- The secrets contained in authenticators are based on either public key pairs (asymmetric keys) or shared secrets (symmetric keys). A public key and a related private key comprise a public key pair. The private key is stored on the authenticator and is used by the claimant to prove possession and control of the authenticator. A verifier, knowing the claimant's public key through some credential (typically a public key certificate), can use an authentication protocol to verify the claimant's identity by proving that the claimant has possession and control of the associated private key authenticator. -->

Authenticator 上に保存される　Shared Secret は, Symmetric Key ないしは Memorized Secret (e.g., Password や PIN) となる. 上述の Asymmetric Key のケースとはことなり, Subscriber はこれらを Verifier と共有する必要がある. Symmetric Key も Password も同じようなプロトコルで利用可能だが, どのように Subscriber と関連づけられるかという点が大きく異なる. Symmetric Key は一般的に Subscriber が管理するハードウェアないしソフトウェア内に保存されるが, Password は Subscriber に記憶されることが想定される. ほとんどのユーザーは記憶および入力しやすい短い Password を選ぶため, Password は Cryptographic Key よりも短くなりがちである. さらに, 乱数を用いてシステム的に鍵を生成する場合と比べ, ユーザーはその長さのパスワードの候補空間の非常に小さなサブセットの中から記憶可能な Password を選びがちであり, その多くは似た値になりがちである. したがって, Cryptographic Key は通常 Network ベースの推測攻撃が不可能なほど十分長くなるが, ユーザーが選択した Password は, 特に何の防御策もない場合, 脆弱である可能性がある.

<!-- Shared secrets stored on authenticators may be either symmetric keys or memorized secrets (e.g., passwords and PINs), as opposed to the asymmetric keys described above, which subscribers need not share with the verifier. While both keys and passwords can be used in similar protocols, one important difference between the two is how they relate to the subscriber. While symmetric keys are generally stored in hardware or software that the subscriber controls, passwords are intended to be memorized by the subscriber. Since most users choose short passwords to facilitate memorization and ease of entry, passwords typically have fewer characters than cryptographic keys. Further, whereas systems choose keys at random, users attempting to choose memorable passwords will often select from a very small subset of the possible passwords of a given length, and many will choose very similar values. As such, whereas cryptographic keys are typically long enough to make network-based guessing attacks untenable, user-chosen passwords may be vulnerable, especially if no defenses are in place. -->

本 Vol. では, Authenticator は常にシークレットを含む. 古典的 Authentication Factor の中には直接 Digital Authentication に適用されないものもある. 例えば物理的な運転免許証は Something you have であり, 人間 (e.g., 警備員) に対して Authenticate する際には利用可能であるが, それ自体は Digital Authentication のための Authenticator とはならない. Something you know に分類される Authentication Factor は, 必ずしもシークレットであるとは限らない. Claimant に対して Claimant のみが知っているであろう質問に答えるよう求める Knowledge-based Authentication も, Digital Authentication で利用可能なシークレットとはならない. Biometric もシークレットとはならない. よって本ガイドライン群では Authentication のために Biometric を使うのは, それが強固に物理的 Authenticator に紐づけられている場合に限る.

<!-- In this volume, authenticators always contain a secret. Some of the classic authentication factors do not apply directly to digital authentication. For example, a physical driver's license is something you have, and may be useful when authenticating to a human (e.g., a security guard), but is not in itself an authenticator for digital authentication. Authentication factors classified as something you know are not necessarily secrets, either. Knowledge-based authentication, where the claimant is prompted to answer questions that are presumably known only by the claimant, also does not constitute an acceptable secret for digital authentication. A biometric also does not constitute a secret. Accordingly, these guidelines only allow the use of biometrics for authentication when strongly bound to a physical authenticator. -->

Digital Authentication システムは, 以下の2つの方法のどちらかで複数の要素を内包する.

<!-- A digital authentication system may incorporate multiple factors in one of two ways: -->

1. 複数の要素が Verifier に提示される.
2. ある要素が Verifier に提示されるシークレットを保護するために利用される.

<!-- 1. The system may be implemented so that multiple factors are presented to the verifier; or
2. Some factors may be used to protect a secret that will be presented to the verifier. -->

例えば, 上記1は Memorized Secret (what you know) を Out-of-band Device (what you have) と組み合わせることで実現可能である.　両方の Authenticator Output が Verifier に提示され, Claimant の Authentication に使われる. 一方, 上記2は, Cryptographic Key を内包するハードウェア (Authenticator) があり, Cryptographic Key への Access が指紋により保護されている場合を考えるとよい. Biometric と共に利用すると, Cryptographic Key を使って Claimant を Authenticate するための Output が出力される.

<!-- For example, item 1 can be satisfied by pairing a memorized secret (what you know) with an out-of-band device (what you have). Both authenticator outputs are presented to the verifier to authenticate the claimant. For item 2, consider a piece of hardware (the authenticator) that contains a cryptographic key (the authenticator secret) where access is protected with a fingerprint. When used with the biometric, the cryptographic key produces an output that is used to authenticate the claimant. -->

上述のように, Biometrics が Authentication の1要素として用いられる場合, それ自体は Digital Authentication で利用可能なシークレットとはならないが, Digital Identity の Authentication においてはその利用箇所が存在する. Biometric 特性はユニークな個人の Attribute であり, 検証時に対面の人間の Identity を検証するためには利用可能である. 顔の特徴, 指紋, 虹彩パターン, 声紋等, 多くの Biometric 特性が存在する. [SP 800-63A](sp800-63a.html) *Enrollment and Identity Proofing* では, Enrollment プロセスにおいて Biometrics を収集し, 登録した Subscriber による Enrollment の否認を防止し, 不正な Enrollment を行った人物を特定するために利用することを推奨している.

<!-- As noted above, biometrics, when employed as a single factor of authentication, do not constitute acceptable secrets for digital authentication &mdash; but they do have their place in the authentication of digital identities. Biometric characteristics are unique personal attributes that can be used to verify the identity of a person who is physically present at the point of verification. They include facial features, fingerprints, iris patterns, voiceprints, and many other characteristics. [SP 800-63A](sp800-63a.html), *Enrollment and Identity Proofing* recommends that biometrics be collected in the enrollment process to later help prevent a registered subscriber from repudiating the enrollment, and to help identify those who commit enrollment fraud. -->

#### 4.3.2 Credentials

前セクションで述べた通り, Credential は発行プロセスにおいて Authenticator と Subscriber を識別子を通じて紐づける. Credential は CSP によって保管・管理されるが, Claimant が保持することもある. Claimant は Authenticator を保持するが, 必ずしも Credential を保持する必要はない. 例えば, あるユーザーの Attribute を含んだデータベースエントリーは, 本ドキュメントの目的においては Credential であると見なされますが, これは Verifier が保持するものです. X.509 Public Key Certificate は Claimant が保持しうる Credential の古典的な例です.

<!-- As described in the preceding sections, a credential binds an authenticator to the subscriber, via an identifier, as part of the issuance process. A credential is stored and maintained by the CSP, though the claimant may possess it. The claimant possesses an authenticator, but is not necessarily in possession of the credential. For example, database entries containing the user attributes are considered to be credentials for the purpose of this document but are possessed by the verifier. X.509 public key certificates are a classic example of credentials the claimant can, and often does, possess. -->

#### 4.3.3 Authentication Process

Authentication プロセスは, Claimant が Verifier に Authenticator の保持・管理を示すところから始まる. ここで Authenticator は Authentication Protocol を通じて Asserted Identity に紐づけられている. 一度 Authenticator の保持・管理が示されれば, Verifier は, 通常 CSP とのインタラクションを通じて, 当該 Credential が依然有効であるかどうかを確認する.

<!-- The authentication process begins with the claimant demonstrating to the verifier possession and control of an authenticator that is bound to the asserted identity through an authentication protocol. Once possession and control have been demonstrated, the verifier verifies that the credential remains valid, usually by interacting with the CSP. -->

Authentication Protocol における Verifier と Claimant の間のインタラクションは, システム全体のセキュリティーにとって極めて重要である. よく設計されたプロトコルは, Authentication の最中および事後において, Claimant と Verifier の間のコミュニケーションの Integrity (完全性) および Confidentiality (機密性) を保護し, Attacker が正当な Verifier であるかのように偽装できてしまった場合の被害を限定的にする.

<!-- The exact nature of the interaction between the verifier and the claimant during the authentication protocol is extremely important in determining the overall security of the system. Well-designed protocols can protect the integrity and confidentiality of communication between the claimant and the verifier both during and after the authentication, and can help limit the damage that can be done by an attacker masquerading as a legitimate verifier. -->

また, Verifier 側で Attacker による Authentication 試行レートを制限したり不正な試行を遅延させたりすることで, Password や PIN といったエントロピーの低いシークレットに対する Online Guessing Attack の影響を軽減できる. 一般的に Online Guessing Attack ではほとんどの試行が失敗するので, その対策は失敗試行数を制限するというような方式となる.

<!-- Additionally, mechanisms located at the verifier can mitigate online guessing attacks against lower entropy secrets &mdash; like passwords and PINs &mdash; by limiting the rate at which an attacker can make authentication attempts, or otherwise delaying incorrect attempts. Generally, this is done by keeping track of and limiting the number of unsuccessful attempts, since the premise of an online guessing attack is that most attempts will fail. -->

Verifier は機能的役割であるが, しばしば CSP, RP ないしはその両方と合わせて実装される. Verifier が CSP から独立した主体である場合, 一般的には Authentication プロセス中に Verifier が Subscriber の Authenticator Secret を知ることがないよう保証できることが望ましい. 少なくとも Verifier が CSP に保管されているシークレットに無制限にアクセスできるような状況ではないことが保証されるべきである.

<!-- The verifier is a functional role, but is frequently implemented in combination with the CSP, the RP, or both. If the verifier is a separate entity from the CSP, it is often desirable to ensure that the verifier does not learn the subscriber's authenticator secret in the process of authentication, or at least to ensure that the verifier does not have unrestricted access to secrets stored by the CSP. -->

### 4.4 Federation and Assertions

Normative 要件は [SP 800-63C](sp800-63c.html), *Federation and Assertions* に従うこと.

<!-- Normative requirements can be found in [SP 800-63C](sp800-63c.html), *Federation and Assertions*. -->

全体として, SP 800-63 は Federated Identity アーキテクチャーを前提とはしていない. むしろ本ガイドライン群は市場に存在するモデルについては感知せず, 各機関は自身の要件にそった Digital Authentication スキームを導入できる. しかしながら, 単一の機関や RP が運営するサイロ化した多数の Identity システムよりも, Identity Federation の方が好ましい.

<!-- Overall, SP 800-63 does not presuppose a federated identity architecture; rather, these guidelines are agnostic to the types of models that exist in the marketplace, allowing agencies to deploy a digital authentication scheme according to their own requirements. However, identity federation is preferred over a number of siloed identity systems that each serve a single agency or RP. -->

Federated アーキテクチャーには, 以下にあげたようなものをはじめとする多くの利点がある.

<!-- Federated architectures have many significant benefits, including, but not limited to: -->

* ユーザーエクスペリエンスの向上. 例えば, ある個人がひとたび Identity Proofing を終えると, 発行された Credential を複数の RP に対して再利用できる.
* ユーザーと各機関双方にとってコスト低減効果がある. (ユーザーにとっては Authenticator の減少, 各機関にとっては情報テクノロジーインフラストラクチャーの縮小)
* 各機関が Personal Information を保存するにあたっての, 収集, 保管, 処理, 法令遵守活動のための活動費用が不要となり, データ最小化につながる.
* 各機関はサービス提供に必要な最小限の Attribute を要求し, それを Pseudonymous Attribute Assertion の Claim として含めるよう要求できる.
* 各機関は Identity 管理ではなく自身のミッションに集中することができる.

<!-- * Enhanced user experience. For example, an individual can be identity proofed once and reuse the issued credential at multiple RPs.
* Cost reduction to both the user (reduction in authenticators) and the agency (reduction in information technology infrastructure).
* Data minimization as agencies do not need to pay for collection, storage, disposal, and compliance activities related to storing personal information.
* Pseudonymous attribute assertions as agencies can request a minimized set of attributes, to include claims, to fulfill service delivery.
* Mission enablement as agencies can focus on mission, rather than the business of identity management. -->

次のセクションでは, 各機関が Federated Identity アーキテクチャを選択する場合に登場する構成要素について説明します。

<!-- The following sections discuss the components of a federated identity architecture should an agency elect this type of model. -->

#### 4.4.1 Assertions

Upon completion of the authentication process, the verifier generates an assertion containing the result of the authentication and provides it to the RP. The assertion is used to communicate the result of the authentication process, and optionally information about the subscriber, from the verifier to the RP. Assertions may be communicated directly to the RP, or can be forwarded through the subscriber, which has further implications for system design.

An RP trusts an assertion based on the source, the time of creation, how long the assertion is valid from time of creation, and the corresponding trust framework that governs the policies and processes of CSPs and RPs. The verifier is responsible for providing a mechanism by which the integrity of the assertion can be confirmed.

The RP is responsible for authenticating the source (the verifier) and for confirming the integrity of the assertion. When the verifier passes the assertion through the subscriber, the verifier must protect the integrity of the assertion in such a way that it cannot be modified. However, if the verifier and the RP communicate directly, a protected session may be used to preserve the integrity of the assertion. When sending assertions across an open network, the verifier is responsible for ensuring that any sensitive subscriber information contained in the assertion can only be extracted by an RP that it trusts to maintain the information's confidentiality.

Examples of assertions include:

* Security Assertion Markup Language (SAML) assertions are specified using a mark-up language intended for describing security assertions. They can be used by a verifier to make a statement to an RP about the identity of a claimant. SAML assertions may optionally be digitally signed.
* OpenID Connect claims are specified using JavaScript Object Notation (JSON) for describing security, and optionally, user claims. JSON user info claims may optionally be digitally signed.
* Kerberos tickets allow a ticket-granting authority to issue session keys to two authenticated parties using symmetric key based encapsulation schemes.

#### 4.4.2 Relying Parties

An RP relies on results of an authentication protocol to establish confidence in the identity or attributes of a subscriber for the purpose of conducting an online transaction. RPs may use a subscriber's authenticated identity (pseudonymous or non-pseudonymous), the IAL, AAL, and FAL (FAL indicating the strength of the assertion protocol), and other factors to make authorization decisions. The verifier and the RP may be the same entity, or they may be separate entities. If they are separate entities, the RP normally receives an assertion from the verifier. The RP ensures that the assertion came from a verifier trusted by the RP. The RP also processes any additional information in the assertion, such as personal attributes or expiration times. The RP is the final arbiter concerning whether a specific assertion presented by a verifier meets the RP's established criteria for system access regardless of IAL, AAL, or FAL.

