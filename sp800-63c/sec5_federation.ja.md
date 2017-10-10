<a name="federation"></a>

## 5 Federation

*This section is normative.*

Federation プロトコルでは, [Figure 5-1](#63cSec5-Figure1) に示すように Subscriber, IdP, RP の3者の関係が構築される. 各プロトコルによってどのタイムングでどの主体の間でどんな情報がやりとりされるかは異なる. Subscriber は通常ブラウザーを介して IdP と RP の両方とコミュニケーションをとる. RP と IdP の間のコミュニケーション方法は2通りある.

<!-- In a federation protocol, a three-party relationship is formed between the subscriber, the IdP, and the RP, as shown in [Figure 5-1](#63cSec5-Figure1). Depending on the specifics of the protocol, different information passes between the participants at different times. The subscriber communicates with both the IdP and the RP, usually through a browser. The RP and the IdP communicate with each other in two ways: -->

- *Front Channel*, Subscriber を介したリダイレクトを通じたコミュニケーション
- *Back Channel*, Subscriber を介さず RP と IdP の直接のコネクションを通じたコミュニケーション

<!--
 - The *front channel*, through redirects involving the subscriber; or
 - The *back channel*, through a direct connection between the RP and IdP, not involving the subscriber.
-->

<a name="63cSec5-Figure1"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/federation.png" alt="Federation Overview" style="width:628px;height:600px;;min-width: 628px;min-height: 600px;"/>

**Figure 5-1 Federation**

</div>

Subscriber は IdP に対して Authenticate し, Authentication イベントの結果が RP に対して Network 経由で提示される. この Transaction において, IdP は [SP 800-63B](sp800-63b.html) にあるように Credential の Verifier として振る舞う. IdP はこのプロセスにおいて Subject に関する Attribute ステートメントを作成することも可能である. Attribute と Authentication イベントの情報は, [Section 6](#assertions) にあるように Assertion を通じて RP に伝送される. さらなる Attribute が Authorized Credential で保護されたセカンダリープロトコルを通じてやりとりされることもある (MAY).

<!-- The subscriber authenticates to the IdP and the result of that authentication event is asserted to the RP across the network. In this transaction, the IdP acts as the verifier for the credential, as described in [SP 800-63B](sp800-63b.html). The IdP can also make attribute statements about the subscriber as part of this process. These attributes and authentication event information are carried to the RP through the use of an assertion, described in [Section 6](#assertions). Additional attributes MAY be made available through a secondary protocol protected by an authorized credential. -->

### <a name="federation-model"></a> 5.1 Federation Models

Authentication サービスを提供する IdP とそれを利用する RP は Federation の参加者として知られている. IdP の視点から見れば, Federation は自身がサービス提供をする RP から構成される. RP の視点から見れば, Federation は自身が利用する IdP から構成される. 本セクションでは, 今日使われている一般的 Identity Federation モデルに対する要件を概観する. 各モデルにおいて, Federation 参加者間の関係性が確立される.

<!-- IdPs that provide authentication services and RPs that consume those services are known as members of a federation. From an IdP's perspective, the federation consists of the RPs that it serves. From an RP's perspective, the federation consists of the IdPs that it uses. This section provides an overview of and requirements for common identity federation models currently in use. In each model, relationships are established between members of the federation. -->

#### <a name="manual-registration"></a> 5.1.1 Manual Registration

手動の Registration モデルでは, IdP と RP が手動で相互運用する相手に関する設定情報を用意する. IdP は明示的ホワイトリストによって RP を設定し, そこに含まれる RP に関しては Authentication Transaction 中で Authentication や Attribute に関する情報を受け取れるようにしてもよい (MAY). RP がホワイトリストに含まれない場合は, IdP はユーザー情報を提供する前に Authorized な主体によるランタイムでの決断 ([Section 4.2](#runtime-decisions) 参照) を要求とすることとする (SHALL).

<!-- In the manual registration model, the IdP and RP manually provision configuration information about parties with which they expect to interoperate. IdPs MAY configure RPs using an explicit whitelist, allowing these RPs to receive authentication and attribute information as part of the authentication transaction. In cases where an RP is not whitelisted, the IdP SHALL require runtime decisions (see [Section 4.2](#runtime-decisions)) to be made by an authorized party (such as the subscriber) before releasing user information. -->

<a name="63cSec5-Figure2"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/manual.png" alt="Manual Registration" style="width:630px;height:400px;;min-width: 630px;min-height:400px;"/>

**Figure 5-2 Manual Registration**

</div>

[Figure 5-2](#63cSec5-Figure2) に示す通り, 手動の Registration は以下の3ステップからなる.

<!-- As shown in [Figure 5-2](#63cSec5-Figure2), manual registration involves three steps: -->

1. RP のシステム管理者が RP の Attribute を IdP のシステム管理者に共有し, IdP のシステム管理者はその Attribute を RP に関連づける.

2. IdP のシステム管理者が IdP の Attribute を RP のシステム管理者に共有し, RP のシステム管理者はその Attribute を IdP に関連づける.

3. その後 IdP と RP は標準的 Federation プロトコルを使ってコミュニケーションする.

<!-- 1. The RP's system administrator shares the RP's attributes with the IdP's system administrator, who associates those attributes with the RP.

2. The IdP's system administrator shares the IdP's attributes with the RP's system administrator, who associates those attributes with the IdP.

3. The IdP and RP then communicate using a standard federation protocol. -->

IdP と RP は, 自身を自身のオーソリティーとしてもよいし (MAY), [Section 5.1.3](#authorities) のようにオーソリティー権限を外部の主体に移譲してもよい (MAY).

<!-- IdPs and RPs MAY act as their own authorities on who to federate with or MAY externalize those authority decisions to an external party as in [Section 5.1.3](#authorities). -->

鍵情報の伝送を必要とするプロトコルでは, Rigistration プロセスにおいてセキュアな方法で Federated な関係性の運用に必要な鍵情報を交換すること (SHALL). これには Shared Secret も Public Key も含まれる. この関係性を示すために利用される鍵が Symmetric Key である場合は, Federation 参加者ペア毎にユニークでなければならない (SHALL).

<!-- Protocols requiring the transfer of keying information SHALL use a secure method during the registration process to exchange keying information needed to operate the federated relationship, including any shared secrets or public keys. Any symmetric keys used in this relationship SHALL be unique to a pair of federation participants. -->

Federation の関係性に対して, 期待され許容される IAL および AAL についてのパラメーターを確立すること (SHALL).

<!-- Federation relationships SHALL establish parameters regarding expected and acceptable IALs and AALs in connection with the federated relationship. -->

#### <a name="dynamic-registration"></a> 5.1.2 Dynamic Registration

Federation の動的な Registration モデルでは, Transaction 実行時に Federation 参加者間でその関係性を取り決めるすることが可能である. このプロセスにおいて IdP と RP は, 手動 Registration ([Section 5.1.1](#manual-registration) 参照) により手動でコネクションを確立することなく, 相互接続することができる. 動的 Registration をサポートする IdP は, 自身の設定情報 (動的 Registration のエンドポイント等) を取得可能にし, システム管理者の関与を最小化すること (SHALL).

<!-- In the dynamic registration model of federation, it is possible for relationships between members of the federation to be negotiated at the time of a transaction. This process allows IdPs and RPs to be connected together without manually establishing a connection between them using manual registration (See [Section 5.1.1](#manual-registration)). IdPs that support dynamic registration SHALL make their configuration information (such as dynamic registration endpoints) available in such a way as to minimize system administrator involvement. -->

<a name="63cSec5-Figure3"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/dynamic.png" alt="Dynamic Registration" style="width:630px;height:338px;;min-width: 630px;min-height:338px;"/>

**Figure 5-3 Dynamic Registration**

</div>

[Figure 5-3](#63cSec5-Figure3) に示す通り, 動的な Registration は以下の4ステップからなる.

<!-- As shown in [Figure 5-3](#63cSec5-Figure3), dynamic registration involves four steps: -->

1. 発見. RP は IdP の周知な場所に行き, IdP のメタデータを発見する.

2. 確認. RP と RP はお互いの正当性を確認する. これには鍵情報やメタデータ, Software Statement, その他の方法などが利用できる.

3. RP Attribute の登録. RP は自身の Attribute を IdP に送り, IdP はその Attribute を当該 RP に関連づける.

4. Federastion プロトコル. IdP と RP は標準の Federation プロトコルを使ってコミュニケーションする.

<!-- 1. Discover. The RP goes to a well-known location at the IdP to find the IdP's metadata.

2. Validate. The RP and IdP determine each other's validity. This can be accomplished through keying information, metadata, software statements, or other means.

3. Register RP attributes. The RP sends its attributes to the IdP, and the IdP associates those attributes with the RP.

4. Federation Protocol. The IdP and RP then communicate using a standard federation protocol. -->

鍵情報の伝送を必要とするプロトコルでは, Rigistration プロセスにおいてセキュアな方法で Federated な関係性の運用に必要な鍵情報を交換すること (SHALL). これには Shared Secret も Public Key も含まれる. この関係性を示すために利用される鍵が Symmetric Key である場合は, Federation 参加者ペア毎にユニークでなければならない (SHALL).

<!-- Protocols requiring the transfer of keying information SHALL use a secure method during the registration process to establish such keying information needed to operate the federated relationship, including any shared secrets or public keys. Any symmetric keys used in this relationship SHALL be unique to a pair of federation participants. -->

IdP はユーザー情報を提供する前に Authorized な主体 (Subscriber 等) によるランタイムでの決断 ([Section 4.2](#runtime-decisions) 参照) を要求とすることとする (SHALL). 動的 Registration を行う RP を受け入れる IdP は, そういった RP が利用できる Attribute やその他の情報のタイプを制限してもよい (MAY). 動的 Registration を利用可能な RP は, Identity 情報を受け入れる IdP を制限してもよい (MAY).

<!-- IdPs SHALL require runtime decisions (see [Section 4.2](#runtime-decisions)) to be made by an authorized party (such as the subscriber) before releasing user information. An IdP accepting dynamically registered RPs MAY limit the types of attributes and other information made available to such RPs. An RP capable of dynamically registering MAY limit which IdPs it is willing to accept identity information from. -->

動的 Registration モデルの参加者は, しばしばお互いのことを事前に知らないことがある. 可能であれば, Federation 参加者が動的に登録した RP の Attribute のいくつかを暗号論的に検証できるよう, *Software Statement* により補強すべきである (SHOULD). Software Statement は RP ソフトウェアに関する Attribute を列挙したものであり, オーソリティー (IdP 自身, [Section 5.1.3](#authorities) にある Federation Authority, その他の信頼できる主体) により暗号論的に署名されている. この暗号論的に検証可能なステートメントにより, Self-asserted Attribute のみに頼る必要がなくなり, Federation 参加者間のコネクションを確立ないし向上させることができる. ([RFC 7591](#RFC7591) Section 2.3 にあるプロトコルにおける Software Statement の実装に関する詳しい情報がある)

<!-- Parties in a dynamic registration model frequently do not know each other ahead of time. Where possible, this SHOULD be augmented by *software statements*, which allow federated parties to cryptographically verify some attributes of an RP being dynamically registered. Software statements are lists of attributes describing the RP software, cryptographically signed by an authority (either the IdP itself, a federation authority as in [Section 5.1.3](#authorities), or another trusted party). This cryptographically-verifiable statement allows the connection to be established or elevated between the federating parties without relying solely on self-asserted attributes. (See [RFC 7591](#RFC7591) Section 2.3 for more information on one protocol's implementation of software statements.) -->

#### <a name="authorities"></a> 5.1.3 Federation Authorities

一部の Federation 参加主体は, Federation の決定および主体間の関係性構築に関して, *Federation Authority* と呼ばれるオーソリティーに従う. このモデルでは, Federation Authority は Federation に参加する各主体に対して一定レベルの審査を実施し, 所定のセキュリティーおよび完全性基準を遵守しているかを検証するのが一般的である. もし審査を行う場合, 審査レベルは Federation のユースケースやモデルごとにユニークとなる. [Figure 5-4](#63cSec5-Figure4) にはこの審査についての描写がある.

<!-- Some federated parties defer to an authority, known as a *federation authority*, to assist in making federation decisions and to establish the working relationship between parties. In this model, the federation authority generally conducts some level of vetting on each party in the federation to verify compliance with predetermined security and integrity standards. The level of vetting &mdash; if it occurs at all &mdash; is unique to the use cases and models employed within the federation. This vetting is depicted in the left side of [Figure 5-4](#63cSec5-Figure4). -->

Federation Authority は, IdP が特定の IAL, AAL, FAL で運営することを承認する. この情報は, [Figure 5-4](#63cSec5-Figure4) 右にあるように, Relying Party によって利用され, どの Identity Provider が当該 RP の要件に合うかの判断材料となる.

<!-- Federation authorities approve IdPs to operate at certain IALs, AALs, and FALs. This information is used by relying parties, as shown in the right side of [Figure 5-4](#63cSec5-Figure4), to determine which identity providers meet their requirements. -->

Federation Authority は, 自身が有効化する Federated な関係性に関して, 期待され受入可能な IAL, AAL, FAL に関するパラメーターを規定すること (SHALL). Federation Authority は, Federation 参加者を個別に審査し, 期待されるセキュリティー, Identity およびプライバシー基準に準拠しているかを判断すること (SHALL).

<!-- Federation authorities SHALL establish parameters regarding expected and acceptable IALs, AALs, and FALs in connection with the federated relationships they enable. Federation authorities SHALL individually vet each participant in the federation to determine whether they adhere to their expected security, identity, and privacy standards. -->

<a name="63cSec5-Figure4"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/authority.png" alt="Federation Authority" style="width:789px;height:490px;;min-width:789px;min-height:490px;"/>

**Figure 5-4 Federation Authority**

</div>

IdP および RP の審査には, 最低限以下のような項目を確認すること (SHALL).

<!-- Vetting of IdPs and RPs SHALL establish, as a minimum, that: -->

* IdP が生成した Assertion が [Section 6](#assertions) の要件に準拠しているか.
* RP が, Attribute データの保持, 集約, 第三者への開示などについて, IdP が求める要件に準拠しているか.
* RP と IdP の両システムが, Federation プロトコルの承認されているプロファイルを利用しているか.

<!-- * Assertions generated by IdPs adhere to the requirements in [Section 6](#assertions).
* RPs adhere to IdP requirements for handling subscriber attribute data, such as retention, aggregation, and disclosure to third parties.
* RP and IdP systems use approved profiles of federation protocols. -->

Federation Authority は, IdP の設定データを公開したり RP 向けに Software Statement を発行するなど, メンバー間の技術的接続および設定プロセスを支援してもよい (MAY).

<!-- Federation authorities MAY assist the technical connection and configuration process between members, such as by publishing configuration data for IdPs or by issuing software statements for RPs. -->

オーソリティーに管理された Federation は, ほとんどの場合シンプルなメンバーシップモデルを形成する. このモデルでは, ある主体が Federation に参加しているか否かのみを扱う. より洗練された Federation においては, 複数のメンバーシップ階層が設けられ, ある主体が他の主体に比べてより入念に審査されたかどうかを知ることができるようになっていることもある (MAY). IdP はある Subscriber の情報を一定以上の階層の RP にのみ受け渡すようにしてもよいし (MAY), RP はある情報を一定以上の階層の IdP からのみ受け入れるようにしてもよい (MAY).

<!-- Most federations managed through authorities have a simple membership model: parties are either in the federation or they are not. More sophisticated federations MAY have multiple memberhsip tiers that federated parties can use to tell whether other parties in the federation have been more thoroughly vetted. IdPs MAY decide that certain subscriber information is only releasable to RPs in higher tiers and RPs MAY decide to accept certain information only from IdPs in higher tiers. -->

#### <a name="proxied"></a> 5.1.4 Proxied Federation

Proxied Federation では, IdP と RP の通信は2者間の直接通信を妨げる形で仲介される. これを実現する方法は複数あるが, 共通事項として以下のような項目が挙げられる.

<!-- In a proxied federation, communication between the IdP and the RP is intermediated in a way that prevents direct communication between the two parties. There are multiple methods to achieve this effect. Common configurations include: -->

* 第三者が Federation Proxy (または *Broker*) として動作する.
* 通信を振り分けるノードの Network が存在する.

<!-- * A third party that acts as a federation proxy (or *broker*)
* A network of nodes that distributes the communications -->

Proxy を利用する場合, 当該 Proxy は一方で IdP として振る舞い, もう一方では RP として振る舞う. したがって, IdP と RP に求められる全ての Normative 要件が, 当該 Proxy にも課せられる (SHALL).

<!-- Where proxies are used, they function as an IdP on one side and an RP on the other. Therefore, all normative requirements that apply to IdPs and RPs SHALL apply to proxies in their respective roles. -->

<a name="63cSec5-Figure5"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/broker.png" alt="Federation Proxy" style="width:600px;height:150px;;min-width:600px;min-height:150px;"/>

**Figure 5-5 Federation Proxy**
</div>

Proxied Federation モデルにはいくつかの利点がある. Federation Proxy においてインテグレーションのための共通インターフェースを提供することで, RP と IdP の技術的インテグレーションを単純化することができる. さらに, Proxy が RP と IdP を互いに効果的にブラインドことで, Subscriber のリストを相互に保護したい組織間でのビジネス上の機密性を実現することもできる. また, Proxy は [Section 5.2](#privacy-reqs) に述べるようにいくらかのプライバシーリスクを低減することもできる.

<!-- A proxied federation model can provide several benefits. Federation proxies can simplify technical integration between the RP and IdP by providing a common interface for integration. Additionally, to the extent a proxy effectively blinds the RP and IdP from each other, it can provide some business confidentiality for organizations that want to guard their subscriber lists from each other. Proxies can also mitigate some of the privacy risks described in [Section 5.2](#privacy-reqs) below. -->

ブラインディング技術とその利用, 限界に関しては, [Section 9.5](#blinding) に詳しい.

<!-- See [Section 9.5](#blinding) for further information on blinding techniques, their uses, and limitations. -->

### <a name="privacy-reqs"></a> 5.2 Privacy Requirements

Federation involves the transfer of personal attributes from a third party that is not otherwise involved in a transaction &mdash; the IdP. Federation also potentially gives the IdP broad visibility into subscriber activities. Accordingly, there are specific privacy requirements associated with federation.

Communication between the RP and the IdP could reveal to the IdP where the subscriber is conducting a transaction. Communication with multiple RPs allows the IdP to build a profile of subscriber transactions that would not have existed without federation. This aggregation could enable new opportunities for subscriber tracking and use of profile information that do not always align with subscribers' privacy interests.

The IdP SHALL NOT disclose information on subscriber activities at an RP to any party, nor use the subscriber's information for any purpose other than federated authentication, related fraud mitigation, to comply with law or legal process, or in the case of a specific user request, to transmit the information. The IdP SHOULD employ technical measures, such as the use of pairwise pseudonymous identifiers described in [Section 6.3](#ppi) or privacy-enhancing cryptographic protocols, to provide unlinkability and discourage subscriber activity tracking and profiling.

An IdP MAY disclose information on subscriber activities to other RPs within the federation for security purposes, such as communication of compromised subscriber accounts.

The following requirements apply specifically to federal agencies:

1. The agency SHALL consult with their Senior Agency Official for Privacy (SAOP) to conduct an analysis determining whether the requirements of the Privacy Act are triggered by the agency that is acting as an IdP, by the agency that is acting as an RP, or both (see [Section 9.4](#agency-privacy)).

2. The agency SHALL publish or identify coverage by a System of Records Notice (SORN) as applicable.

3. The agency SHALL consult with their SAOP to conduct an analysis determining whether the requirements of the E-Government Act are triggered by the agency that is acting as an IdP, the agency that is acting as an RP, or both.

4. The agency SHALL publish or identify coverage by a Privacy Impact Assessment (PIA) as applicable.

### 5.3 <a name="federation-session"></a> Reauthentication and Session Requirements in Federated Environments

In a federated environment, the RP manages its sessions separately from any sessions at the IdP. The session at the RP starts when the RP processes the federation protocol from the IdP. At the time of a federated login, the subscriber MAY have an existing session at the IdP which MAY be used as part of the authentication process to the RP. The IdP SHALL communicate any information it has regarding the time of the latest authentication event at the IdP, and the RP MAY use this information in determining its access policies. Depending on the capabilities of the federation protocol in use, the IdP SHOULD allow the RP to request that the subscriber re-authenticate at the IdP as part of a federation request.

Due to the distributed nature of a federated system, the subscriber is capable of terminating sessions with the IdP and RP independently of one another. The RP SHALL NOT assume that the subscriber has an active session at the IdP past the establishment of the federated log in. The IdP SHALL NOT assume that termination of the subscriber's session at the IdP will propagate to any sessions that subscriber would have at downstream RPs.

See [SP 800-63B Section 7](sp800-63b.html#sec7) for more information about session management requirements.
