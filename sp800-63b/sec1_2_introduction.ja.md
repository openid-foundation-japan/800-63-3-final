<a name="sec1"></a>

## 1 Purpose

_本セクションは参考情報である._
<!--
_This section is informative._
-->

本書及び付随文書である[Special Publication (SP) 800-63](sp800-63-3.html)、[SP 800-63A](sp800-63a.html)および[SP 800-63C](sp800-63c.html)は、政府機関に対してDigital Authenticationの実装のための技術的なガイドラインを提供する。

<!--
This document and its companion documents, [Special Publication (SP) 800-63](sp800-63-3.html), [SP 800-63A](sp800-63a.html), and [SP 800-63C](sp800-63c.html), provide technical guidelines to agencies for the implementation of digital authentication.
-->

<a name="sec2"></a>

## 2 Introduction

_本セクションは参考情報である._
<!--
_This section is informative._
-->

Digital Identityはオンライン取引に関わるSubjectの一意な表現である。Digital Identityはデジタルサービスの文脈では常に一意だが、必ずしも現実のSujectまで追跡できる必要はない。言い換えれば、デジタルサービスにアクセスするということが、根本的なSubjectの現実の表現が知られていることを意味していなくてもよい。Identity ProofingはSubjectが実際には彼らが何者であるかを確認する。Digital Authenticationは、Digital Identityを主張するために利用いる一つ以上のAuthenticatorの妥当性を決定するプロセスである。Authentcationはデジタルサービスに対してアクセスしようとしているSubjectが、Authenticateするための技術を制御しているということを確認する行為である。再訪問するようなサービスでは、正常にAuthenticateすることが、今日サービスにアクセスしているSubjectが以前サービスにアクセスした人と同一であるということを示す合理的なリスクベースの保証をもたらす。Digital Identityは、多くの場合オープンなネットワークを介した個人のProofingを伴い、常にオープンなネットワークを介した個人のAuthenticationが必要となるため、技術的な技術的な課題がある。この課題には、SubjectのDigital Identityを不正にかたることにつながる、なりすましや他の攻撃の可能性が複数存在している。

<!--
Digital identity is the unique representation of a subject engaged in an online transaction. A digital identity is always unique in the context of a digital service, but does not necessarily need to be traceable back to a specific real-life subject. In other words, accessing a digital service may not mean that the underlying subject's real-life representation is known. Identity proofing establishes that a subject is actually who they claim to be. Digital authentication is the process of determining the validity of one or more authenticators used to claim a digital identity. Authentication establishes that a subject attempting to access a digital service is in control of the technologies used to authenticate. For services in which return visits are applicable, successfully authenticating provides reasonable risk-based assurances that the subject accessing the service today is the same as the one who accessed the service previously. Digital identity presents a technical challenge because it often involves the proofing of individuals over an open network and always involves the authentication of individuals over an open network. This presents multiple opportunities for impersonation and other attacks which can lead to fraudulent claims of a subject's digital identity.
-->

Subscriberの継続的なAuthenticationは、Subscriberを彼らのオンラインでの活動と結びつけるプロセスの中心である。Subscriber Authenticationは、Claimantが指定されたSubscriberと関連付けられている一つ以上の*Authenticator*(以前のバージョンのSP 800-63では*token*と呼ばれていたもの)を制御していることを検証することで実施される。Authenticationが成功した結果は、Relying Party(RP)に対する、仮名または仮名でない識別子のAssertionであり、オプションで他のIdentity情報も対象となる。

<!--
The ongoing authentication of subscribers is central to the process of associating a subscriber with their online activity. Subscriber authentication is performed by verifying that the claimant controls one or more *authenticators* (called *tokens* in earlier versions of SP 800-63) associated with a given subscriber. A successful authentication results in the assertion of an identifier, either pseudonymous or non-pseudonymous, and optionally other identity information, to the relying party (RP).
-->

本書は、様々な*Authenticator Assurance Level*(AAL)で利用されるAuthenticatorの選択を含む、Authenticationプロセスの分類における推奨を提供する。さらに本書は、紛失や盗難に際しての取り消しを含む、Authenticatorのライフサイクルにおける推奨を提供する。

<!--
This document provides recommendations on types of authentication processes, including choices of authenticators, that may be used at various *Authenticator Assurance Levels* (AALs). It also provides recommendations on the lifecycle of authenticators, including revocation in the event of loss or theft.
-->

この技術的ガイドラインは、ネットワーク越しのシステムに対するSubjectのDigital Authenticationに適用される。ガイドラインは(ビルなどへの)物理アクセスのための人物のAuthenticationについては考慮していないが、デジタルアクセスのために利用されるものと同じクレデンシャルが、物理アクセスのAuthenticationの目的にも使われてもよい。さらにこの技術的ガイドラインは、Authenticationプロトコルに参加する連邦政府機関のシステム及びサービスの提供者が、Subscriberに対してAuthenticateされることを要求する。

<!--
This technical guideline applies to digital authentication of subjects to systems over a network. It does not address the authentication of a person for physical access (e.g., to a building), though some credentials used for digital access may also be used for physical access authentication. This technical guideline also requires that federal systems and service providers participating in authentication protocols be authenticated to subscribers.
-->

Authenticationトランザクションの強度はAALとして知られている分類によって特徴付けられる。より強力な認証(より高いAAL)では、悪意のある当事者がAuthenticationプロセスを成功裏に覆すために一層の機能及びリソースが必要となる。より高いAALでのAuthenticationは攻撃リスクを効果的に減少させることができる。個々のAALに求められる技術的な要件の高度なサマリを以下に記載する; 特別な標準要求については、本書の [Section 4](#sec4) 及び [5](#sec5) を参照。
<!--
The strength of an authentication transaction is characterized by an ordinal measurement known as the AAL. Stronger authentication (a higher AAL) requires malicious actors to have better capabilities and expend greater resources in order to successfully subvert the authentication process. Authentication at higher AALs can effectively reduce the risk of attacks. A high-level summary of the technical requirements for each of the AALs is provided below; see [Sections 4](#sec4) and [5](#sec5) of this document for specific normative requirements.
-->

**Authenticator Assurance Level 1** - AAL 1はSubscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという、いくらかの保証を提供する。AAL 1では幅広く利用可能なAuthentication技術を利用した、単一要素または多要素のAuthenticationを必要とする。Authenticationが成功するには、そのClaimantが、セキュアなAuthenticationプロトコルを介して、自身がそのAuthenticatorを所有・制御していることを証明する必要がある。
<!--
**Authenticator Assurance Level 1**: AAL1 provides some assurance that the claimant controls an authenticator bound to the subscriber's account. AAL1 requires either single-factor or multi-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove possession and control of the authenticator through a secure authentication protocol.
-->

**Authenticator Assurance Level 2** - AAL 2は、Subscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという高い確実性を提供する。セキュアなAuthenticationプロトコルを介して、異なる2つのAuthentication要素を所有・制御していることを証明する必要がある。AAL 2及びそれ以上では、Approved Cryptography技術が必要とされる。
<!--
**Authenticator Assurance Level 2**: AAL2 provides high confidence that the claimant controls an authenticator(s) bound to the subscriber's account. Proof of possession and control of two different authentication factors is required through secure authentication protocol(s). Approved cryptographic techniques are required at AAL2 and above.
-->

**Authenticator Assurance Level 3** - AAL 3は、Subscriberのアカウントに対して結び付けられているAuthenticatorをClaimantが制御しているという非常に高い確実性を持つ。AAL 3におけるAuthenticationは、暗号プロトコルを介した鍵を所有していることの証明に基づいている。AAL 3のAuthenticationは、ハードウェアベースのAuthenticatorまたはVerifierに対してなりすまし耐性を提供するAuthenticatorを要求す。この際、同じデバイスが両方の要件を満たしていても良い。AAL 3でAuthenticateするために、ClaimantはセキュアなAuthenticationプロトコルを介して2つの異なるAuthentication要素を所有・制御していることを証明する必要がある。Approved Cryptography技術が必要とされる。
<!--
**Authenticator Assurance Level 3**: AAL3 provides very high confidence that the claimant controls authenticator(s) bound to the subscriber's account. Authentication at AAL3 is based on proof of possession of a key through a cryptographic protocol. AAL3 authentication requires a hardware-based  authenticator and an authenticator that provides verifier impersonation resistance; the same device may fulfill both these requirements. In order to authenticate at AAL3, claimants are required to prove possession and control of two distinct authentication factors through secure authentication protocol(s). Approved cryptographic techniques are required.
-->

次の表は本文書の各セクションが標準であるか参考情報であるかを示している:
<!--
The following table states which sections of the document are normative and which are informative:
-->


|セクション名|標準/参考情報
|----|:--:|
|1. 目的|参考情報|
|2. はじめに|参考情報|
|3. 定義及び略語|参考情報|
|4. Authenticator Assurance Levels|標準|
|5. Authenticator及びVerifierの要件|標準|
|6. Authenticatorライフサイクルの要件|標準|
|7. セッション管理|標準|
|8. 脅威とセキュリティに関する考慮事項|参考情報|
|9. プライバシに関する考慮事項|参考情報|
|10. ユーザビリティに関する考慮事項|参考情報|
|11. 参照|参考情報|
|付録A &mdash; 記憶シークレットの強度|参考情報|

<!--
|Section Name|Normative/Informative|
|----|:--:|
|1. Purpose|Informative|
|2. Introduction|Informative|
|3. Definitions and Abbreviations|Informative|
|4. Authenticator Assurance Levels|Normative|
|5. Authenticator and Verifier Requirements|Normative|
|6. Authenticator Lifecycle Management|Normative|
|7. Session Management|Normative|
|8. Threat and Security Considerations|Informative|
|9. Privacy Considerations|Informative|
|10. Usability Considerations|Informative|
|11. References|Informative|
|Appendix A &mdash; Strength of Memorized Secrets|Informative|
-->


