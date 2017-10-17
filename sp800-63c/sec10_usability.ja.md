<div class="breaker"></div>

<a name="usability"></a>

## 10 Usability Considerations

*This section is informative.*

[ISO/IEC 9241-11](#ISO9241-11) はユーザビリティーを "特定のユーザーが特定の利用コンテキストにおいて,  有効, 効率的かつ満足できる程度に特定の目的を達成するためにプロダクトを利用できる程度" と定義している. この定義は, 有効性, 効率性, 満足度を達成するために必要な主要因として, ユーザーと目標, 利用コンテキストに着目している. ユーザビリティーを達成するには, これらのキー要素を考慮した全体的アプローチが必要である.

<!-- [ISO/IEC 9241-11](#ISO9241-11) defines usability as the "extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency and satisfaction in a specified context of use." This definition focuses on users, goals, and context of use as key elements necessary for achieving effectiveness, efficiency and satisfaction. A holistic approach considering these key elements is necessary to achieve usability. -->

ユーザビリティーの観点からは, Federated Identity システムの最大の潜在的メリットの一つとして, 複数の Authentictor を管理することに関連するユーザーの疲労という問題への取り組みがあげられる. 歴史的にこれはユーザーネームとパスワードの問題であったが, ユーザーが Authenticator を管理する必要性が向上するにつれ, それが物理的なものでもデジタルなものでも, ユーザビリティーの課題が立ちはだかるようになった.

<!-- From the usability perspective, one of the major potential benefits of federated identity systems is to address the problem of user fatigue associated with managing multiple authenticators. While this has historically been a problem with usernames and passwords, the increasing need for users to manage many authenticators — whether physical or digital — presents a usability challenge. -->

多くの他の Authentication へのアプローチが, 広範囲に研究され, かつ確立されたユーザビリティーガイドラインを持っているが, Federated Identity はより新しく, 従って研究結果の深さと決定性が不足している. 進行中のユーサビリティー研究が成熟するにつれ, Federated Identity システムに関するユーザビリティーガイドラインはより強力な支援データを持つこととなろう. 例えば, 技術的 Attribute の名前と値をユーザーフレンドリーな言語に翻訳するガイダンスを指示するには, さらなるデータが必要である.

<!-- While many other approaches to authentication have been researched extensively and have well-established usability guidelines, federated identity is more nascent and, therefore, lacks the depth and conclusiveness of research findings. As ongoing usability research matures, usability guidelines for federated identity systems will have stronger supporting data. For example, additional data is needed to support guidance on the translation of technical attribute names and values into user-friendly language. -->

800-63A と 800-63B のユーサビリティーセクションで述べたように, いかなる Authentication 手法においても全体のユーザーエクスペリエンスは不可欠である. Federation は多くのユーザーにとってまだ慣れないインタラクションパラダイムであるため, これは Federated Identity システムにおいては特に当てはまる. ユーザーの過去の Authentication 経験は, ユーザーの期待に影響を及ぼしうる.

<!-- As stated in the usability sections in 800-63A and 800-63B, overall user experience is critical to the success of any authentication method. This is especially true for federated identity systems as federation is a less familiar user interaction paradigm for many users. Users' prior authentication experiences may influence their expectations. -->

Federated Identity システムにおける全体のユーザーエクスペリエンスは, 可能な限りスムーズかつ容易であるべきである. これは以下のユーザビリティー標準 (ISO 25060 シリーズの標準など) やユーザーインタラクションデザインのための確立されたベストプラクティスによって達成できる.

<!-- The overall user experience with federated identity systems should be as smooth and easy as possible. This can be accomplished by following usability standards (such as the ISO 25060 series of standards) and established best practices for user interaction design. -->

ASSUMPTIONS

本セクションでは, "User" とは "Claimant" ないし "Subscriber" を意味し, "Entity" とは Federated システムに関与する主体を意味する.

<!-- In this section, the term "users" means "claimants" or "subscribers." The terms "entity" and "entities" refer to the parties of federated systems. -->

ガイドラインおよび考慮事項はユーザー視点で記述されている.

<!-- Guidelines and considerations are described from the users' perspective. -->

アクセシビリティーはユーザビリティーとは異なり, 本 Vol. の扱うところではない. [Section 508](#Section508) は情報技術の障壁を排除するために制定され, 連邦政府機関に対して, 電子的かつ情報技術を活用し障害者が公開コンテンツにアクセス可能になるよう求めている. アクセシビリティーガイドラインについては Section 508 の法と標準を参照のこと.

<!-- Accessibility differs from usability and is out of scope for this volume. [Section 508](#Section508) was enacted to eliminate barriers in information technology and requires federal agencies to make their electronic and information technology public content accessible to people with disabilities. Refer to Section 508 law and standards for accessibility guidance. -->

### 10.1 General Usability Considerations

Federated Identity システムは以下を満たすべきである.

<!-- Federated identity systems should: -->

* ユーザーの負担 (e.g., フラストレーション, 学習カーブ) を最小化する.
  * 必要なユーザーアクション数を最小化する.
  * ユーザーが素早く容易に同一 IdP 上の複数のアカウントを選択できるようにする. 例えば [Account Chooser](http://openid.net/wg/ac/) のようなアプローチでは, ユーザーが IdP リストから自身が利用したい IdP を選択するところから Federation プロセスを開始するのではなく, ユーザーが最近 Access したアカウントリストからアカウント選択を可能にしている.
  * ユーザーの負担の最小化とユーザーが十分に理解した上での決断を可能にする十分な情報提供の必要性のバランスを取る.

<!--
* Minimize user burden (e.g., frustration, learning curve)
  * Minimize the number of user actions required.
  * Allow users to quickly and easily select among multiple accounts with a single IdP. For example, approaches such as [Account Chooser](http://openid.net/wg/ac/) allow users to select from a list of accounts they have accessed in the recent past, rather than start the federation process by selecting their IdP from a list of potential IdPs.
  * Balance minimizing user burden with the need to provide sufficient information to enable users to make informed decisions.
-->

* 使い慣れていない技術用語や詳細の使用を最小限に抑える. (e.g., 基本的なコンセプトが明確に説明できれば, ユーザーは IdP や RP といった用語を知る必要はない.)

<!-- * Minimize the use of unfamiliar technical jargon and details (e.g., users do not need to know the terms IdP and RP if the basic concepts are clearly explained). -->

* IdP と RP で一貫性のある統合されたユーザーエクスペリエンスを目指す.

<!-- * Strive for a consistent and integrated user experience across the IdP and RP. -->

* グラフィックス, イラスト, FAQ, チュートリアル, 例などのリソースを提供し, ユーザーが Identity を理解するのを助ける. そういったリソースでは, ユーザーの情報がどのように取り扱われ, Transaction に携わる各主体 (e.g., RP, IdP, および Broker) がどのように相互関与するかを説明すべきである.

<!-- * Help users establish an understanding of identity by providing resources to users such as graphics, illustrations, FAQs, tutorials and examples. Resources  should explain how users' information is treated and how transacting parties (e.g., RPs, IdPs, and brokers) relate to each other. -->

* 明確, 正直かつ有意義なユーザーとのコミュニケーションを行う. (i.e., コミュニケーションは明白で理解しやすいべきである)

<!-- * Provide clear, honest, and meaningful communications to users (i.e., communications should be explicit and easy to understand). -->

* 場所やデバイスに関係なくユーザーにオンラインサービスを提供する.

<!-- * Provide users online services independent of location and device. -->

* 十分に理解した上での信頼の決定を容易にするため, ユーザーに対して信頼関係を明白にする. 信頼関係はしばしばダイナミックでコンテキスト依存である. ユーザーは, 特定の Attribute を持っていたり特定の Transaction において, ある IdP および RP を他より信頼するかもしれない. 例えば, 貴重な Personal Information (金融情報や健康情報など) を含んだ Web サイトでは, ユーザーは Federated Identity システムの利用をためらうかもしれない. ユーザーが知覚する Personal Data のセンシティブさによって, ユーザーはソーシャルネットワークプロバイダーを IdP として使いたがらないこともある. これは人々がしばしばソーシャルネットワーキング実装のブロードキャスト的性質を気にするからであろう.

<!-- * Make trust relationships explicit to users to facilitate informed trust decisions. Trust relationships are often dynamic and context dependent. Users may be more likely to trust some IdPs and RPs with certain attributes or transactions more than others. For example, users may be more hesitant to use federated identity systems on websites that contain valuable personal information (such as financial or health). Depending on the perceived sensitivity of users' personal data, users may be less comfortable with social network providers as IdPs since people are often concerned with the broadcasting nature of social networking implementations. -->

* ユーザーが触れるすべての情報について, [SP 800-63A, Section 9](sp800-63a.html#sec9) に示すユーザービリティー上の考慮点に従う.

<!-- * Follow the usability considerations specified in [SP 800-63A, Section 9](sp800-63a.html#sec9) for any user-facing information. -->

* どこでどのようにして技術的な支援を得ることができるかを明確に伝える. 例えば, ユーザーにオンラインセルフサービス機能へのリンクや, ヘルプデスクサポートのためのチャットや電話番号を提供する. Transaction に関わる主体間 (e.g., RP, IdP, および Broker) でユーザーをたらい回しにするような技術的支援は避けること.

<!-- * Clearly communicate how and where to acquire technical assistance. For example, provide users with information such as a link to an online self-service feature, chat sessions or a phone number for help desk support. Avoid redirecting users back and forth among transacting parties (e.g., RPs, IdPs, and brokers) to receive technical assistance. -->

* 適切なコンテキストで, 代表的なユーザーと現実的なタスクに対して, 統合的かつ継続的なユーザビリティー評価を行い, Federated Identity システムをユーザー視点で成功していることを保証する.

<!-- * Perform integrative and continuous usability evaluations with representative users and realistic tasks in an appropriate context to ensure success of federated identity systems from the users' perspectives. -->


### 10.2 Specific Usability Considerations

This section addresses the specific usability considerations that have been identified with federated identity systems. This section does not attempt to present exhaustive coverage of all usability factors related to federated identity systems. Rather it is focused on the larger, more pervasive themes in the usability literature, primarily users' perspectives on identity, user adoption, trust, and perceptions of federated identity space. In some cases, implementation examples are provided. However, specific solutions are not prescribed. The implementations mentioned are examples to encourage innovative technological approaches to address specific usability needs. See standards for system design and coding, specifications, APIs, and current best practices (such as OpenID and OAuth) for additional examples. Implementations are sensitive to many factors that prevent a one-size-fits-all solution.

#### 10.2.1 User Perspectives on Online Identity

Even when users are familiar with federated identity systems, there are different approaches to federated identity (especially in terms of privacy and the sharing of information) that make it necessary to establish reliable expectations for how users' data are treated. Users and implementers have different concepts of identity. Users think of identity as logging in and gaining access to their own private space. Implementers think of identity in terms of authenticators and assertions, assurance levels, and the necessary set of identity attributes to provide a service. Given this disconnect between users' and implementers' concepts of identity, it is essential to help users form an accurate concept of identity as it applies to federated identity systems. A good model of identity provides users a foundation for understanding the benefits and risks of federated systems and encourage user adoption and trust of these systems.

Many properties of identity have implications for how users manage identities, both within and among federations. Just as users manage multiple identities based on context outside of cyberspace, users must learn to manage their identity in a federated environment. Therefore, it must be clear to users how identity and context are used. The following factors should be considered:

* Provide users the requisite context and scope in order to distinguish among different user roles. For example, whether the user is acting on their own behalf or on behalf of another, such as their employer.

* Provide users unique, meaningful, and descriptive identifiers to distinguish among entities.

* Provide users with information on data ownership and those authorized to make changes. Identities, and the data associated with them, can sometimes be updated and changed by multiple actors. For example, some healthcare data is updated and owned by the patient, while some data is only updated by a hospital or doctor's practice.

* Provide users with the ability to easily verify, view, and update attributes. Identities and user roles are dynamic and not static; they change over time (e.g., age, health, and financial data). The ability to update attributes or make attribute release decisions may or may not be offered at the same time. Ensure the process for how users can change attributes is well known, documented, and easy to perform.

* Provide users means for updating data, even if the associated entity no longer exists.

* Provide users means to delete their identities completely, removing all information about themselves, including transaction history. Consider applicable audit, legal, or policy constraints that may preclude such action. In certain cases, full deactivation is more appropriate than deletion.

* Provide users with clear, easy-to-find, site/application data retention policy information.

* Provide users with appropriate anonymity and pseudonymity options, and the ability to switch among such identity options as desired, in accordance with an organization's data access policies.

* Provide means for users to manage each IdP to RP connection, including complete separation as well as the removal of RP access to one or more attributes.

#### 10.2.2 User Perspectives of Trust and Benefits


Many factors can influence user adoption of federated identity systems. As with any technology, users may value some factors more than others. Users often weigh perceived benefits versus risks before making technology adoption decisions. It is critical that IdPs and RPs provide users with sufficient information to enable them to make informed decisions. The concepts of trust and tiers of trust — fundamental principles in federated identity systems — can drive user adoption. Finally, a positive user experience may also result in increased user demand for federation, triggering increased adoption by RPs.

This sub-section is focused primarily on user trust and user perceptions of benefits versus risks.

To encourage user adoption, IdPs and RPs need to establish and build trust with users and provide them with an understanding of the benefits and risks of adoption. The following factors should be considered:

* Allow users to control their information disclosure and provide explicit consent through the appropriate use of notifications (see SP 800-63C, Section 9.2, Notice and Consent). Balancing the content, size, and frequency of notifications is necessary to avoid thoughtless user click-through.

* For attribute sharing, consider the following:
  * Provide a means for users to verify those attributes and attribute values that will be shared. Follow good security practices (see [Section 7](#presentation)).
  * Enable users to consent to a partial list of attributes, rather than an all-or-nothing approach. Allow users some degree of online access, even if the user does not consent to share all information.
  * Allow users to update their consent to their list of shared attributes.
  * Minimize unnecessary information presented to users. For example, do not display system generated attributes (such as pairwise pseudonymous identifiers) even if they are shared with the RP as part of the authentication response.
  * Minimize user steps and navigation. For example, build attribute consent into the protocols so they're not a feature external to the federated transaction. Examples can be found in standards such as OAuth or OpenID Connect.
  * Provide effective and efficient redress methods such that a user can recover from invalid attribute information claimed by the IdP (see [Section 7](#presentation)).
  * Minimize the number of times a user is required to consent to attribute sharing. Limiting the frequency of consent requests avoids user frustration from multiple requests to share the same attribute.

* Collect information for constrained usage only, and minimize information disclosure (see [Section 9.3](#minimization)). User trust is eroded by unnecessary and superfluous information collection and disclosure or user tracking without explicit user consent. For example, only request attributes from the user that are relevant to the current transaction, not for all possible transactions a user may or may not access at the RP.

* Clearly and honestly communicate potential benefits and risks of using federated identity to users. Benefits that users value include time savings, ease of use, reduced number of passwords to manage, and increased convenience.

User concern over risk can negatively influence willingness to adopt federated identity systems. Users may have trust concerns, privacy concerns, security concerns, and single-point-of-failure concerns. For example, users may be fearful of losing access to multiple accounts if a single IdP is unavailable, either temporarily or permanently. Additionally, users may be concerned or confused about learning a new authentication process. In order to foster the adoption of federated identity systems, the perceived benefits must outweigh the perceived risks.

#### 10.2.3 User Models and Beliefs

Users' beliefs and perceptions predispose them to expect certain results and to behave in certain ways. Such beliefs, perceptions, and predispositions are referred to in the social sciences as mental models. For example, people have a mental model of dining out which guides their behavior and expectations at each establishment, such as fast food restaurants, cafeterias, and more formal restaurants. Thus, it is not necessary to be familiar with every establishment to understand how to interact appropriately at each one.

Assisting users in establishing good and complete mental models of federation allows users to generalize beyond a single specific implementation. If federated identity systems are not designed from users' perspectives, users may form incorrect or incomplete mental models that impact their willingness to adopt these systems. The following factors should be considered:

* Clearly explain the working relationship and information flow among the transacting parties (e.g., RPs, IdPs, and brokers) to avoid user misconceptions. Use the actual names of the entities in the explanation rather than using the generic terms IdPs and RPs.
  * Provide prominent visual cues and information so that users understand why seemingly unrelated entities have a working relationship. For example, users may be concerned with mixing online personal activities with government services due to a lack of understanding of the information flow in federated identity systems.
  * Provide prominent visual cues and information to users about redirection when an RP needs to redirect control from their site to an IdP. For example, display RP branding within the IdP user interface to inform users when they are logging in with their IdP for access to the destination RP.

* Provide users with clear and usable ways (e.g., visual assurance) to determine the authenticity of the transacting  parties (e.g., RPs, IdPs, and brokers). This will also help to alleviate user concern over leaving one domain for another, especially if the root domain changes (e.g., .gov to .com). For example, display the URL of the IdP so that the user can verify that they are not being phished by a malicious site.

* Provide users with clear information, including visual cues, regarding implicit logins and explicit logouts. Depending on the implementation, logging into an RP with an IdP account may authenticate users to both the IdP and RP. Users may not realize that ending their session with the RP will not necessarily end their session with the IdP; users will need to explicitly "log out" of the IdP. Users require clear information to remind them if explicit logouts are required to end their IdP sessions.