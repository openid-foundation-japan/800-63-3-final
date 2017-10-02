<a name="sec5"></a>

<div class="breaker"></div>

## 5 Digital Identity Risk Management

_This section is normative._

本セクションおよび対応する Risk Assessment ガイダンス は, [NIST Risk Management Framework (RMF)](#NIST-RMF) およびその構成要素となる Special Publication を補完する. これは各機関にさらなる Risk Management プロセスを課すものではなく, 全ての関連する RMF ライフサイクルフェーズ実行に際する Digital Identity のリスクに関しての, 各機関の RP が適用しなければならない (SHALL) 具体的なガイダンスを提供するものである.

<!-- This section and the corresponding risk assessment guidance supplement the [NIST Risk Management Framework (RMF)](#NIST-RMF) and its component special publications. This does not establish additional risk management processes for agencies. Rather, requirements contained herein provide specific guidance related to digital identity risk that agency RPs SHALL apply while executing all relevant RMF lifecycle phases. -->

### <a name="5-1-overview"></a> 5.1 Overview

今日のデジタルサービスでは, Proofing と Authenticator と Federation の各要件をひとくくりにすると, 意図しない結果が生じ, 実装組織に不必要な実装負担をかけることがある. 単一の包括的な LOA ではなく, Digital Authentication の個々の構成要素ごとに失敗時のリスクと影響を評価することで, 機関は高確率で最も効果的に Identity Service を提供できることになるであろう. 以上のことから, 本ガイドライン群では Authentication エラーは全ての要件を満たすシングルトンではないという認識のもとに立つ.

<!-- In today's digital services, combining proofing, authenticator, and federation requirements into a single bundle sometimes has unintended consequences and can put unnecessary implementation burden on the implementing organization. It is quite possible that an agency can deliver the most effective set of identity services by assessing the risk and impacts of failures for each individual component of digital authentication, rather than as a single, all-encompassing LOA. To this end, these guidelines recognize that an authentication error is not a singleton that drives all requirements. -->

本 Vol. では各機関が避けるべき要件をまとめる.

<!-- This volume details requirements to assist agencies in avoiding: -->

1. Identity Proofing エラー (i.e., 偽の Applicant が正当なふりをして Identity を主張する)
2. Authentication エラー (i.e., 本来正当でない偽の Claimant が正当なふりをして Credential を利用する)
3. Federation エラー (i.e., Identity Assertion が毀損する)

<!-- 1. Identity proofing errors (i.e., a false applicant claiming an identity that is not rightfully theirs);
2. Authentication errors (i.e., a false claimant using a credential that is not rightfully theirs); and
3. Federation errors (i.e., an identity assertion is compromised). -->

Identity Proofing の失敗という観点からは, 潜在的に以下の2種類の影響が考えられる.

<!-- From the perspective of an identity proofing failure, there are two dimensions of potential failure: -->

1. サービスを異なる Subject に提供してしまうことによる影響. (e.g., Attacker が他人になりすませてしまう)
2. 過度の Identity Proofing による影響. (i.e., デジタルサービス提供のために, ある人物に関する必要以上に多くの情報を収集し, セキュアに保管してしまう)

<!-- 1. The impact of providing a service to the wrong subject (e.g., an attacker successfully proofs as someone else).
2. The impact of excessive identity proofing (i.e., collecting and securely storing more information about a person than is required to successfully provide the digital service). -->

そのため, 各機関は Proofing, Authentication および Federation のリスクを個別に評価し, 各トランザクションに必要な Assurance Level を決定する必要がある (SHALL).

<!-- As such, agencies SHALL assess the risk of proofing, authentication, and federation errors separately to determine the required assurance level for each transaction. -->

RMF の全体的な適用を支援するため, [Section 5.3](#section5-3) には Digital Identity 固有の影響カテゴリーを提示している.

<!-- [Section 5.3](#section5-3) provides impact categories specific to digital identity to assist in the overall application of the RMF. -->

Risk Assesment は, Identity Proofing, Authentication, Federation の各プロセスにおいて, どのようなリスクを軽減するべきかを決定するものである. こういった決定は, リスク明確化に役立つ技術への欲求を引き起こすものではなく, 適用可能な技術とリスク軽減策の選択を推進するものである. ひとたび機関が全体の Risk Assessment を終え, Identity Proofing, Authentication, (および該当する場合は) Federation それぞれに対する Assurance Level を選択し, それぞれの Assurance Level を満たすために採用すべきプロセスや技術を選定すると, 機関は [SP 800-53A](#SP800-53A) IA-1 a.1 に従い "Digital Identity Acceptance Statement" を策定すること (SHALL). [Section 5.5](#daps) に "Digital Identity Acceptance Statement" に必要なコンテンツを詳説する.

<!-- Risk assessments determine the extent to which risk must be mitigated by the identity proofing, authentication, and federation processes. These determinations drive the relevant choices of applicable technologies and mitigation strategies, rather than the desire for any given technology driving risk determinations. Once an agency has completed the overall risk assessment; selected individual assurance levels for identity proofing, authentication, and federation (if applicable); and determined the processes and technologies they will employ to meet each assurance level, agencies SHALL develop a "Digital Identity Acceptance Statement", in accordance with [SP 800-53A](#SP800-53A) IA-1 a.1. See [Section 5.5](#daps) for more detail on the necessary content of the Digital Identity Acceptance Statement. -->

### 5.2 <a name="5-2"></a> Assurance Levels

機関の RP はリスクに基づき以下の個々の Assurance Level を選択すること (SHALL).

<!-- An agency RP SHALL select, based on risk, the following individual assurance levels: -->

* IAL: 個人の Identity を確信を持って決定するための Identity Proofing プロセスの頑強性. IAL は潜在的 Identity Proofing エラーを軽減することを目的に選択される.
* AAL: Authentication プロセス自体, および Authenticator と特定個人の識別子の紐付けの頑強性. AAL は Authentication エラーを軽減することを目的に選択される. (i.e., 本来正当でない偽の Claimant が正当なふりをして Credential を利用する)
* FAL: Federation 時に Authentication および Attribute の情報をやり取りするための Assertion Protocol の頑強性. すべての Digital システムが Federated Identity アーキテクチャーを採用する訳ではないため, FAL はオプションである. FAL は Federation エラー (Identity Assertion が毀損するなど) を軽減することを目的に選択される.

<!-- * IAL: The robustness of the identity proofing process to confidently determine the identity of an individual. IAL is selected to mitigate potential identity proofing errors.
* AAL: The robustness of the authentication process itself, and the binding between an authenticator and a specific individual's identifier. AAL is selected to mitigate potential authentication errors (i.e., a false claimant using a credential that is not rightfully theirs).
* FAL: The robustness of the assertion protocol the federation uses to communicate authentication and attribute information (if applicable) to an RP. FAL is optional as not all digital systems will leverage federated identity architectures. FAL is selected to mitigate potential federation errors (an identity assertion is compromised). -->

Identity, Authenticator, Federation Assurance Level の概要はそれぞれ以下にまとめる.

<!-- A summary of each of the identity, authenticator, and federation assurance levels is provided below. -->

**Table 5-1 Identity Assurance Levels**

| Identity Assurance Level |
|:----------------------|
| **IAL1:** IAL1 では, Attribute がある場合それらは Self-asserted であるか, もしくは Self-asserted として扱われるべきである. |
| **IAL2:** IAL2 では, Remote ないしは対面での Identity Proofing が必須となる. IAL2 では, 識別に用いられる Attribute に関しては, [SP 800-63A](sp800-63a.html) に従い, 対面ないしは Remote で検証する必要がある. |
| **IAL3:** IAL3 では, 対面での Identity Proofing が必須となる. 識別に用いられる Attribute に関しては, [SP 800-63A](sp800-63a.html) に従い, Authorize された CSP の担当者によって物理ドキュメントを用いた検証がなされる必要がある. |

<!-- | Identity Assurance Level |
|:----------------------|
| **IAL1:** At IAL1, attributes, if any, are self-asserted or should be treated as self-asserted.|
| **IAL2:** At IAL2, either remote or in-person identity proofing is required. IAL2 requires identifying attributes to have been verified in person or remotely using, at a minimum, the procedures given in [SP 800-63A](sp800-63a.html).|
| **IAL3:** At IAL3, in-person identity proofing is required. Identifying attributes must be verified by an authorized CSP representative through examination of physical documentation as described in [SP 800-63A](sp800-63a.html).| -->

**Table 5-2 Authenticator Assurance Levels**

|Authenticator Assurance Level|
|:----------------------|
|**AAL1:** AAL1 では, Claimant が Subscriber に紐づく Authenticator を管理下に置いていることが, ある程度の確からしさで確認できる. AAL1 では Single-factor Authentication が必須となり, そこでは幅広い Authentication 技術が利用可能である. Authentication を成功させるには, Claimant がセキュアな Authentication Protocol を通じて Authenticator を保持・管理していることを証明する必要がある. |
| **AAL2:** AAL2 では, Claimant が Subscriber に紐づく Authenticator を管理下に置いているということが, 高い確度で保証される. セキュアな Authentication Protocol によって, 2つの異なる Authentication Factor を保持・管理していることを証明する必要がある. AAL2 以上では, Approved Cryptographic テクノロジーも必要となる. |
|**AAL3:** AAL3 では, Claimant が Subscriber のアカウントに紐づく Authenticator を管理下に置いているということが, 非常に高い確度で保証される. AAL3 の Authentication は, 暗号プロトコルによる鍵所有証明 (Proof of Possession) に基づいている. AAL3 は AAL2 と似ているが, AAL2 に加え Verifier Inpersonation 耐性のある "ハードの" Cryptographic Authenticator を要求する. |

<!-- |Authenticator Assurance Level|
|:----------------------|
|**AAL1:** AAL1 provides some assurance that the claimant controls an authenticator registered to the subscriber. AAL1 requires single-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove possession and control of the authenticator(s) through a secure authentication protocol.|
| **AAL2:** AAL2 provides high confidence that the claimant controls authenticator(s) registered to the subscriber. Proof of possession and control of two different authentication factors is required through a secure authentication protocol. Approved cryptographic techniques are required at AAL2 and above.|
|**AAL3:** AAL3 provides very high confidence that the claimant controls authenticator(s) registered to the subscriber. Authentication at AAL3 is based on proof of possession of a key through a cryptographic protocol. AAL3 is like AAL2 but also requires a "hard" cryptographic authenticator that provides verifier impersonation resistance.| -->

**Table 5-3 Federation Assurance Levels**

|Federation Assurance Level|
|:----------------------|
|**FAL1:** FAL1 では, RP は Identity Provider (IdP) から Bearer Assertion を受け取ることができる. IdP は Approved Cryptography を使って Assertion に署名する必要がある. |
|**FAL2:** FAL2 では, 上記に加え, RP のみが復号可能なかたちで, Assertion に対する暗号化が必要になる. 暗号化には Approved Cryptography を用いる. |
|**FAL3:** FAL3 では, Subscriber が Assertion および Assertion Artifact から参照される Cryptographic Key を保持していることを証明する必要がある. Assertion は Approved Cryptography を使って署名され, Approved Cryptography を使って RP に対して暗号化されなければならない. |

<!-- |Federation Assurance Level|
|:----------------------|
|**FAL1:** FAL1 permits the RP to receive a bearer assertion from an identity provider (IdP). The IdP must sign the assertion using approved cryptography.|
|**FAL2:** FAL2 adds the requirement that the assertion be encrypted using approved cryptography such that the RP is the only party that can decrypt it.|
|**FAL3:** FAL3 requires the subscriber to present proof of possession of a cryptographic key reference to in the assertion and the assertion artifact itself. The assertion must be signed using approved cryptography and encrypted to the RP using approved cryptography.| -->

総称的ないしは一括で扱う場合, 本ガイドラン群では IAL, AAL, FAL を **_ xAL _** と呼ぶこととする.

<!-- When described generically or bundled, these guidelines will refer to IAL, AAL, and FAL as **_xAL_**. -->

### <a name="section5-3"></a> 5.3 Risk and Impacts

本セクションでは IAL, AAL, FAL を決定する際に利用される影響カテゴリーについて述べる.

<!-- This section provides details on the impact categories used to determine IAL, AAL, and FAL. -->

潜在的影響カテゴリー: ユーザーの Asserted Identity の適切な Assurance Level を決定するため, 各機関は潜在リスクを評価し, その影響を最小限に抑える手段を特定する必要がある (SHALL).

<!-- Potential Impact Categories: To determine the appropriate level of assurance of the user's asserted identity, agencies SHALL assess the potential risks and identify measures to minimize their impact. -->

より悪影響が予想される Authentication, Proofing, および Federation エラーには, より高い Asssurance Level が求められる. ビジネスプロセスやポリシー, 技術などがそのリスク低減に役立つ.

<!-- Authentication, proofing, and federation errors with potentially worse consequences require higher levels of assurance. Business process, policy, and technology may help reduce risk. -->

被害と影響のカテゴリーは次のとおりである.

<!-- Categories of harm and impact include: -->

1. 不便, 苦痛, または社会的地位やレピュテーションの毀損.
2. 経済的損失または機関の負債.
3. 機関のプログラムや公共の利益への損害.
4. Authorize のないセンシティブ情報の公開.
5. 個人の安全.
6. 民事または刑事上の違反.

<!-- 1. Inconvenience, distress, or damage to standing or reputation;
2. Financial loss or agency liability;
3. Harm to agency programs or public interests;
4. Unauthorized release of sensitive information;
5. Personal safety; and
6. Civil or criminal violations. -->

Digital Transaction に要求される Assurance Level は, Federal Information Processing Standard (FIPS) 199 [[FIPS 199]](#FIPS199) が示す潜在的影響度合いを利用し, 上記カテゴリーごとの潜在的影響評価を行うことで決定できる.

<!-- Required assurance levels for digital transactions are determined by assessing the potential impact of each of the above categories using the potential impact values described in Federal Information Processing Standard (FIPS) 199 [[FIPS 199]](#FIPS199). -->

上記潜在的影響度合いには, 以下の3つの値がある.

<!-- The three potential impact values are: -->

1. 影響度 Low
2. 影響度 Moderate
3. 影響度 High

<!-- 1. Low impact,
2. Moderate impact, and
3. High impact. -->

#### 5.3.1 Business Process vs. Online Transaction

Assurance Level の決定は, Digital システムの一部をなす Transaction にのみ基づいて行われる. あるオンライン Transaction は, オフライン処理や完全にセグメント化されたシステム上でのオンライン処理を必要とする完全なビジネスプロセスとは等価でないこともありうる. 適切な Assurance Level の選択において, 当該機関は, 提供する便益やサービスに関連するビジネスプロセス全体の評価ではなく, 自身のデジタルサービスにおけるオンライン Transaction に関連するリスクの評価を行うべきである. たとえばオンラインアンケートでは Personal Information が収集されることがあるが, 当該情報が保存後に情報提供者に対してオンラインで提供されることはない. このような場合, バックエンドシステムで注意深く情報を保護することは重要だが, 情報提供者自身がシステムや関連する便益に Access するために当該ユーザーに対して Identity Proofing や Authentication を実施する必要はない. オンライン Transaction は単にデータの提出処理のみである. ビジネスプロセス全体ではかなりのデータ検証処理が必要となる可能性があるが, 正規の人物が情報を提出したかどうかを知る必要はない. このシナリオでは, Identity Proofing も Authentication も必要ではない.

<!-- The assurance level determination is only based on transactions that are part of a digital system. An online transaction may not be equivalent to a complete business process that requires offline processing, or online processing in a completely segmented system. In selecting the appropriate assurance levels, the agency should assess the risk associated with online transactions they are offering via the digital service, not the entire business process associated with the provided benefit or service. For example, in an online survey, personal information may be collected, but it is never made available online to the submitter after the information is saved. In this instance, it is important for the information to be carefully protected in backend systems, but there is no reason to identity proof or even authenticate the user providing the information for the purposes of their own access to the system or its associated benefits. The online transaction is solely a submission of the data. The entire business process may require a significant amount of data validation, without ever needing to know if the correct person submitted the information. In this scenario, there is no need for any identity proofing nor authentication. -->

機関がオンライン Transaction の要件ではなくビジネスプロセス全体を評価した場合にリスク評価が変わりうるその他の事例としては, 公開求人情報応募用の履歴書受取デジタルサービスが挙げられる. このユースケースでは, 当該デジタルサービスは個人が他人の代理で履歴書を提出することは許可する, ないしは最低でも制限はせず, その後にサイトに再訪された時にはさまざまな目的のため履歴書に Access する. 履歴書の情報は後の Session でもユーザーから利用可能であり, また Personal Information を含むため, Personal Information が Self-asserted であったとしても, 当該機関は MFA を必要とする AAL を選択する必要がある. この場合, [[EO 13681]](#EO13681) の要件が適用され, アプリケーションは AAL2 以上で提供されなければならない. しかしながら Identity Proofing 要件は依然不確定である. 履歴書を検査し最終的に雇用し新人研修を施すといったビジネスプロセス全体では, 相当の Identity Proofing が必要である. 採用決定時には, 求人情報への Applicant が実際にオンライン提出された履歴書の Subject であるという高レベルの確信が必要となる. しかしこのレベルの Proofing はオンラインでの履歴書投稿には必要ではない. Identity Proofing はデジタルな世界での Transaction を完了させるためには必要とならない. 投稿者に対して Identity Proofing を行うと, デジタル求人アプリケーションポータルによって提供される採用プロセスでの必要性を過えた Personal Information を収集することに繋がるため, 必要以上にリスクを増大させ, ユーザビリティを低下させることにつながる. 従って最も適切な IAL は1となるであろう. 当該オンライン Transaction には Identity Proofing は不要である. オンラインポータル自体に対するこの決定は, 偽の Applicant による応募を防ぐためビジネスプロセス全体で求められるであろう Identity Proofing 要件とは独立している.

<!-- Another example where the assessed risk could differ if the agency evaluated the entire business process rather than the online transaction requirements is a digital service that accepts résumés to apply for open job postings. In this use case, the digital service allows an individual to submit – or at least does not restrict an individual from submitting – a résumé on behalf of anyone else, and in subsequent visits to the site, access the résumé for various purposes. Since the résumé information is available to the user in later sessions, and is likely to contain personal information, the agency must select an AAL that requires MFA, even though the user self-asserted the personal information. In this case, the requirements of [[EO 13681]](#EO13681) apply and the application must provide at least AAL2. However, the identity proofing requirements remain unclear. The entire business process of examining a résumé and ultimately hiring and onboarding a person requires a significant amount of identity proofing. The agency needs a high level of confidence that the job applicant is in fact the subject of the résumé submitted online if a decision to hire is made. Yet this level of proofing is not required to submit the résumé online. Identity proofing is not required to complete the digital portion of the transaction successfully. Identity proofing the submitter would create more risk than required in the online system as excess personal information would be collected when no such information is needed for the portion of the hiring process served by the digital job application portal and may reduce usability. Therefore, the most appropriate IAL selection would be 1. There is no need to identity proof the user to successfully complete the online transaction. This decision for the online portal itself is independent of a seemingly obvious identity proofing requirement for the entire business process, lest a job be offered to a fraudulent applicant. -->

#### 5.3.2 Impacts per Category

本セクションでは各被害カテゴリーごとの潜在的影響を定義する. IAL, AAL, および (Federated Identity を受け入れないしは評価する場合は) FAL の各 Assurance Level は個別に評価すること (SHALL).

<!-- This section defines the potential impacts for each category of harm. Each assurance level, IAL, AAL, and FAL (if accepting or asserting a federated identity) SHALL be evaluated separately. -->

> Note: もし Identity システムのエラーがカテゴリーに測定可能な結果を及ぼさない場合, 影響はないものとする.

<!-- > Note: If an error in the identity system causes no measurable consequences for a category, there is no impact. -->

_不便, 苦痛, または社会的地位やレピュテーションの毀損に関する潜在的影響:_

<!-- _Potential impact of inconvenience, distress, or damage to standing or reputation:_     -->

- Low: 最悪でも, 任意の主体に対する, 限定的かつ短期間の不便, 苦痛, 困難.
- Moderate: 最悪でも, 任意の主体に対する, 相当かつ短期間ないしは限定的だが長期間の不便, 苦痛, 社会的地位やレピュテーションの毀損.
- High: 任意の主体に対する, 重度または重大かつ長期的な不便, 苦痛, 社会的地位やレピュテーションの毀損. これは通常, 特に重大な影響を及ぼしたり, 多くの個人に影響を及ぼす可能性のある状況を想定したレベルである.

<!-- - Low: at worst, limited, short-term inconvenience, distress, or embarrassment to any party.
- Moderate: at worst, serious short-term or limited long-term inconvenience, distress, or damage to the standing or reputation of any party.
- High: severe or serious long-term inconvenience, distress, or damage to the standing or reputation of any party. This is ordinarily reserved for situations with particularly severe effects or which potentially affect many individuals. -->

_経済的損失に関する潜在的影響:_

<!-- _Potential impact of financial loss:_ -->

- Low: 最悪でも, 任意の主体に対する, ささいで取るに足らない経済的損失ないしは機関の負債.
- Moderate: 最悪でも, 任意の主体に対する, 相当な経済的損失ないしは機関の負債.
- High: 任意の主体に対する, 重大または致命的な経済的損失ないしは機関の負債.

<!-- - Low: at worst, an insignificant or inconsequential financial loss to any party, or at worst, an insignificant or inconsequential agency liability.
- Moderate: at worst, a serious financial loss to any party, or a serious agency liability.
- High: severe or catastrophic financial loss to any party, or severe or catastrophic agency liability. -->

_機関のプログラムや公共の利益への損害に関する潜在的影響:_

<!-- _Potential impact of harm to agency programs or public interests:_ -->

- Low: 最悪でも, 組織の運用や資産, 公共の利益への限定的な悪影響. 限定的な悪影響の例としては, (i) 一定範囲および期間にわたる, 組織のミッション遂行能力の低下による組織の主たる機能の処理効率の目に見えた低下, (ii) 組織資産または公益への軽微な損害, などがある.
- Moderate: 最悪でも, 組織の運用や資産, 公共の利益への相当な悪影響. 相当な悪影響の例としては, (i) 一定範囲および期間にわたる, 組織のミッション遂行能力の著しい低下による組織の主たる機能の処理効率の著しい低下, (ii) 組織資産または公益への著しい損害, などがある.
- High: 組織の運用や資産, 公共の利益への重大または致命的な悪影響. 重大または致命的な悪影響の例としては, (i) 一定範囲および期間にわたる, 組織のミッション遂行能力の重大な低下や喪失による組織の主たる機能の処理不能, (ii) 組織資産または公益への深刻な損害, などがある.

<!-- - Low: at worst, a limited adverse effect on organizational operations or assets, or public interests. Examples of limited adverse effects are: (i) mission capability degradation to the extent and duration that the organization is able to perform its primary functions with noticeably reduced effectiveness, or (ii) minor damage to organizational assets or public interests.
- Moderate: at worst, a serious adverse effect on organizational operations or assets, or public interests. Examples of serious adverse effects are: (i) significant mission capability degradation to the extent and duration that the organization is able to perform its primary functions with significantly reduced effectiveness; or (ii) significant damage to organizational assets or public interests.
- High: a severe or catastrophic adverse effect on organizational operations or assets, or public interests. Examples of severe or catastrophic effects are: (i) severe mission capability degradation or loss of to the extent and duration that the organization is unable to perform one or more of its primary functions; or (ii) major damage to organizational assets or public interests. -->


_Authorize のないセンシティブ情報の公開に関する潜在的影響:_

<!-- _Potential impact of unauthorized release of sensitive information:_ -->

- Low: 最悪でも, FIPS 199 で定義された低インパクトの Confidentiality (機密性) 喪失をもたらす, Authorize されていない主体に対する限定的な Personal Information, U.S. 政府にとってないしは商業的にセンシティブな情報の公開.
- Moderate: 最悪でも, FIPS 199 で定義された中インパクトの Confidentiality (機密性) 喪失をもたらす, Authorize されていない主体に対する限定的な Personal Information, U.S. 政府にとってないしは商業的にセンシティブな情報の公開.
- High: FIPS 199 で定義された高インパクトの Confidentiality (機密性) 喪失をもたらす, Authorize されていない主体に対する限定的な Personal Information, U.S. 政府にとってないしは商業的にセンシティブな情報の公開.

<!-- - Low: at worst, a limited release of personal, U.S. government sensitive, or commercially sensitive information to unauthorized parties resulting in a loss of confidentiality with a low impact as defined in FIPS 199.
- Moderate: at worst, a release of personal, U.S. government sensitive, or commercially sensitive information to unauthorized parties resulting in loss of confidentiality with a moderate impact as defined in FIPS 199.
- High: a release of personal, U.S. government sensitive, or commercially sensitive information to unauthorized parties resulting in loss of confidentiality with a high impact as defined in FIPS 199. -->

_個人の安全に関する潜在的影響:_

<!-- _Potential impact to personal safety:_ -->

- Low: 最悪でも, 治療を必要としない軽傷.
- Moderate: 最悪でも, 軽傷に関する中程度のリスク, ないしは治療を必要とする怪我に関する限定的リスク.
- High: 重大な傷害または死亡に関するリスク.

<!-- - Low: at worst, minor injury not requiring medical treatment.
- Moderate: at worst, moderate risk of minor injury or limited risk of injury requiring medical treatment.
- High: a risk of serious injury or death. -->

_民事または刑事上の違反に関する潜在的影響:_

<!-- _The potential impact of civil or criminal violations is:_ -->

- Low: 最悪でも, 通常は執行努力の対象とはならない種類の民事または刑事上の違反のリスク.
- Moderate: 最悪でも, 執行努力の対象とりうる民事または刑事上の違反のリスク.
- High: 執行プログラムにとって特に重要な民事または刑事上の違反のリスク

<!-- - Low: at worst, a risk of civil or criminal violations of a nature that would not ordinarily be subject to enforcement efforts.
- Moderate: at worst, a risk of civil or criminal violations that may be subject to enforcement efforts.
- High: a risk of civil or criminal violations that are of special importance to enforcement programs. -->

### 5.4 Risk Acceptance and Compensating Controls

SP 800-63 スイートは Assurance Level に基づき Digital Identity サービスに対する基本要件を示す. 各機関は本ガイドライン群の要件に従って Identity サービスを実装すべきであり (SHOULD), さらにシステムをセキュアにしたりプライバシーを強化するべく追加の技法や技術を検討すべきである (SHOULD).

<!-- The SP 800-63 suite specifies baseline requirements for digital identity services based on assurance level. Agencies SHOULD implement identity services per the requirements in these guidelines and SHOULD consider additional techniques and technologies to further secure and privacy-enhance their services. -->

各機関は, ミッション, リスク許容範囲, 既存のビジネスプロセス, 特定の人々への特別な考慮事項, 本スイートに記載されているものと同様の緩和策を実現するためのデータの可用性, 当該組織固有のその他の能力などに基づき, 評価された xALs に対して NIST 推奨ガイダンス代替策を講じてもよい (MAY).

<!-- Agencies MAY determine alternatives to the NIST-recommended guidance, for the assessed xALs, based on their mission, risk tolerance, existing business processes, special considerations for certain populations, availability of data that provides similar mitigations to those described in this suite, or due to other capabilities that are unique to the agency. -->

適用可能な SP 800-63 要件が完全には実装されていない場合, 各機関は任意の代替策の比較可能性を示さなければならない (SHALL). 例えば, National Information Assurance Partnership (NIAP) 保護プロファイルが FIPS 要件と同等もしくはより強固である場合, 当該機関は FIPS の代わりに National Information Assurance Partnership (NIAP) 保護プロファイルを選択してもよい. 機関は機関自身の能力に基づいて評価済 xAL を変更してはならないが (SHALL NOT), SP 800-63 に明記されていない手段によりリスクを低減する能力に基づいて自身のソリューションの実装を調整することは可能である (MAY). 機関は Normative 要件から逸脱する正当な理由と, 自身が採用する代替策の詳細をドキュメント化するべく手順化しなければならない (SHALL).

<!-- Agencies SHALL demonstrate comparability of any chosen alternative, to include any compensating controls, when the complete set of applicable SP 800-63 requirements is not implemented. For example, an agency may choose a National Information Assurance Partnership (NIAP) protection profile over FIPS, where the profile is equivalent to or stronger than the FIPS requirements. That said, agencies SHALL NOT alter the assessed xAL based on agency capabilities. Rather, the agency MAY adjust their implementation of solutions based on the agency's ability to mitigate risk via means not explicitly addressed by SP 800-63 requirements. The agency SHALL implement procedures to document both the justification for any departure from normative requirements and detail the compensating control(s) employed. -->

本ガイダンスは Authentication と Identity Proofing エラーに関するリスクのみを扱う. NIST Special Publication 800-30 Risk Management Guide for Information Technology Systems [[SP 800-30]](#SP800-30) は, 政府システムにおいてリスクを管理する一般的方法論を推奨している.

<!-- This guidance addresses only those risks associated with authentication and identity proofing errors. NIST Special Publication 800-30, Risk Management Guide for Information Technology Systems [[SP 800-30]](#SP800-30) recommends a general methodology for managing risk in federal systems. -->

### <a name="daps"></a> 5.5 Digital Identity Acceptance Statement

各機関は SA＆A を達成するために必要な既存の成果物にこの情報を含めるべきである (SHOULD).

<!-- Agencies SHOULD include this information in existing artifacts required to achieve a SA&A. -->

このステートメントには, 最低限以下の情報を含めること (SHALL).

<!-- The statement SHALL include, at a minimum: -->

1. 評価済 xAL.
2. 実装済 xAL.
3. 実装済 xAL が評価済 xAL と異なる場合は, その根拠.
4. 適用可能な 800-63 要件が完全には実装されていない場合, 代替策の比較可能性.
5. Federated Identity を採用していない場合は, その根拠.

<!-- 1. Assessed xAL,
2. Implemented xAL,
3. Rationale, if implemented xAL differs from assessed xAL,
4. Comparability demonstration of compensating controls when the complete set of applicable 800-63 requirements are not implemented, and
5. If not accepting federated identities, rationale. -->

### 5.6 Migrating Identities

本ガイドライン群は改訂され要件にも変更が起こるため, CSP はそれが自身のユーザーに与える影響を考慮しなければならない (SHALL). ユーザーに影響がない場合もあるが, ユーザーに移行手続を要求することもあるでしょう. 例えば, 改訂後の最初のログイン時に, CSP は新しい IAL 要件を遵守すべくユーザーに追加の身元確認書類を要求するかもしれません. これは CSP, 当該 CSP を利用する RP, ミッション, 対象ユーザーといったコンテキストを考慮して, リスクに基づいて決定すること (SHALL). 以下の考慮点は, 機関が要件変更の影響を考慮する場合の向けのガイドである.

<!-- As these guidelines are revised, CSPs SHALL consider how changes in requirements affect their user population. In some instances, the user population will be unaffected, yet in others, the CSP will require users undergo a transitional activity. For example, CSPs may request users &mdash; upon initial logon since last revision &mdash; to supply additional proofing evidence to adhere to new IAL requirements. This SHALL be a risk-based decision, made in context of the CSP, any RPs that use the CSP, mission, and the population served. The following considerations serve only as a guide to agencies when considering the impacts of requirements changes: -->

1. RP で Identity 関連の詐欺が発生している場合は, 移行が有益である可能性がある. そうでなければ移行には価値がないかもしれない.
2. 新しくより強固ないしはよりユーザーフレンドリーな Authentication の選択肢が個々の AAL に追加されれば, CSP は新しい Authenticator を発行したり, ユーザーがすでに持っている Authenticator を登録させることが可能になる.
3. Federation 要件はユーザー影響があるかもしれないしないかもしれない. 例えば, 同意要件やインフラストラクチャー要件により, インフラストラクチャーやプロトコルのアップグレードが必要になることもある.
4. xAL の追加や削除は移行を必要としないかもしれないが, RP 側での変更が必要かどうかを決定すべく新規に Risk Assessment を行うことになるであろう.

<!-- 1. If the RP is experiencing identity-related fraud, a migration may prove beneficial. If not, migration may not be an added value.
2. New, stronger, or user-friendly authentication options are added to individual AALs the CSP could issue new authenticators or allow users to register authenticators they already have.
3. Federation requirements may or may not have a user impact. For example, consent requirements or infrastructure requirements could necessitate an infrastructure or protocol upgrade.
4. Addition or removal of xALs may not require a migration, but would trigger a new risk assessment to determine if a change is necessary for the RP. -->

本ガイダンスでは, 必ずしも移行を行う必要があるとはしておらず, 改訂版がリリースされた時点で考慮が必要であることのみを定めている. 両者のリスク許容範囲とミッションに基づいた最良のアプローチの決定は, CSP と RP の判断に委ねられる.

<!-- The guidance does not prescribe that any migration needs to occur, only that it be considered as revisions are released. It is up to the CSP and RP, based on their risk tolerance and mission, to determine the best approach. -->
