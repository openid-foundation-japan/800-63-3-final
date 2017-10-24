<a name="sec4"></a>

<div class="breaker"></div>

## <a name="ial-section"></a> 4 Identity Assurance Level Requirements

_This section contains both normative and informative material._

本ドキュメントは, Applicant に対する Identity Proofing および Enrollment プロセスによって, Identity Evidence と Attribute の収集が行われ, ある集団ないしはコンテキストの中でユニークかつ単一の Identity として識別可能になり, 確認および検証が行われるまでの, 共通のパターンについて記述する. 最適な IAL の選択については [SP 800-63-3](sp800-63-3.html) Section 6.1 を参照のこと. CSP はこういった Attribute を Authenticator に紐づけるかもしれない ([SP 800-63B](sp800-63b.html) 参照).

<!-- This document describes the common pattern in which an applicant undergoes an identity proofing and enrollment process whereby their identity evidence and attributes are collected, uniquely resolved to a single identity within a given population or context, then validated and verified. See [SP 800-63-3](sp800-63-3.html) Section 6.1 for details on how to choose the most appropriate IAL. A CSP may then bind these attributes to an authenticator (described in [SP 800-63B](sp800-63b.html)). -->

Identity Proofing の唯一の目的は, あらかじめ定められた確実性でもって, Applicant が彼ら自身が主張するものであることを保証することである. このプロセスにおいては, Identity Proofing を達成するために必要最小限の Attribute の提示, 確認, 検証が行われる. 必要最小限といっても多様な組み合わせがあり得るため, CSP はプライバシーとユーザーが必要とするユーザビリティーのバランスを取りつつ, および将来 Digital Identity を利用する際に必要となるであろう Attribute を考慮した上で, 必要最小限の組み合わせを選択するべきである. 例えば, 必要最小限な Attribute の例として, 以下のような組み合わせが考えられる.

<!-- Identity proofing's sole objective is to ensure the applicant is who they claim to be to a stated level of certitude. This includes presentation, validation, and verification of the minimum attributes necessary to accomplish identity proofing.  There may be many different sets that suffice as the minimum, so CSPs should choose this set to balance privacy and the user's usability needs, as well as the likely attributes needed in future uses of the digital identity. For example, such attributes &mdash; to the extent they are the minimum necessary &mdash; could include: -->

1. Full name
2. Date of birth
3. Home address

また本ドキュメントは, Identity Proofing 以外の目的で利用される追加情報を収集する際の CSP に対する要件も示している.

<!-- This document also provides requirements for CSPs collecting additional information used for purposes other than identity proofing. -->

### 4.1 Process Flow

_This section is normative._

[Figure 4-1](#63aSec4-Figure1) は Identity Proofing および Enrollment の基本的な流れを概観したものである.

<!-- [Figure 4-1](#63aSec4-Figure1) outlines the basic flow for identity proofing and enrollment. -->

<a name="63aSec4-Figure1"></a>

<div class="text-center" markdown="1">
<img src="sp800-63a/media/ProofingProcess.png" alt="Identity Proofing Process" style="width:1074px;height:496px;;min-width: 1074px;min-height: 496px;"/>

**Figure 4-1 The Identity Proofing User Journey**
</div>

以下では, Identity Proofing プロセス中において CSP と Applicant がどのようにインタラクションを行うかを例示する.

<!-- The following provides a sample of how a CSP and an applicant interact during the identity proofing process: -->

<div class="text-left" markdown="0">

<ol type="1" start="1">
  <li><strong>Resolution</strong></li>
    <ol type="a" start="a">
      <li>CSP が Applicant から名前, 住所, 誕生日, Email, 電話番号などの PII を収集する.</li>
      <li>さらに CSP は, 運転免許証とパスポートなど, 2種類の Identity Evidence を収集する. 例えば CSP は, ラップトップのカメラを使って, 両 Identity Evidence の裏表の写真をキャプチャーすることができる.</li>
    </ol>
  <li><strong>Validation</strong></li>
    <ol type="a" start="a">
      <li>CSP は Authoritative Source に照会を行い 1a で提供された情報を確認する. CSP は Applicant が提出した情報が彼らのレコードとマッチすることを確認する.</li>
      <li>CSP は免許証とパスポートの画像をチェックし, 修正などされておらず, QR コードにエンコードされているデータが平文の情報とマッチし, 識別番号が標準フォーマットに従っていることを確認する.</li>
      <li>CSP は免許証とパスポートの Issuing Source に照会をかけ, 情報がマッチすることを確認する.</li>
    </ol>
  <li><strong>Verification</strong></li>
    <ol type="a" start="a">
      <li>CSP は Applicant に免許書とパスポートにマッチする彼ら自身の写真を要求する.</li>
      <li>CSP は免許書とパスポートにある写真を Applicant の写真と比較し, 両者がマッチすることを確認する.</li>
      <li>CSP は Enrollment コードを Applicant の確認済電話番号に送信し, ユーザーはその Enrollment コードを CSP に提示する. CSP は両者がマッチすることを確認し, 当該ユーザーが検証済電話番号を管理下においていることを検証する.</li>
      <li>Applicant は Proofing に成功する.</li>
    </ol>
</ol>

<!--
<ol type="1" start="1">
  <li><strong>Resolution</strong></li>
    <ol type="a" start="a">
      <li>The CSP collects PII from the applicant, such as name, address, date of birth, email, and phone number.</li>
      <li>The CSP also collects two forms of identity evidence, such as a driver's license and a passport. For example, using the camera of a laptop, the CSP can capture a photo of both sides of both pieces of identity evidence.</li>
    </ol>
  <li><strong>Validation</strong></li>
      <ol type="a" start="a">
      <li>The CSP validates the information supplied in 1i by checking an authoritative source. The CSP determines the information supplied by the applicant matches their records.</li>
      <li>The CSP checks the images of the license and the passport, determines there are no alterations, the data encoded in the QR codes matches the plain-text information, and that the identification numbers follow standard formats.</li>
      <li>The CSP queries the issuing sources for the license and passport and validates the information matches.</li>
    </ol>
  <li><strong>Verification</strong></li>
    <ol type="a" start="a">
      <li>The CSP asks the applicant for a photo of themselves to match to the license and passport.</li>
      <li>The CSP matches the pictures on the license and the passport to the applicant picture and determines they match.</li>
      <li>The CSP sends an enrollment code to the validated phone number of the applicant, the user provides the enrollment code to the CSP, and the CSP confirms they match, verifying the user is in possession and control of the validated phone number.</li>
      <li>The applicant has been successfully proofed.</li>
    </ol>
</ol>
-->

</div>

> Note: Identity Proofing プロセスは複数のサービスプロバイダーによって行われうる. 単一の組織やプロセス, テクニックやテクノロジーがこのプロセスの各ステップを実行することが可能であるが, そのような想定をするものではない.

<!-- > Note: The identity proofing process can be delivered by multiple service providers. It is possible, but not expected, that a single organization, process, technique, or technology will fulfill these process steps. -->


### <a name="genProofReqs"></a> 4.2 General Requirements

IAL2 ないしは IAL3 で Identity Proofing を行う CSP には, 以下の要件が課せられる.

<!-- The following requirements apply to any CSP performing identity proofing at IAL2 or IAL3. -->

<div class="text-left" markdown="0">
  <ol type="1" start="1">
    <li>Identity Proofing は, サービスまたはメリットに Access するための適格性や資格を決定するために実施してはならない (SHALL NOT).</li>
    <li><a name="4.2-r2"></a>PII の収集は, Claimed Identity の存在確認, および Identity Resolution, Validation, Verification のために Identity Evidence を提示している Applicant と Claimed Identity との関連づけに必要最小限な程度に制限すること (SHALL). この PII には, Identity Evidence を Authoritative Source と関連づける Attribute や, RP が Authorization の決定を行うために利用する Attribute を含みうる (MAY).</li>
    <li><a name="4.2-r3"></a>CSP は, 収集時に Applicaint に明示的な通知を行い, Identity Proofing に必要な Attribute の収集・記録管理の目的を知らせなければならない (SHALL). これには, Identity Proofing プロセスを完了するためにどの Attribute が任意でありどの Attribute が必須であるかや, Attribute を提供しない場合の影響といった情報を含む.</li>
    <li><a name="4.2-r4"></a>CSP は, Identity Proofing プロセスにおいて収集・管理することとなった Attribute を, CSP が明確な通知を行い Subscriber からの同意を得た場合を除き, Identity Proofing, Authentication, Attribute Assertion, 法律や法的プロセスに従う以外の目的で利用してはならない (SHALL NOT). CSP はこういった追加の目的をサービス提供条件としてはならない (SHALL NOT).</li>
    <li><a name="4.2-r5"></a>CSP は, Identity Proofing を起因とする Applicant からの苦情や問題の是正のためのメカニズムを提供しなければならない (SHALL). また CSP は, そのメカニズムによって苦情や問題の解決が有効になされているか, 評価しなければならない (SHALL).</li>
    <li><a name="4.2-r6"></a>Identity Proofing と Enrollmet プロセスは, 適用可能な書面によるポリシー, または Identity を検証するための特定の手続きを規定する <i>practice statement</i> に従って行うこととする (SHALL). <i>practice statement</i> は, CSP がどのように Applicant の登録失敗につながるような Proofing エラーを取り扱うかを詳説する制御情報を含むこと (SHALL). これには例えば, 許容されるリトライ回数, 代替の Proofing 方法 (e.g., Remote が失敗した場合は対面), 異常検知時の不正対策などが含まれる.</li>
    <li><a name="4.2-r7"></a>CSP は, 監査ログを含む Applicant の Identity を検証する際のすべての手続きの記録を管理するものとし (SHALL), Proofing プロセスにおいて提示された Identity Evidence のタイプを記録するものとする (SHALL). CSL は, プライバシーおよびセキュリティーに関する Risk Assessment を含む Risk Management プロセスを実施し, 以下の項目を定めること.</li>
      <ol type="a" start="a">
        <li>ここで指定された必須要件を超えて, Applicant の Identity を検証するために必要なステップ.</li>
        <li>Biometrics, 画像, スキャン, その他 Identity Evidence のコピーを含む PII. CSP はこれらを Identity Proofing の記録として管理することになる. (Note: 特別な連邦政府要件が課せられることもある)</li>
        <li>これらの記録の保持スケジュール. (Note: CSP には, 適用可能な National Archives and Records Administration (NARA) 記録保持スケジュールを含む, 適用可能な法律, 規則, ポリシーに従って, 特定の保持ポリシーが課せられることもある)</li>
      </ol>
    <li><a name="4.2-r8"></a>Enrollmet プロセスにおいて収集されたすべての PII は, Confidentiality (機密性), Integrity (完全性), 情報源の帰属を保証するよう保護すること (SHALL).</li>
    <li><a name="4.2-r9"></a>第三者が関与する Transaction を含み, Proofing Transaction 全体を Authenticated Protected Channel 上で実行すること (SHALL).</li>
    <li><a name="4.2-r10"></a>CSP は, 追加の対策がここで規定される必須要件に代わるものでない限り, 不正防止策 (e.g., ジオロケーションの検査, Applicant のデバイス特性の調査, 行動特性の評価, Death Master File <a href="sp800-63a.html#dmf">[DMF]</a> などのバイタル統計レポジトリーのチェック) を用いて Identity Proofing の信頼性を向上させるべきである (SHOULD). CSP が不正防止策を行う場合, CSP はこれらの防止策に関してプライバシー Risk Assessment を行うこと (SHALL). こういったアセスメントには, プライバシーリスク軽減策 (e.g., リスクの受容や転嫁, 制限付き保持, 使用制限, 通知), その他の技術的対策 (e.g., 暗号化), 上記 4.2(7) に記載された対策などが含まれる.</li>
    <li><a name="4.2-r11"></a>CSP が Identity Proogin および Enrollment プロセスを終える場合, CSP は PII は PII を含むセンシティブデータの完全な廃棄または破棄, または保持期間中の Unauthorized な Access からの保護を行う責任を持つ (SHALL).</li>
    <li><a name="4.2-r12"></a>CSP が政府機関か民間のプロバイダーかに関わらず, Proofing サービスを提供したり利用するには以下の要件が適用される.</li>
      <ol type="a" start="a">
        <li>機関は, Senior Agency Official for Privacy (SAOP) と協議し, Identity Proofing を実施するための PII 収集において Privacy Act 要件が適用されるかどうか判断するための分析を行うこと (SHALL).</li>
        <li>機関は, 該当する場合は System of Records Notice (SORN) を公開し, そういった収集について記載すること.</li>
        <li>機関は, SAOP と協議し, Identity Proofing を実施するための PII 収集において E-Government Act of 2002 要件が適用されるかどうか判断するための分析を行うこと (SHALL).</li>
        <li>機関は, 該当する場合は Privacy Impact Assessment (PIA) を公開し, そういった収集について記載すること.</li>
      </ol>
    <li><a name="4.2-r13"></a>CSP は, Identity Resolution に必要でない限り, また Identity Resolution がその他の Attribute または Attribute の組み合わせによって実現不可能でない限り, Social Security Number (SSN) を収集すべきではない (SHOULD NOT).</li>
  </ol>
</div>

<!--
<div class="text-left" markdown="0">
  <ol type="1" start="1">
    <li>Identity proofing SHALL NOT be performed to determine suitability or entitlement to gain access to services or benefits.</li>
    <li><a name="4.2-r2"></a>Collection of PII SHALL be limited to the minimum necessary to validate the existence of the claimed identity and associate the claimed identity with the applicant providing identity evidence for appropriate identity resolution, validation, and verification. This MAY include attributes that correlate identity evidence to authoritative sources and to provide RPs with attributes used to make authorization decisions.</li>
    <li><a name="4.2-r3"></a>The CSP SHALL provide explicit notice to the applicant at the time of collection regarding the purpose for collecting and maintaining a record of the attributes necessary for identity proofing, including whether such attributes are voluntary or mandatory to complete the identity proofing process, and the consequences for not providing the attributes.
    </li>
    <li><a name="4.2-r4"></a>The CSP SHALL NOT use attributes collected and maintained in the identity proofing process for any purpose other than identity proofing, authentication, or attribute assertions, or to comply with law or legal process unless the CSP provides clear notice and obtains consent from the subscriber for additional uses. CSPs SHALL NOT make consent with these additional purposes a condition of the service.</li>
    <li><a name="4.2-r5"></a>The CSP SHALL provide mechanisms for redress of applicant complaints or problems arising from the identity proofing. These mechanisms SHALL be easy for applicants to find and use. The CSP SHALL assess the mechanisms for their efficacy in achieving resolution of complaints or problems.</li>
    <li><a name="4.2-r6"></a>The identity proofing and enrollment processes SHALL be performed according to an applicable written policy or *practice statement* that specifies the particular steps taken to verify identities. The *practice statement* SHALL include control information detailing how the CSP handles proofing errors that result in an applicant not being successfully enrolled. For example, the number of retries allowed, proofing alternatives (e.g., in-person if remote fails), or fraud counter-measures when anomalies are detected.</li>
    <li><a name="4.2-r7"></a>The CSP SHALL maintain a record, including audit logs, of all steps taken to verify the identity of the applicant and SHALL record the types of identity evidence presented in the proofing process. The CSP SHALL conduct a risk management process, including assessments of privacy and security risks to determine:</li>
      <ol type="a" start="a">
        <li>Any steps that it will take to verify the identity of the applicant beyond any mandatory requirements specified herein;</li>
        <li>The PII, including any biometrics, images, scans, or other copies of the identity evidence that the CSP will maintain as a record of identity proofing (Note: Specific federal requirements may apply.); and</li>
        <li>The schedule of retention for these records (Note: CSPs may be subject to specific retention policies in accordance with applicable laws, regulations, or policies, including any National Archives and Records Administration (NARA) records retention schedules that may apply).</li>
      </ol>
    <li><a name="4.2-r8"></a>All PII collected as part of the enrollment process SHALL be protected to ensure confidentiality, integrity, and attribution of the information source.</li>
    <li><a name="4.2-r9"></a>The entire proofing transaction, including transactions that involve a third party, SHALL occur over an authenticated protected channel.</li>
    <li><a name="4.2-r10"></a>The CSP SHOULD obtain additional confidence in identity proofing using fraud mitigation measures (e.g., inspecting geolocation, examining the device characteristics of the applicant, evaluating behavioral characteristics, checking vital statistic repositories such as the Death Master File <a href="sp800-63a.html#dmf">[DMF]</a>, so long as any additional mitigations do not substitute for the mandatory requirements contained herein. In the event the CSP uses fraud mitigation measures, the CSP SHALL conduct a privacy risk assessment for these mitigation measures. Such assessments SHALL include any privacy risk mitigations (e.g., risk acceptance or transfer, limited retention, use limitations, notice) or other technological mitigations (e.g., cryptography), and be documented per requirement 4.2(7) above.</li>
    <li><a name="4.2-r11"></a>In the event a CSP ceases to conduct identity proofing and enrollment processes, the CSP SHALL be responsible for fully disposing of or destroying any sensitive data including PII, or its protection from unauthorized access for the duration of retention.</li>
    <li><a name="4.2-r12"></a>Regardless of whether the CSP is an agency or private sector provider, the following requirements apply to the agency offering or using the proofing service:</li>
      <ol type="a" start="a">
        <li>The agency SHALL consult with their Senior Agency Official for Privacy (SAOP) to conduct an analysis determining whether the collection of PII to conduct identity proofing triggers Privacy Act requirements.</li>
        <li>The agency SHALL publish a System of Records Notice (SORN) to cover such collection, as applicable.</li>
        <li>The agency SHALL consult with their SAOP to conduct an analysis determining whether the collection of PII to conduct identity proofing triggers E-Government Act of 2002 requirements.</li>
        <li>The agency SHALL publish a Privacy Impact Assessment (PIA) to cover such collection, as applicable.</li>
      </ol>
    <li><a name="4.2-r13"></a>The CSP SHOULD NOT collect the Social Security Number (SSN) unless it is necessary for performing identity resolution, and identity resolution cannot be accomplished by collection of another attribute or combination of attributes.</li>
  </ol>
</div>
-->

### 4.3 Identity Assurance Level 1

_This section is normative._

1. IAL1 のみをサポートする CSP は Attribute を確認したり検証してはならない (SHALL NOT).
2. CSP はサービス提供のために Applicant に0個以上の Self-asserted Attribute を要求してもよい (MAY).
3. IAL2 や IAL3 の CSP は, ユーザーの同意があれば, IAL1 を必要とする RP をサポートすべきである (SHOULD).

<!--
1. A CSP that supports only IAL1 CSP SHALL NOT validate and verify attributes.
2. The CSP MAY request zero or more self-asserted attributes from the applicant to support their service offering.
3. An IAL2 or IAL3 CSP SHOULD support RPs that only require IAL1, if the user consents.
-->

### 4.4 Identity Assurance Level 2

_This section is normative._

IAL2 では **Remote** および **In-person** (対面) での Identity Proofing を許可している. IAL2 は, より多くのユーザーに選択され, フォルスネガティブ (Identity Proofing を通過できない正当な Applicant) を削減し, 悪意ある Applicant による不正な Identity の提示を可能な限り検出するため, 広範囲の受け入れ可能な Identity Proofing テクニックをサポートする.

<!-- IAL2 allows for **remote** or **in-person** identity proofing. IAL2 supports a wide range of acceptable identity proofing techniques in order to increase user adoption, decrease false negatives (legitimate applicants that cannot successfully complete identity proofing), and detect to the best extent possible the presentation of fraudulent identities by a malicious applicant. -->

CSP は [Section 4.4.1](#normal) ないしは [Section 4.4.2](#referee) の要件に従って Proofing を行わなければならない (SHALL). CSP は [Section 4.4.1](#normal) に従って Identity Proofing を実装すべきである (SHOULD). CSP がサービスを提供する対象によっては, CSP は [Section 4.4.2](#referee) に従って Identity Proofing を実装してもよい (MAY).

<!-- A CSP SHALL proof according to the requirements in [Section 4.4.1](#normal) or [Section 4.4.2](#referee). A CSP SHOULD implement identity proofing in accordance with [Section 4.4.1](#normal). Depending on the population the CSP serves, the CSP MAY implement identity proofing in accordance with [Section 4.4.2](#referee). -->

#### <a name="normal"></a>4.4.1 IAL2 Conventional Proofing Requirements

#### 4.4.1.1 Resolution Requirements

PII の収集は, 所与のコンテキストにおいてある Identity をユニークに識別可能にするために必要最低限な範囲に限定すること (SHALL). これにはデータの照会の助けとなるような Attribute の収集を含んでも良い (MAY). 一般的な Resolution 要件は [Section 5.1](#resolve) を参照のこと.

<!-- Collection of PII SHALL be limited to the minimum necessary to resolve to a unique identity in a given context. This MAY include the collection of attributes that assist in data queries. See [Section 5.1](#resolve) for general resolution requirements. -->

#### 4.4.1.2 Evidence Collection Requirements

CSP は以下を Applicant から収集すること (SHALL).

<!-- The CSP SHALL collect the following from the applicant: -->

1. **もし** エビデンスの Issuing Source が, 発行時の Identity Proofing イベントにおいて, SUPERIOR あるいは STRONG なエビデンスを2つ以上利用して Claimed Identity の確認を行っており, **かつ** CSP が直接 Issuing Source との間でそのエビデンスを確認したのであれば, そのようなプロセスを経て発行された SUPERIOR ないしは STRONG なエビデンスを1つ. **もしくは**
2. STRONG なエビデンスを2つ. **もしくは**
3. STRONG なエビデンスを1つと FAIR なエビデンスを2つ.

<!--
1. One piece of SUPERIOR or STRONG evidence **if** the evidence's issuing source, during its identity proofing event, confirmed the claimed identity by collecting two or more forms of SUPERIOR or STRONG evidence **and** the CSP validates the evidence directly with the issuing source; **OR**
2. Two pieces of STRONG evidence; **OR**
3. One piece of STRONG evidence plus two pieces of FAIR evidence.
-->

受け入れ可能な Identity Evidence についての詳細は [Section 5.2.1 Identity Evidence Quality Requirements](#evidence-quality) を参照のこと.

<!-- See [Section 5.2.1 Identity Evidence Quality Requirements](#evidence-quality) for more information on acceptable identity evidence. -->

#### <a name="4-4-1-3"></a>4.4.1.3 Validation Requirements

CSP は Identity Evidence を以下のように確認すること (SHALL).

<!-- The CSP SHALL validate identity evidence as follows: -->

それぞれのエビデンスは, 提示されたエビデンスと同じ強度のプロセスによって確認すること (SHALL). 例えば2つの STRONG な Identity Evidence が提示された場合は, それぞれを STRONG な強度で確認することとなる.

<!-- Each piece of evidence SHALL be validated with a process that can achieve the same strength as the evidence presented. For example, if two forms of STRONG identity evidence are presented, each piece of evidence will be validated at a strength of STRONG. -->

Identity Evidence の確認についての詳細は [Section 5.2.2 Validating Identity Evidence](#evidence_validation) を参照のこと.

<!-- See [Section 5.2.2 Validating Identity Evidence](#evidence_validation) for more information on validating identity evidence. -->

#### 4.4.1.4 Verification Requirements

CSP は Identity Evidence を以下のように検証すること.

<!-- The CSP SHALL verify identity evidence as follows: -->

1. 最低限, Applicant と Identity Evidence の紐付けは, 強度 STRONG を達成できるプロセスによって検証しなければならない.
2. Knowledge-Based Verification (KBV) は対面 (物理的ないしは監視下における Remote) の Identity 検証のために利用してはならない (SHALL NOT).

<!--
1. At a minimum, the applicant's binding to identity evidence must be verified by a process that is able to achieve a strength of STRONG.
2. Knowledge-based verification (KBV) SHALL NOT be used for in-person (physical or supervised remote) identity verification.
-->

Identity Evidence の検証についての詳細は [Section 5.2.2 Validating Identity Evidence](#evidence_validation) を参照のこと.

<!-- NOTE: 多分原文が間違ってコピペしてる. -->
<!-- See [Section 5.3 Identity Verification](#verify) for more information on acceptable identity evidence. -->

#### 4.4.1.5 Presence Requirements

CSP は対面ないしは Remote での Identity Proofing をサポートすること (SHALL). CSP は両方を提供すべきである (SHOULD).

<!-- The CSP SHALL support in-person or remote identity proofing. The CSP SHOULD offer both in-person and remote proofing. -->

#### <a name="4-4-1-6"></a> 4.4.1.6 Address Confirmation

<div class="text-left" markdown="0">

<ol type="1" start="1">
  <li>有効な住所確認用のレコードは, Issuing Source ないしは Authoritative Source によるものでなければならない.</li>
  <li>CSP は Address of Record を確認しなければならない (SHALL). CSP は, 提示された有効な Identity Evidence のいずれかに記載された住所の確認を通じて, Address of Record の確認を行うべきである (SHOULD). CSP は, Applicant が提供した, いかなる有効な Identity Evidence にも記載されていない情報の確認を通じて, Address of Record の確認を行ってもよい (MAY).</li>
  <li>記録時に未確認な Self-asserted の住所データは, 確認に用いてはならない (SHALL NOT).</li>
  <li><strong>CSP が対面 での Proofing (物理的ないしは監視下における Remote) を行う場合は</strong></li>
    <ol type="a" start="a">
      <li>CSP は確認された Address of Record に対して Proofing の通知を送るべきである (SHOULD).</li>
      <li>Subscriber と Authenticator の紐付けが後日発生する場合は, CSP は Enrollment コードを直接 Subscriber に提示してもよい (MAY).</li>
      <li>Enrollment コードは最大7日間まで有効なものとする (SHALL).</li>
    </ol>
  <li><strong>CSP が Remote の Proofing (非監視下) を行う場合</strong></li>
    <ol type="a" start="a">
      <li>CSP は確認された Applicant の Address of Record に Enrollment コードを送信しなければならない (SHALL).</li>
      <li>Applicant は Identity Proofing プロセスを完了するために有効な Enrollment コードを提示しなければならない (SHALL)</li>
      <li>CSP はレコード中の確認済郵便住所に Enrollment コードを送信すべきである (SHOULD). CSP は, 確認済であれば, 携帯電話 (SMS ないしは音声), 固定電話, Email に Enrollment コードを送信してもよい (MAY).</li>
      <li>Enrollment コードが Authentication Factor としての用途も兼ねている場合は, 一度利用されたものはリセットすること (SHALL).</li>
      <li>郵便住所に送信された Enrollment コードは最大10日間まで有効なものとする (SHALL). ただし郵送先住所が United States と地続きでない場所の場合, 例外的に30日間まで有効期間を延長してもよい (MAY). 電話で送信された Enrollment コードは最大10分間まで有効なものとする (SHALL). Email で送信された Enrollment コードは最大24時間まで有効なものとする (SHALL).</li>
      <li>CSP は, Enrollment コードと Proofing の通知を, それぞれ異なる Address of Record に送信するよう保証すること (SHALL). 例えば, もし CSP が Enrollment コードを確認済の電話番号に送ったとすれば, Proofing 通知は, 確認済の郵便住所や, 確認および検証済みの運転免許証のようなエビデンスに記載された郵便住所に送ることになろう.</li>
    </ol>
</ol>

<!--
<ol type="1" start="1">
  <li>Valid records to confirm address SHALL be issuing source(s) or authoritative source(s).</li>
  <li>The CSP SHALL confirm address of record. The CSP SHOULD confirm address of record through validation of the address contained on any supplied, valid piece of identity evidence. The CSP MAY confirm address of record by validating information supplied by the applicant that is not contained on any supplied piece of identity evidence.</li>
  <li>Self-asserted address data that has not been confirmed in records SHALL NOT be used for confirmation.</li>
  <li><strong>If CSP performs in-person proofing (physical or supervised remote):</strong></li>
    <ol type="a" start="a">
      <li>The CSP SHOULD send a notification of proofing to a confirmed address of record.</li>
      <li>The CSP MAY provide an enrollment code directly to the subscriber if binding to an authenticator will occur at a later time.</li>
      <li>The enrollment code SHALL be valid for a maximum of 7 days.</li>
    </ol>
  <li><strong>If the CSP performs remote proofing (unsupervised):</strong></li>
    <ol type="a" start="a">
      <li>The CSP SHALL send an enrollment code to a confirmed address of record for the applicant.</li>
      <li>The applicant SHALL present a valid enrollment code to complete the identity proofing process.</li>
      <li>The CSP SHOULD send the enrollment code to the postal address that has been validated in records. The CSP MAY send the enrollment code to a mobile telephone (SMS or voice), landline telephone, or email if it has been validated in records.</li>
      <li>If the enrollment code is also intended to be an authentication factor, it SHALL be reset upon first use.</li>
      <li>Enrollment codes sent to a postal address of record SHALL be valid for a maximum of 10 days but MAY be made valid up to 30 days via an exception process to accommodate addresses outside the contiguous United States. Enrollment codes sent by telephone SHALL be valid for a maximum of 10 minutes. Enrollment codes sent via email SHALL be valid for a maximum of 24 hours.</li>
      <li>The CSP SHALL ensure the enrollment code and notification of proofing are sent to different addresses of record. For example, if the CSP sends an enrollment code to a phone number validated in records, a proofing notification will be sent to the postal address validated in records or obtained from validated and verified evidence, such as a driver's license.</li>
    </ol>
</ol>
-->

</div>

> Note: 郵便住所は, Enrollment コードの通知を含む, Applicant との間のあらゆるコミュニケーションを行う手段として選好される. しかしながら, 本ガイドライン群は, 物理的であってもデジタルであっても, あらゆる確認済 Address of Record をサポートする.

<!-- > Note: Postal address is the preferred method of sending any communications, including enrollment code and notifications, with the applicant. However, these guidelines support any confirmed address of record, whether physical or digital. -->

#### <a name="4-4-1-7"></a>4.4.1.7 Biometric Collection

CSP は Non-repudiation (否認防止) や Re-proofing を目的として Biometrics を収集してもよい (MAY). Biometrics 収集に関する詳細は [SP 800-63B, Section 5.2.3](sp800-63b.html#biometric_use) を参照のこと.

<!-- The CSP MAY collect biometrics for the purposes of non-repudiation and re-proofing. See [SP 800-63B, Section 5.2.3](sp800-63b.html#biometric_use) for more detail on biometric collection. -->

#### 4.4.1.8 Security Controls

CSP は, [SP 800-53](#SP800-53) やそれに相当する連邦政府標準 (e.g., [FEDRAMP](#FEDRAMP)) や業界標準に定められた, Moderate ないしは High 基準のセキュリティー制御策から, 制御強化を含み, 適切に調整されたセキュリティー制御策を採用しなければならない (SHALL). CSP は *moderate-impact* システムやそれに相当するものに対する Assurance 関連の最低限の制御策が実施されていることを保証しなければならない (SHALL).

<!-- The CSP SHALL employ appropriately tailored security controls, to include control enhancements, from the moderate or high baseline of security controls defined in [SP 800-53](#SP800-53) or equivalent federal (e.g., [FEDRAMP](#FEDRAMP)) or industry standard. The CSP SHALL ensure that the minimum assurance-related controls for *moderate-impact* systems or equivalent are satisfied. -->

#### <a name="referee"></a>4.4.2 IAL2 Trusted Referee Proofing Requirements

個人が [Section 4.4.1](#normal) に規定された Identity Evidence 要件を満たすことができない場合, 機関は信頼できる身元保証人に Applicant の Identity Proofing を手伝わせてもよい (MAY).

<!-- In instances where an individual cannot meet the identity evidence requirements specified in [Section 4.4.1](#normal), the agency MAY use a trusted referee to assist in identity proofing the applicant. See [Section 5.3.4](#trustref) for more details. -->

### <a name="ial3-requirements"></a> 4.5 Identity Assurance Level 3

_This section is normative._

IAL3 では IAL2 よりさらに厳格であり, さらに強度の高いエビデンスの提供が求められると共に, なりすましや不正, その他の有害なダメージから当該 Identity および RP を保護する特定の追加プロセス (Biometrics の利用を含む) も求められることになる. Biometrics は, 不正な Enrollment や 重複した Enrollment を検出するために利用され, Credential への紐付けを再確立する手段としても利用される. 加えて, IAL3 での Identity Proofing は対面 (監視下にある Remote を含む) で行われる. 詳細は [Section 5.3.3](#vip) を参照のこと.

<!-- IAL3 adds additional rigor to the steps required at IAL2, to include providing further evidence of superior strength, and is subject to additional and specific processes (including the use of biometrics) to further protect the identity and RP from impersonation, fraud, or other significantly harmful damages. Biometrics are used to detect fraudulent enrollments, duplicate enrollments, and as a mechanism to re-establish binding to a credential. In addition, identity proofing at IAL3 is performed in-person (to include supervised remote). See [Section 5.3.3](#vip) for more details. -->

#### 4.5.1 Resolution Requirements

PII の収集は, Identity をユニークに識別可能にするために必要最低限な範囲に限定すること (SHALL). これにはデータの照会の助けとなるような Attribute の収集を含んでも良い (MAY). 一般的な Resolution 要件は [Section 5.1](#resolve) を参照のこと.

<!-- Collection of PII SHALL be limited to the minimum necessary to resolve to a unique identity record. This MAY include the collection of attributes that assist in data queries. See [Section 5.1](#resolve) for general resolution requirements. -->

#### 4.5.2 Evidence Collection Requirements

CSP は以下を Applicant から収集すること (SHALL).

<!-- The CSP SHALL collect the following from the applicant: -->

1. 2つの SUPERIOR なエビデンス. **もしくは**
2. **もし** STRONG なエビデンスの Issuing Source が, 発行時の Identity Proofing イベントにおいて, SUPERIOR あるいは STRONG なエビデンスを2つ以上利用して Claimed Identity の確認を行っており, **かつ** CSP が直接 Issuing Source との間でそのエビデンスを確認したのであれば,  SUPERIOR なエビデンスとそのようなプロセスを経て発行された STRONG なエビデンスを1つずつ.
3. STRONG なエビデンスを2つと FAIR なエビデンスを1つ.

<!--
1. Two pieces of SUPERIOR evidence; **OR**
2. One piece of SUPERIOR evidence and one piece of STRONG evidence **if** the issuing source of the STRONG evidence, during its identity proofing event, confirmed the claimed identity by collecting two or more forms of SUPERIOR or STRONG evidence **and** the CSP validates the evidence directly with the issuing source; **OR**
3. Two pieces of STRONG evidence plus one piece of FAIR evidence.
-->


受け入れ可能な Identity Evidence についての詳細は [Section 5.2.1 Identity Evidence Quality Requirements](#evidence-quality) を参照のこと.

<!-- See [Section 5.2.1 Identity Evidence Quality Requirements](#evidence-quality) for more information on acceptable identity evidence. -->

#### <a name="4-5-3"></a>4.5.3 Validation Requirements

CSP は Identity Evidence を以下のように確認すること (SHALL).

<!-- The CSP SHALL validate identity evidence as follows: -->

それぞれのエビデンスは, 提示されたエビデンスと同じ強度のプロセスによって確認すること. 例えば2つの STRONG な Identity Evidence が提示された場合は, それぞれを STRONG な強度で確認することとなる.

<!-- Each piece of evidence must be validated with a process that is able to achieve the same strength as the evidence presented. For example, if two forms of STRONG identity evidence are presented, each piece of evidence will be validated at a strength of STRONG. -->

Identity Evidence の確認についての詳細は [Section 5.2.2 Validating Identity Evidence](#evidence_validation) を参照のこと.

<!-- See [Section 5.2.2 Validating Identity Evidence](#evidence_validation) for more information on validating identity evidence -->

#### 4.5.4 Verification Requirements


CSP は Identity Evidence を以下のように検証すること.

<!-- The CSP SHALL verify identity evidence as follows: -->

1. 最低限, Applicant と Identity Evidence の紐付けは, 強度 SUPERIOR を達成できるプロセスによって検証しなければならない.
2. KBV は対面 (物理的ないしは監視下における Remote) の Identity 検証のために利用してはならない (SHALL NOT).

<!--
1. At a minimum, the applicant's binding to identity evidence must be verified by a process that is able to achieve a strength of SUPERIOR.
2. KBV SHALL NOT be used for in-person (physical or supervised remote) identity verification.
-->

Identity Evidence の検証についての詳細は [Section 5.2.2 Validating Identity Evidence](#evidence_validation) を参照のこと.

<!-- NOTE: 多分原文が間違ってコピペしてる. -->
<!-- See [Section 5.3 Identity Verification](#verify) for more information on acceptable identity evidence. -->

#### 4.5.5 Presence Requirements

CSP は Identity Proofing の全ステップを Applicant と対面で行うこと (SHALL). 詳細は [Section 5.3.3](#vip) を参照のこと.

<!-- The CSP SHALL perform all identity proofing steps with the applicant in-person. See [Section 5.3.3](#vip) for more details. -->

#### <a name="4-5-6"></a>4.5.6 Address Confirmation

1. CSP は Address of Record を確認しなければならない (SHALL). CSP は, 提示された有効な Identity Evidence のいずれかに記載された住所の確認を通じて, Address of Record の確認を行うべきである (SHOULD). CSP は, Applicant が提供した, いかなる有効な Identity Evidence にも記載されていない情報の確認を通じて, Address of Record の確認を行ってもよい (MAY).
2. Self-asserted な住所データは, 確認に用いてはならない (SHALL NOT).
3. 確認された Address of Record に Proofing の通知を送らねばならない (SHALL).
4. Subscriber と Authenticator の紐付けが後日発生する場合は, CSP は Enrollment コードを直接 Subscriber に提示してもよい (MAY). Enrollment コードは最大7日間まで有効なものとする (SHALL).

<!--
1. The CSP SHALL confirm address of record. The CSP SHOULD confirm address of record through validation of the address contained on any supplied, valid piece of identity evidence. The CSP MAY confirm address of record by validating information supplied by the applicant, not contained on any supplied, valid piece of identity evidence.
2. Self-asserted address data SHALL NOT be used for confirmation.
3. A notification of proofing SHALL be sent to the confirmed address of record.
4. The CSP MAY provide an enrollment code directly to the subscriber if binding to an authenticator will occur at a later time. The enrollment code SHALL be valid for a maximum of 7 days.
-->

#### <a name="4-5-7"></a>4.5.7 Biometric Collection


CSP は, Non-repudiation (否認防止) や Re-proofing を目的として, Proofing 時に Biometrics サンプルを収集・記録すること (SHALL). Biometrics 収集に関する詳細は [SP 800-63B, Section 5.2.3](sp800-63b.html#biometric_use) を参照のこと.

<!-- The CSP SHALL collect and record a biometric sample at the time of proofing (e.g., facial image, fingerprints) for the purposes of non-repudiation and re-proofing. See Section 5.2.3 of [SP 800-63B](sp800-63b.html) for more detail on biometric collection. -->

#### 4.5.8 Security Controls

CSP は, [SP 800-53](#SP800-53) やそれに相当する連邦政府標準 (e.g., [FEDRAMP](#FEDRAMP)) や業界標準に定められた, High 基準のセキュリティー制御策から, 制御強化を含み, 適切に調整されたセキュリティー制御策を採用しなければならない (SHALL). CSP は *high-impact* システムやそれに相当するものに対する Assurance 関連の最低限の制御策が実施されていることを保証しなければならない (SHALL).

<!-- The CSP SHALL employ appropriately tailored security controls, to include control enhancements, from the high baseline of security controls defined in [SP 800-53](#SP800-53) or an equivalent federal (e.g., [FEDRAMP](#FEDRAMP)) or industry standard. The CSP SHALL ensure that the minimum assurance-related controls for *high-impact* systems or equivalent are satisfied. -->

### <a name="enrollmentcode"></a> 4.6 Enrollment Code

_This section is normative._

Enrollment コードにより, CSP は Applicant が Address of Record を管理下に置いていることを確認できるほか, Applicant と Enrollment レコードの再紐付けを行えるようにもなる. この紐付けは, もととなる Identity Proofing Transaction と同一の Session で完了する必要はない (NEET NOT).

<!-- An enrollment code allows the CSP to confirm that the applicant controls an address of record, as well as offering the applicant the ability to reestablish binding to their enrollment record. Binding NEED NOT be completed in the same session as the original identity proofing transaction. -->

Enrollment コードは以下の特徴を持つこと (SHALL).

<!-- An enrollment code SHALL be comprised of one of the following: -->

1. 最低限, 6文字の英数字, またはそれ相当のエントロピーを持つもの. 例えば, 承認された乱数生成器を使って生成されたコードや, 物理ハードウェア Authenticator のシリアル番号.
2. ランダムな6文字の英数字と同じかそれ以上のエントロピーを持つデータを含んだ, QR コードなどの機械可読光学ラベル.

<!--
1. Minimally, a random six character alphanumeric or equivalent entropy. For example, a code generated using an approved random number generator or a serial number for a physical hardware authenticator.
2. A machine-readable optical label, such as a QR Code, that contains data of similar or higher entropy as a random six character alphanumeric.
-->

### 4.7 Summary of Requirements

_This section is informative._

[Table 4-1](#63aSec4-Table1) は各 Identity Assurance Level の要件を要約したものである.

<!-- NOTE: 多分原文が間違ってコピペしてる. -->
<!-- [Table 4-1](#63aSec4-Table1) summarizes the requirements for each of the authenticator assurance levels: -->

<a name="63aSec4-Table1"></a>

<div class="text-center" markdown="1">

**Table 4-1 IAL Requirements Summary**

</div>

Requirement | IAL1 | IAL2 | IAL3
------------|-------|-------|-------
Presence | 要件なし | 対面および非監視下の Remote | 対面および監視下の Remote
Resolution | 要件なし | Identity Resolution に必要最低限な Attribute.<br><br>KBV により信頼を高めてもよい. | IAL2 同様
Evidence | Identity Evidence は収集しない | Issuing Source が実施した Proofing および検証の強度次第で, 1つの SUPERIOR もしくは STRONG なエビデンス, もしくは<br><br>2つの STRONG なエビデンス, もしくは<br><br>1つの STRONG なエビデンスと2つの FAIR なエビデンス. | 2つの SUPERIOR なエビデンス, もしくは<br><br>Issuing Source が実施した Proofing および検証の強度次第で, 1つの SUPERIOR もしくは STRONG なエビデンス, もしくは<br><br>2つの STRONG なエビデンスと1つの FAIR なエビデンス.
Validation | 確認なし | それぞれのエビデンスを, エビデンスと同じ強度のプロセスで確認しなければならない. | IAL2 同様
Verification | 検証なし | STRONGの強度のプロセスによって検証する. | SUPERIOR の強度のプロセスによって検証される.
Address Confirmation | 要件なし | 必須. Enrollment コードを任意の Address of Record に送信する. 通知は Enrollment コードとは別の経路で送信する. | 必須. Proofing の通知は郵便住所に対して送信する.
Biometric Collection | No | Optional | Mandatory
Security Controls | N/A | [SP 800-53](#SP800-53) Moderate 基準 (もしくはそれ相当の連邦 / 業界標準). | [SP 800-53](#SP800-53) High 基準 (もしくはそれ相当の連邦 / 業界標準).

<!--
Requirement | IAL1 | IAL2 | IAL3
------------|-------|-------|-------
Presence|No requirements|In-person and unsupervised remote.|In-person and supervised remote.
Resolution|No requirements|The minimum attributes necessary to accomplish identity resolution.<br><br>KBV may be used for added confidence.| Same as IAL2.
Evidence|No identity evidence is collected| One piece of SUPERIOR or STRONG evidence depending on strength of original proof and validation occurs with issuing source, or<br><br> Two pieces of STRONG evidence, or <br><br> One piece of STRONG evidence plus two (2) pieces of FAIR evidence.|Two pieces of SUPERIOR evidence, or<br><br> One piece of SUPERIOR evidence and one piece of STRONG evidence depending on strength of original proof and validation occurs with issuing source, or<br><br> Two pieces of STRONG evidence plus one piece of FAIR evidence.
Validation|No validation|Each piece of evidence must be validated with a process that is able to achieve the same strength as the evidence presented.|Same as IAL2.
Verification| No verification |Verified by a process that is able to achieve a strength of STRONG.|Verified by a process that is able to achieve a strength of SUPERIOR.<br>
Address Confirmation|No requirements for address confirmation|Required. Enrollment code sent to any address of record. Notification sent by means different from enrollment code.|Required. Notification of proofing to postal address.
Biometric Collection|No|Optional|Mandatory
Security Controls|N/A|[SP 800-53](#SP800-53) Moderate Baseline (or equivalent federal or industry standard).|[SP 800-53](#SP800-53) High Baseline (or equivalent federal or industry standard).
-->
