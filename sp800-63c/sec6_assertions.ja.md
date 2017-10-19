<div class="breaker"></div>
<a name="assertions"></a>

## 6 Assertions

*This section is normative.*

Authentication 目的で利用される Assertion は, Federated Identity システム内で IdP から RP に伝搬される, Authenticated Subscriber に関するもしくは Authenticated Subscriber に紐づいた, Attribute Value や Attribute Reference のパッケージ化されたセットである. Assertion は Assertion Metadata, Subscriber に関する Attribute Value や Attribute Reference, RP が利用できるその他の情報 (制約や有効期限など) など, 多様な情報を含む. Assertion の第一の機能は RP に対してユーザーを Authenticate することであるが, Assertion 経由で伝搬される情報は RP により多様なユースケースで利用されうる. 例としては, Web サイトにおける Authorization やパーソナライゼーションなどが挙げられる. 本ガイドライン群は, 選択されたソリューションがここに含まれるすべての必須要件を満たす限り, RP のユースケースや Identity を Federate するためのプロトコルタイプやデータタイプに関しては制限しない.

<!-- An assertion used for authentication is a packaged set of attribute values or attribute references about or associated with an authenticated subscriber that is passed from the IdP to the RP in a federated identity system. Assertions contain a variety of information, including: assertion metadata, attribute values and attribute references about the subscriber, and other information that the RP can leverage (such as restrictions and expiration time). While the assertion's primary function is to authenticate the user to an RP, the information conveyed in the assertion can be used by the RP for a number of use cases &mdash; for example, authorization or personalization of a website. These guidelines do not restrict RP use cases nor the type of protocol or data payload used to federate an identity, provided the chosen solution meets all mandatory requirements contained herein. -->

Assertion は単一の Authentication イベントのみを表現することもあれば (MAY), Subscriber に関する Attribute Value や Attribute Reference を表現することもある (MAY).

<!-- Assertions MAY represent only an authentication event, or MAY also represent attribute values and attribute references regarding the subscriber. -->

すべての Assertion は, 以下にあげる Assertion Metadata を含むこととする (SHALL).

<!-- All assertions SHALL include the following assertion metadata: -->

1. Subject: 当該 Assertion が指し示す主体の識別子. (i.e., Subscrier)
2. Issuer: Assertion を発行した IdP の識別子.
3. Audience: Assertion を利用することが想定される主体の識別子 (i.e., RP)
4. Issuance: Assertion が IdP に発行された日時を示すタイムスタンプ.
5. Expiration: Assertion の有効期限を示すタイムスタンプ. RP は有効期限が切れた Assertion を有効な Assertion として受け入れないこと (SHALL). (i.e., Assertion の有効期限切れであり, RP における Session の有効期限切れではない)
6. Identifier: 当該 Assertion 自身を識別するランダムでユニークな値. Attacker による以前の Assertion の再利用を防ぐために利用される.
7. Signature: IdP に紐づいた鍵の識別子や公開鍵を含んだ, Assertion 全体に対する Digital Signature もしくは Message Authentication Code (MAC).
8. Authentication Time: (可能であれば) IdP が Primary Authentication Event を通じて Subscriber を認証した日時を示すタイムスタンプ.

<!-- 1. Subject: An identifier for the party that the assertion is about (i.e., the subscriber).
2. Issuer: An identifier for the IdP that issued the assertion.
3. Audience: An identifier for the party intended to consume the assertion (i.e., the RP).
4. Issuance: A timestamp indicating when the IdP issued the assertion.
5. Expiration: A timestamp indicating when the assertion expires and SHALL no longer be accepted as valid by the RP (i.e., the expiration of the assertion and not the expiration of the session at the RP).
6. Identifier: A value uniquely identifying this assertion, used to prevent attackers from replaying prior assertions.
7. Signature: Digital signature or message authentication code (MAC), including key identifier or public key associated with the IdP, for the entire assertion.
8. Authentication Time: A timestamp indicating when the IdP last verified the presence of the subscriber at the IdP through a primary authentication event (if available). -->

Assertion はさらに以下の情報を含んでもよい (MAY).

<!-- Assertions MAY also include the following information: -->

1. Key binding: Subscriber が保持する鍵の Public Key ないしは識別子であり, [Section 6.1.2](#holderofkey) にあるように当該 Assertion と Subscriber が保持する鍵 との Binding を証明するために使われる.
2. Attribute Value および Attribute Reference: Subscriber に関する情報.
3. Attribute Metadata: 一つ以上の Subscriber Attribute に関する追加の情報. NIST Internal Report 8112 [[NISTIR 8112]](#nistir8112) に述べられているものなどが例として挙げられる.

<!-- 1. Key binding: Public key or key identifier of subscriber-held key to demonstrate their binding with the assertion described in [Section 6.1.2](#holderofkey).
2. Attribute values and attribute references: Information about the subscriber.
3. Attribute metadata: Additional information about one or more subscriber attributes, such as that described in NIST Internal Report 8112 [[NISTIR 8112]](#nistir8112). -->

Assertion は Authentication イベントが Assert された際の AAL と Identity Proofed Attribute (ないしはその Reference) が Assert された際の IAL を明記すべきである (SHOULD). もし明記がない場合, RP は当該 Assertion に対していかなる IAL, AAL も割り当ててはならない (SHALL NOT).

<!-- Assertions SHOULD specify the AAL when an authentication event is being asserted and IAL when identity proofed attributes (or references based thereon) are being asserted. If not specified, the RP SHALL NOT assign any specific IAL or AAL to the assertion. -->

RP は Subject 識別子をグローバルにユニークであるものとして扱わないこと (SHALL). 代わりに, Assertion 中の Subject 識別子は, 通常 Assertion Issuer 管理下のネームスペースに所属している. これにより RP は異なる IdP から提示された Subject を誤ってまとめてしまうことなく, 複数の IdP と対話することができる.

<!-- An RP SHALL treat subject identifiers as not inherently globally unique. Instead, the value of the assertion's subject identifier is usually in a namespace under the assertion issuer's control. This allows an RP to talk to multiple IdPs without incorrectly conflating subjects from different IdPs. -->

Assertion は追加の Attribute を含むこともある (MAY). [Section 7](#presentation) は Assertion に Attribute を含めて提示する際のプライバシー要件を含んでいる. RP は, Assertion と一緒に発行された Authorization Credential を利用して, 別 Transaction で IdP から追加の Identity Attribute を取得してもよい (MAY). こういった追加の Attribute 取得能力は, Assertion を処理することと同等に扱ってはならない (SHALL NOT).

<!-- Assertions MAY include additional attributes. [Section 7](#presentation) contains privacy requirements for presenting attributes in assertions. The RP MAY fetch additional identity attributes from the IdP in one or more separate transactions using an authorization credential issued alongside the original assertion. The ability to successfully fetch such additional attributes SHALL NOT be treated as equivalent to processing the assertion. -->

詳細は利用する Federation プロトコルによって様々であるが, Assertion は RP における単一のログインイベントのみを表すように利用されるべきである (SHOULD). RP が Assertion を利用したのちは, RP は Session Management ([SP 800-63B Section 7](sp800-63b.html#sec7)) 参照) を開始し, Assertion はそこに含まれる有効期限を超えて利用されてはならない (SHALL NOT). しかしながら RP における Session 有効期限は, Assertion 自体の有効期限よりも先に切れることもある (MAY). 詳細は [Section 5.3](#federation-session) を参照のこと.

<!-- Although details vary based on the exact federation protocol in use, an assertion SHOULD be used only to represent a single login event at the RP. After the RP consumes the assertion, session management by the RP comes into play (see [SP 800-63B Section 7](sp800-63b.html#sec7)); an assertion SHALL NOT be used past the expiration time contained therein. However, the expiration of the session at the RP MAY occur prior to the assertion's expiration. See [Section 5.3](#federation-session) for more information. -->

Assertion のライフタイムは発行時から有効期限までの間である. このライフタイムは, RP が Assertion を処理してから Subscriber に対してローカルのアプリケーション Session を払い出すまでに十分な長さである必要があるが, 必要以上に長くするべきではない. 長期間有効な Assertion は詐取やリプレイのリスクが高く, ライフタイムの短い Assertion の方がそういったリスクへの耐性を持つ. Assertion ライフタイムは RP 上の Session を制限するために利用してはならない (SHALL NOT). 詳細は [Section 5.3](#federation-session) を参照のこと.

<!-- The assertion's lifetime is the time between its issuance and its expiration. This lifetime needs to be long enough to allow the RP to process the assertion and create a local application session for the subscriber, but should not be longer than necessary for such establishment. Long-lived assertions have a greater risk of being stolen or replayed; a short assertion lifetime mitigates this risk. Assertion lifetimes SHALL NOT be used to limit the session at the RP. See [Section 5.3](#federation-session) for more information. -->

### 6.1 Assertion Binding <a name="assertion-binding"></a>

Assertion Binding は, Assertion と Subscriber の紐付けを行うのに, Assertion の Claimant が Assertion ないしは Assertion Reference を提示すれば十分か, Assertion が Subscriber に紐づいていることを示す追加の証明を RP が要求するか, という点に基づいて分類することができる.

<!-- Assertion binding can be classified based on whether presentation by a claimant of an assertion, or an assertion reference, is sufficient for binding to the subscriber, or if the RP requires additional proof that the assertion is bound to the subscriber. -->

#### 6.1.1 Bearer Assertions <a name="bearer"></a>

Bearer Assertion は, いかなる主体でも, Bearer の Identity の証明として提示することができる. もし Attacker が, Subscriber を示す正当な Assertion ないし Assertion Reference を詐取・偽造でき, 当該 Assertion ないし Assertion Reference を RP に提示することができれば, Attacker は RP において Subscriber になりすますことができる.

<!-- A bearer assertion can be presented by any party as proof of the bearer's identity. If an attacker can capture or manufacture a valid assertion or assertion reference representing a subscriber and can successfully present that assertion or reference to the RP, then the attacker could be able to impersonate the subscriber at that RP. -->

Bearer Assertion や Bearer Assertion Reference を所有しているだけでは, Subscriber になりすますには必ずしも十分ではないことに注意すること. 例えば Assertion が Back-channel Federation モデル ([Section 7.1](#back-channel) 参照) において提示される場合, Transaction 中でさらなる統制 (RP の識別や Assertion インジェクション対策など) が行われており, RP が不正なアクティビティーから保護されていることもある (MAY).

<!-- Note that mere possession of a bearer assertion or reference is not always enough to impersonate a subscriber. For example, if an assertion is presented in the back-channel federation model (described in [Section 7.1](#back-channel)), additional controls MAY be placed on the transaction (such as identification of the RP and assertion injection protections) that help further protect the RP from fraudulent activity. -->

#### 6.1.2 <a name="holderofkey"></a>Holder-of-Key Assertions

Holder-of-Key Assertion は Subscriber に所持され Subscriber を表現する鍵への参照を含む. Holder-of-Key Assertion 中の鍵の参照は Subscriber を示すものであり, ブラウザー, IdP, RP など当該システム中のいかなる他の主体をも示すものではない. 鍵への参照は Assertion の Issuer によって Assert (ないしは署名) されていることに注意.

<!-- A holder-of-key assertion contains a reference to a key possessed by and representing the subscriber. The key referenced in a holder-of-key represents the subscriber, not any other party in the system including the browser, IdP, or RP. Note that the reference to the key is asserted (and signed) by the issuer of the assertion. -->

RP が Holder-of-Key Assertion を受け取ると, Subscriber は Assertion から参照された鍵を所有していることを直接 RP に証明する. Subscriber は IdP との間で鍵ベースの Authentication 方法を利用することもできるが, IdP 上の Primary Authentication と RP 上の Federated Authentication は独立したものとみなされ, 同じ鍵や関連した Session が利用されるとは想定されない.

<!-- When the RP receives the holder-of-key assertion, the subscriber proves possession of the key referenced in the assertion directly to the RP. While the subscriber could also have used a key-based means of authenticating to the IdP, the primary authentication at the IdP and the federated authentication at the RP are considered separately and are not assumed to use the same keys or related sessions. -->

Subscriber が RP に対して鍵所有証明を行うに際して, Claimant はさらに Assertion の正当な Subject であることをある程度の確からしさで証明することになる. Subscriber 向けに発行された Holder-of-Key Assertion に加え, そこから参照された鍵そのものを詐取する必要があるため, Attacker が詐取した Holder-of-Key Assertion を利用するのはより困難である.

<!-- In proving possession of the subscriber's key to the RP, the claimant also proves with a certain degree of assurance that they are the rightful subject of the assertion. It is more difficult for an attacker to use a stolen holder-of-key assertion issued to a subscriber, since the attacker would need to steal the referenced key material as well. -->

Holder-of-Key Assertion には以下のすべての要件が適用される.

<!-- The following requirements apply to all holder-of-key assertions: -->

1. Subscriber は, Assertion 自体の提示に加えて, RP に対して鍵所有証明を行う必要がある (SHALL).
2. Subscriber が保持する鍵の参照を含み, 鍵所有証明がなされない場合, RP は当該 Assertion を [Bearer Assertion](#bearer) とみなさなければならない (SHALL).
3. 所与の鍵への参照は, Assertion 内のその他の全ての情報と同レベルで信頼すること (SHALL).
4. Assertion には, Holder-of-Key による提示で利用する Private Key や Symmetric Key を, 暗号化せずに含めてはならない (SHALL NOT).
5. 当該鍵は Subscriber が IdP に Authentication する際に利用する鍵とは異なることもある (MAY).
6. 当該鍵は Symmetric Key でもいいし Private Key に紐づいた Public Key でもいい (MAY).
7. RP は Claimant が当該鍵を所有していることを IdP と連動して検証してもよい (MAY). これには, 暗号論的なチャレンジに対して Claimant が計算した署名や MAC を IdP に検証してもらう, などといった例が挙げられる.

<!-- 1. The subscriber SHALL prove possession of that key to the RP, in addition to presentation of the assertion itself.
2. An assertion containing a reference to a key held by the subscriber for which key possession has not been proven SHALL be considered a [bearer assertion](#bearer) by the RP.
3. Reference to a given key SHALL be trusted at the same level as all other information within the assertion.
4. The assertion SHALL NOT include an unencrypted private or symmetric key to be used with holder-of-key presentation.
5. The key MAY be distinct from any key used by the subscriber to authenticate to the IdP.
6. The key MAY be a symmetric key or a public key that corresponds to a private key.
7. The RP MAY verify the claimant's possession of the key in conjunction with the IdP, for example, by requesting that the IdP verify a signature or MAC calculated by the claimant in response to a cryptographic challenge. -->


### 6.2 Assertion Protection

Biding メカニズム ([Section 6.1](#assertion-binding) 参照) や Federation モデル ([Section 5.1](#federation-model) 参照) とは独立して, Assertion は, Attacker が有効な Assertion を偽造したり, 詐取した Assertion を全く異なる RP に対して再利用するといった攻撃を防ぐための一連の保護策を施さなければならない (SHALL). 必要な保護策は考慮されるユースケースの詳細に依存しているが, ここでは推奨される保護策を列挙する.

<!-- Independent of the binding mechanism (discussed in [Section 6.1](#assertion-binding)) or the federation model used to obtain them (described in [Section 5.1](#federation-model)), assertions SHALL include a set of protections to prevent attackers from manufacturing valid assertions or reusing captured assertions at disparate RPs. The protections required are dependent on the details of the use case being considered, and recommended protections are listed here. -->

#### <a name="assertion-id"></a>6.2.1 Assertion Identifier

Assertion は, 対象となる RP が一意に識別できる程度に, 十分ユニークでなければならない (SHALL). Assertion は Nonce, 発行日時, Assertion Identifier やそれらの組み合わせを含めたり, その他のテクニックによってこのユニーク性を達成することができる (MAY).

<!-- Assertions SHALL be sufficiently unique to permit unique identification by the target RP. Assertions MAY accomplish this by use of an embedded nonce, issuance timestamp, assertion identifier, or a combination of these or other techniques. -->

#### 6.2.2 <a name="signed-assertion"></a>Signed Assertion

Assertion は IdP によって暗号論的に署名されること (SHALL). RP は, Issuer の鍵に基づいて各 Assertion の Digital Signature や MAC を確認すること (SHALL). 署名は, Assertion Identifier, Issuer, Audience, Subject および有効期限を含め, Assertion 全体をカバーすること (SHALL).

<!-- Assertions SHALL be cryptographically signed by the issuer (IdP). The RP SHALL validate the digital signature or MAC of each such assertion based on the issuer's key. This signature SHALL cover the entire assertion, including its identifier, issuer, audience, subject, and expiration. -->

Assertion の署名は, Asymmetric Key を利用した Digital Signature か, RP と Issuer の間で共有される Symmetric Key を用いた MAC とすること (SHALL). 本目的のために IdP に利用される Shared Symmetric Key は, Assertion を送信する RP ごとに独立とし (SHALL), 通常は RP 登録時に確立される. Digital Signature の検証に用いる Public Key については, IdP がホストする HTTPS URL を通じてなど, セキュアな方法でランタイムに取得してもよい (MAY).

<!-- The assertion signature SHALL either be a digital signature using asymmetric keys or a MAC using a symmetric key shared between the RP and issuer. Shared symmetric keys used for this purpose by the IdP SHALL be independent for each RP to which they send assertions, and are normally established during registration of the RP. Public keys for verifying digital signatures MAY be fetched by the RP in a secure fashion at runtime, such as through an HTTPS URL hosted by the IdP. Approved cryptography SHALL be used. -->

#### 6.2.3 <a name="encrypted-assertion"></a>Encrypted Assertion

Assertion を暗号化する場合, IdP は RP の Public Key か Shared Symmetric Key を使って Assertion のコンテンツを暗号化すること (SHALL). 本目的のために IdP に利用される Shared Symmetric Key は, Assertion を送信する RP ごとに独立とし (SHALL), 通常は RP 登録時に確立される. 暗号化に用いる Public Key については, IdP がホストする HTTPS URL を通じてなど, セキュアな方法でランタイムに取得してもよい (MAY).

<!-- When encrypting assertions, the IdP SHALL encrypt the contents of the assertion using either the RP's public key or a shared symmetric key. Shared symmetric keys used for this purpose by the IdP SHALL be independent for each RP to which they send assertions, and are normally established during registration of the RP. Public keys for encryption MAY be fetched by the IdP in a secure fashion at runtime, such as through an HTTPS URL hosted by the RP. -->

すべての Assertion の暗号化には Approved Cryptography を利用すること (SHALL).

<!-- All encryption of assertions SHALL use approved cryptography. -->

Assertion がブラウザーなどの第三者を介してやりとりされる場合は, Assertion の暗号化を行うこと (SHALL). 例えば SAML Assertion は XML-Encryption により暗号化することができ, OpenID Connect ID Token は JSON Web Encryption (JWE) により暗号化することができる. IdP から直接 RP に渡される Assertion に関しては, 暗号化してもよい (MAY). 暗号化を行わない場合は Authenticated Protected Channel を介して送ること (SHALL).

<!-- When assertions are passed through third parties, such as a browser, the actual assertion SHALL be encrypted. For example, a SAML assertion can be encrypted using XML-Encryption, or an OpenID Connect ID Token can be encrypted using JSON Web Encryption (JWE). For assertions that are passed directly between IdP and RP, the actual assertion MAY be encrypted. If it is not, the assertion SHALL be sent over an authenticated protected channel. -->

> NOTE: Assertion Encryption は FAL2 と FAL3 で要求される.

<!-- > Note: Assertion encryption is required at FAL2 and FAL3. -->

#### 6.2.4 Audience Restriction

Assertion には Audience Restriction テクニックを用い, RP が自身が Assertion 発行対象となっているか否かを判断できるようにすること (SHALL). すべての RP は, Assertion の Audience に自身の識別子が含まれているかチェックし, ある RP に対して生成された Assertion が他の RP に対してインジェクトされたりリプレイされないようにすること (SHALL).

<!-- Assertions SHALL use audience restriction techniques to allow an RP to recognize whether or not it is the intended target of an issued assertion. All RPs SHALL check that the audience of an assertion contains an identifier for their RP to prevent the injection and replay of an assertion generated for one RP at another RP. -->

#### <a name="ppi"></a>6.3 Pairwise Pseudonymous Identifiers

状況によっては, IdP 上の Subscriber アカウントに対する共通の識別子を通じて, 複数の RP 間で当該 Subscriber が簡単にリンクされないようにすることが望ましい.

<!-- In some circumstances, it is desirable to prevent the subscriber's account at the IdP from being easily linked at multiple RPs through use of a common identifier. -->

#### 6.3.1 General Requirements

IdP が RP に対して生成する Assertion において Pairwise Pseudonymous Subject Identifier を利用する場合, IdP は [Section 6.3.2](#ppi-gen) に述べるように各 RP に異なる識別子を生成すること (SHALL).

<!-- When using pairwise pseudonymous subject identifiers within the assertions generated by the IdP for the RP, the IdP SHALL generate a different identifier for each RP as described in [Section 6.3.2](#ppi-gen) below. -->

RP に対して Attribute を添えて Pairwise Pseudonymous Identifier を利用する場合は, 複数の RP が結託し, Identity Attribute をもとにシステム間で相関づけることで, Subscriber を Re-identify (再識別) することが可能かもしれない. 例えば2つの独立した RP が異なる Pairwise Pseudonymous Identifier によって識別される同一の Subscriber を観察しているとすると, 当該 RP たちは, それぞれが受け取る Assertion 中に Pairwise Pseudonymous Identifier と共に含まれる, 名前, メールアドレス, 物理アドレス, その他の識別に用いられる Attribute を比較することにより, 当該 Subscriber が同一人物であることを知るかもしれない. そういった相関づけはプライバシーポリシーによって禁じられるべきであり (SHOULD), Pairwise Pseudonymous Identifier は Attribute の相関づけに必要な管理努力を増大させることでこういったポリシーの有効性を高めることができる.

<!-- When pairwise pseudonymous identifiers are used with RPs alongside attributes, it may still be possible for multiple colluding RPs to re-identify a subscriber by correlation across systems using these identity attributes. For example, if two independent RPs each see the same subscriber identified with different pairwise pseudonymous identifiers, they could still determine that the subscriber is the same person by comparing the name, email address, physical address, or other identifying attributes carried alongside the pairwise pseudonymous identifier in the respective assertions. Privacy policies SHOULD prohibit such correlation, and pairwise pseudonymous identifiers can increase effectiveness of these policies by increasing the administrative effort in managing the attribute correlation. -->

Proxied Federation モデルでは, IdP は Proxy によって Subscriber が Access しようとしている RP を知ることができない可能性があり, 最初の IdP が最後の RP に対して Pairwise Pseudonymous Identifier を生成できないこともあるので注意すること. そのような状況では, Pairwise Pseudonymous Identifier は通常 IdP と Federation Proxy の間で確立される. Proxy は IdP として機能し, ダウンストリームの RP に対して Pairwise Pseudonymous Identifier を提供することができる. プロトコルによっては, Identity プロトコルを機能させるため, Federation Proxy は Pairwise Pseudonymous Identifier をアップストリーム IdP から送られてくる関連する識別子と紐づける必要がある. そのようなケースでは, Proxy は同一の Subscriber を示す各 RP ごとの Pairwise Pseudonymous Identifier を判定し, トラックすることができる. Proxy は, Pairwise Pseudonymous Identifier とその他の識別子間のマッピングを第三者に開示したり, そのマッピング情報を Federated Authentication とそれに関連する不正防止, 法律や法的手続きへの従属, ユーザーからの当該情報の送信を求める特定の要求への応答以外の目的で利用してはならない (SHALL NOT).

<!-- Note that in a proxied federation model, the initial IdP may be unable to generate a pairwise pseudonymous identifier for the ultimate RP, since the proxy could blind the IdP from knowing which RP is being accessed by the subscriber. In such situations, the pairwise pseudonymous identifier is generally established between the IdP and the federation proxy itself. The proxy, acting as an IdP, can itself provide pairwise pseudonymous identifiers to downstream RPs. Depending on the protocol, the federation proxy may need to map the pairwise pseudonymous identifiers back to the associated identifiers from upstream IdPs in order to allow the identity protocol to function. In such cases, the proxy will be able to track and determine which pairwise pseudonymous identifiers represent the same subscriber at different RPs. The proxy SHALL NOT disclose the mapping between the pairwise pseudonymous identifier and any other identifiers to a third party or use the information for any purpose other than federated authentication, related fraud mitigation, to comply with law or legal process, or in the case of a specific user request for the information. -->

#### 6.3.2 <a name="ppi-gen"></a>Pairwise Pseudonymous Identifier Generation

Pairwise Pseudonymous Identifier には, Subscriber に関するいかなる識別情報も含めないようにすること (SHALL). また Subscriber を識別する情報への Access を持つ主体によって推測されないようにすること (SHALL). Pairwise Pseudonymous Identifier は, ランダムに生成し IdP が Subscriber に紐づけるようにしてもよく (MAY), Subscriber に関するその他の情報から不可逆で推測不可能な方法 (e.g., シークレット鍵を利用した鍵付きハッシュ関数を利用) により導出してもよい (MAY). 通常この識別子は, 対となるエンドポイント間 (e.g., IdP-RP) のみが知っており, 当該エンドポイント間のみで利用されることとする (SHALL). ただし IdP は以下の場合, RP の要求にしたがって, 複数の RP に同一の識別子を生成してもよい (MAY).

<!-- Pairwise pseudonymous identifiers SHALL contain no identifying information about the subscriber. They SHALL also be unguessable by a party having access to some information identifying the subscriber. Pairwise pseudonymous identifiers MAY be generated randomly and assigned to subscribers by the IdP or MAY be derived from other subscriber information if the derivation is done in an irreversible, unguessable manner (e.g., using a keyed hash function with a secret key). Normally, the identifiers SHALL only be known by and used by one pair of endpoints (e.g., IdP-RP). However, an IdP MAY generate the same identifier for a subscriber at multiple RPs at the request of those RPs, provided: -->

* 当該 RP 群が, セキュリティードメインや法的所有権を共有するなど, 運用上相関関係を持つ正当な理由があることを実証可能な関係性にある.
* 識別子を共有するすべての RP が, そのような方法で関連づけられることに同意している.

<!-- * Those RPs have a demonstrable relationship that justifies an operational need for the correlation, such as a shared security domain or shared legal ownership; and
* All RPs sharing an identifier consent to being correlated in such a manner. -->

RP は, Privacy Risk Assessment を実施し, 共通の識別子を要求する場合のプライバシーリスクについて考慮すること (SHALL). プライバシー上の考慮点についての詳細は [Section 9.2](#notice) を参照のこと.

<!-- The RPs SHALL conduct a privacy risk assessment to consider the privacy risks associated with requesting a common identifier. See [Section 9.2](#notice) for further privacy considerations. -->

IdP は意図した RP のみが相関関係にあることを保証すること (SHALL). さもないと悪意ある RP が不正に一連の相関関係にある RP になりすまし, 当該 RP 群に対して発行された Pseudonymous Identifier を知ることができてしまうかもしれない.

<!-- The IdP SHALL ensure that only intended RPs are correlated; otherwise, a rogue RP could learn of the pseudonymous identifier for a set of correlated RPs by fraudulently posing as part of that set. -->
