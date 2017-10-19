<a name="privacy"></a>

## <a name="privacy-section-header"></a> 9 Privacy Considerations

*This section is informative.*

### 9.1 Minimizing Tracking and Profiling

Federation は RP と Subscriber に多くのメリットをもたらすが, Subscriber が IdP を信頼するよう要求する. さらに Federated モデルにおいて Subscriber の信頼を確立するには, Subscriber のデータが適切に収集時の目的に制限および限定して利用されていることが重要である. 提案された用途がこれらの許可された用途の範囲内に入るかどうかについて疑問がある場合は, SAOP に相談すること. [Sections 5](#federation), [5.1.4](#proxied), および [6.3](#ppi) は, Subscriber に対するトラッキングやプロファイリングの機会増大によるプライバシーリスクを最小化するための多くの技術的要件をカバーしている. 例えば複数の RP に対して Authenticate するために同じ IdP を利用している Subscriber がいるとすると, 当該 Subscriber は IdP に対して Federation しなかった場合には発生しなかった Subscriber Transaction のプロファイルを構築することを可能にする. このようなデータは, Subscriber の予期ないし希望しない用途に対して脆弱であり, Subscriber が Federated サービスを利用するのを妨げる可能性もある.

<!-- Federation offers numerous benefits to RPs and subscribers, but requires subscribers to have trust in the IdP. Accordingly, to build subscriber trust in a federated model, it is important that uses of subscriber data are appropriately limited and scoped to the purpose for which it was originally collected. Consult your SAOP if there are questions about whether proposed uses fall within the scope of these permitted uses. [Sections 5](#federation), [5.1.4](#proxied), and [6.3](#ppi) cover a number of technical requirements, the objective of which is to minimize privacy risks arising from increased capabilities to track and profile subscribers. For example, a subscriber using the same IdP to authenticate to multiple RPs allows the IdP to build a profile of subscriber transactions that would not have existed absent federation. The availability of such data makes it vulnerable to uses that may not be anticipated or desired by the subscriber and may inhibit subscriber adoption of federated services. -->

また [Section 5.2](#privacy-reqs) は Unlinkability を提供し Subscriber の行動をトラッキングしたりプロファイリングすることを抑制する技術的対策の利用を推奨している. IdP のポリシーおよび手続きは適切な利用制限や目的特定の原則の遵守徹底に重要であるが, [Section 5.1.4](#proxied) で述べた Proxied Federation や [Section 6.3](#ppi) で述べた Pairwise Pseudonymous Identifier のような技術的対策は, 運用要件を超えて Subscriber をトラックしたりプロファイリングすることを困難にし, IdP ポリシーの有効性を向上する.

<!-- [Section 5.2](#privacy-reqs) also encourages the use of technical measures to provide unlinkability and prevent subscriber activity tracking and profiling. While IdP policies and procedures are important in ensuring adherence to appropriate use limitation and purpose specification principles, technical measures such as outlined in [Section 5.1.4](#proxied) for proxied federation and [Section 6.3](#ppi) for pairwise pseudonymous identifiers, can increase the effectiveness of these policies by making it more difficult to track or profile subscribers beyond operational requirements. -->

### <a name="notice"></a> 9.2 Notice and Consent

Federation において Subscriber の信頼を確立するには, Subscriber が自身の情報がどのように処理されるかについて信頼できる仮定を
立てられる必要がある. 例えば, どの情報が送信されるのか, その Transaction においてどの Attribute が必須でありどれがオプションであるかを理解でき, RP にオプションの Attribute を送信するか否かの決定権があることが, Subscriber にとって有用であろう. したがって [Section 7](#presentation) では, Subscriber に関する Attribute が RP に送信される前に Subscriber に肯定的確認を得るよう求めている. [Section 6.3.2](#ppi-gen) にように, 一連の RP 群がおなじ Pairwise Pseudonymous Identifier を共有すべきかどうかを決定する際には, IdP は Subscriber がそのような RP のグルーピングを理解できること, およびそのような理解を助ける通知を行う役目について配慮すること. 効果的な通知には, ユーザーエクスペリエンスのデザイン標準および研究, および情報処理により発生する可能性のあるプライバシーリスクの評価を考慮することになろう. Subscriber が情報の処理について持つ仮定の信頼性や, Federation に関与するその他の主体の役割など, 考慮すべき要素は数多い. しかしながら, 複雑で法律に固執したプライバシーポリシーや, 相当数の Subscriber が読んだり理解したりしないような利用規約へのリンクは, 決して効果的な通知でなはい.

<!-- To build subscriber trust in federation, subscribers need to be able to develop reliable assumptions about how their information is being processed. For instance, it can be helpful for subscribers to understand what information will be transmitted, which attributes for the transaction are required versus optional, and to have the ability to decide whether to transmit optional attributes to the RP. Accordingly, [Section 7](#presentation) requires that positive confirmation be obtained from the subscriber before any attributes about the subscriber are transmitted to any RP. In determining when a set of RPs should share a common pairwise pseudonymous identifier as in [Section 6.3.2](#ppi-gen), the IdP considers the subscriber's understanding of such a grouping of RPs and the role of notice in assisting such understanding. An effective notice will take into account user experience design standards and research, as well as an assessment of privacy risks that may arise from the information processing. There are various factors to be considered, including the reliability of the assumptions subscribers may have about the processing and the role of different entities involved in federation. However, a link to a complex, legalistic privacy policy or general terms and conditions that a substantial number of subscribers do not read or understand is never an effective notice. -->

[Section 7](#presentation) はどの主体が通知を行うかは指定していない. 場合によっては Federation に関わる主体が Subscriber に通知し同意を得るための直接的な接続関係にないこともある. 通知を行うべく選択されうる主体は複数存在するが, Subscriber が通知に注意を払い情報に基づいた選択ができることを中心においた要因に基づいて決定されている限り, 事前に契約やトラストフレームワークのポリシーによりどの主体が通知と同意取得を行うかを決定しておくことは許容される.

<!-- [Section 7](#presentation) does not specify which party should provide the notice. In some cases, a party in a federation may not have a direct connection to the subscriber in order to provide notice and obtain consent. Although multiple parties may elect to provide notice, it is permissible for parties to determine in advance, either contractually or through trust framework policies, which party will provide the notice and obtain confirmation, as long as the determination is being based upon factors that center on enabling the subscriber to pay attention to the notice and make an informed choice. -->

IdP が [Section 4.2](#runtime-decisions) に述べたように RP のホワイトリストを利用している場合, 当該リストの RP はいずれも Authentication Transaction 中で Subscriber に提示されない. IdP はランタイムにおいて Subscriber に通知を行わないため, ホワイトリストに掲載された RP を Subscriber から確認可能にし, どの RP がどの Subscriber Attribute に Access できるか確認できるようにする. IdP は Subscriber が関与する Authentication Transaction 外では Subscriber の Authentication 情報や Attribute をホワイトリスト上の RP と共有できないため ([Section 5.2](#privacy-reqs) 参照), RP がリスト上に存在することがそのまま Subscriber の情報が共有されることを意味するわけではない. しかしながら Subscriber が IdP を使ってホワイトリスト上の任意の RP にログインすれば, 表明された Attribute は Authentication Transaction 中で共有されることとなろう.

<!-- If an IdP is using a whitelist of RPs as described in [Section 4.2](#runtime-decisions), any RPs on that list are not presented to the subscriber during an authentication transaction. Since the IdP does not provide notice to the subscriber at runtime, the IdP makes its list of whitelisted RPs available to the subscriber so that the subscriber can see which RPs on the whitelist have access to which of the subscriber's attributes in an authentication transaction. Since IdPs can not share a subscriber's authentication information or attributes with a whitelisted RP outside of an authentication transaction involving the subscriber (see [Section 5.2](#privacy-reqs)), the existence of an RP on a list of IdPs does not indicate that the subscriber's information will be shared. However, if the subscriber logs into any of the whitelisted RPs using the IdP, the attributes indicated will be shared as part of the authentication transaction. -->

Subscriber のランタイムでの決定が将来の Transaction を促進するために IdP に保存されている場合は, IdP は Subscriber にランタイムの決定によりすでに許可された RP を閲覧したり許可を無効化できるようにする必要がある. このリストにはどの Attribute が許可されているかという情報を含む.

<!-- If a subscriber's runtime decisions were stored by the IdP to facilitate future transactions, the IdP also needs to allow the subscriber to view and revoke any RPs that were previously approved during a runtime decision. This list includes information on which attributes were approved. -->

### <a name="minimization"></a> 9.3 Data Minimization

Federation は RP に晒されるデータの最小化を可能にし, 結果として Subscriber のプライバシーは強化される. IdP は自身のユースケースのために RP の要求を超えて追加の Attribute を収集するかもしれないが, RP が明示的に要求した Attribute のみが IdP によって送信される. 場合によっては, RP は完全な Attribute Value を要求しないかもしれない. 例えば, RP は Subscriber が13歳以上かどうかを知る必要があるが, 完全な生年月日を知る必要はないこともある. 潜在的にセンシティブな PII の収集を最小化するため, RP は Attribute Reference (e.g., Subscriber が13歳か否かという, Y/N や Pass/Fail で答えられる質問) を要求することができる. こうすることで RP による潜在的にセンシティブかつ不要な PII の収集を最小化できる. さらに [Section 7.3](#protecting-information) は RP に可能であれば完全な Attribute Value ではなく Attribute Reference を要求するよう求めている. この RP 要件を指示するため, IdP には Attribute Reference をサポートすることが求められる.

<!-- Federation enables the data exposed to an RP to be minimized &mdash; resultantly, the subscriber's privacy is enhanced. Although an IdP may collect additional attributes beyond what the RP requires for its use case, only those attributes that were explicitly requested by the RP are to be transmitted by the IdP. In some instances, an RP does not require a full value of an attribute. For example, an RP may need to know whether the subscriber is over 13 years old, but has no need for the full date of birth. To minimize collection of potentially sensitive PII, the RP may request an attribute reference (e.g., Question: Is the subscriber over 13 years old? Response: Y/N or Pass/Fail). This minimizes the RP's collection of potentially sensitive and unnecessary PII. Accordingly, [Section 7.3](#protecting-information) requires the RP to, where feasible, request attribute references rather than full attribute values. To support this RP requirement IdPs are, in turn, required to support attribute references. -->

### <a name="agency-privacy"></a>9.4 Agency-Specific Privacy Compliance

[Section 5.2](#privacy-reqs) は, 機関に対して SAOP に相談してプライバシーコンプライアンス要件を決定するよう要件を定めている. プライバシーリスクの評価と対応策を施し, 機関に当該 Federation が Privacy Act of 1974 や E-Government Act of 2002 の求める PIA の実施を必要とするかといったコンプライアンス遵守に関するアドバイスを行うため, 機関の SAOP が Digital Authentication システムの開発初期段階で関わることは非常に重要である. 例えば, 当該機関が Federation における IdP を提供している場合, Credential は IdP と Federate する RP に代わって IdP に管理されることになるため, Privacy Act 要件が課せられることとなり, 新規もしくは既存の Privacy Act の記録システムによるカバレッジが必要となる. しかしながら, 機関が第三者の IdP を利用する RP の場合, RP から渡されたどのデータが RP として機関に管理されるかによっては (その場合, 機関はそのようなデータをカバーする, より広範かつプログラム的 SORN を持つことになるかもしれない), Digital Authentication には Privacy Act 要件は課されないかもしれない.

<!-- [Section 5.2](#privacy-reqs) identifies agency requirements to consult their SAOP to determine privacy compliance requirements. It is critical to involve your agency's SAOP in the earliest stages of digital authentication system development to assess and mitigate privacy risks and advise the agency on compliance obligations such as whether the federation triggers the Privacy Act of 1974 or the E-Government Act of 2002 requirement to conduct a PIA. For example, if the Agency is serving as an IdP in a federation, it is likely that the Privacy Act requirements will be triggered and require coverage by either a new or existing Privacy Act system of records since credentials would be maintained at the IdP on behalf of any RP it federates with. If, however, the agency is an RP and using a third-party IdP, digital authentication may not trigger the requirements of the Privacy Act, depending on what data passed from the RP is maintained by the agency as the RP (in such instances the agency may have a broader programmatic SORN that covers such data). -->

SAOP は同様に PIA が必要かどうかの決定において機関を援助できる. この考慮点は, Federated Credential の利用のためだけに, Privacy Act SORN や PIA が要件となるというふうに読むべきではない. 多くの場合, Digital Authentication プロセス全体を網羅する, ないしは Digital Authentication プロセスを機関がオンライン Access を確立するプログラムや利点に関して議論するより大きなプログラム的 PIA の一部に含む, PIA および SORN を草稿することが最も理にかなっている.

<!-- The SAOP can similarly assist the agency in determining whether a PIA is required. These considerations should not be read as a requirement to develop a Privacy Act SORN or PIA for use of a federated credential alone. In many cases it will make the most sense to draft a PIA and SORN that encompasses the entire digital authentication process or includes the digital authentication process as part of a larger programmatic PIA that discusses the program or benefit the agency is establishing online access. -->

Digital Authentication の構成要素は多岐に渡るため, SAOP が個々の要素に気づいており理解していることは重要である. 例えば, Data Use Agreement, Computer Matching Agreement など, Federated IdP ないし RP サービスを提供ないし利用する機関に適用可能なその他のプライバシー上の副作用がありうる. SAOP は機関にどのような追加要件が適用されるかを決定する手助けをすることができる. さらに Digital Authentication の個々の要素を綿密に理解することにより, SAOP はコンプライアンスプロセスやその他の手段を通じてプライバシーリスクを徹底的に評価し, 緩和することができる.

<!-- Due to the many components of digital authentication, it is important for the SAOP to have an awareness and understanding of each individual component. For example, other privacy artifacts may be applicable to an agency offering or using federated IdP or RP services, such as Data Use Agreements, Computer Matching Agreements, etc. The SAOP can assist the agency in determining what additional requirements apply. Moreover, a thorough understanding of the individual components of digital authentication will enable the SAOP to thoroughly assess and mitigate privacy risks either through compliance processes or by other means. -->


### 9.5 <a name="blinding"></a>Blinding in Proxied Federation

典型的にはインテクレーションを単純化することを主目的する Proxy など, Proxy 構造によっては追加の Subscriber のプライバシー保護を提供しないものもあるが, Blinding 技術を用いて多様なレベルのプライバシーを Subscriber に提供するものもある. プライバシーポリシーにおいて, Subscriber Attribute と Authentication Transaction データ (e.g., 末端の IdP および RP の識別子) の IdP, RP, および Federation Proxy による適切な利用について記述してもよい. Bliding などの技術的手段はデータ取得を困難にし, そういったポリシーの有効性を高めることができる. Blindng レベルが上がるほど, 技術的および運用上の実装複雑性は上昇する. Proxy は Transaction をいずれかの側の適切な主体にマッピングし, Transaction 内のすべての関係者の鍵を管理する必要がある.

<!-- While some proxy structures — typically those that exist primarily to simplify integration — may not offer additional subscriber privacy protection, others offer varying levels of privacy to the subscriber through a range of blinding technologies. Privacy policies may dictate appropriate use of the subscriber attributes and authentication transaction data (e.g., identities of the ultimate IdP and RP) by the IdP, RP, and the federation proxy. Technical means such as blinding can increase effectiveness of these policies by making the data more difficult to obtain. As the level of blinding increases, the technical and operational implementation complexity may increase. Proxies need to map transactions to the appropriate parties on either side as well as manage the keys for all parties in the transaction. -->

Bliding 技術を使っても, Blind された主体は, 提供された Attribute データやメタデータなどから, タイムスタンプや Attribute Bundle のサイズ, Attribute への署名者情報などを解析するなどして, 依然保護された Subscriber 情報を推測することができる. IdP は追加のプライバシー強化アプローチを検討し, Federation に参加している主体の識別可能情報の開示リスクを低減してもよい.

<!-- Even with the use of blinding technologies, a blinded party may still infer protected subscriber information through released attribute data or metadata, such as by analysis of timestamps, attribute bundle sizes, or attribute signer information. The IdP could consider additional privacy-enhancing approaches to reduce the risk of revealing identifying information of the entities participating in the federation. -->

以下の表は Proxied Federation で利用される Bliding 実装の範囲を示したものである. なお, この表は説明を目的としたものであり, 網羅的でも技術に特化したものでもない.

<!-- The following table illustrates a spectrum of blinding implementations used in proxied federation. This table is intended to be illustrative, and is neither comprehensive nor technology-specific. -->

<div class="text-center" markdown="1">

**Table 9-1 Federation Proxies**

</div>


|Proxy Type|RP knows IdP|IdP knows RP|Proxy can track subscriptions between RP and IdP|Proxy can see attributes of Subscriber|
|---|:---:|:---:|:---:|:---:|
|Non-Blinding Proxy with Attributes|Yes|Yes|Yes|Yes|
|Non-Blinding Proxy|Yes|Yes|Yes|N/A|
|Double Blind Proxy with Attributes|No|No|Yes|Yes|
|Double Blind Proxy|No|No|Yes|N/A|
|Triple Blind Proxy with or without Attributes|No|No|No|No|
