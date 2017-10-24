<a name="sec5"></a>

<div class="breaker"></div>

## <a name="ipv-section"></a> 5 Identity Resolution, Validation, and Verification

_This section is normative._

本セクションでは, Identity および提示された Identity Evidence の導出, 確認, 検証に関する要件を示す. これらの要件は, Claimed Identity が CSP に Enroll しようとしている Subject の実際の Identity であり, 多数の Enroll 済の個人に影響を及ぼしうるスケーラブルな攻撃がシステムによって保護されているリソースの価値よりも大きな時間およびコストを必要とすることを, 確実にするためのものである.

<!-- This section lists the requirements to resolve, validate, and verify an identity and any supplied identity evidence. The requirements are intended to ensure the claimed identity is the actual identity of the subject attempting to enroll with the CSP and that scalable attacks affecting a large population of enrolled individuals require greater time and cost than the value of the resources the system is protecting. -->

### <a name="resolve"></a>5.1 Identity Resolution

Identity Resolution のゴールは, ある個人を所与の集団やコンテキスト内でユニークに区別することである. 効率的に Identity Resolution が行えれば, 最小の Attribute セットによって固有の個人を識別可能になる. これは CSP にとって Identity Proofing プロセス全体の重大な出発点であり, 潜在的な不正の初期検出を含むが, 決してそれ単体では完全かつ成功した Identity Proofing Transaction にはならない.

<!-- The goal of identity resolution is to uniquely distinguish an individual within a given population or context. Effective identity resolution uses the smallest set of attributes necessary to resolve to a unique individual. It provides the CSP an important starting point in the overall identity proofing process, to include the initial detection of potential fraud, but in no way represents a complete and successful identity proofing transaction. -->

1. Proofing プロセスで利用される情報の完全一致によるマッチングは困難である. CSP は, 適切なマッチングアルゴリズムを用いて, 多様な Identity Evidence, Issuing Source および Authoritative Source にまたがった Personal Information やその他関連する Proofing データの差異を把握することができる (MAY). 使用するマッチングアルゴリズムとルールは公開すべきであり, 少なくとも関連する利益共同体には提示されるべきである (SHOULD). 例えば, それらは文書化されたポリシーや [Section 4.2](#genProofReqs) で言及された _practice statement_ に含めることができる.
2. KBV (Knowledge-Based Authentication とも呼ばれる) は, 歴史的に, 公開データベースから得られた情報に対して Applicant の知識をテストすることによって, Claimed Identity を検証するために使用されてきた. CSP は KBV を使って, ユニークな Claimed Identity を識別可能にしてもよい (MAY).

<!--
1.  Exact matches of information used in the proofing process can be difficult to achieve. The CSP MAY employ appropriate matching algorithms to account for differences in personal information and other relevant proofing data across multiple forms of identity evidence, issuing sources, and authoritative sources. Matching algorithms and rules used SHOULD be available publicly or, at minimum, to the relevant community of interest. For example, they may be included as part of the written policy or _practice statement_ referred to in [Section 4.2](#genProofReqs).
2.  KBV (sometimes referred to as knowledge-based authentication) has historically been used to verify a claimed identity by testing the knowledge of the applicant against information obtained from public databases. The CSP MAY use KBV to resolve to a unique, claimed identity.
-->

### <a name="validate"></a>5.2 Identity Evidence Collection and Validation

Identity Validation のゴールは, Applicant からもっとも適切な Identity Evidence を収集し, その Authenticity, 正当性, 正確性を判断することである. Identity Validation は, 適切な Identity Evidence の収集, 当該エビデンスが本物かつ正当であることの確認, Identity Evidence に含まれるデータが正当, 最新, かつ現実世界の Subject に関連していることの確認, の3ステップからなる.

<!-- The goal of identity validation is to collect the most appropriate identity evidence (e.g., a passport or driver's license) from the applicant and determine its authenticity, validity, and accuracy. Identity validation is made up of three process steps: collecting the appropriate identity evidence, confirming the evidence is genuine and authentic, and confirming the data contained on the identity evidence is valid, current, and related to a real-life subject. -->

#### <a name="evidence-quality"></a> 5.2.1 Identity Evidence Quality Requirements

本セクションでは, Identity Proofing 段階で収集される Identity Evidence の品質要件について述べる.

<!-- This section provides quality requirements for identity evidence collected during identity proofing. -->

[Table 5-1](#63aSec5-Table1) には, 正当な Identity を確立するために収集する Identity Evidence に関しての, Unacceptable から Superior までの強度を列挙する. 特に記載がない限り, これらの強度を達成するために, 当該エビデンスは最低限ここに列挙されたすべての品質を満たす必要がある (SHALL).

<!-- [Table 5-1](#63aSec5-Table1) lists strengths, ranging from unacceptable to superior, of identity evidence that is collected to establish a valid identity. Unless otherwise noted, to achieve a given strength the evidence SHALL, at a minimum, meet all the qualities listed. -->

<a name="63aSec5-Table1"></a>

<div class="text-center" markdown="1">

**Table 5-1 Strengths of Identity Evidence**

</div>

| Strength | Qualities of Identity Evidence |
|:---:|:------------------------------|
| Unacceptable | - 受け入れ可能な Identity Evidence ではない. |
| Weak | - 当該エビデンスの Issuing Source が Identity Proofing を行なっていない.<br><br>- 当該エビデンスの発行プロセスでは, 当該エビデンスが合理的に Applicant の管理下に送達されることが想定できる.<br><br>- 当該エビデンスが以下を含む.<br>&nbsp;&nbsp;&nbsp;&nbsp;- 当該エビデンス自体, もしくは紐づいている人物を一意に識別できる, 少なくとも1つの参照番号.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 紐づいている人物の写真もしくは Biometrics テンプレート (様式は問わない). |
| Fair | - 当該エビデンスの Issuing Source が Identity Proofing プロセスを通じて Claimed Identity を確認している.<br><br>- 当該エビデンスの発行プロセスでは, 当該エビデンスが合理的にそのエビデンスに紐づく人物の管理下に送達されることが想定できる.<br><br>- 当該エビデンスが以下を満たす.<br>&nbsp;&nbsp;&nbsp;&nbsp;- 紐づいている人物を一意に識別できる, 少なくとも1つの参照番号.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 紐づいている人物の写真もしくは Biometrics テンプレート (様式は問わない).<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- KBV を通じて所有権を確認可能.<br><br>- 当該エビデンスにデジタル情報が含まれる場合, その情報は暗号化やプロプラエタリーな方法, またはその両方により保護され, 情報の Integrity を確保して Claimed Issuing Source の Authenticity が確認できる.<br><br>- 当該エビデンスに物理セキュリティー機能が含まれる場合, それを再現するためのプロプラエタリーな知識が必要である.<br><br>- 当該エビデンスは有効期限切れしていない. |
| Strong | - 当該エビデンスの Issuing Source が, 現実世界の当人の Identity についての合理的な確信を持てるように設計されている文書化された手続きを通じて, Claimed Identity を確認している. このような手続きは, 規制当局または公的に責任がある機関によって定期的に監督されることとする. そのような手続きの例としては, USA PATRIOT Act of 2001 や Fair and Accurate Credit Transaction Act of 2003 (FACT Act) Section 114 に定められた [Red Flags Rule](#rfr) に呼応して確立された, Customer Identification Program ガイドラインなどが挙げられる.<br><br>- 当該エビデンスの発行プロセスでは, 当該エビデンスがそのエビデンスに紐づく Subject の管理下に送達されることが保証される.<br><br>- 当該エビデンスに紐づいている人物を一意に識別できる, 少なくとも1つの参照番号が含まれる.<br><br>- 当該エビデンスに記載されたフルネームは, 当人が発行時点においてオフィシャルに認識されている名前でなければならない. 仮名, エイリアス, イニシャルなどは許容されない.<br><br>- The:<br> &nbsp;&nbsp;&nbsp;&nbsp;- 当該エビデンスは, 紐づいている人物の写真もしくは Biometrics テンプレート (様式は問わない) を含む.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- Applicant が, 最低限 IAL2 の Identity に紐づいた AAL2 の Authenticator を保持していることを証明する.<br><br>- 当該エビデンスにデジタル情報が含まれる場合, その情報は暗号化やプロプラエタリーな方法, またはその両方により保護され, 情報の Integrity を確保して Claimed Issuing Source の Authenticity が確認できる.<br><br>- 当該エビデンスに物理セキュリティー機能が含まれる場合, それを再現するためのプロプラエタリーな知識およびテクノロジーが必要である.<br><br>- 当該エビデンスは有効期限切れしていない. |
| Superior | - 当該エビデンスの Issuing Source が, 現実世界の Subject の Identity について確実に信頼できるように設計されている文書化された手続きを通じて, Claimed Identity を確認している. このような手続きは, 規制当局または公的に責任がある機関によって定期的に監督されることとする.<br><br>- Issuing Source は Applicant を視覚的に識別し, 当人の存在確認のためのさらなるチェックを行なった.<br><br>- 当該エビデンスの発行プロセスでは, 当該エビデンスがそのエビデンスに紐づく人物の管理下に送達されることが保証される.<br><br>- 当該エビデンスに紐づいている人物を一意に識別できる, 少なくとも1つの参照番号が含まれる.<br><br>- 当該エビデンスに記載されたフルネームは, 当人が発行時点においてオフィシャルに認識されている名前でなければならない. 仮名, エイリアス, イニシャルなどは許容されない.<br><br>- 当該エビデンスは, 紐づいている人物の写真を含む.<br><br>- 当該エビデンスは, 紐づいている人物の Biometrics テンプレート (様式は問わない) を含む.<br><br>- 当該エビデンスはデジタル情報が含み, その情報は暗号化やプロプラエタリーな方法, またはその両方により保護され, 情報の Integrity を確保して Claimed Issuing Source の Authenticity が確認できる.<br><br>- 当該エビデンスに物理セキュリティー機能を含み, それを再現するためのプロプラエタリーな知識およびテクノロジーが必要である.<br><br>- 当該エビデンスは有効期限切れしていない. |

<!--
|Strength|Qualities of Identity Evidence|
|:---:|:------------------------------|
|Unacceptable|- No acceptable identity evidence provided. |
|Weak|- The issuing source of the evidence did not perform identity proofing.<br><br> - The issuing process for the evidence means that it can reasonably be assumed to have been delivered into the possession of the applicant.<br><br> - The evidence contains:<br>&nbsp;&nbsp;&nbsp;&nbsp;- At least one reference number that uniquely identifies itself or the person to whom it relates.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- The issued identity evidence contains a photograph or biometric template (of any modality) of the person to whom it relates.|
|Fair| - The issuing source of the evidence confirmed the claimed identity through an identity proofing process.<br><br> - The issuing process for the evidence means that it can reasonably be assumed to have been delivered into the possession of the person to whom it relates.<br><br>- The evidence:<br>&nbsp;&nbsp;&nbsp;&nbsp;- contains at least one reference number that uniquely identifies the person to whom it relates. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- contains a photograph or biometric template (any modality) of the person to whom it relates.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- can have ownership confirmed through KBV.<br><br> - Where the evidence includes digital information, that information is protected using cryptographic or proprietary methods, or both, and those methods ensure the integrity of the information and enable the authenticity of the claimed issuing source to be confirmed. <br><br> - Where the evidence includes physical security features, it requires proprietary knowledge to be able to reproduce it.<br><br> - The issued evidence is unexpired.|
|Strong|- The issuing source of the evidence confirmed the claimed identity through written procedures designed to enable it to form a reasonable belief that it knows the real-life identity of the person. Such procedures shall be subject to recurring oversight by regulatory or publicly-accountable institutions. For example, the Customer Identification Program guidelines established in response to the USA PATRIOT Act of 2001 or the [Red Flags Rule](#rfr), under Section 114 of the Fair and Accurate Credit Transaction Act of 2003 (FACT Act).<br><br> - The issuing process for the evidence ensured that it was delivered into the possession of the subject to whom it relates.<br><br> - The issued evidence contains at least one reference number that uniquely identifies the person to whom it relates.<br><br> - The full name on the issued evidence must be the name that the person was officially known by at the time of issuance. Not permitted are pseudonyms, aliases, an initial for surname, or initials for all given names<br><br>- The:<br> &nbsp;&nbsp;&nbsp;&nbsp;- Issued evidence contains a photograph or biometric template (of any modality) of the person to whom it relates.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- Applicant proves possession of an AAL2 authenticator bound to an IAL2 identity, at a minimum.<br><br> - Where the issued evidence includes digital information, that information is protected using cryptographic or proprietary methods, or both, and those methods ensure the integrity of the information and enable the authenticity of the claimed issuing source to be confirmed.<br><br> - Where the issued evidence contains physical security features, it requires proprietary knowledge and proprietary technologies to be able to reproduce it.<br><br> - The evidence is unexpired.|
|Superior|- The issuing source of the evidence confirmed the claimed identity by following written procedures designed to enable it to have high confidence that the source knows the real-life identity of the subject. Such procedures shall be subject to recurring oversight by regulatory or publicly accountable institutions.<br><br> - The issuing source visually identified the applicant and performed further checks to confirm the existence of that person. <br><br> - The issuing process for the evidence ensured that it was delivered into the possession of the person to whom it relates.<br><br> - The evidence contains at least one reference number that uniquely identifies the person to whom it relates.<br><br> - The full name on the evidence must be the name that the person was officially known by at the time of issuance. Not permitted are pseudonyms, aliases, an initial for surname, or initials for all given names.<br><br> - The evidence contains a photograph of the person to whom it relates.<br><br> - The evidence contains a biometric template (of any modality) of the person to whom it relates.<br><br> - The evidence includes digital information, the information is protected using cryptographic or proprietary methods, or both, and those methods ensure the integrity of the information and enable the authenticity of the issuing source to be confirmed.<br><br> - The evidence includes physical security features that require proprietary knowledge and proprietary technologies to be able to reproduce it.<br><br> - The evidence is unexpired.|
-->

#### <a name="evidence_validation"></a> 5.2.2 Validating Identity Evidence

ひとたb Identity Evidence を取得すると, CSP はその正確さ, Authenticity, Integrity, および関連情報を Authoritative Source に照会し, 提示されたエビデンスに対して以下の項目を判断する.

<!-- Once the CSP obtains the identity evidence, the accuracy, authenticity, and integrity of the evidence and related information is checked against authoritative sources in order to determine that the presented evidence:   -->

* 偽造されていない真正なものであること.
* 正しい情報が記載されていること.
* 実在する Subject に関する情報が記載されていること.

<!--
* Is genuine, authentic, and not a counterfeit, fake, or forgery;
* Contains information that is correct; and
* Contains information that relates to a real-life subject.
-->

[Table 5-2](#63aSec5-Table2) には, 当該 Proofing Session において提示されたエビデンス, およびそこに記載された情報のに対する, CSP が実施する Identity Validation に関しての, Unacceptable から Superior までの強度を列挙する.

<!-- [Table 5-2](#63aSec5-Table2) lists strengths, ranging from unacceptable to superior, of identity validation performed by the CSP to validate the evidence presented for the current proofing session and the information contained therein. -->

<a name="63aSec5-Table2"></a>

<div class="text-center" markdown="1">

**Table 5-2 Validating Identity Evidence**

</div>

|Strength|Method(s) performed by the CSP|
|:---:|:------------------------------|
| Unacceptable | - Evidence は未確認, もしくは確認できない. |
| Weak | - エビデンスから得られるすべての個人に関する詳細は, Authoritative Source が保有ないしは公開している情報と比較して正当性が確認された. |
| Fair | - 当該エビデンスは<br>&nbsp;&nbsp;&nbsp;&nbsp;- 詳細が Issuing Source ないしは Authoritative Source が保有ないしは公開している情報と比較して正当性が確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 適切なテクノロジーによって, 物理セキュリティー機能の Integrity が確認され, 当該エビデンスが不正・改ざんされておらず, 本物であることが確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR** <br>&nbsp;&nbsp;&nbsp;&nbsp;- 当該エビデンスが, 訓練を受けた担当者により真正であると確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR** <br>&nbsp;&nbsp;&nbsp;&nbsp;- 暗号論的セキュリティー機能の Integrity が確認され, 当該エビデンスが真正であると確認された. |
| Strong | - 以下のように当該エビデンスが真正であると確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;- 適切なテクノロジーによって, 物理セキュリティー機能の Integrity が確認され, 当該エビデンスが不正・改ざんされていないことを確認した.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 訓練を受けた担当者もしくは適切なテクノロジーによって, 物理セキュリティー機能の Integrity が確認され, 当該エビデンスが不正・改ざんされていないことを確認した.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 暗号論的セキュリティー機能の Integrity を確認した.<br><br>- エビデンスから得られるすべての個人およびエビデンスに関する詳細は, Issuing Source ないしは Authoritative Source が保有ないしは公開している情報と比較して正当性が確認された. |
| Superior | - 訓練を受けた担当者, および物理セキュリティーと暗号論的セキュリティー機能の Integrity を含む適切なテクノロジーによって, 当該エビデンスが真正であると確認された.<br><br>- エビデンスから得られるすべての個人およびエビデンスに関する詳細は, Issuing Source ないしは Authoritative Source が保有ないしは公開している情報と比較して正当性が確認された. |

<!--
|Strength|Method(s) performed by the CSP|
|:---:|:------------------------------|
|Unacceptable|- Evidence validation was not performed, or validation of the evidence failed.|
|Weak|- All personal details from the evidence have been confirmed as valid by comparison with information held or published by an authoritative source.|
|Fair| - The evidence:<br>&nbsp;&nbsp;&nbsp;&nbsp;- details have been confirmed as valid by comparison with information held or published by the issuing source or authoritative source(s).<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- has been confirmed as genuine using appropriate technologies, confirming the integrity of physical security features and that the evidence is not fraudulent or inappropriately modified.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR** <br>&nbsp;&nbsp;&nbsp;&nbsp;- The evidence has been confirmed as genuine by trained personnel. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR** <br>&nbsp;&nbsp;&nbsp;&nbsp;- The issued evidence has been confirmed as genuine by confirmation of the integrity of cryptographic security features.|
|Strong| - The evidence has been confirmed as genuine:<br>&nbsp;&nbsp;&nbsp;&nbsp;- using appropriate technologies, confirming the integrity of physical security features and that the evidence is not fraudulent or inappropriately modified. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- by trained personnel and appropriate technologies, confirming the integrity of the physical security features and that the evidence is not fraudulent or inappropriately modified.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- by confirmation of the integrity of cryptographic security features.<br><br> - All personal details and evidence details have been confirmed as valid by comparison with information held or published by the issuing source or authoritative source(s).|
|Superior| - The evidence has been confirmed as genuine by trained personnel and appropriate technologies including the integrity of any physical and cryptographic security features.<br><br> - All personal details and evidence details from the evidence have been confirmed as valid by comparison with information held or published by the issuing source or authoritative source(s).|
-->

担当者がエビデンスを確認する際の訓練に関する要件は, CSP ないしは RP のポリシー, ガイドライン, 要件に基づくこと (SHALL).

<!-- Training requirements for personnel validating evidence SHALL be based on the policies, guidelines, or requirements of the CSP or RP. -->

### 5.3 <a name="verify"></a> Identity Verification

Identity Verification のゴールは, Claimed Identity とエビデンスを提示している現実世界に存在する Subject との紐付けを, 確認および確立することである.

<!-- The goal of identity verification is to confirm and establish a linkage between the claimed identity and the real-life existence of the subject presenting the evidence. -->

#### 5.3.1 Identity Verification Methods

[Table 5-3](#63aSec5-Table3) には, ある Identity Verification 強度を達成するために必要な検証手段が詳説されている. CSP は, Identity 検証に KBV を利用する際は, [Section 5.3.2](#kbv) の要件に従うこと (SHALL).

<!-- [Table 5-3](#63aSec5-Table3) details the verification methods necessary to achieve a given identity verification strength. The CSP SHALL adhere to the requirements in [Section 5.3.2](#kbv) if KBV is used to verify an identity. -->


<a name="63aSec5-Table3"></a>

<div class="text-center" markdown="1">

**Table 5-3 Verifying Identity Evidence**

</div>

|Strength|Identity Verification Methods|
|:---:|:------------------------------|
| Unacceptable | - エビデンスは未検証, もしくは検証できない. Applicant が Claimed Identity の所有者であることが確認できない. |
| Weak | - Applicant は Claimed Identity を裏付けるために提出されたエビデンスへの Access 権限を持っていることが確認された. |
| Fair | - Applicant が Claimed Identity の所有者であることが, 以下のように確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;- KBV. 詳細は [Section 5.3.2.](#kbv) を参照のこと.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- Applicant と, Claimed Identity を裏付けるために提示されたものの中でもっとも強度の高い Identity Evidence との, 物理的な比較. Remote で物理比較を行なう際は, [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use) に示すすべての要件に従うこと (SHALL).<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- Applicant と Identity Evidence の Biometric 比較. Remote で Biometric 比較を行なう際は, [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use) に示すすべての要件に従うこと (SHALL). |
| Strong | - Applicant が Claimed Identity の所有者であることが, 以下のように確認された.<br>&nbsp;&nbsp;&nbsp;&nbsp;- 適切なテクノロジーを利用した, Claimed Identity を裏付けるために提示されたものの中でもっとも強度の高い Identity Evidence に対する, 写真による物理比較. Remote で物理比較を行なう際は, [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use) に示すすべての要件に従うこと (SHALL).<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- 適切なテクノロジーを利用した, Applicant と Claimed Identity を裏付けるために提示されたものの中でもっとも強度の高い Identity Evidence との Biometric 比較. Remote で Biometric 比較を行なう際は, [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use) に示すすべての要件に従うこと (SHALL). |
| Superior | - Applicant が Claimed Identity の所有者であることが, Applicant と Claimed Identity を裏付けるために提示されたものの中でもっとも強度の高い Identity Evidence との, 適切なテクノロジーを利用した Biometric 比較により確認された. Remote で Biometric 比較を行なう際は, [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use) に示すすべての要件に従うこと (SHALL). |

<!--
|Strength|Identity Verification Methods|
|:---:|:------------------------------|
|Unacceptable|- Evidence verification was not performed or verification of the evidence failed. Unable to confirm that the applicant is the owner of the claimed identity.|
|Weak|- The applicant has been confirmed as having access to the evidence provided to support the claimed identity.|
|Fair| - The applicant's ownership of the claimed identity has been confirmed by:<br>&nbsp;&nbsp;&nbsp;&nbsp;- KBV. See [Section 5.3.2.](#kbv) for more details. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- a physical comparison of the applicant to the strongest piece of identity evidence provided to support the claimed identity. Physical comparison performed remotely SHALL adhere to all requirements as specified in [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use). <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- biometric comparison of the applicant to the identity evidence. Biometric comparison performed remotely SHALL adhere to all requirements as specified in [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use). |
|Strong| - The applicant's ownership of the claimed identity has been confirmed by: <br>&nbsp;&nbsp;&nbsp;&nbsp;- physical comparison, using appropriate technologies, to a photograph, to the strongest piece of identity evidence provided to support the claimed identity. Physical comparison performed remotely SHALL adhere to all requirements as specified in [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use). <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**<br>&nbsp;&nbsp;&nbsp;&nbsp;- biometric comparison, using appropriate technologies, of the applicant to the strongest piece of identity evidence provided to support the claimed identity. Biometric comparison performed remotely SHALL adhere to all requirements as specified in [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use).|
|Superior| - The applicant's ownership of the claimed identity has been confirmed by biometric comparison of the applicant to the strongest piece of identity evidence provided to support the claimed identity, using appropriate technologies. Biometric comparison performed remotely SHALL adhere to all requirements as specified in [[SP 800-63B, Section 5.2.3.]](sp800-63b.html#biometric_use).|
-->

#### <a name="kbv"></a>5.3.2 Knowledge-Based Verification Requirements

IAL2 および IAL3 の Identity Verification では, 以下の要件が適用される. KBV を Identity Resolution に用いる場合は特に制約はない.

<!-- The following requirements apply to the identity verification steps for IAL2 and IAL3. There are no restrictions for the use of KBV for identity resolution. -->

<div class="text-left" markdown="0">
  <ol type="1" start="1">
    <li>CSP は, 2つ以上の確認済 Identity Evidence に対して KBV を用いて Applicant の Identity 検証を行なってはならない (SHALL NOT).</li>
    <li>CSP は, KBV プロセス開始に必要な情報を含め, Applicant と Authoritative Source のみが知っていると期待される情報のみを使用することとする (SHALL). 自由に取得可能な情報, パブリックドメインにおいて課金することで手に入る情報, ブラックマーケット経由で手に入る情報は使用しないこと (SHALL NOT).</li>
    <li>CSP は, Resolution および Validation が完了した Identity に対して, Verification のために KBV 以外のプロセスを利用できるようなオプトアウト手段を提供すること (SHALL).</li>
    <li>CSP は, CSP が参加していた最近の Transaction ヒストリーに関する知識を検証することで, KBV を行なうべきである (SHOULD). CSP は, Transaction 情報が最低限20ビットのエントロピーを持つよう保証すること (SHALL). 例えば, 最小のエントロピー要件に到達するには, Applicant に正規の銀行口座に対する少額デポジットのデポジット額および Transaction ナンバーを尋ねることで, 検証を行なうことができる. この例では全7桁以上の数値を聞くことになる.</li>
    <li>CSP は, Applicant が Claimed Identity の所有者であることを示す質問を投げかけ, KBV を実行しても良い. しかしながらその場合は以下の要件を満たすこと.</li>
      <ol type="a" start="a">
        <li>KBV は複数の Authoritative Source に基づくこと.</li>
          <li>CSP は最低限4つの質問を行い, それぞれが正解することをもって KBV ステップを成功とすること (SHALL).</li>
          <li>CSP は自由回答方式の KBV 質問を行うべきである (SHOULD). CSP は選択式質問を行っても良いが (MAY), その場合は各質問に4つ以上の選択肢を用意すること (SHALL).</li>
          <li>CSP は KBV を完了するために Applicant に2度の試行を許すべきである (SHOULD). CSP は3回以上の試行を許容してはならない (SHALL NOT).</li>
          <li>CSP は各質問ごとに2分間の無反応状態があれば KBV Session をタイムアウトさせること (SHALL). Session がタイムアウトした場合, CSP は KBV プロセス全体をリスタートし, 当該試行は失敗と扱うこと (SHALL).</li>
          <li>CSP は KBV の大部分を陽動となるような質問としてはならない (SHALL NOT). (i.e., "none of the above" が正解となるようなもの)</li>
          <li>CSP は同じ KBV 質問を連続した試行において尋ねるべきではない (SHOULD NOT).</li>
          <li>CSP は, 単一の Session ないしは失敗試行の次の Session において, 後の KBV 質問に役立つ情報を提供するような KBV 質問をしてはならない (SHALL NOT).</li>
          <li>CSP は正解が不変な KBV 質問を利用してはならない (SHALL NOT). (e.g., "What was your first car?")</li>
          <li>CSP は, いかなる KBV 質問も, Applicant がまだ提示していない PII や, KBV Session 中の他の情報と組み合わせて特定の個人の識別につながるような Personal Information を漏洩させることのないよう保証すること (SHALL).</li>
        </ol>
  </ol>
</div>

<!--
<div class="text-left" markdown="0">
  <ol type="1" start="1">
    <li>The CSP SHALL NOT use KBV to verify an applicant's identity against more than one piece of validated identity evidence.</li>
    <li>The CSP SHALL only use information that is expected to be known only to the applicant and the authoritative source, to include any information needed to begin the KBV process. Information accessible freely, for a fee in the public domain, or via the black market SHALL NOT be used.</li>
    <li>The CSP SHALL allow a resolved and validated identity to opt out of KBV and leverage another process for verification.</li>
    <li>The CSP SHOULD perform KBV by verifying knowledge of recent transactional history in which the CSP is a participant. The CSP SHALL ensure that transaction information has at least 20 bits of entropy. For example, to reach minimum entropy requirements, the CSP could ask the applicant for verification of the amount(s) and transaction numbers(s) of a micro-deposit(s) to a valid bank account, so long as the total number of digits is seven or greater.</li>
    <li>The CSP MAY perform KBV by asking the applicant questions to demonstrate they are the owner of the claimed information. However, the following requirements apply:</li>
      <ol type="a" start="a">
        <li>KBV SHOULD be based on multiple authoritative sources.</li>  
          <li>The CSP SHALL require a minimum of four KBV questions with each requiring a correct answer to successfully complete the KBV step.</li>
          <li>The CSP SHOULD require free-form response KBV questions. The CSP MAY allow multiple choice questions, however, if multiple choice questions are provided, the CSP SHALL require a minimum of four answer options per question.</li>
          <li>The CSP SHOULD allow two attempts for an applicant to complete the KBV. A CSP SHALL NOT allow more than three attempts to complete the KBV.</li>
          <li>The CSP SHALL time out KBV sessions after two minutes of inactivity per question. In cases of session timeout, the CSP SHALL restart the entire KBV process and consider this a failed attempt.</li>
          <li>The CSP SHALL NOT present a majority of diversionary KBV questions (i.e., those where "none of the above" is the correct answer).</li>
          <li>The CSP SHOULD NOT ask the same KBV questions in subsequent attempts.</li>
          <li>The CSP SHALL NOT ask a KBV question that provides information that could assist in answering any future KBV question in a single session or a subsequent session after a failed attempt.</li>
          <li>The CSP SHALL NOT use KBV questions for which the answers do not change (e.g., "What was your first car?").</li>
          <li>The CSP SHALL ensure that any KBV question does not reveal PII that the applicant has not already provided, nor personal information that, when combined with other information in a KBV session, could result in unique identification.</li>
        </ol>
  </ol>
</div>
-->

#### <a name="vip"></a>5.3.3 In-person Proofing Requirements

対面の Proofing には, 以下の2通りの方法がある.

<!-- In-person proofing can be satisfied in two ways: -->

- オペレーターによる Applicant との物理的インタラクション.
- [Section 5.3.3.2](#supervised) にある特別な要件に従った, オペレーターによる Applicant との Remote インタラクション.

<!--
- A physical interaction with the applicant, supervised by an operator.
- An remote interaction with the applicant, supervised by an operator, based on the specific requirements in [Section 5.3.3.2](#supervised).
-->

#### 5.3.3.1 General Requirements

1. CSP は, 不自然な材料の存在チェックのためにオペレーターに Biometric 情報源 (e.g., 指, 顔) を確認させ, Proofing プロセスの一部としてそのような検査を行うこと (SHALL).
2. CSP は, 当該 Biometric が他の Subject ではなく当該 Applicant から収集されたことが保証される方法により Biometric を収集すること (SHALL). Biometric の実行要件については [SP 800-63B, Section 5.2.3](sp800-63b.html#biometric_use) を参照のこと.

<!--
1. The CSP SHALL have the operator view the biometric source (e.g., fingers, face) for presence of non-natural materials and perform such inspections as part of the proofing process.
2. The CSP SHALL collect biometrics in such a way that ensures that the biometric is collected from the applicant, and not another subject. All biometric performance requirements in [SP 800-63B, Section 5.2.3](sp800-63b.html#biometric_use) apply.
-->

#### <a name="supervised"></a> 5.3.3.2 Requirements for Supervised Remote In-person Proofing

CSP は, Remote Proofing プロセスを採用し, 対面と同等レベルの信頼性およびセキュリティーを実現することもできる. 以下の要件は, Applicant が CSP と物理的に同じ場所にいる対面での Transaction と, Applicant が Remote にいる場合の間の比較可能性を示している.

<!-- CSPs can employ remote proofing processes to achieve comparable levels of confidence and security to in-person events. The following requirements establish comparability between in-person transactions where the applicant is in the same physical location as the CSP to those where the applicant is remote. -->

Supervised Remote (監視下にある Remote での) Identity Proofing および Enrollment Transaction においては, [Section 4.6](#ial3-requirements) に示した IAL3 での Validation および Verification 要件に加えて, 以下の要件に従うこと (SHALL).

<!-- Supervised remote identity proofing and enrollment transactions SHALL meet the following requirements, in addition to the IAL3 validation and verification requirements specified in [Section 4.6](#ial3-requirements): -->

1. CSP は, Applicant が Session から離れることのないよう (SHALL NOT), 全体の Identity Proofing Session を監視すること (SHALL). これには例えば, Applicant の継続的な高解像度ビデオ伝送などの手段があげられる.
2. CSP は, Identity Proofing Session 全体を通じて, Applicant から Remote でリアルタイムにオペレーターを関与させること (SHALL).
3. CSP は, Identity Proofing Session 全体を通じて, Applicant が行った全てのアクションを, Remote オペレーターにはっきりと見えるようにすること (SHALL).
4. CSP は, エビデンスに対するあらゆるデジタル検証 (e.g., チップやワイヤレス技術による) が, 統合されたスキャナーやセンサーによって実行されるようにすること (SHALL).
5. CSP は, 潜在的な不正を検出し正しく仮想の対面 Proofing Session を実行するため, オペレーターに訓練プログラムを受けさせること (SHALL).
6. CSP は, 環境に応じた適切な物理的改ざんの検出策および対抗策を施すこと (SHALL). 例えば, 制限されたエリアや信頼できる個人によって監視されているエリアにあるキオスクは, ショッピングモールのコンコースなどの半公開エリアにあるキオスクよりも, 改ざん検出の必要性は低い.
7. CSP は, 全ての通信が双方向の Authenticated Protected Channel 経由で行われるよう保証すること (SHALL).

<!--
1. The CSP SHALL monitor the entire identity proofing session, from which the applicant SHALL NOT depart — for example, by a continuous high-resolution video transmission of the applicant.
2. The CSP SHALL have a live operator participate remotely with the applicant for the entirety of the identity proofing session.
3. The CSP SHALL require all actions taken by the applicant during the identity proofing session to be clearly visible to the remote operator.
4. The CSP SHALL require that all digital verification of evidence (e.g., via chip or wireless technologies) be performed by integrated scanners and sensors.
5. The CSP SHALL require operators to have undergone a training program to detect potential fraud and to properly perform a virtual in-process proofing session.
6. The CSP SHALL employ physical tamper detection and resistance features appropriate for the environment in which it is located. For example, a kiosk located in a restricted area or one where it is monitored by a trusted individual requires less tamper detection than one that is located in a semi-public area such as a shopping mall concourse.
7. The CSP SHALL ensure that all communications occur over a mutually authenticated protected channel.
-->

#### <a name="trustref"></a> 5.3.4 Trusted Referee Requirements

1. CSP は, 交渉人や法的保護者, 医療専門家, 後見人, 法定代理人, その他の訓練を受け承認されたもの, または認定されたものなど, 適切な法律, 規則, 機関のポリシーに従って, Applicant の身元を保証したり代理人となれる信頼できる身元引き受け人 (Trusted Referee) とやり取りをしても良い (MAY). CSP は Remote, 対面どちらのプロセスでも,  Trusted Referee とやり取りをしても良い (MAY).
2. CSP は, Trusted Referee がどのように決定されるか, および取り消し, 一時停止, その他いかなる制約も含め, Trusted Referee 自身のステータスのライフサイクルについて, ポリシーや手順を明文化すること (SHALL).
3. CSP は, Applicant の Proofing と同じ IAL で, Trusted Referee に対する Proofing を行うこと (SHALL). また CSP は, Trusted Referee と Applicant の関係性を測るために必要な最低限のエビデンスを決定すること (SHALL).
4. CSP は, [Section 4.4.1](#normal) の要件を満たすことをゴールとして, 上記1で示された文書化されたポリシーに定義された規則的なインターバルで, Subscriber に対して Re-proofing を行うべきである (SHOULD).

<!--
1. The CSP MAY use trusted referees &mdash; such as notaries, legal guardians, medical professionals, conservators, persons with power of attorney, or some other form of trained and approved or certified individuals &mdash; that can vouch for or act on behalf of the applicant in accordance with applicable laws, regulations, or agency policy. The CSP MAY use a trusted referee for both remote and in-person processes.
2. The CSP SHALL establish written policy and procedures as to how a trusted referee is determined and the lifecycle by which the trusted referee retains their status as a valid referee, to include any restrictions, as well as any revocation and suspension requirements.
3. The CSP SHALL proof the trusted referee at the same IAL as the applicant proofing. In addition, the CSP SHALL determine the minimum evidence required to bind the relationship between the trusted referee and the applicant.
4. The CSP SHOULD perform re-proofing of the subscriber at regular intervals defined in the written policy specified in item 1 above, with the goal of satisfying the requirements of [Section 4.4.1](#normal).
-->

#### Considerations for Minors

1. CSP は, [Children's Online Privacy Protection Act of 1998](#COPPA) およびその他の法律が適用される場合, それらに遵守すべく, Identity Proofing のエビデンス要件を満たすことができない未成年とのインタラクションに関する法的制約を特別に考慮すること (SHALL).
2. 13歳以下の未成年に関しては, CSP は COPPA およびその他の法律の遵守が求められ (SHALL), 確実に遵守するためには特別な配慮が必要となる.
3. CSP は, 本セクションですでに述べたように, 未成年の Applicant のための Trusted Referee として, 親または法定成人後見人を関与させるべきである (SHOULD).

<!--
1. The CSP SHALL give special consideration to the legal restrictions of interacting with minors unable to meet the evidence requirements of identity proofing to ensure compliance with the [Children's Online Privacy Protection Act of 1998](#COPPA), and other laws, as applicable.
2. Minors under age 13 require additional special considerations under COPPA, and other laws, to which the CSP SHALL ensure compliance, as applicable.
3. The CSP SHOULD involve a parent or legal adult guardian as a trusted referee for an applicant that is a minor, as described elsewhere in this section.
-->

### 5.4 Binding Requirements

Authenticator と Subscriber の紐付けに関しては, [800-63B](sp800-63b.html) Section 6.1 Authenticator Binding を参照のこと.

<!-- [800-63B](sp800-63b.html) Section 6.1 Authenticator Binding for instructions on binding authenticators to subscribers. -->
