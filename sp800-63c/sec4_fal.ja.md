<a name="fal"></a>

## 4 Federation Assurance Level (FAL)

*This section is normative.*

本セクションでは, 許容可能な Federation Assurance Level, FAL を定義する. FAL はある Transaction において Assertion を構成および保護するための要件について述べたものである. これらのレベルは, ある Transaction において RP が要求することもあれば, RP と IdP との間の設定で必要とされることもある.

<!-- This section defines allowable Federation Assurance Levels, or FAL. The FAL describes requirements for how assertions are constructed and secured for a given transaction. These levels can be requested by an RP or required by the configuration of both the RP and the IdP for a given transaction. -->

すべての Assertion は [Section 4](#federation) に述べるように Federation プロトコルと共に用いなければならない (SHALL). すべての Assertion は [Section 6](#assertions) に詳説する要件に従わなければならない (SHALL). すべての Assertion は [Section 7](#presentation) に述べるいずれかの方法で提示されなければならない (SHALL). 多様な Federation 実装パターンがありうるが, FAL はよりセキュアな構築オプションを示す明確な推奨事項を提供することを意図している. FAL の表に無いさまざまな側面がありうるが, それらは本 Vol. の扱うところではない. 最適な FAL の詳しい選択方法については [SP 800-63 Section 6.3](sp800-63-3.html#FAL_CYOA) を参考のこと.

<!-- All assertions SHALL be used with a federation protocol as described in [Section 4](#federation). All assertions SHALL comply with the detailed requirements in [Section 6](#assertions). All assertions SHALL be presented using one of the methods described in [Section 7](#presentation). While many different federation implementation options are possible, the FAL is intended to provide clear implementation recommendations representing increasingly secure deployment options. Combinations of aspects not found in the FAL table are possible but outside the scope of this volume. See [SP 800-63 Section 6.3](sp800-63-3.html#FAL_CYOA) for details on how to choose the most appropriate FAL. -->

本表は各 FAL ごとに異なる要件を示す. 一連の各レベルは, より低いレベルのすべての要件を含み, 満たしている. プロキシを介した Federation は, プロキシされる Transaction の中で最も低いレベルとなるものとする (SHALL).

<!-- This table presents different requirements for each FAL. Each successive level subsumes and fulfills all requirements of lower levels. Federations presented through a proxy SHALL be represented by the lowest level used during the proxied transaction. -->

<a name="63cSec4-Table1"></a>

<div class="text-center" markdown="1">


**Table 4-1 Federation Assertion Levels**

</div>

|FAL|Requirement|
|:--:|----|----|
|1|Bearer assertion, signed by IdP.|
|2|Bearer assertion, signed by IdP and encrypted to RP.|
|3|Holder of key assertion, signed by IdP and encrypted to RP.|

例えば, FAL1 は特に機能追加の無い OpenID Connect Basic Client プロファイルや Security Assertion Markup Language (SAML) Web SSO Artifact Binding プロファイルに相当する. FAL2 は, それに加え Assertion (e.g., the OpenID Connect ID Token ないしは SAML Assertion) に対する RP の公開鍵による暗号化を要求する. FAL3 では, FAL2 のすべての要件に加え, Subscriber が暗号論的に Assertion に紐づく鍵の所有証明を行う (e.g., Cryptographic Authenticator を利用) 必要がある. FAL3 で新たに登場した鍵は Subscriber が IdP に対して Authenticate する際に利用する鍵と同一でなくてもいい.

<!-- For example, FAL1 maps to the OpenID Connect Basic Client profile or Security Assertion Markup Language (SAML) Web SSO Artifact Binding profile with no additional features. FAL2 additionally requires that the assertion (e.g., the OpenID Connect ID Token or SAML Assertion) be encrypted to a public key representing the RP in question. FAL3 requires the subscriber to cryptographically prove possession of a key bound to the assertion (e.g., the use of a cryptographic authenticator) along with all requirements of FAL2. The additional key presented at FAL3 need not be the same key used by the subscriber to authenticate to the IdP. -->

RP のリクエストやプロトコルの要件に関わらず, RP は Federation プロトコルにおいて提示される Assertion の性質を観察するだけで, 容易に利用している FAL を知ることができる. したがって RP は, 特定の Authentication Transaction において受け入れる FAL を決定し, 当該 Transaction が FAL 要件を満たすことを保証する責任がある.

<!-- Regardless of what the RP requests or what the protocol requires, the RP can easily detect the FAL in use by observing the nature of the assertion as it is presented as part of the federation protocol. Therefore, the RP is responsible for determining which FALs it is willing to accept for a given authentication transaction and ensuring that the transaction meets that FAL's requirements. -->

RP が [Section 7.2](#front-channel) にある Front-channel 提示手法 (e.g., OpenID Connect Implicit Client プロファイルや SAML Web SSO プロファイル) を用いている場合, Assertion に含まれる情報が意図した RP をのぞく Transaction 中のブラウザやその他の主体に漏洩することを防ぐため, FAL2 以上が必要となる (SHALL).

<!-- If the RP is using a front-channel presentation mechanism, as defined in [Section 7.2](#front-channel) (e.g., the OpenID Connect Implicit Client profile or the SAML Web SSO profile), it SHALL require FAL2 or greater in order to protect the information in the assertion from disclosure to the browser or other parties in the transaction other than the intended RP. -->

さらに IdP は, [SP 800-53](#SP800-53) に定義されている Moderate ないしは High 基準のセキュリティー制御やそれに相当する連邦政府標準 (e.g., [FEDRAMP](#FEDRAMP)) や業界標準から, (制御強化を含む) 適切に適合したセキュリティー制御を採用しなければならない (SHALL).

<!-- Additionally, the IdP SHALL employ appropriately-tailored security controls (to include control enhancements) from the moderate or high baseline of security controls defined in [SP 800-53](#SP800-53) or equivalent federal (e.g., [FEDRAMP](#FEDRAMP)) or industry standard. -->

### <a name="key-mgmt"></a>4.1 Key Management

どの FAL においても, IdP は Assertion を Approved Cryptography による署名および鍵で保護し, RP がその他の RP に対して IdP になりすますことができないよう保証しなければならない (SHALL). Assertion が Asymmetric Key を使った Digital Signature により保護されている場合, IdP は同じ Public Key と Private Key のペアを複数の RP に対する署名に利用することができる (MAY). IdP は, 自身の Public Key を, HTTPS で保護された周知の URL を通じてなど, 検証可能な形で公開することもできる (MAY). Assertion が Shared Key を用いた MAC によって保護されている場合, IdP は RP ごとに異なる Shared Key を使わねばならない (SHALL).

<!-- At any FAL, the IdP SHALL ensure that an RP is unable to impersonate the IdP at another RP by protecting the assertion with a signature and key using approved cryptography. If the assertion is protected by a digital signature using an asymmetric key, the IdP MAY use the same public and private key pair to sign assertions to multiple RPs. The IdP MAY publish its public key in a verifiable fashion, such as at an HTTPS-protected URL at a well-known location. If the assertion is protected by a MAC using a shared key, the IdP SHALL use a different shared key for each RP. -->

政府が運営する AAL2 での Authentication を行う IdP と AAL3 での Authentication を行うすべての IdP は, [FIPS 140](#FIPS140) Level 1 以上の手段で Assertion の署名および暗号化に使う鍵を保護しなければならない (SHALL).

<!-- Government-operated IdPs asserting authentication at AAL2 and all IdPs asserting authentication at AAL3 SHALL protect keys used for signing or encrypting those assertions with mechanisms validated at [FIPS 140](#FIPS140) Level 1 or higher. -->

### 4.2 <a name="runtime-decisions"></a>Runtime Decisions

Federate するという事実をもって情報を提供する許可を得たと解釈してはならない (SHALL NOT). Authentication を行うかどうかや Attribute を提供するかどうかは, ホワイトリストやブラックリスト, Authorized な主体によるランタイムでの決断などによって決定されることもある.

<!-- The fact that parties have federated SHALL NOT be interpreted as permission to pass information. The decision of whether an authentication can occur or attributes may be passed can be determined by the use of a whitelist, a blacklist, or a runtime decision by an authorized party. -->

IdP は RP のホワイトリストを作成し, そこに含まれる RP に対しては Subscriber によるランタイムでの決断なしに IdP による Authentication 結果や Attribute を受け取れるようにすることもできる (MAY). IdP のホワイトリストに含まれるすべての RP は, SP 800-63 スイートの規定と要件に従わなければならない (SHALL). IdP は, [Section 9.2](#notice) にあるように, Subscriber がホワイトリストを確認可能にするものとする (SHALL). IdP は RP のブラックリストを作成し, そこに含まれる RP に対しては Subscriber からの要求があっても IdP による Authentication 結果や Attribute を受け取れないようにすることもできる (MAY). ホワイトリストにおいてもブラックリストにおいても, 利用する Federation プロトコルごとに, RP はドメインや十分にユニークな識別子を用いて識別されることとなる. ホワイトリストにもブラックリストにも含まれない RP はグレーゾーンに配置し, そういった RP に対しては Authorized な主体によるランタイムでの決断に基づいた処理を行うこととする (SHALL). ここでいう Authorized な主体とは, 通常 Subscriber を指す. IdP はある RP に対する Subscriber の Authorization の決定を記憶してもよい (MAY). ただしその場合 IdP は Subscriber が記憶済 Access を将来無効化できるようにすること (SHALL).

<!-- IdPs MAY establish whitelists of RPs authorized to receive authentication and attributes from the IdP without a runtime decision from the subscriber. All RPs in an IdP's whitelist SHALL abide by the provisions and requirements in the SP 800-63 suite. IdPs SHALL make whitelists available to subscribers as described in [Section 9.2](#notice). IdPs MAY also establish blacklists of RPs not authorized to receive authentication or attributes from the IdP, even when requested by the subscriber. Both whitelists and blacklists identify RPs by their domain or other sufficiently unique identifier, depending on the federation protocol in use. Every RP not on a whitelist or a blacklist SHALL be placed by default in a gray area where runtime authorization decisions will be made by an authorized party, usually the subscriber. The IdP MAY remember a subscriber's decision to authorize a given RP, provided that the IdP SHALL allow the subscriber to revoke such remembered access at a future time. -->

RP は IdP のホワイトリストを作成し, そこに含まれる IdP に関しては Subscriber によるランタイムでの決断なしに Authentication 結果や Attribute を受け入れるようにしてもよい (MAY). RP のホワイトリストに含まれるすべての IdP は, SP 800-63 スイートの規定と要件に従わなければならない (SHALL). RP は IdP のブラックリストを作成し, そこに含まれる IdP に関しては Subscriber からの要求があっても Authentication 結果や Attribute を受け入れないようにすることもできる (MAY). ホワイトリストにおいてもブラックリストにおいても, 利用する Federation プロトコルごとに, IdP はドメインや十分にユニークな識別子を用いて識別されることとなる. ホワイトリストにもブラックリストにも含まれない IdP はグレーゾーンに配置し, そういった IdP に対しては Authorized な主体によるランタイムでの決断に基づいた処理を行うこととする (SHALL). ここでいう Authorized な主体とは, 通常 Subscriber を指す. RP はある IdP に対する Subscriber の Authorization の決定を記憶してもよい (MAY). ただしその場合 IdP は Subscriber が記憶済 Access を将来無効化できるようにすること (SHALL).

<!-- RPs MAY establish whitelists of IdPs that the RP will accept authentication and attributes from without a runtime decision from the subscriber. All IdPs in an RP's whitelist SHALL abide by the provisions and requirements in the 800-63 suite. RPs MAY also establish blacklists of IdPs that the RP will not accept authentication or attributes from, even when requested by the subscriber. Both whitelists and blacklists identify IdPs by their domain or other sufficiently unique identifier, depending on the federation protocol in use. Every IdP that is not on a whitelist or a blacklist SHALL be placed by default in a gray area where runtime authorization decisions will be made by an authorized party, usually the subscriber. The RP MAY remember a subscriber's decision to authorize a given IdP, provided that the RP SHALL allow the subscriber to revoke such remembered access at a future time. -->

たとえ相互にホワイトリストに含まれていたとしても, [Section 5.2](#privacy-reqs) に記載する目的以外では, Subscriber に関する情報を IdP と RP の間でやりとりしてはならない (SHALL NOT).

<!-- A subscriber's information SHALL NOT be transmitted between IdP and RP for any purpose other than those described in [Section 5.2](#privacy-reqs), even when those parties are whitelisted. -->

Authorize なしでのセンシティブ情報の漏洩リスク (e.g., ショルダーサーフィング) を軽減するため, IdP はデフォルトではセンシティブ情報をマスクして Subscriber に提示すること (SHALL). IdP は一時的にそれらのマスクを外す手段を Subscriber に提供し, Subscriber が全体の値を閲覧できるようにすること (SHALL). IdP は Subscriber の苦情や問題 (e.g., Subscriber によって Attribute Value が不正確であることが発見される) の是正のための有効な手段を提供すること (SHALL). マスキングと是正についての詳細については, [Section 10](#usability) のユーザビリティーの考察を参照のこと.

<!-- To mitigate the risk of unauthorized exposure of sensitive information (e.g., shoulder surfing), the IdP SHALL, by default, mask sensitive information displayed to the subscriber. The IdP SHALL provide mechanisms for the subscriber to temporarily unmask such information in order for the subscriber to view full values. The IdP SHALL provide effective mechanisms for redress of applicant complaints or problems (e.g., subscriber identifies an inaccurate attribute value). For more details on masking and redress, please see [Section 10](#usability) on usability considerations. -->

Subscriber がランタイムでの決断を行う場合, Subscriber は明示的な通知を受け取り, Subscriber の Attribute が RP に送信される前に肯定的な確認を行えなければならない (SHALL). 最低限 [Section 9.2](#notice) に従って, 最も効果的な通知を行える立場にあり, 確認を得ることになる主体が, 通知を行うべきである (SHOULD). もし利用するプロトコルでオプショナルな Attribute が利用可能であれば, Subscriber はそれらの Attribute を RP に提供するか否かの選択肢を与えられなければならない (SHALL). IdP はなんらかの記憶メカニズムを採用し, 同一 RP に対して同一 Attribute を再送するようにしてもよい (MAY).

<!-- When the subscriber is involved in a runtime decision, the subscriber SHALL receive explicit notice and be able to provide positive confirmation before any attributes about the subscriber are transmitted to any RP. At a minimum, the notice SHOULD be provided by the party in the position to provide the most effective notice and obtain confirmation, consistent with [Section 9.2](#notice). If the protocol in use allows for optional attributes, the subscriber SHALL be given the option to decide whether to transmit those attributes to the RP. An IdP MAY employ mechanisms to remember and re-transmit the exact attribute bundle to the same RP. -->
