<div class="text-right" markdown="1">

# <a name="800-63-3"></a> NIST Special Publication 800-63
# Revision 3

![](sp800-63-3/media/div-1.png)  

# Digital Identity Guidelines (翻訳版)

![](sp800-63-3/media/div-2.png)  

Paul A. Grassi  
Michael E. Garcia  
James L. Fenton  

This publication is available free of charge from:  
https://doi.org/10.6028/NIST.SP.800-63-3  

![](sp800-63-3/media/csd.png)  
![](sp800-63-3/media/nist_logo.png)

</div><div class="breaker text-right" markdown="1">

# NIST Special Publication 800-63-3

# Digital Identity Guidelines

<table class="authors">
  <tr>
    <td>Paul A. Grassi<br>Michael E. Garcia<br><i>Applied Cybersecurity Division</i><br><i>Information Technology Laboratory</i></td>
    <td>James L. Fenton<br><i>Altmode Networks</i><br><i>Los Altos, CA</i></td>
  </tr>
  <tr>
    <td></td>
    <td><strong>翻訳者:</strong><br>Nov Matake<br><i>YAuth.jp LLC</i></td>
  </tr>
</table>


This publication is available free of charge from:  
https://doi.org/10.6028/NIST.SP.800-63-3  

June 2017

![](sp800-63-3/media/commerce_logo.png)

U.S. Department of Commerce  
*Wilbur L. Ross, Jr., Secretary*  

National Institute of Standards and Technology  
*Kent Rochford, Acting NIST Director and Under Secretary of Commerce for Standards and
Technology*

</div>

<div class="breaker"/>

<div class="text-center" markdown="1">

### Authority

</div>

This publication has been developed by NIST in accordance with its statutory responsibilities under the Federal Information Security Modernization Act (FISMA) of 2014, 44 U.S.C. § 3551 et seq., Public Law (P.L.) 113-283. NIST is responsible for developing information security standards and guidelines, including minimum requirements for federal systems, but such standards and guidelines shall not apply to national security systems without the express approval of appropriate federal officials exercising policy authority over such systems. This guideline is consistent with the requirements of the Office of Management and Budget (OMB) Circular A-130.

Nothing in this publication should be taken to contradict the standards and guidelines made mandatory and binding on federal agencies by the Secretary of Commerce under statutory authority. Nor should these guidelines be interpreted as altering or superseding the existing authorities of the Secretary of Commerce, Director of the OMB, or any other federal official. This publication may be used by nongovernmental organizations on a voluntary basis and is not subject to copyright in the United States. Attribution would, however, be appreciated by NIST.

<div class="text-center" markdown="1">

National Institute of Standards and Technology Special Publication 800-63-3  
Natl. Inst. Stand. Technol. Spec. Publ. 800-63-3, 73 pages (June 2017)  
CODEN: NSPUE2

This publication is available free of charge from:  
https://doi.org/10.6028/NIST.SP.800-63-3  

</div>

<div class="text-justify" markdown="1">
>Certain commercial entities, equipment, or materials may be identified in this document in order to describe an experimental procedure or concept adequately. Such identification is not intended to imply recommendation or endorsement by NIST, nor is it intended to imply that the entities, materials, or equipment are necessarily the best available for the purpose.
<br /><br />
>There may be references in this publication to other publications currently under development by NIST in accordance with its assigned statutory responsibilities. The information in this publication, including concepts and methodologies, may be used by federal agencies even before the completion of such companion publications. Thus, until each publication is completed, current requirements, guidelines, and procedures, where they exist, remain operative. For planning and transition purposes, federal agencies may wish to closely follow the development of these new publications by NIST.
<br /><br />
>Organizations are encouraged to review all draft publications during public comment periods and provide feedback to NIST. Many NIST cybersecurity publications, other than the ones noted above, are available at [http://csrc.nist.gov/publications/](http://csrc.nist.gov/publications/).
</div>

<div class="text-center" markdown="1">

**Comments on this publication may be submitted to:**

National Institute of Standards and Technology  
Attn: Applied Cybersecurity Division, Information Technology Laboratory  
100 Bureau Drive (Mail Stop 2000) Gaithersburg, MD 20899-2000  
Email: <dig-comments@nist.gov>

All comments are subject to release under the Freedom of Information Act (FOIA).

</div>

<div class="text-center" markdown="1">

### Reports on Computer Systems Technology

</div>

The Information Technology Laboratory (ITL) at the National Institute of
Standards and Technology (NIST) promotes the U.S. economy and public
welfare by providing technical leadership for the nation's measurement
and standards infrastructure. ITL develops tests, test methods,
reference data, proof of concept implementations, and technical analyses
to advance the development and productive use of information technology.
ITL's responsibilities include the development of management,
administrative, technical, and physical standards and guidelines for the
cost-effective security and privacy of other than national
security-related information in federal systems. The Special
Publication 800-series reports on ITL's research, guidelines, and
outreach efforts in system security, and its collaborative
activities with industry, government, and academic organizations.

<div class="text-center" markdown="1">

### Abstract

</div>

These guidelines provide technical requirements for federal agencies
implementing digital identity services and are not intended to constrain
the development or use of standards outside of this purpose. The
guidelines cover identity proofing and authentication of users (such as employees,
contractors, or private individuals) interacting with government IT
systems over open networks. They define technical requirements in each of the areas of identity proofing,
registration, authenticators, management processes, authentication protocols, federation, and
related assertions. This publication supersedes NIST Special Publication 800-63-2.

<div class="text-center" markdown="1">

### Keywords

</div>

authentication; authentication assurance; authenticator; assertions; credential service provider;
digital authentication; digital credentials; identity proofing; federation;
passwords; PKI.

<div class="text-center" markdown="1">

### Acknowledgements

</div>

The authors gratefully acknowledge Kaitlin Boeckl for her artistic graphics contributions to all volumes in the SP 800-63 suite and the contributions of our many reviewers, including Joni Brennan from the Digital ID & Authentication Council of Canada (DIACC), Ellen Nadeau and Ben Piccarreta from NIST, and Danna Gabel O'Rourke from Deloitte & Touche LLP.

In addition, the authors would like to acknowledge the thought leadership and innovation of the original authors: Donna F. Dodson, Elaine M. Newton, Ray A. Perlner, W. Timothy Polk, Sarbari Gupta, and Emad A. Nabbus. Without their tireless efforts, we would not have had the incredible baseline from which to evolve SP 800-63 to the document it is today.

<div class="text-center" markdown="1">

### <a name="notation"></a> Requirements Notation and Conventions

</div>

The terms "SHALL" and "SHALL NOT" indicate requirements to be followed strictly in order to conform to the publication and from which no deviation is permitted.

The terms "SHOULD" and "SHOULD NOT" indicate that among several possibilities one is recommended as particularly suitable, without mentioning or excluding others, or that a certain course of action is preferred but not necessarily required, or that (in the negative form) a certain possibility or course of action is discouraged but not prohibited.

The terms "MAY" and "NEED NOT" indicate a course of action permissible within the limits of the publication.

The terms "CAN" and "CANNOT" indicate a possibility and capability, whether material, physical or causal or, in the negative, the absence of that possibility or capability.

<div class="breaker"/>

## Executive Summary

_This section is informative._

Digital Identity とはある Subject のオンライン上の Persona であり, その単一的な定義に関しては国際的に議論されている. Persona という語は, Subject がオンライン上で自身を多様に表現できるということを示す適した用語であろう. ある個人は, Email を利用する際の Digital Identity を持ちつつ, パーソナルファイナンス用に別の Digital Identity を持ちうる. ある個人のラップトップは, 誰かの音楽ストリーミングサーバーでありつつ, 複雑な遺伝子計算を行う分散コンピューターネットワーク内の1ワーカーボットでもありうる. コンテキストを考慮しないと, 全てを満たす単一の定義に帰着することは困難である.

<!-- Digital identity is the online persona of a subject, and a single definition is widely debated internationally. The term persona is apropos as a subject can represent themselves online in many ways. An individual may have a digital identity for email, and another for personal finances. A personal laptop can be someone's streaming music server yet also be a worker-bot in a distributed network of computers performing complex genome calculations. Without context, it is difficult to land on a single definition that satisfies all. -->

法律上の Identity としての Digital Identity はさらに定義を複雑にし, Digital Identity をソーシャルやエコノミクスのユースケースにまたがって広く利用することも困難にする. Digital Identity とは難しいものである. ある人が, 自身の主張する人物であるということを - 特にリモートでデジタルサービスを通じて - 証明することは難しく, Attacker が誰かになりすます機会に満ちている. [Peter Steiner in The New Yorker](#steiner) にも描かれている通り, "インターネットでは, 誰もあなたが犬であるとは知る由もない (On the internet, nobody knows you're a dog.)" のである. 本ガイドラインはオンライン固有の脆弱性に対する対策を提供する. また対策の提示に際しては, 低リスクのデジタルサービスに Access する際には "being a dog" であっても問題ない一方, 高リスクのサービスでは当該 Digital Identity が実際の Subject の正当な代理であることを一定のレベルで保証できなければならない, ということを念頭に置く.

<!-- Digital identity as a legal identity further complicates the definition and ability to use digital identities across a range of social and economic use cases. Digital identity is hard. Proving someone is who they say they are — especially remotely, via a digital service — is fraught with opportunities for an attacker to successfully impersonate someone. As correctly captured by [Peter Steiner in The New Yorker](#steiner), "On the internet, nobody knows you're a dog." These guidelines provide mitigations to the vulnerabilities inherent online, while recognizing and encouraging that when accessing some low-risk digital services, "being a dog" is just fine; while other, high-risk services need a level of confidence that the digital identity accessing the service is the legitimate proxy to the real life subject. -->

本ガイドライン群では, Digital Identity とは, オンライント上の Transaction に関与するある Subject を一意に表現するものである. Digital Identity は, 常にあるデジタルサービスのコンテキストにおいて一意となるが, すべてのコンテキストをまたいで Subject を一意に識別することは要件とはならない. 言い換えれば, デジタルサービスに Access したからといって, Subject の現実世界のアイデンティティが明らかになるとは限らない.

<!-- For these guidelines, digital identity is the unique representation of a subject engaged in an online transaction. A digital identity is always unique in the context of a digital service, but does not necessarily need to uniquely identify the subject in all contexts. In other words, accessing a digital service may not mean that the subject's real-life identity is known. -->

Identity Proofing は, ある Subject が自身で主張する主体であることを証明する行為である. Digital Authentication は, デジタルサービスに Access しようとしている Subject が, 当該 Subject の Digital Identity に紐付けられた正当な Authenticator を管理下に置いていることを証明する行為である. 繰り返し訪問されるサービスにおいて, Authentication に成功するということは, いまサービスに Access している Subject が以前に Access していた Subject と同一であることを, 適切なリスクに基づいて保証されたということである. Digital Identity は, しばしばオープンな Network を介した個人の Proofing を伴い, 政府のデジタルサービスに Access する際にはつねにオープンな Network を介した Subject の Authentication を伴うことから, 技術的課題をもたらす. Digital Identity を確立し利用するための一連のプロセスおよび技術は, なりすましやその他の Attack の機会と隣り合わせである.

<!-- Identity proofing establishes that a subject is who they claim to be. Digital authentication establishes that a subject attempting to access a digital service is in control of one or more valid authenticators associated with that subject's digital identity. For services in which return visits are applicable, successfully authenticating provides reasonable risk-based assurances that the subject accessing the service today is the same as that which accessed the service previously. Digital identity presents a technical challenge because this process often involves proofing individuals over an open network, and always involves the authentication of individual subjects over an open network to access digital government services. The processes and technologies to establish and use digital identities offer multiple opportunities for impersonation and other attacks. -->

本技術ガイドライン群は NIST Special Publication SP 800-63-2 に取って代わる. 各政府機関はこれらのガイドラインを自身のデジタルサービスの Risk Assessment および実装の一部として利用することとなる. 本ガイドライン群では, Identity Assurance を個別要素ごとに分割し, Authentication の誤りがもたらすネガティブインパクトへの対策を提供する. Non-federated なシステムでは, 政府機関はそれらのうち *Identity Assurance Level (IAL)* と *Authenticator Assurance Level (AAL)* という2つの要素を用いるであろう. Federated なシステムでは, それに加えて3つ目の要素となる *Federation Assurance Level (FAL)* も用いることとなろう.

<!-- These technical guidelines supersede NIST Special Publication SP 800-63-2. Agencies use these guidelines as part of the risk assessment and implementation of their digital service(s). These guidelines provide mitigations of an authentication error's negative impacts by separating the individual elements of identity assurance into discrete, component parts. For non-federated systems, agencies will select two components, referred to as *Identity Assurance Level (IAL)* and *Authenticator Assurance Level (AAL)*. For federated systems, agencies will select a third component, *Federation Assurance Level (FAL)*. -->

本ガイドライン群は, 各実装固有の要件を追いやる単一の序数としての Level of Assurance (LOA) というコンセプトを諦め, 適切なビジネスおよびプライバシーに関する Risk Assessment のもと, 各機関が IAL, AAL, FAL を個別に選択するようにする. 多くのシステムで IAL, AAL, FAL がそれぞれ同じレベル値となるとしても, その値自体は要件ではなく, 各機関はいかなるシステムでもこの値が適切であるとみなすべきでもない.

<!-- These guidelines retire the concept of a level of assurance (LOA) as a single ordinal that drives implementation-specific requirements. Rather, by combining appropriate business and privacy risk management side-by-side with mission need, agencies will select IAL, AAL, and FAL as distinct options. While many systems will have the same numerical level for each of IAL, AAL, and FAL, this is not a requirement and agencies should not assume they will be the same in any given system. -->

Identity Assurance の構成要素は以下のガイドライン群に詳しい.

<!-- The components of identity assurance detailed in these guidelines are as follows: -->

* **IAL** は, Identity Proofing プロセスについて述べる.
* **AAL** は, Authentication プロセスについて述べる.
* **FAL** は, Federated な環境において Authentication 情報 (および場合によっては Attribute 情報) を Relying Party (RP) に伝達する Assertion の強度について述べる.

<!-- * **IAL** refers to the identity proofing process.
* **AAL** refers to the authentication process.
* **FAL** refers to the strength of an assertion in a federated environment, used to communicate authentication and attribute information (if applicable) to a relying party (RP). -->

これらのカテゴリーを分割することで, 各機関は Identity ソリューション選択の自由を獲得し, いかなる Assurance Level においても Identity システムの基本要素としてプライバシー強化手法を採用する余地を高める. 例えば, 本ガイドライン群では, 強固な多要素 Authenticator を用いる場合でも, Pseudonymous インタラクションを可能としている. また本ガイドライン群は, Federated Identity Provider (IdP) にデータ問い合わせに関する幅広い選択肢の用意を求め, 識別情報拡散の最小化を推奨している. このような選択肢の例としては, 生年月日をまるごと取得するのではなく, ある年齢より上かどうかを問い合わせられるようにするといったことがあげられる. 各機関が持つ多くのユースケースでは, 個人が完全に識別されていることが求められるであろうが, 本ガイドライン群は可能な限り政府のデジタルサービスへの Pseudonymous Access を推奨する. また完全な識別が必要な場合でも, 収集する Personal Information を最小化することが推奨される.

<!-- The separation of these categories provides agencies flexibility in choosing identity solutions and increases the ability to include privacy-enhancing techniques as fundamental elements of identity systems at any assurance level. For example, these guidelines support scenarios that will allow pseudonymous interactions even when strong, multi-factor authenticators are used. In addition, these guidelines encourage minimizing the dissemination of identifying information by requiring federated identity providers (IdPs) to support a range of options for querying data, such as asserting whether an individual is older than a certain age rather than querying the entire date of birth. While many agency use cases will require individuals to be fully identified, these guidelines encourage pseudonymous access to government digital services wherever possible and, even where full identification is necessary, limiting the amount of personal information collected as much as possible. -->

今日では, 組織における Identity ソリューションは単一システムや同一ベンダーが全機能を提供するといったモノリシックなものとは限らない. Identity サービスのマーケットは細分化され, 組織や機関は標準準拠かつプラガブルな Identity ソリューションを目的に合わせて採用することができるようになっている. そのようなことから, SP 800-63 は一連のドキュメントに分割されたのである. 以降この一連のドキュメント一式を "本ガイドライン群 (the guidelines)" と呼び, 個々のドキュメントは "Vol. (volumes)" と呼ぶ. RP は SP 800-63 を採用することが要求される. 残りの Vol. は, 各機関が求める要素サービスに応じて, 個別に用いても良いし一体的に用いても良い.

<!-- In today's environment, an organization's identity solution need not be a monolith, where one system or vendor provides all functionality. The market for identity services is componentized, allowing organizations and agencies to employ standards-based, pluggable identity solutions based on mission need. As such, SP 800-63 has been split into a suite of documents. The suite as a whole is referred to as "the guidelines," with the individual documents referred to as "volumes." RPs are required to use SP 800-63; the remaining volumes may be used independently or in an integrated fashion, depending on the component service(s) an agency requires. -->

各 Vol. は様々な標準化団体で規範ないしは要件を示す国際的に認められた用語を用いる. 本ガイドライン群で規範的表現を用いるときには, それらは明示的に大文字表記 (CAPITALIZED) することとする. 例えば, SHALL は必須要件を示し, SHOULD は推奨されるが必須ではないということを示す. これらの用語の詳細は, 各ドキュメント冒頭の [Requirements Notation and Conventions](#notation) を参照のこと.

<!-- Each volume has adopted verbs that are internationally recognized in standards organizations as normative and requirements-based. When used in a normative statement in these guidelines, they are CAPITALIZED for ease of identification. For example, SHALL is used to denote a mandatory requirement, while SHOULD refers to a technique, technology, or process that is recommended but not mandatory. For more details on the definitions of these terms see the [Requirements Notation and Conventions](#notation) at the beginning of each document. -->

本ドキュメント群は E-Commerce などの連邦政府以外のアプリケーションにおける標準技術の開発・利用に関して言及することもあるが, 決してそれらのアプリケーションに対してなんらかの制限や制約を課すものではない.

<!-- These documents may inform — but do not restrict or constrain — the development or use of standards for application outside the federal government, such as e-commerce transactions. -->

本ガイドライン群は以下のような構成となっている.

<!-- These guidelines are organized as follows: -->

**SP 800-63 Digital Identity Guidelines** (This document)

SP 800-63 では, 一般的な Identity Framework およびデジタルシステムにおける, Authenticator, Credential, Assertion の利用について概観し, リスクベースプロセスに基づく各 Assurance Level の選択方法について述べる. _SP 800-63 contains both normative and informative material._

<!-- SP 800-63 provides an overview of general identity frameworks, using authenticators, credentials, and assertions together in a digital system, and a risk-based process of selecting assurance levels. _SP 800-63 contains both normative and informative material._ -->

[**SP 800-63A Enrollment and Identity Proofing**](sp800-63a.ja.html)

NIST SP 800-63-A では, Applicant が自身の Identity を提示し, 正当な Subscriber として Identity システムに登録されるまでの一連の流れについて記述する. この Vol. では, Remote と対面の両シナリオにおいて, Applicant が Identity を証明し登録する際のリスクレベルを3段階に分け, それぞれのレベルにおける要件をまとめる. _SP 800-63A contains both normative and informative material._

<!-- NIST SP 800-63-A addresses how applicants can prove their identities and become enrolled as valid subscribers within an identity system. It provides requirements by which applicants can both identity proof and enroll at one of three different levels of risk mitigation in both remote and physically-present scenarios. _SP 800-63A contains both normative and informative material._ -->

SP 800-63A は所与の IAL を満たす要件を決める. 3つの IAL は, Attacker による不正な Identity の主張が成功してしまった場合を想定した各機関によるリスクプロファイリングと被害想定に基づいて, 各機関が選択できる選択肢を示す. 各 IAL は以下のとおりである.

<!-- SP 800-63A sets requirements to achieve a given IAL. The three IALs reflect the options agencies may select from based on their risk profile and the potential harm caused by an attacker making a successful false claim of an identity. The IALs are as follows: -->

**IAL1**: Applicant を特定の現実世界の Identity と紐づける必要はない. Authentication プロセスにおいて提供されるいかなる Attribute も Self-asserted であるものとする. (Credential Service Provider (CSP) が RP に対して Assert する Attribute も含む)

<!-- **IAL1**: There is no requirement to link the applicant to a specific real-life identity. Any attributes provided in conjunction with the authentication process are self-asserted or should be treated as such (including attributes a Credential Service Provider, or CSP, asserts to an RP). -->

**IAL2**: Claimed Identity が現実世界に存在し, Applicant が現実世界の当該 Identity に適切に紐づいていることを検証し, それを証明すること. IAL2 では Remote もしくは対面での Identity Proofing が必要となる. CSP は, 検証済 Attribute を含む Pseudonymous Identity を許容しつつ, RP に対して Attribute を Assert する.

<!-- **IAL2**: Evidence supports the real-world existence of the claimed identity and verifies that the applicant is appropriately associated with this real-world identity. IAL2 introduces the need for either remote or physically-present identity proofing. Attributes can be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. -->

**IAL3**: 対面での Identity Proofing が要求される. 識別に用いられる Attribute は, 認可されトレーニングされた CSP の担当者によって検証される必要がある. IAL2 同様, CSP は, 検証済 Attribute を含む Pseudonymous Identity を許容しつつ, RP に対して Attribute を Assert する.

<!-- **IAL3**: Physical presence is required for identity proofing. Identifying attributes must be verified by an authorized and trained representative of the CSP. As with IAL2, attributes can be asserted by CSPs to RPs in support of pseudonymous identity with verified attributes. -->


[**SP 800-63B Authentication and Lifecycle Management**](sp800-63b.ja.html)

繰り返し訪問されるサービスにおいては, Authentication に成功することで, 今日当該サービスに Access している Subscriber が以前にサービスに Access してきた人物と同一であることが, 適切なリスクのもとで確かめられる. この信頼の頑健性は AAL カテゴリーによって記述される. NIST SP 800-63B では, デジタルサービスに Access する個人が CSP に対してセキュアに Authenticate されるプロセスを扱う. _SP 800-63B contains both normative and informative material._

<!-- For services in which return visits are applicable, a successful authentication provides reasonable risk-based assurances that the subscriber accessing the service today is the same as that which accessed the service previously. The robustness of this confidence is described by an AAL categorization. NIST SP 800-63B addresses how an individual can securely authenticate to a CSP to access a digital service or set of digital services. _SP 800-63B contains both normative and informative material._ -->

3つの AAL は, Attacker が Authenticator を手中に収め政府機関のシステムに Access できてしまった場合を想定した各機関によるリスクプロファイリングと被害想定に基づいて, 各機関が選択できる選択肢のサブセットを定義する. 各 AAL は以下のとおりである.

<!-- The three AALs define the subsets of options agencies can select based on their risk profile and the potential harm caused by an attacker taking control of an authenticator and accessing agencies' systems. The AALs are as follows: -->

**AAL1**: AAL1 では, Claimant が Subscriber のアカウントに紐づく Authenticator を管理下に置いているということが, ある程度の確度で保証される. AAL1 では Single-facgtor ないしは Multi-factor Authenticator が求められるが, それらの Authenticator では幅広い種類の Authentication テクノロジーが利用可能である. Authentication を成功させるには, セキュアな Authentication Protocol によって Claimant が Authenticator を保持し管理下に置いていることを証明する必要がある.

<!-- **AAL1**: AAL1 provides some assurance that the claimant controls an authenticator bound to the subscriber's account. AAL1 requires either single-factor or multi-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove possession and control of the authenticator through a secure authentication protocol. -->

**AAL2**: AAL2 では, Claimant が Subscriber のアカウントに紐づく Authenticator を管理下に置いているということが, 高い確度で保証される. セキュアな Authentication Protocol によって, [2つの異なる Authentication Factor](#mfa-definition) を所有し管理下に置いていることを証明する必要がある. AAL2 以上では, [Approved Cryptographic](#approved) テクノロジーも必要となる.

<!-- **AAL2**: AAL2 provides high confidence that the claimant controls authenticator(s) bound to the subscriber's account. Proof of possession and control of [two distinct authentication factors](#mfa-definition) is required through secure authentication protocol(s). [Approved cryptographic](#approved) techniques are required at AAL2 and above. -->

**AAL3**: AAL3 では, Claimant が Subscriber のアカウントに紐づく Authenticator を管理下に置いているということが, 非常に高い確度で保証される. AAL3 の Authentication は, 暗号プロトコルによる鍵所有証明 (Proof of Possession) に基づいている. AAL3 の Authentication ではハードウェアベースの Cryptographic Authenticator および Verifier Inpersonation 耐性のある Authenticator の利用が必須となる (SHALL). 同一デバイスがこれらの要件を同時に満たしてもよい (MAY). AAL3 で Authenticate するには, セキュアな Authentication Protocol によって, Claimant が [2つの異なる Authentication Factor](#mfa-definition) を所有し管理下に置いていることを証明する必要がある (SHALL). [Approved Cryptographic](#approved) テクノロジーも必要となる.

<!-- **AAL3**: AAL3 provides very high confidence that the claimant controls authenticator(s) bound to the subscriber's account. Authentication at AAL3 is based on proof of possession of a key through a cryptographic protocol. AAL3 authentication SHALL use a hardware-based cryptographic authenticator and an authenticator that provides verifier impersonation resistance; the same device MAY fulfill both these requirements. In order to authenticate at AAL3, claimants SHALL prove possession and control of [two distinct authentication factors](#mfa-definition) through secure authentication protocol(s). [Approved cryptographic](#approved) techniques are required. -->

[**SP 800-63C Federation and Assertions**](sp800-63c.ja.html)

NIST SP 800-63C では, Federated Identity アーキテクチャーを採用したり, Authentication プロセスの結果と関連する Identity 情報を機関のアプリケーションに伝送する際に Assertion を利用するにあたっての要件について述べる. さらにこの Vol. では, 正当かつ Authenticated な Subject についての情報を共有する際のプライバシー強化手法や, Subject が Pseudonymous なまま強固な Multi-factor Authentication (MFA) を行う手法についても述べる. _SP 800-63C contains both normative and informative material._

<!-- NIST SP 800-63C provides requirements when using federated identity architectures and assertions to convey the results of authentication processes and relevant identity information to an agency application. In addition, this volume offers privacy-enhancing techniques to share information about a valid, authenticated subject and describes methods that allow for strong multi-factor authentication (MFA) while the subject remains pseudonymous to the digital service. _SP 800-63C contains both normative and informative material._ -->

3つの FAL は, Attacker が Federated Transaction をコントロールできる状況に陥った場合を想定した各機関によるリスクプロファイリングと被害想定に基づいて, 各機関が選択できる選択肢を示す. 各 FAL は以下のとおりである.

<!-- The three FALs reflect the options agencies can select based on their risk profile and the potential harm caused by an attacker taking control of federated transactions. The FALs are as follows: -->

**FAL1**: Subscriber は RP が Bearer Assertion を受け取ることを許容することができる. Assertion は Approved Cryptography を用いて IdP によって署名される.

<!-- **FAL1**: Allows for the subscriber to enable the RP to receive a bearer assertion. The assertion is signed by the IdP using approved cryptography. -->

**FAL2**: 上記に加え, Assertion は Approved Cryptography によって暗号化され, RP 以外が復号できないようになっていなければならない.

<!-- **FAL2**: Adds the requirement that the assertion be encrypted using approved cryptography such that the RP is the only party that can decrypt it. -->

**FAL3**: Subscriber は Assertion Artifact に加え, Assertion が参照する Cryptographic Key の所有証明 (Proof of Possession) を提示する必要がある. Assertion は Approved Cryptography を用いて IdP によって署名され, RP に向けて暗号化されている必要がある.

<!-- **FAL3**: Requires the subscriber to present proof of possession of a cryptographic key referenced in the assertion in addition to the assertion artifact itself. The assertion is signed by the IdP and encrypted to the RP using approved cryptography. -->

本ガイドライン群は, 各機関が構築ないし調達可能な幅広い Identity サービスのアーキテクチャーについて感知しているわけではなく, 機関がどのようなアプローチをとったとしても適用できることを目的としている. しかしながら, 各機関が可能な場合には Federation を用いることを推奨し, Federated アーキテクチャーを採用する際に IAL, AAL, FAL をうまく組み合わせられるよう意図している. Federation は, 連邦政府の人々が政府のデジタルサービスに Access する際に Privacy を強化するための鍵となる.

<!-- These guidelines are agnostic to the vast array of identity service architectures that agencies can develop or acquire, and are meant to be applicable regardless of the approach an agency selects. However, agencies are encouraged to use federation where possible, and the ability to mix and match IAL, AAL, and FAL is simplified when federated architectures are used. Further, federation is a keystone in the ability to enhance the privacy of the federal government's constituents as they access valuable government digital services. -->

<div class="breaker"/>

## Table of Contents

[1. Purpose](#sec1)

[2. Introduction](#sec2)

[3. Definitions and Abbreviations](#sec3)

[4. Digital Identity Model](#sec4)

[5. Digital Identity Risk Management](#sec5)

[6. Selecting Assurance Levels](#sec6)

[7. Federation Considerations](#sec7)

[8. References](#references)

[Appendix A &mdash; Definitions and Abbreviations](#def-and-acr)
