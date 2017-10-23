<a name="sec1"></a>

<div class="breaker"></div>

## 1 <a name="purpose"></a> Purpose

_This section is informative._

本ドキュメントでは, 各 Identity Assurance Level (IAL) ごとに, リソースへの Access を希望する Applicant に対する, Enrollment および Identity Proofing に関する要件をまとめる. 要件は, Subscriber が自身の Identity を主張する際に提示する Identity Evidence の受け入れ可能性, 妥当性確認, 検証のそれぞれに関して詳細化されている. さらに本ドキュメントは, Enrollment レコードの作成と保守, および Authenticator (CSP が発行したものも Subscriber が提供したものも) と Enrollment レコードの紐付けに関して, Credential Service Providers (CSP) の責任を明確化する.

<!-- This document provides requirements for enrollment and identity proofing of applicants that wish to gain access to resources at each Identity Assurance Level (IAL). The requirements detail the acceptability, validation, and verification of identity evidence that will be presented by a subscriber to support their claim of identity. This document also details the responsibilities of Credential Service Providers (CSPs) with respect to establishing and maintaining enrollment records and binding authenticators (either CSP-issued or subscriber-provided) to the enrollment record. -->

<a name="sec2"></a>

## 2 <a name="intro"></a> Introduction

_This section is informative._

Digital Identity に関する課題の1つに, 一連のオンラインアクションを単一の特定の主体と関連付けることがある. こういった関連付けが不要であったり望ましくない (e.g., Anonymity (匿名性) や Pseudonymity (仮名性) が求められる) シチュエーションもあるが, 現実世界の Subject との関係性を確実に確立するために重要となるシチュエーションもある. ヘルスケア情報を取得したり金融取引を実行するといったシチュエーションは, その良い例である. また何らかの規制 (e.g., USA PATRIOT Act of 2001 により確立された金融業界の 'Know Your Customer' 要件) や, ハイリスクなアクション (e.g., ダムの放水率を変える) に対する説明責任の確立のために, そういった関連付けが必須となるシチュエーションもある.

<!-- One of the challenges associated with digital identity is the association of a set of online activities with a single specific entity. While there are situations where this is not required or is even undesirable (e.g., use cases where anonymity or pseudonymity are required), there are others where it is important to reliably establish an association with a real-life subject. Examples include obtaining health care and executing financial transactions. There are also situations where the association is required for regulatory reasons (e.g., the financial industry's 'Know Your Customer' requirements, established in the implementation of the USA PATRIOT Act of 2001) or to establish accountability for high-risk actions (e.g., changing the release rate of water from a dam). -->

Replying Party (RP) が Transaction を実行する Subscriber に関して何らかを知っているが, 現実世界の Identity については知らないという状況が望ましい場合もある. 例えば, 国勢調査や選出された公務員への嘆願のためには, Subscriber の自宅の郵便番号のみを知っている状態が望ましいかもしれない. どちらのケースでも, サービス提供のためには郵便番号がわかれば十分であり, 当該人間の見えない Identity を知ることは必要でないし望ましくもない.

<!-- There are also instances where it is desirable for a relying party (RP) to know something about a subscriber executing a transaction, but not know their real-life identity. For example, it may be desirable to only know a subscriber's home ZIP code for purposes of census-taking or petitioning an elected official. In both instances, the ZIP code is sufficient to deliver the service; it is not necessary or desirable to know the underlying identity of the person. -->

下表は, 本ドキュメントのどのセクションが Normative (規範) であり, どのセクションが Informative (参考) であるかを示している.

<!-- The following table states which sections of this document are normative and which are informative: -->

|Section Name|Normative/Informative|
|----|:--:|
|1. Purpose|Informative|
|2. Introduction|Informative|
|3. Definitions and Abbreviations|Informative|
|4. Identity Assurance Level Requirements|Normative|
|5. Identity Resolution, Validation, and Verification|Normative|
|6. Derived Credentials|Normative|
|7. Threats and Security Considerations|Informative|
|8. Privacy Considerations|Informative|
|9. Usability Considerations|Informative|
|10. References|Informative|

## 2.1 Expected Outcomes of Identity Proofing

Subject に対して Identity Proofing を行う際には, 以下のようなことが期待される.

<!-- When a subject is identity proofed, the expected outcomes are: -->

* Claimed Identity を, CSP がサービスを提供するユーザー集団のコンテキストにおいて, 単一かつユニークな Identity に帰着させる.
* 提供された全てのエビデンスが正しく本物である (e.g., 偽造・悪用されていない) ことを確認する.
* Claimed Identity が現実世界に存在することを確認する.
* Claimed Identity が Identity Evidence を提示した現実世界の人間と関連づいていることを検証する.

<!--
* Resolve a claimed identity to a single, unique identity within the context of the population of users the CSP serves.
* Validate that all supplied evidence is correct and genuine (e.g., not counterfeit or misappropriated).
* Validate that the claimed identity exists in the real world.
* Verify that the claimed identity is associated with the real person supplying the identity evidence.
-->

## 2.2 Identity Assurance Levels

Subscriber の Identity に関する Assurance は以下の3つの IAL を利用して記述される.

<!-- Assurance in a subscriber's identity is described using one of three IALs: -->

**IAL1**: Applicant を現実世界の特定の Identity 紐づける必要はない. Subject の行動に関連して提供される Attribute は, Self-asserted であるか, Self-asserted として扱われるべきである (CSP が RP に対して Assert する Attribute を含む). Self-asserted Attribute は確認も検証もされない.

<!-- **IAL1**: There is no requirement to link the applicant to a specific real-life identity. Any attributes provided in conjunction with the subject's activities are self-asserted or should be treated as self-asserted (including attributes a CSP asserts to an RP). Self-asserted attributes are neither validated nor verified. -->

**IAL2**: エビデンスにより, Claimed Identity が現実世界に存在することを示す材料とし, Applicant が現実世界の当該 Identity と適切に関連づけられていることを証明する. IAL2 では Remote ないしは対面での Identity Proofing が必要となる. Attribute は RP に対して CSP によって Assert されることもあり, Pseudonymous Identity が検証済 Attribute を持つこともサポートされる. IAL2 をサポートする CSP は, ユーザーの同意があれば IAL1 の Transaction をサポートしてもよい.

<!-- **IAL2**: Evidence supports the real-world existence of the claimed identity and verifies that the applicant is appropriately associated with this real-world identity. IAL2 introduces the need for either remote or physically-present identity proofing. Attributes could be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. A CSP that supports IAL2 can support IAL1 transactions if the user consents. -->

**IAL3**: 対面での Identity Proofing が必要である. 識別に用いる Attribute は Authorized かつ訓練を受けた CSP の代理人によって検証される必要がある. IAL2 と同様, Attribute は RP に対して CSP によって Assert されることもあり, Pseudonymous Identity が検証済 Attribute を持つこともサポートされる. IAL3 をサポートする CSP は, ユーザーの同意があれば IAL1 および IAL2 の Transaction をサポートしてもよい.

<!-- **IAL3**: Physical presence is required for identity proofing. Identifying attributes must be verified by an authorized and trained CSP representative. As with IAL2, attributes could be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. A CSP that supports IAL3 can support IAL1 and IAL2 identity attributes if the user consents. -->

IAL2 と IAL3 では, CSP から RP に送信する Attribute の数やその提示方法を制限することで, Federated 環境での Pseudonymity が実現可能である. 例えば, RP が正確な誕生日のみを必要とし, その他の個人の詳細については知らなくて良い時, RP は CSP に Subscriber の誕生日のみを要求すべきである. また可能であれば, RP は CSP に Attribute Reference を要求すべきである. 例えば, RP が Subscriber が18歳以上かどうか知る必要がある場合, RP は完全な誕生日ではなく真偽値のみを要求すべきである. 逆に言えば, より低い Assurance Level の Transaction によいて, より高い Assurance を持つ CSP を利用することは, ユーザーにとって有益たりうる. 例えば, ユーザーは IAL3 の Identity を管理し, その CSP を IAL2 や IAL1 の Transaction においても利用できるべきである.

<!-- At IAL2 and IAL3, pseudonymity in federated environments is enabled by limiting the number of attributes sent from the CSP to the RP, or the way they are presented. For example, if a RP needs a valid birthdate but no other personal details, the RP should leverage a CSP to request just the birthdate of the subscriber. Wherever possible, the RP should ask the CSP for an attribute reference. For example, if a RP needs to know if a claimant is older than 18 they should request a boolean value, not the entire birthdate, to evaluate age. Conversely, it may be beneficial to the user that uses a high assurance CSP for transactions at lower assurance levels.  For example, a user may maintain an IAL3 identity, yet should be able to use their CSP for IAL2 and IAL1 transactions. -->

当該個人は Enrollment 時に Identity Proofing プロセスを経るであろうから, CSP との個別のインタラクションに関する Transaction は必ずしも Pseudonymous とは限らない.

<!-- Since the individual will have undergone an identity proofing process at enrollment, transactions with respect to individual interactions with the CSP may not necessarily be pseudonymous. -->

各 IAL の詳細な要件は [Section 4](#ial-section) および [Section 5](#ipv-section) で述べる.

<!-- Detailed requirements for each of the IALs are given in [Section 4](#ial-section) and [Section 5](#ipv-section). -->
