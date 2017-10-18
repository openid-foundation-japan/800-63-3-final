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

本セクションでは Federated Identity システムに対する特別なユーザビリティー上の考慮点を扱う. 本セクションは, Federated Identity システムに関連する全てのユーザビリティー要素を網羅的にカバーすることを意図するものではない. ここでは, ユーザビリティーに関する文献におけるより大きくより普及したテーマである, ユーザーの Identity に対する捉え方, ユーザーの選択, 信頼, Federated Identity 空間の認識に焦点を当てる. 場合によっては実装例が提供されることもあるが, 特定のソリューションを規定することはない. 言及される実装は, 特定のユーザビリティー上のニーズに対応する革新的な技術的アプローチを推奨するための例である. さらなる例については, システム設計とコーディング, 仕様, API, 最新のベストプラクティス (OpenID や OAuth など) の標準を参照のこと. 各実装は多くの要因に対して敏感であり, ワンサイズフィットオーフなソリューションは存在しない.

<!-- This section addresses the specific usability considerations that have been identified with federated identity systems. This section does not attempt to present exhaustive coverage of all usability factors related to federated identity systems. Rather it is focused on the larger, more pervasive themes in the usability literature, primarily users' perspectives on identity, user adoption, trust, and perceptions of federated identity space. In some cases, implementation examples are provided. However, specific solutions are not prescribed. The implementations mentioned are examples to encourage innovative technological approaches to address specific usability needs. See standards for system design and coding, specifications, APIs, and current best practices (such as OpenID and OAuth) for additional examples. Implementations are sensitive to many factors that prevent a one-size-fits-all solution. -->

#### 10.2.1 User Perspectives on Online Identity

ユーザーが Federated Identity システムに慣れ親しんでいたとしても, (特にプライバシーと情報共有の点で) Federated Identity に対する異なるアプローチも存在し, そこではユーザーのデータ処理方法に対する信頼性の高い期待を確立する必要がある. ユーザーと実装者は異なる Identity の概念を持つ. ユーザーはログインして自身のプライベートな空間への Access を得るものとして Identity を捉えるが, 実装者は Authenticator と Assertion, Assurance Level, サービス提供に必要な一式の Identity Attribute という視点で Identity を捉える. このように, ユーザーと実装者では Identity の捉え方が異なるため, ユーザーが Federated Identity システムに適用される Identity の概念を正確に理解できるよう手助けすることが不可欠である. 優れた Identity モデルは, ユーザーが Federated システムの利点とリスクを理解し, こういったシステムを選択および信頼するよう促すための基礎となる.

<!-- Even when users are familiar with federated identity systems, there are different approaches to federated identity (especially in terms of privacy and the sharing of information) that make it necessary to establish reliable expectations for how users' data are treated. Users and implementers have different concepts of identity. Users think of identity as logging in and gaining access to their own private space. Implementers think of identity in terms of authenticators and assertions, assurance levels, and the necessary set of identity attributes to provide a service. Given this disconnect between users' and implementers' concepts of identity, it is essential to help users form an accurate concept of identity as it applies to federated identity systems. A good model of identity provides users a foundation for understanding the benefits and risks of federated systems and encourage user adoption and trust of these systems. -->

Identity の特性の多くは, Federation 内, および Federation 間の両方で, ユーザーがどのように Identity を管理するかに影響を及ぼす. サイバースペースの外でコンテキストに基づいて複数の Identity を管理するのと同じように, ユーザーは自身の Identity を Federated な環境で管理するすべを学ぶ必要がある. したがって, Identity とコンテキストがどのように扱われるのかは, ユーザーに対して明確でなければならない. そのため, 以下の点が考慮されるべきである.

<!-- Many properties of identity have implications for how users manage identities, both within and among federations. Just as users manage multiple identities based on context outside of cyberspace, users must learn to manage their identity in a federated environment. Therefore, it must be clear to users how identity and context are used. The following factors should be considered: -->

* 異なるユーザーの役割を区別するため, ユーザーに必要なコンテキストとスコープを提供する. 例えば, ユーザーが自身の代理として行動しているのか, 自身の雇用主など他者の代理として行動しているのかなど.

<!-- * Provide users the requisite context and scope in order to distinguish among different user roles. For example, whether the user is acting on their own behalf or on behalf of another, such as their employer. -->

* Entity を区別するため, ユーザーにユニークで意味のある記述的な識別子を提供する.

<!-- * Provide users unique, meaningful, and descriptive identifiers to distinguish among entities. -->

* ユーザーにデータ所有権とデータ変更権限のある Authorized なユーザーに関する情報を提供する. Identity およびそれに関連するデータは, 複数の主体によって更新・変更可能な場合もある. 例えば, ヘルスケアデータは患者のものであるが, 一部のデータは病院や医師の診療にのってのみ更新される.

<!-- * Provide users with information on data ownership and those authorized to make changes. Identities, and the data associated with them, can sometimes be updated and changed by multiple actors. For example, some healthcare data is updated and owned by the patient, while some data is only updated by a hospital or doctor's practice. -->

* ユーザーが簡単に Attribute を検証, 閲覧, 更新できるようにする. Identity とユーザーの役割はスタティックではなくダイナミックなものであり, 時間経過 (e.g., 年齢, 健康および金融データ) とともに変わりうる. Attribute を更新したり Attribute 提供の決定を行う機能は, 同時に提供されることもあればそうでないこともある. ユーザーが Attribute を変更するプロセスがよく知られており, ドキュメント化され, 容易に実行できることを保証すること.

<!-- * Provide users with the ability to easily verify, view, and update attributes. Identities and user roles are dynamic and not static; they change over time (e.g., age, health, and financial data). The ability to update attributes or make attribute release decisions may or may not be offered at the same time. Ensure the process for how users can change attributes is well known, documented, and easy to perform. -->

* 関連する Entity がすでに存在しない場合でも, ユーザーにデータをアップデートする手段を提供すること.

<!-- * Provide users means for updating data, even if the associated entity no longer exists. -->

* ユーザーが, 自身の Identity を完全に消去したり, Transaction 履歴を含む自身に関するすべての情報を消去したりできるようにすること. そういったアクションを妨げる可能性のある, 適用可能な監査, 法律, ポリシー上の制約を考慮すること. 場合によっては, 消去よりも完全な無効化の方が適切なこともある.

<!-- * Provide users means to delete their identities completely, removing all information about themselves, including transaction history. Consider applicable audit, legal, or policy constraints that may preclude such action. In certain cases, full deactivation is more appropriate than deletion. -->

* ユーザーに, 明確かつみつけやすい, サイト / アプリケーションのデータ保持ポリシー情報を提供すること.

<!-- * Provide users with clear, easy-to-find, site/application data retention policy information. -->

* 組織のデータ Access ポリシーにしたがって, ユーザーに適切な Anonymity (匿名性) や Pseudonymity (仮名性) オプションを提供し, 要望に応じてそういった Identity オプションを切り替えられるようにすること.

<!-- * Provide users with appropriate anonymity and pseudonymity options, and the ability to switch among such identity options as desired, in accordance with an organization's data access policies. -->

* ユーザーに各 IdP および RP 間のコネクションを管理する手段を提供すること. これには, 完全な分断, 特定の RP の1つ以上の Attribute への Access 権限の削除を含む.

<!-- * Provide means for users to manage each IdP to RP connection, including complete separation as well as the removal of RP access to one or more attributes. -->

#### 10.2.2 User Perspectives of Trust and Benefits

ユーザーによる Federation Identity システムの選択には, 多くの要素が影響を及ぼしうる. どのような技術においても, ユーザーはある要素を他より重視しうる. ある技術を選択する決断の前に, ユーザーはしばしば知覚されるメリットとリスクをはかりにかける. ユーザーがよく理解した上で決断できるように, IdP と RP が十分な情報を提供するのは, 非常に重要である. 信頼と信頼階層 (Tiers of Trust) というコンセプトは, Federated Identity システムの基本原理であり, ユーザーによる選択を促進する可能性がある. 最後に, ユーザーエクスペリエンスが向上すると, Federation に対するユーザーの需要が増加し, RP による Federation の選択も増加する可能性がある.

<!-- Many factors can influence user adoption of federated identity systems. As with any technology, users may value some factors more than others. Users often weigh perceived benefits versus risks before making technology adoption decisions. It is critical that IdPs and RPs provide users with sufficient information to enable them to make informed decisions. The concepts of trust and tiers of trust — fundamental principles in federated identity systems — can drive user adoption. Finally, a positive user experience may also result in increased user demand for federation, triggering increased adoption by RPs. -->

本サブセクションは, 主にユーザーの信頼とユーザーによるメリットとリスクの知覚に焦点を当てる.

<!-- This sub-section is focused primarily on user trust and user perceptions of benefits versus risks. -->

ユーザーによる採用を促進するため, IdP と RP はユーザーとの信頼を確立おこび構築し, ユーザーに採用によるメリットとリスクを理解させる必要がある. 考慮点としては以下のようなものが挙げられる.

<!-- To encourage user adoption, IdPs and RPs need to establish and build trust with users and provide them with an understanding of the benefits and risks of adoption. The following factors should be considered: -->

* ユーザーが自身の情報の開示をコントロールし, 適切な通知により明示的同意を行えるようにする (SP 800-63C, Section 9.2, Notice and Consent 参照). 通知の内容, サイズ, 頻度のバランスは, ユーザーが何も考えずにクリックスルーしてしまうことを避けるために必須である.

<!-- * Allow users to control their information disclosure and provide explicit consent through the appropriate use of notifications (see SP 800-63C, Section 9.2, Notice and Consent). Balancing the content, size, and frequency of notifications is necessary to avoid thoughtless user click-through. -->

* Attribute 共有のためには以下の点を考慮すること.
  * ユーザーに共有される自身の Attribute および Attribute Value を検証する手段を提供すること. よくできたセキュリティープラクティスに従うこと ([Section 7](#presentation) 参照).
  * オールオアナッシングアプローチではなく, ユーザーが部分的な Attribute リストに対して同意できるようにすること. ユーザーが全情報の共有に同意しない場合でも, ある程度のオンライン Access を可能にすること.
  * ユーザーが共有済 Attribute リストへの同意を更新できるようにすること.
  * ユーザーに提示される不必要な情報を最小化すること. 例えば, Authentication レスポンスの一部として共有されるとしても, システムにより生成された Attribute (Pairwise Pseudonymous Identifier など) を見せないなど.
  * ユーザーのステップおよびナビゲーションを最小化すること. 例えば, Attribute 共有の同意をプロトコルに組み込み, Federated Transaction 外の機能としないなど. OAuth や OpenID Connect といった標準にこういった例が見られる.
  * ユーザーが IdP により不正な Attribute 情報を付与された状況から回復できるよう, 効果的かつ効率的な是正手段を提供すること ([Section 7](#presentation) 参照).
  * ユーザーに Attribute 共有の同意を要求する回数を最小化すること. 同意要求の頻度を限定することで, 何度も同じ Attribute の共有要求を受けることによるユーザーのフラストレーションを避けることができる.

<!--
* For attribute sharing, consider the following:
  * Provide a means for users to verify those attributes and attribute values that will be shared. Follow good security practices (see [Section 7](#presentation)).
  * Enable users to consent to a partial list of attributes, rather than an all-or-nothing approach. Allow users some degree of online access, even if the user does not consent to share all information.
  * Allow users to update their consent to their list of shared attributes.
  * Minimize unnecessary information presented to users. For example, do not display system generated attributes (such as pairwise pseudonymous identifiers) even if they are shared with the RP as part of the authentication response.
  * Minimize user steps and navigation. For example, build attribute consent into the protocols so they're not a feature external to the federated transaction. Examples can be found in standards such as OAuth or OpenID Connect.
  * Provide effective and efficient redress methods such that a user can recover from invalid attribute information claimed by the IdP (see [Section 7](#presentation)).
  * Minimize the number of times a user is required to consent to attribute sharing. Limiting the frequency of consent requests avoids user frustration from multiple requests to share the same attribute.
-->

* 制約内の利用目的のためにのみ情報を収集し, 情報開示を最小化すること ([Section 9.3](#minimization) 参照). ユーザーの明示的な同意なしに不必要かつ過剰な情報の収集や開示, またはユーザーのトラッキングを行うと, ユーザーの信頼は失われる. 例えば, ユーザーに対して現在の Transaction に関連する Attribute のみを要求し, RP でユーザーが Access するかどうかわからないすべてのありうる Transaction のために Attribute を要求しないようにするなど.

<!-- * Collect information for constrained usage only, and minimize information disclosure (see [Section 9.3](#minimization)). User trust is eroded by unnecessary and superfluous information collection and disclosure or user tracking without explicit user consent. For example, only request attributes from the user that are relevant to the current transaction, not for all possible transactions a user may or may not access at the RP. -->

* Federated Identity を利用することによる潜在的利点とリスクを, ユーザーに明確かつ正直に伝えること. ユーザーが価値を感じる利点としては, 時間節約, 使いやすさ, 管理するパスワード数の減少, 利便性向上などがある.

<!-- * Clearly and honestly communicate potential benefits and risks of using federated identity to users. Benefits that users value include time savings, ease of use, reduced number of passwords to manage, and increased convenience. -->


リスクに対するユーザーの懸念は, Federated Identity システムの選択意欲に悪影響を与えうる. ユーザーは, 信頼, プライバシー, セキュリティー, Single-point-of-failure といった点において, 懸念を抱く可能性がある. 例えば, ひとつの IdP が一時的または永続的に利用不可となった場合, ユーザーは複数のアカウントへの Access を失うおそれがある. さらに, ユーザーは新しい Authentication プロセスを学ぶことに懸念を抱いたり混乱する可能性もある. Federated Identity システムの選択を促進するには, 知覚されるメリットが知覚されるリスクを上回らねばならない.

<!-- User concern over risk can negatively influence willingness to adopt federated identity systems. Users may have trust concerns, privacy concerns, security concerns, and single-point-of-failure concerns. For example, users may be fearful of losing access to multiple accounts if a single IdP is unavailable, either temporarily or permanently. Additionally, users may be concerned or confused about learning a new authentication process. In order to foster the adoption of federated identity systems, the perceived benefits must outweigh the perceived risks. -->

#### 10.2.3 User Models and Beliefs

ユーザーは何かを信じたりと知覚することによって, 特定の結果を期待し, 特定の方法で行動する傾向にある. そのように信じたり知覚したり何らかの傾向を示したりすることは, 社会科学においてメンタルモデルと呼ばれる. 例えば, ファーストフードレスランやカフェテリア, よりフォーマルなレストランなど, 人々は施設によって行動や期待を異にするような, 食事に関するメンタルモデルを持っている. したがって, それぞれの施設に精通していなくても, それぞれでどのように振る舞うのが適切かを理解することができる.

<!-- Users' beliefs and perceptions predispose them to expect certain results and to behave in certain ways. Such beliefs, perceptions, and predispositions are referred to in the social sciences as mental models. For example, people have a mental model of dining out which guides their behavior and expectations at each establishment, such as fast food restaurants, cafeterias, and more formal restaurants. Thus, it is not necessary to be familiar with every establishment to understand how to interact appropriately at each one. -->

Federation におけるよくできた完全なメンタルモデルをユーザーが構築できるよう支援することで, ユーザーはある特定の実装を超えて一般化を行うことができる. Federated Identity システムがユーザー視点でデザインされていなければ, ユーザーは間違ったもしくは不完全なメンタルモデルを形成し, 彼らによるシステムの選択意思に影響を及ぼすかもしれない. 考慮点としては以下のようなものが挙げられる.

<!-- Assisting users in establishing good and complete mental models of federation allows users to generalize beyond a single specific implementation. If federated identity systems are not designed from users' perspectives, users may form incorrect or incomplete mental models that impact their willingness to adopt these systems. The following factors should be considered: -->

* ユーザーの誤解を避けるため, Transaction 関係者 (e.g., RP, IdP, および Broker) 間の関係性と情報の流れを明確に説明すること. 一般的用語である IdP と RP という語を使用するのではなく, 実際の Entity の名前を使用して説明すること.
  * 人目をひく視覚的合図や情報を提供し, 一見無関係な Entity が相互に関係している理由を理解できるようにすること. 例えば, ユーザーは Federated Identity システムにおける情報の流れの理解が不足しており, オンラインでの個人的な行動と政府サービスが混ぜ合わされてしまうのではないかと心配するかもしれない.
  * 人目をひく視覚的合図や情報を提供し, RP が制御を自身のサイトから IdP にリダイレクトする必要がある際に, リダイレクトに関してユーザーに知らせること. 例えば, IdP のユーザーインターフェース内に RP のブランドを表示し, 目的とする RP に Access するために当該 IdP にログインしようとしていることをユーザーに知らせるなど.

<!--
* Clearly explain the working relationship and information flow among the transacting parties (e.g., RPs, IdPs, and brokers) to avoid user misconceptions. Use the actual names of the entities in the explanation rather than using the generic terms IdPs and RPs.
  * Provide prominent visual cues and information so that users understand why seemingly unrelated entities have a working relationship. For example, users may be concerned with mixing online personal activities with government services due to a lack of understanding of the information flow in federated identity systems.
  * Provide prominent visual cues and information to users about redirection when an RP needs to redirect control from their site to an IdP. For example, display RP branding within the IdP user interface to inform users when they are logging in with their IdP for access to the destination RP.
-->

* Transaction 関係者 (e.g., RP, IdP, および Broker) の信憑性 (Authenticity) を判断するため, ユーザーに明確で利用しやすい手段 (e.g., 視覚的保証) を提供すること. これは, 特にルートドメインが変わる (e.g., .gov から .com) 場合など, あるドメインから別のドメインに移る際のユーザーの懸念を緩和するにも役立つであろう. 例えば, IdP の URL を表示して, ユーザーが悪意あるサイトにフィッシングされていないことを検証できるようにするなど.

<!-- * Provide users with clear and usable ways (e.g., visual assurance) to determine the authenticity of the transacting  parties (e.g., RPs, IdPs, and brokers). This will also help to alleviate user concern over leaving one domain for another, especially if the root domain changes (e.g., .gov to .com). For example, display the URL of the IdP so that the user can verify that they are not being phished by a malicious site. -->

* 暗黙的なログインと明示的なログアウトに関して, ユーザーに視覚的合図を含む明確な情報を提供すること. 実装によっては, IdP アカウントで RP にログインすると, ユーザーは IdP と RP 双方に対して Authenticate されることもある. その場合, ユーザーは RP での Session を終了したとしても, 必ずしも IdP の Session が終了されるわけではなく, IdP から明示的に "ログアウト" する必要がある, ということに気づかないかもしれない. IdP の Session を終了するために明示的なログアウトが必要な場合, ユーザーはそれを想起させる明確な情報を必要とする.

<!-- * Provide users with clear information, including visual cues, regarding implicit logins and explicit logouts. Depending on the implementation, logging into an RP with an IdP account may authenticate users to both the IdP and RP. Users may not realize that ending their session with the RP will not necessarily end their session with the IdP; users will need to explicitly "log out" of the IdP. Users require clear information to remind them if explicit logouts are required to end their IdP sessions. -->
