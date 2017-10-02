<a name="sec1"></a>

<div class="breaker"></div>

## 1 <a name="purpose"></a>Purpose

This section is informative.

本リコメンデーションおよび [Special Publication (SP) 800-63A](sp800-63a.ja.html), [SP 800-63B](sp800-63b.ja.html), [SP 800-63C](sp800-63c.ja.html) は, 政府機関に対して Digital Authentication の実装に際した技術的なガイドラインを提示する.

<!-- This recommendation and its companion volumes, [Special Publication (SP) 800-63A](sp800-63a.html), [SP 800-63B](sp800-63b.html), and [SP 800-63C](sp800-63c.html), provide technical guidelines to agencies for the implementation of digital authentication. -->

<a name="sec2"></a>

## 2 <a name="intro"></a>Introduction

*This section is informative.*

Digital Identity はオンライン Transaction に関与する Subject を一意に表現するものである. Digital Identity は常にデジタルサービスのコンテキスト内でユニークであるが, 必ずしもあらゆるコンテキストをまたいで一意に Subject を識別するものである必要はない. 言い換えれば, あるデジタルサービスに Access する際に, Subject の現実世界での Identity を知る必要はないのである. Identity Proofing は, Subject が確かに自身が主張するものであるということを確立する. Digital Authentication は, Digital Identity を主張するために1つ以上の Authenticator の有効性を判断するプロセスである. Authentication により, あるデジタルサービスに Access しようとしている Subject が Authenticate のためのテクノロジーを管理下に置いていることが明らかになる. Authentication に成功すると, サービスに Access している Subject が以前に当該サービスに Access した主体と同一であることが, 適度なリスクベースの確からしさが得られる. Digital Identity に対するこういったプロセスにおいては, 個人に対してオープンな Network 越しに Proofing を行い, 典型的には個々の Subject がデジタル政府サービスにアクセスする際にオープンな Network 越しに Authentication を行うことになるため, Digital Identity には技術的なチャレンジがつきものである. そこでは, なりすましやその他の Attack など, 不正に他の Subject であると主張する機会が様々ある.

<!-- Digital identity is the unique representation of a subject engaged in an online transaction. A digital identity is always unique in the context of a digital service, but does not necessarily need to uniquely identify the subject in all contexts. In other words, accessing a digital service may not mean that the subject's real-life identity is known. Identity proofing establishes that a subject is who they claim to be. Digital authentication is the process of determining the validity of one or more authenticators used to claim a digital identity. Authentication establishes that a subject attempting to access a digital service is in control of the technologies used to authenticate. Successful authentication provides reasonable risk-based assurances that the subject accessing the service today is the same as that which previously accessed the service. Digital identity presents a technical challenge because this process often involves  proofing  individuals over an open network, and typically involves the authentication of individual subjects over an open network to access digital government services. There are multiple opportunities for impersonation and other attacks that fraudulently claim another subject's digital identity. -->

本リコメンデーションは, 各機関に対して, 政府システムにおいて Subject を Network 越しに Digital Authentication する際の技術的ガイドラインを提供する. 本リコメンデーションは Credential Service Provider (CSP), Verifier, Relying Party (RP) 向けのガイドラインも提供する.

<!-- This recommendation provides agencies with technical guidelines for digital authentication of subjects to federal systems over a network. This recommendation also provides guidelines for credential service providers (CSPs), verifiers, and relying parties (RPs). -->

本ガイドライン群では, 適切な Digital Identity サービスの選択に際する Risk Management プロセスや, Identity Assurance Level, Authenticator Assurance Level, Federation Assurance Level をリスクに基づいて実装する際の詳細について述べる. 本ガイドライン群が提供する Risk Assessment ガイダンスは, *NIST Risk Management Framework* [[NIST RMF]](#NIST-RMF) およびその構成要素となる Special Publication を補完するものとなる. 本ガイドラインは各機関にさらなる Risk Management プロセスを課すものではなく, 全ての関連する RMF ライフサイクルフェーズ実行に際する Digital Identity のリスクに関しての具体的なガイダンスを提供するものである.

<!-- These guidelines describe the risk management processes for selecting appropriate digital identity services and the details for implementing identity assurance, authenticator assurance, and federation assurance levels based on risk. Risk assessment guidance in these guidelines supplements the *NIST Risk Management Framework* [[NIST RMF]](#NIST-RMF) and its component special publications. This guideline does not establish additional risk management processes for agencies. Rather, requirements contained herein provide specific guidance related to digital identity risk while executing all relevant RMF lifecycle phases. -->

Digital Authentication は, 個人の情報への Unauthorized Access のリスクを軽減することによりプライバシー保護に寄与する. しかしながら同時に, Identity Proofing, Authentication, Authorization, Federation といった個々のフェーズにおいて個人の情報を扱うため, プライバシーリスクをもたらすことにもなる. したがって本ガイドライン群は, 潜在的に関連するプライバシーリスクを軽減するためのプライバシー要件や検討事項を含む.

<!-- Digital authentication supports privacy protection by mitigating risks of unauthorized access to individuals' information. At the same time, because identity proofing, authentication, authorization, and federation involve the processing of individuals' information, these functions can also create privacy risks. These guidelines therefore include privacy requirements and considerations to help mitigate potential associated privacy risks. -->

本ガイドライン群は, Identity Assurance を個別要素ごとに分割することで, Authentication の誤りがもたらすネガティブインパクトの軽減に寄与する. Non-federated なシステムでは, 各機関はそれらのうち *Identity Assurance Level (IAL)* と *Authenticator Assurance Level (AAL)* という2つの要素を用いるであろう. Federated なシステムでは, それに加えて3つ目の要素となる *Federation Assurance Level (FAL)* も用いることとなろう. [Section 5, Digital Identity Risk Management](#sec5) では Risk Assesment プロセスの詳細について述べる. [Section 6, Selecting Assurance Levels](#sec6) は, Risk Assessment の結果と追加のコンテキストをふまえ, 機関によるリスクに応じた適切な IAL, AAL, FAL の選択の一助となる.

<!-- These guidelines support the mitigation of the negative impacts induced by an authentication error by separating the individual elements of identity assurance into discrete, component parts. For non-federated systems, agencies will select two components, referred to as *Identity Assurance Level (IAL)* and *Authenticator Assurance Level (AAL)*. For federated systems, a third component, *Federation Assurance Level (FAL)*, is included. [Section 5, Digital Identity Risk Management](#sec5) provides details on the risk assessment process. [Section 6, Selecting Assurance Levels](#sec6) combines the results of the risk assessment with additional context to support agency selection of the appropriate IAL, AAL, and FAL combinations based on risk. -->

本ガイドライン群は, 実装固有の要件をもたらす単一の序数としての Level of Assurance (LOA) を構成するものではなく, ビジネス, セキュリティー, プライバシーのための適切な Risk Management をミッションニーズと組み合わせ, 各機関が個別に IAL, AAL, FAL を選択するためのものである. 特に本ドキュメントは, 各政府機関が以前利用し OMB M-04-04 でも述べられている4つの LOA モデルを認めず, 各機関が実施している各機能ごとに個別に各レベルを選択するよう求めている. 多くのシステムで IAL, AAL, FAL がそれぞれ同じレベル値となるとしても, その値自体は要件ではなく, 各機関はいかなるシステムでもこの値が適切であるとみなすべきでもない.

<!-- These guidelines do not consider nor result in a composite level of assurance (LOA) in the context of a single ordinal that drives implementation-specific requirements. Rather, by combining appropriate risk management for business, security, and privacy side-by-side with mission need, agencies will select IAL, AAL, and FAL as distinct options. Specifically, this document does not recognize the four LOA model previously used by federal agencies and described in OMB M-04-04, instead requiring agencies to individually select levels corresponding to each function being performed. While many systems will have the same numerical level for each IAL, AAL, and FAL, this is not a requirement, and agencies should not assume they will be the same in any given system or application. -->

本ガイドライン群において詳しく扱う Identity Assurance の構成要素は以下の通りである.

<!-- The components of identity assurance detailed in these guidelines are as follows: -->

* **IAL** は, Identity Proofing プロセスについて述べる.
* **AAL** は, Authentication プロセスについて述べる.
* **FAL** は, Federated な環境において Authentication 情報 (および場合によっては Attribute 情報) を Relying Party (RP) に伝達する Assertion Protocol について述べる.

<!-- * **IAL** refers to the identity proofing process.
* **AAL** refers to the authentication process.
* **FAL** refers to the assertion protocol used in a federated environment to communicate authentication and attribute information (if applicable) to an RP. -->

SP 800-63 は以下のような一連の Vol. から構成される.

<!-- As such, SP 800-63 is organized as a suite of volumes as follows: -->

SP 800-63 *Digital Identity Guidelines*:　SP 800-63 では, Risk Assesment の方法論, デジタルシステムにおける Authenticator, Credential, Assertion を利用した一般的な Identity Framework の概観, およびリスクベースプロセスに基づく各 Assurance Level の選択方法について述べる. _SP 800-63 contains both normative and informative material._

<!-- SP 800-63 *Digital Identity Guidelines*: Provides the risk assessment methodology and an overview of general identity frameworks, using authenticators, credentials, and assertions together in a digital system, and a risk-based process of selecting assurance levels. _SP 800-63 contains both normative and informative material._ -->

SP 800-63A *Enrollment and Identity Proofing*: NIST SP 800-63-A では, Applicant が自身の Identity を証明し, 正当な Subscriber として Identity システムに登録されるまでの一連の流れについて記述する. この Vol. では, Remote と対面の両シナリオにおいて, Applicant が Identity を証明し登録する際のリスクレベルを3段階に分け, それぞれのレベルにおける要件をまとめる. _SP 800-63A contains both normative and informative material._

<!-- SP 800-63A *Enrollment and Identity Proofing*: Addresses how applicants can prove their identities and become enrolled as valid subjects within an identity system. It provides requirements for processes by which applicants can both proof and enroll at one of three different levels of risk mitigation in both remote and physically-present scenarios. _SP 800-63A contains both normative and informative material._ -->

SP 800-63B *Authentication and Lifecycle Management*: NIST SP 800-63B では, デジタルサービスに Access する個人が CSP に対してセキュアに Authenticate されるプロセスを扱う. 本 Vol. では Authenticator を Identity に紐づけるプロセスについても記述する. _SP 800-63B contains both normative and informative material._

<!-- SP 800-63B *Authentication and Lifecycle Management*: Addresses how an individual can securely authenticate to a CSP to access a digital service or set of digital services. This volume also describes the process of binding an authenticator to an identity. _SP 800-63B contains both normative and informative material._ -->

SP 800-63C *Federation and Assertions*: NIST SP 800-63C では, Federated Identity アーキテクチャーを採用したり, Authentication プロセスの結果と関連する Identity 情報を機関のアプリケーションに伝送する際に Assertion を利用するにあたっての要件について述べる. さらにこの Vol. では, 正当かつ Authenticated な Subject についての情報を共有する際のプライバシー強化手法や, Subject が Pseudonymous なまま強固な Multi-factor Authentication (MFA) を行う手法についても述べる. _SP 800-63C contains both normative and informative material._

<!-- SP 800-63C *Federation and Assertions*: Provides requirements on the use of federated identity architectures and assertions to convey the results of authentication processes and relevant identity information to an agency application. Further, this volume offers privacy-enhancing techniques to share information about a valid, authenticated subject, and describes methods that allow for strong multi-factor authentication (MFA) while the subject remains pseudonymous to the digital service. _SP 800-63C contains both normative and informative material._ -->

NIST では, 本ガイドライン群中の個々の Vol. が非同期に改訂されることを想定している. いかなる場合でも, 各 Vol. のもっとも最新のリビジョンを用いること (e.g., ある時点において SP 800-63A-1 および SP 800-63B-2 がそれぞれの最新リビジョンであれば, 互いのリビジョン番号がずれていたとしてもそれらを同時に利用するべきである). 互換性エラーを最小化するため, ベースドキュメント (i.e., SP 800-63-3 ではなく SP 800-63) は常に本ドキュメントの最新バージョンを参照することとする.

<!-- NIST anticipates that individual volumes in these guidelines will be revised asynchronously. At any time, the most recent revision of each should be used (e.g., if at a time in the future SP 800-63A-1 and SP 800-63B-2 are the most recent revisions of each volume, they should be used together even though the revision numbers do not match). To minimize the risk of compatibility errors, a reference to the base document (i.e., SP 800-63 rather than SP 800-63-3) always refers to the current version of the document. -->

下表は, 本 Vol. のどのセクションが Normative (規範) であり, どのセクションが Informative (参考) であるかを示している.

<!-- The following table states which sections of this volume are normative and which are informative: -->

|Section Name|Normative/Informative|
|----|:--:|
|1. Purpose|Informative|
|2. Introduction|Informative|
|3. Definitions and Abbreviations|Informative|
|4. Digital Identity Model|Informative|
|5. Digital Identity Risk Management|Normative|
|6. Selecting Assurance Levels|Normative|
|7. Federation Considerations|Informative|
|8. References|Informative|

### 2.1 Applicability

全てのデジタルサービスが Authentication や Identity Proofing を必要とするわけではないが, 本ガイダンスはサービス対象 (e.g. 市民, ビジネスパートナー, 政府機関) によらず Digital Identity や Authentication が必要な全ての Transaction に適用される.

<!-- Not all digital services require authentication or identity proofing; however, this guidance applies to all such transactions for which digital identity or authentication are required, regardless of the constituency (e.g. citizens, business partners, government entities). -->

44 U.S.C. § 3542(b)(2) で定義される国家安全システム関連の Transaction は, 本ガイダンスでは扱わない. プライベートセクター組織や州, 地域, 部族政府は, 自身のデジタルプロセスが多様な Assurance Level を要求するものであれば, 適切な箇所で本標準を採用することを検討しても良い.

<!-- Transactions not covered by this guidance include those associated with national security systems as defined in 44 U.S.C. § 3542(b)(2). Private sector organizations and state, local, and tribal governments whose digital processes require varying levels of assurance may consider the use of these standards where appropriate. -->

本ガイドライン群は, 市民が社会福祉サービスにアクセスしたり, プライベートセクターのパートナーが情報共有コラボレーションスペースにアクセスするなど, 主に連邦政府以外の主体と対話を行う機関サービスにフォーカスしている. しかしながら, 機関の従業員や契約業者がアクセスする内部システムにも適用される. こういったユーザーは, 主として Personal Identity Verification (PIV) カードないしはそれから派生した PIV といった, 正当な政府発行 Credential を保持しているものと期待される. したがって [SP 800-63A](sp800-63a.html) および [SP 800-63B](sp800-63b.html) は [FIPS 201](#FIPS201) およびその関連 Special Publication の要件および組織固有の指示に次ぐ二時的存在となる. しかしながら [SP 800-63C](sp800-63c.html) およびリスクベースによる適切な FAL の選択は, 内部ユーザーの持つ Credential タイプに関係なく適用される. 各機関は FAL を選択することで, 各アプリケーションのシステムリスクに応じた PIV 採用方法について, ガイダンスと柔軟性を得ることができる.

<!-- These guidelines primarily focus on agency services that interact with the non-federal workforce, such as citizens accessing benefits or private sector partners accessing information sharing collaboration spaces. However, it also applies to internal agency systems accessed by employees and contractors. These users are expected to hold a valid government-issued credential, primarily the Personal Identity Verification (PIV) card or a derived PIV. Therefore [SP 800-63A](sp800-63a.html) and [SP 800-63B](sp800-63b.html) are secondary to the requirements of [FIPS 201](#FIPS201) and its corresponding set of special publications and agency-specific instructions. However, [SP 800-63C](sp800-63c.html) and the risk-based selection of an appropriate FAL applies, regardless of the credential type the internal user holds. FAL selection provides agencies guidance and flexibility in how to PIV-enable their applications based on system risk. -->

### 2.2 Considerations, Other Requirements, and Flexibilities

各機関はここに指定されていない他のリスク軽減策および補完的統制を採用してもよい. ただし採用するいかなる対策および補完的統制も, 自身が選択した Assurance Level のセキュリティー・プライバシー保護レベルを低下させることがないよう保証すること. 各機関はデジタルサービスの機能を分割し, センシティブでない機能を, より低い Authentication Assurance Level および Identity Assurance Level のもとで提供することを検討してもよい.

<!-- Agencies may employ other risk mitigation measures and compensating controls not specified herein. Agencies need to ensure that any mitigations and compensating controls do not degrade the selected assurance level's intended security and privacy protections. Agencies may consider partitioning the functionality of a digital service to allow less sensitive functions to be available at a lower level of authentication and identity assurance. -->

各機関は, 自身の Risk Analysis を元に, 特定のコンテキストでは追加の措置を行うよう取り決めても良い. 特に, プライバシー要件と法的リスクにより, 追加の Authentication 措置やその他のプロセス保護が望ましいとすることもあるであろう. Digital Authentication プロセスや Digital Authentication システムを構築する際には, 各機関は *OMB Guidance for Implementing the Privacy Provisions of the E-Government Act of 2002* [[M-03-22]](#M-03-22) を参照すべきである. また, 特に 1) Proofing の法的基準への準拠や, 2) 否認防止といったニーズに関連する法的リスクに関する追加情報は *Use of Electronic Signatures in Federal Organization Transactions* [[ESIG]](#ESIG) を参照のこと.

<!-- Agencies may determine based on their risk analysis that additional measures are appropriate in certain contexts. In particular, privacy requirements and legal risks may lead agencies to determine that additional authentication measures or other process safeguards are appropriate. When developing digital authentication processes and systems, agencies should consult *OMB Guidance for Implementing the Privacy Provisions of the E-Government Act of 2002* [[M-03-22]](#M-03-22). See the *Use of Electronic Signatures in Federal Organization Transactions* [[ESIG]](#ESIG) for additional information on legal risks, especially those related to the need to 1) satisfy legal standards of proof and 2) prevent repudiation. -->

さらに, 本ガイドライン群を実装する政府機関は, Federal Information Security Modernization Act (FISMA) of 2014, 44 U.S.C. § 3551 et seq., Public Law (P.L.) 113-283 [[FISMA]](#FISMA), および関連する NIST 標準およびガイドラインに基づく法定責任に準拠すべきである. FISMA は連邦政府機関に対して, 機関の業務と資産を支える情報およびシステムのセキュリティーを担保する, 機関全体にわたるプログラムを開発, 文書化, 実装するよう指示している. これには Digital Authentication を支える IT システムの Security Authorization and Accreditation (SA&A) を含む. NIST は, 本ガイドライン群を実装する非連邦政府主体に対して, デジタルシステムのセキュアな運用を確実なものにするべく, 上記と等価な標準に従うよう推奨している.

<!-- Additionally, federal agencies implementing these guidelines should adhere to their statutory responsibilities under the Federal Information Security Modernization Act (FISMA) of 2014, 44 U.S.C. § 3551 et seq., Public Law (P.L.) 113-283 [[FISMA]](#FISMA), and related NIST standards and guidelines. FISMA directs federal agencies to develop, document, and implement agency-wide programs to provide security for the information and systems that support the agency's operations and assets. This includes the security authorization and accreditation (SA&A) of IT systems that support digital authentication. NIST recommends that non-federal entities implementing these guidelines follow equivalent standards to ensure the secure operations of their digital systems. -->

### 2.3 A Few Limitations

Authenticator によってはデジタル Access のみならず物理的 Access 時の Authentication の為にも利用可能なものもあるが, 本技術ガイドライン群は物理的 Access (e.g., ビル入館) に際する Subject の Authentication に関しては扱わない. さらに, 本ガイドライン群の本リビジョンでは, しばしば Machine-to-Machene (Router-to-Router など) Authentication や相互接続デバイスと呼ばれ, 一般的には Internet of Things (IoT) とも呼ばれる Device Identity については明示的には扱わない. つまり, 本ガイドライン群は可能な限り一般的 Subject について言及し, デバイスへの適用可能性を残している. また対人間の Authentication Protocol でデバイスを用いる際に, デバイスに Authenticator を発行する固有の要件についても除外されている.

<!-- These technical guidelines do not address the authentication of subjects for physical access (e.g., to buildings), though some authenticators used for digital access may also be used for physical access authentication. Additionally, this revision of these guidelines does not explicitly address device identity, often referred to as machine-to-machine (such as router-to-router) authentication or interconnected devices, commonly referred to as the internet of things (IoT). That said, these guidelines are written to refer to generic subjects wherever possible to leave open the possibility for applicability to devices. Also excluded are specific requirements for issuing authenticators to devices when they are used in authentication protocols with people. -->

### 2.4 How to Use this Suite of SPs

Identity サービスを提供する際のビジネスモデル, マーケットプレイス, 構成は, 最初のバージョンの SP 800-63 がリリースされて以降, 劇的に変化している. 特に CSP はコンポーネント化され, 独立して運営・保有される複数のビジネス主体により構成されるケースも出てきた. さらに Identity Proofing が必要ないケースでも強固な Authenticator を利用する大きなセキュリティー上の利点もありうる. したがって本リビジョンでは, 800-63 という呼称の元に一連の SP を置き, 上記のような新しいモデルを促進し, 全体の Digital Identity モデルの中である主体が提供可能な機能に対する特定の要件に容易にたどり着けるようにしている.

<!-- The business model, marketplace, and composition of how identity services are delivered has drastically changed since the first version of SP 800-63 was released. Notably, CSPs can be componentized and comprised of multiple independently-operated and owned business entities. Further, there may be a significant security benefit to using strong authenticators even if no identity proofing is required. Therefore, in this revision, a suite of SPs under the 800-63 moniker has been created to facilitate these new models and make it easy to access the specific requirements for the function an entity may serve under the overall digital identity model. -->

### 2.5 Change History

#### 2.5.1 SP 800-63-1

NIST SP 800-63-1 は, 最新の Authenticator ("Token" と呼ばれた) 技術を反映し, 今日使われている Digital Identity アーキテクチャーモデルをよりよく理解すべく, NIST SP 800-63 を改訂したものである. 追加の (最小限の) 技術要件が, CSP, Authentication 情報伝達プロトコル, および Digital Identity モデル中で利用されていれば Assertion に対して規定された.

<!-- NIST SP 800-63-1 updated NIST SP 800-63 to reflect current authenticator (then referred to as "token") technologies and restructured it to provide a better understanding of the digital identity architectural model used here. Additional (minimum) technical requirements were specified for the CSP, protocols used to transport authentication information, and assertions if implemented within the digital identity model. -->

#### 2.5.2 SP 800-63-2

NIST SP 800-63-2 は SP 800-63-1 の限定的アップデートであり, 実質的変更は Section 5 *Registration and Issuance Processes* のみであった. 改訂 Draft の実質的変更は, Identity Proofing プロセスにおいて専門資格の使用を促進し, Level 3 の Remote Registration における Credential 発行のため Address of Record に郵便を送る必要性を低減させることを意図したものであった. Section 5 のその他の変更は, 軽微な説明と明確化であった.

<!-- NIST SP 800-63-2 was a limited update of SP 800-63-1 and substantive changes were made only in Section 5, *Registration and Issuance Processes*. The substantive changes in the revised draft were intended to facilitate the use of professional credentials in the identity proofing process, and to reduce the need to send postal mail to an address of record to issue credentials for level 3 remote registration. Other changes to Section 5 were minor explanations and clarifications. -->

#### 2.5.3 SP 800-63-3

NIST SP 800-63-3 は SP 800-63-2 の大幅なアップデートと再構成を伴っている. SP 800-63-3 では Digital Authentication Assurance の個々の構成要素となる AAL, IAL, FAL を導入し, Authentication の強度と個々の Claimed Identity の確実性を独立して扱いたい (e.g., 強固な Pseudonymous Authentication) という高まる要求に応えている. 本ガイドラインには, Risk Assessment 方法論とその IAL, AAL, FAL への適用が含まれる. SP 800-63-3 では, SP 800-63 がカバーする Digital Identity ガイダンス全体を, Authentication について述べる単一のドキュメントから, (上述の個々の構成要素に個別に対処するべく) SP 800-63-3 をトップレベルのドキュメントとする一連の4つのドキュメント群へと分割する.

<!-- NIST SP 800-63-3 is a substantial update and restructuring of SP 800-63-2. SP 800-63-3 introduces individual components of digital authentication assurance &mdash; AAL, IAL, and FAL &mdash; to support the growing need for independent treatment of authentication strength and confidence in an individual's claimed identity (e.g., in strong pseudonymous authentication). A risk assessment methodology and its application to IAL, AAL, and FAL has been included in this guideline. It also moves the whole of digital identity guidance covered under SP 800-63 from a single document describing authentication to a suite of four documents (to separately address the individual components mentioned above) of which SP 800-63-3 is the top-level document. -->

800-63-3 でのその他の変更点は以下の通りである.

<!-- Other areas updated in 800-63-3 include: -->

- Identity Proofing および Federation をスコープに含めていることを正しく示すべく, "Digital Identity Guidelines" に改名し, 将来のリビジョンで Device Identity や Machine-to-Machene Authentication を扱えるようスコープを拡大する余地を含めた.
- Assertion 技術における *Token* との混同を避けるため *Token* の代わりに *Authenticator* という用語を用いるなど, 用語変更を行った.
- Authentication および Assertion の要件を更新し, セキュリティー技術および脅威の進化を反映した.
- Verifier が Long-term Secret を保管する際の要件を定めた.
- Identity Proofing モデルを再構成した.
- Remote Identity Proofing に関連する要件を更新した.
- 独立したチャネルやデバイスを "something you have" として用いるということを明確化した.
- 事前登録済の Knowledge Token (Autnenticator) は, (時として非常に弱い) パスワードの特別な形態という認識のもと **削除** した.
- Authenticator の紛失や盗難時のアカウントリカバリーに関する要件を定めた.
- Out-of-band Authenticator 用の有効なチャネルとしての Email を **削除** した.
- Re-authentication やセッションマネージメントに関するより深い議論を追加した.
- Identity Federation に関するより深い議論を追加し, Federation コンテキストにおける Assertion の再構成を行った.

<!-- - Renamed to "Digital Identity Guidelines" to properly represent the scope includes identity proofing and federation, and to support expanding the scope to include device identity, or machine-to-machine authentication in future revisions.
- Terminology changes, including the use of *authenticator* in place of *token* to avoid conflicting use of the word *token* in assertion technologies.
-	Updates to authentication and assertion requirements to reflect advances in both security technology and threats.
-	Requirements on the storage of long-term secrets by verifiers.
-  Restructured identity proofing model.
-	Updated requirements regarding remote identity proofing.
-	Clarification on the use of independent channels and devices as "something you have".
-	**Removal** of pre-registered knowledge tokens (authenticators), with the recognition that they are special cases of (often very weak) passwords.
-	Requirements regarding account recovery in the event of loss or theft of an authenticator.
-	**Removal** of email as a valid channel for out-of-band authenticators.
-   Expanded discussion of reauthentication and session management.
-   Expanded discussion of identity federation; restructuring of assertions in the context of federation. -->
