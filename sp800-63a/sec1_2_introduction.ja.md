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

When a subject is identity proofed, the expected outcomes are:

* Resolve a claimed identity to a single, unique identity within the context of the population of users the CSP serves.
* Validate that all supplied evidence is correct and genuine (e.g., not counterfeit or misappropriated).
* Validate that the claimed identity exists in the real world.
* Verify that the claimed identity is associated with the real person supplying the identity evidence.

## 2.2 Identity Assurance Levels

Assurance in a subscriber's identity is described using one of three IALs:

**IAL1**: There is no requirement to link the applicant to a specific real-life identity. Any attributes provided in conjunction with the subject's activities are self-asserted or should be treated as self-asserted (including attributes a CSP asserts to an RP). Self-asserted attributes are neither validated nor verified.

**IAL2**: Evidence supports the real-world existence of the claimed identity and verifies that the applicant is appropriately associated with this real-world identity. IAL2 introduces the need for either remote or physically-present identity proofing. Attributes could be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. A CSP that supports IAL2 can support IAL1 transactions if the user consents.

**IAL3**: Physical presence is required for identity proofing. Identifying attributes must be verified by an authorized and trained CSP representative. As with IAL2, attributes could be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. A CSP that supports IAL3 can support IAL1 and IAL2 identity attributes if the user consents.

At IAL2 and IAL3, pseudonymity in federated environments is enabled by limiting the number of attributes sent from the CSP to the RP, or the way they are presented. For example, if a RP needs a valid birthdate but no other personal details, the RP should leverage a CSP to request just the birthdate of the subscriber. Wherever possible, the RP should ask the CSP for an attribute reference. For example, if a RP needs to know if a claimant is older than 18 they should request a boolean value, not the entire birthdate, to evaluate age. Conversely, it may be beneficial to the user that uses a high assurance CSP for transactions at lower assurance levels.  For example, a user may maintain an IAL3 identity, yet should be able to use their CSP for IAL2 and IAL1 transactions.

Since the individual will have undergone an identity proofing process at enrollment, transactions with respect to individual interactions with the CSP may not necessarily be pseudonymous.

Detailed requirements for each of the IALs are given in [Section 4](#ial-section) and [Section 5](#ipv-section).
