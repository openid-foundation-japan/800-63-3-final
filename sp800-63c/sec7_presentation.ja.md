<a name="presentation"></a>

## 7 Assertion Presentation

*This section is normative.*

Assertion は IdP から RP に対して *Back-Channel* ないしは *Front-Channel* で提示される (MAY). それぞれのモデルにはトレードオフがあるが, どちらにおいても Assertion を正しく検証する必要がある. [Section 5.1.4](#proxied) にあるように, ある条件下では Federation を簡単にするため IdP と RP の間を Proxy した状態で Assertion をやりとりすることもある.

<!-- Assertions MAY be presented in either a *back-channel* or *front-channel* manner from the IdP to the RP. There are tradeoffs with each model, but each requires the proper validation of the assertion. Assertions MAY also be proxied to facilitate federation between IdPs and RPs under specific circumstances, as discussed in [Section 5.1.4](#proxied). -->

IdP は RP が明示的に要求した Attribute のみを送信することとする (SHALL). また RP は Privacy Risk Assesment を行い, どの Attribute を要求するか決定することとする (SHALL).

<!-- The IdP SHALL transmit only those attributes that were explicitly requested by the RP. RPs SHALL conduct a privacy risk assessment when determining which attributes to request. -->

### <a name="back-channel"></a> 7.1 Back-Channel Presentation

*Back-Channel* モデルでは, Subscriber は Assertion Reference を渡され, 一般的には Front-Channel を通じてそれを RP に提示することになる. Assertion Reference はそれ自身では Subscriber に関する情報は持たず, Attacker による偽造や改ざんに耐えねばならない (SHALL). RP がは Assertion を取得するため Assertion Reference を IdP に提示する. その際 RP は通常 RP 自信を IdP に対して Authenticate する.

<!-- In the *back-channel* model, the subscriber is given an assertion reference to present to the RP, generally through the front channel. The assertion reference itself contains no information about the subscriber and SHALL be resistant to tampering and fabrication by an attacker. The RP presents the assertion reference to the IdP, usually along with authentication of the RP itself, to fetch the assertion. -->

<a name="63cSec7-Figure1"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/back-channel.png" alt="Back-channel Presentation" style="width:614px;height:600px;;min-width:614px;min-height:600px;"/>

**Figure 7-1 Back Channel Presentation**

</div>

[Figure 7-1](#63cSec7-Figure1) のとおり, Back-Channel Presentation モデルは以下の3ステップからなる.

<!-- As shown in [Figure 7-1](#63cSec7-Figure1), the back-channel presentation model consists of three steps: -->

1. IdP が Assertion Reference を Front Channel 経由で Subscriber に送信する.
2. Subscriber は Assertion Reference を Front Channel 経由で RP に送信する.
3. RP は Assertion Reference と RP 自身の Credential を Back Channel 経由で IdP に提示する. IdP は Credential を確認し, Assertion を返す.

<!-- 1. The IdP sends an assertion reference to the subscriber through the front channel.
2. The subscriber sends the assertion reference to the RP through the front channel.
3. The RP presents the assertion reference and its RP credentials to the IdP through the back channel. The IdP validates the credentials and returns the assertion. -->

Assertion Rference は

<!-- The assertion reference: -->

1. 特定 RP にのみ利用可能な制限を行うこと (SHALL)
2. ワンタイム (single-use) であること (SHALL)
3. 数秒〜数分程度と有効期限が短いこと (SHOULD)
4. RP の Authentication と同時に提示されること (SHOULD)

<!--
 1. SHALL be limited to use by a single RP.
 2. SHALL be single-use.
 3. SHOULD be time limited with a short lifetime of seconds or minutes.
 4. SHOULD be presented along with authentication of the RP.
-->

このモデルでは, RP は第三者 (Subscriber 自身を含む) による傍受・改ざんの機会を最小化しつつ Assertion を IdP に直接要求する.

<!-- In this model, the RP directly requests the assertion from the IdP, minimizing chances of interception and manipulation by a third party (including the subscriber themselves). -->

この方法では, 最初の Authentication Transaction 終了後も, ユーザーを IdP に送り返すことなく Back-Channel 通信を繰り返し行えるため, RP は IdP に Assertion 自体には含まれない追加の Subscriber に関する Attribute を問い合わせることもできる. この問い合わせは [Section 6](#assertions) にあるように Assertion と同時に発行された Authorization Credential を用いて行う.

<!-- This method also allows the RP to query the IdP for additional attributes about the subscriber not included in the assertion itself, since back-channel communication can continue to occur after the initial authentication transaction has been completed without sending the user back to the IdP. This query occurs using an authorization credential issued alongside the assertion, as described in [Section 6](#assertions). -->

Network Transaction がより多く必要となる一方, やりとりされる情報はそれを必要としている主体以外に渡されることはない. RP が IdP から直接 Assertion を受け取るため, 攻撃箇所は限定される. さらに Assertion を RP に直接インジェクトするのはより困難になる.

<!-- More network transactions are required in the back-channel method, but the information is limited to only those parties that need it. Since an RP is expecting to get an assertion only from the IdP directly, the attack surface is reduced. Consequently, it is more difficult to inject assertions directly into the RP. -->

RP は, Cross-Site Scripting 対策やその他のテクニックを利用し, 偽造ないしキャプチャーされた Assertion Reference のインジェクションから自身を保護すること (SHALL).

<!-- The RP SHALL protect itself against injection of manufactured or captured assertion references by use of cross-site scripting protection or other accepted techniques. -->

RP は Assertion に含まれる要素について, 以下のような点を含めて確認すること.

<!-- Elements within the assertion SHALL be validated by the RP, including: -->

- *Issuer Verification*: Assertion が RP の期待する IdP から発行されている旨を保証すること.
- *Signature Validation*: Assertion の署名が, 当該 Assertion を送信した IdP に関連する鍵と合致する旨を保証すること.
- *Time Validation*: 有効期限と発行日時が現在日時に対して許容範囲内である旨を保証すること.
- *Audience Restriction*: 当該 RP がこの Assertion の受信者として意図されている旨を保証すること.

<!--
 - *Issuer verification*: ensuring the assertion was issued by the IdP the RP expects it to be from.
 - *Signature validation*: ensuring the signature of the assertion corresponds to the key related to the IdP sending the assertion.
 - *Time validation*: ensuring the expiration and issue times are within acceptable limits of the current timestamp.
 - *Audience restriction*: ensuring this RP is the intended recipient of the assertion.
-->

IdP から Subscriber, Subscriber から RP へと Assertion Reference を送信する際には, Authenticated Protected Channel を利用すること (SHALL). RP から IdP に Assertion Reference を送信する際, IdP から RP に Assertion を送信する際も, Authenticated Protected Channel を利用すること (SHALL).

<!-- Conveyance of the assertion reference from the IdP to the subscriber, as well as from the subscriber to the RP, SHALL be made over an authenticated protected channel. Conveyance of the assertion reference from the RP to the IdP, as well as the assertion from the IdP to the RP, SHALL be made over an authenticated protected channel. -->

Assertion Reference を提示する際, IdP は Assertion Reference を提示している主体が Authentication を要求した主体と同一であることを検証すること (SHALL). IdP は, RP に対して Assertion Reference 提示時に自身を Authenticate するよう求めたり, その他の似たような方法により, これを実現することができる. (RP 識別手段となるプロトコルの一例としては [RFC 7636](#RFC7636) が参考になる)

<!-- When assertion references are presented, the IdP SHALL verify that the party presenting the assertion reference is the same party that requested the authentication. The IdP can do this by requiring the RP to authenticate itself when presenting the assertion reference to the IdP or through other similar means (see [RFC 7636](#RFC7636) for one protocol's method of RP identification). -->

[Section 5.1.4](#proxied) に述べる Federation Proxy では, IdP は Proxy に対して Assertion Reference と Assertion の Audience Restriction を行い, Proxy はダウンストリーム RP に対して新たに生成した Assertion Reference や Assertion の Audience Restriction を行うことに注意.

<!-- Note that in a federation proxy described in [Section 5.1.4](#proxied), the IdP audience restricts the assertion reference and assertion to the proxy, and the proxy restricts any newly-created assertion references or assertions to the downstream RP. -->

### <a name="front-channel"></a> 7.2 Front-Channel Presentation

*Front-Channel* モデルでは, IdP は Authentication 成功後 Assertion を生成し Subscriber に渡す. Subscriber は渡された Assertion を利用し, 大抵は Subscriber のブラウザ内のメカニズムを通じて, RP に自身を Authenticate する.

<!-- In the *front-channel* model, the IdP creates an assertion and sends it to the subscriber after successful authentication. The assertion is used by the subscriber to authenticate to the RP, often through mechanisms within the subscriber's browser. -->


<a name="63cSec7-Figure2"></a>

<div class="text-center" markdown="1">
<img src="sp800-63c/media/front-channel.png" alt="Front-channel Presentation" style="width:686px;height:600px;;min-width:686px;min-height:600px;"/>

**Figure 7-2 Front Channel Presentation**

</div>

Front-Channel モデルでは, Assertion は Subscriber によって閲覧されうる. これは Assertion に含まれるシステム情報などの漏洩につながる可能性もある. さらにこのモデルでは, RP が IdP に Assertion 提示後に追加の Attribute を問い合わせることがより困難になる.

<!-- An assertion is visible to the subscriber in the front-channel method, which could potentially cause leakage of system information included in the assertion. Further, it is more difficult in this model for the RP to query the IdP for additional attributes after the presentation of the assertion. -->

Assertion は Subscriber のコントロール下に置かれることから, Subscriber はブラウザをリプレイして Assertion を複数の RP に送りつけるなどの手段によって, Assertion を本来意図されない主体に送りつけることもできる. Assertion が Audience Restriction により意図しない RP に拒否されたとしても, 意図しない RP への Assertion の提示は Subscriber に関する情報や Subscriber のオンラインアクティビティの漏洩につながりうる. 意図して複数の RP に提示できるよう設計された Assertion を生成することも可能だが, そのような手法は当該 Assertion に対する Audience Restriction を緩め, 当該 RP 間における Subscriber のプライバシーおよびセキュリティー侵害につながりうる. よってそのような複数 RP に対する利用は推奨しない. RP はそれぞれ個別の Assertion を取得するよう推奨される.

<!-- Since the assertion is under the subscriber's control, the front-channel presentation method also allows the subscriber to submit a single assertion to unintended parties, perhaps by a browser replaying an assertion at multiple RPs. Even if the assertion is audience-restricted and rejected by unintended RPs, its presentation at unintended RPs could lead to leaking information about the subscriber and their online activities. Though it is possible to intentionally create an assertion designed to be presented to multiple RPs, this method can lead to lax audience restriction of the assertion itself, which in turn could lead to privacy and security breaches for the subscriber across these RPs. Such multi-RP use is not recommended. Instead, RPs are encouraged to fetch their own individual assertions. -->

RP は, Cross-Site Scripting 対策やその他のテクニックを利用し, 偽造ないしキャプチャーされた Assertion のインジェクションから自身を保護すること (SHALL).

<!-- The RP SHALL protect itself against injection of manufactured or captured assertions by use of cross-site scripting protection or other accepted techniques. -->

RP は Assertion に含まれる要素について, 以下のような点を含めて確認すること.

<!-- Elements within the assertion SHALL be validated by the RP including: -->

- *Issuer Verification*: Assertion が RP の期待する IdP から発行されている旨を保証すること.
- *Signature Validation*: Assertion の署名が, 当該 Assertion を生成した IdP に関連する鍵と合致する旨を保証すること.
- *Time Validation*: 有効期限と発行日時が現在日時に対して許容範囲内である旨を保証すること.
- *Audience Restriction*: 当該 RP がこの Assertion の受信者として意図されている旨を保証すること.

<!--
 - *Issuer verification*: ensuring the assertion was issued by the expected IdP.
 - *Signature validation*: ensuring the signature of the assertion corresponds to the key related to the IdP making the assertion.
 - *Time validation*: ensuring the expiration and issue times are within acceptable limits of the current timestamp.
 - *Audience restriction*: ensuring this RP is the intended recipient of the assertion.
-->

IdP から Subscriber, Subscriber から RP へと Assertion を送信する際には, Authenticated Protected Channel を利用すること (SHALL).

<!-- Conveyance of the assertion from the IdP to the subscriber, as well as from the subscriber to the RP, SHALL be made over an authenticated protected channel. -->

[Section 5.1.4](#proxied) に述べる Federation Proxy では, IdP は Proxy に対して Assertion の Audience Restriction を行い, Proxy はダウンストリーム RP に対して新たに生成した Assertion の Audience Restriction を行うことに注意.

<!-- Note that in a federation proxy described in [Section 5.1.4](#proxied), the IdP audience restricts the assertion to the proxy, and the proxy restricts any newly-created assertions to the downstream RP. -->

### <a name="protecting-information"></a> 7.3 Protecting Information

IdP と RP の間の通信は, Authenticated Protected Channel を利用して保護すること (SHALL). Subscriber と IdP および RP それぞれとの間の通信 (通常はブラウザーを介して行われる) も Authenticated Protected Channel Channel を介して行うこと (SHALL).

<!-- Communications between the IdP and the RP SHALL be protected in transit using an authenticated protected channel. Communications between the subscriber and either the IdP or the RP (usually through a browser) SHALL be made using an authenticated protected channel. -->

IdP は, RP がセキュリティポリシーを適用する際に有用な情報に Access できる可能性もある. こういった情報としては, Device Identity, 位置情報, システムヘルスチェック情報, 設定管理情報等があげられる. IdP がこういった情報を取得できる場合, Subscriber のプライバシーを侵害しない範囲内で, そういった情報を RP に渡すことも可能であろう. 詳細は [Section 9.2](#notice) を参照のこと.

<!-- Note that the IdP may have access to information that may be useful to the RP in enforcing security policies, such as device identity, location, system health checks, and configuration management. If so, it may be a good idea to pass this information along to the RP within the bounds of the subscriber's privacy preferences described in [Section 9.2](#notice). -->


ユーザーに関する追加の Attribute は, Assertion とは別に, RP から IdP への Authorized なリクエストを通じてやり取りされてもよい (MAY). こういった Attribute への Access に対する Authorization は, Assertion と一緒に発行することもできる (MAY). ユーザーに関する情報をこのように分離することで, ユーザーのプライバシー保護に役立ち, Authentication Assertion 自体に必須な情報に添える識別可能な Attribute を限定することも可能になる.

<!-- Additional attributes about the user MAY be included outside of the assertion itself as part of a separate authorized request from the RP to the IdP. The authorization for access to these attributes MAY be issued alongside the assertion itself. Splitting user information in this manner can aid in protecting user privacy and allow for limited disclosure of identifying attributes on top of the essential information in the authentication assertion itself. -->

RP は, [Section 9.3](#minimization) にあるように, 可能な限り完全な Attribute Value ではなく Attribute Reference を要求し (SHALL), IdP は Attribute Reference をサポートすること (SHALL).

<!-- The RP SHALL, where feasible, request attribute references rather than full attribute values as described in [Section 9.3](#minimization). The IdP SHALL support attribute references. -->

