<a name="security"></a>

## 8 Security

*This section is informative.*

Federated Authentication プロセスには, IdP として振る舞う CSP を含め, 複数の構成要素間の連携がつきものなので, Attacker が Federated Identity Transaction を毀損するチャンスは増加する. 本セクションでは Federation に対する Attack とその対策についてまとめる.

<!-- Since the federated authentication process involves coordination between multiple components, including the CSP which now acts as an IdP, there are additional opportunities for attackers to compromise federated identity transactions. This section summarizes many of the attacks and mitigations applicable to federation. -->

### 8.1 Federation Threats

非 Federated な Authentication においては, Attacker のモチベーションは得てして RP が提供するリソースやサービスへの Access (またはより高度は Access) を取得することである. また, Attacker は Subscriber になりすまそうとすることもある. 悪意ある, もしくは侵害された IdP, RP, ユーザーエージェント (e.g., ブラウザー), 一般的に Federation Transactin の外側にいる主体が, 潜在的な Attacker となる. 攻撃を成功させるため, Attacker は Assertion や Assertion Reference を傍受したり改ざんすることも考えられる. さらに, 2者以上の主体が直接 Assertion データの Integrity (完全性) や Confidentiality (機密性) を毀損し, Federation プロトコルを台無しにしようとするかもしれない. こういったタイプの脅威を考慮すると, 自身の権限を超えた権限を取得しようとするあらゆる Authorized な主体は, Attacker とみなされる.

<!-- As in non-federated authentication, attackers' motivations is typically to gain access (or a greater level of access) to a resource or service provided by an RP. Attackers may also attempt to impersonate a subscriber. Rogue or compromised IdPs, RPs, user agents (e.g., browsers), and parties outside of a typical federation transaction are potential attackers. To accomplish their attack, they might intercept or modify assertions and assertion references. Further, two or more entities may attempt to subvert federation protocols by directly compromising the integrity or confidentiality of the assertion data. For the purpose of these types of threats, any authorized parties who attempt to exceed their privileges are considered attackers. -->

場合によっては, RP が認識できるように, Subscriber に秘匿情報を発行することもある. この情報を知っているかどうかで, Subscriber と Subscriber になりすまそうとする Attacker を見分けられる. Holder-of-Key Assertion のケースでは, このシークレットは Federation プロトコル開始前に IdP との間で確立されうる.

<!-- In some cases, the subscriber is issued some secret information so they can be recognized by the RP. Knowledge of this information distinguishes the subscriber from attackers who wish to impersonate them. In the case of holder-of-key assertions, this secret could have been established with the IdP prior to the initiation of the federation protocol. -->

<div class="text-center" markdown="1">

**Table 8-1 Federation Threats**

</div>

| **Federation Threats/Attacks**  | **Description**  | **Examples** |
|---------------------------------|------------------|--------------|
| Assertion 偽造 / 改ざん | Attacker が偽の Assertion を生成する. | 侵害を受けた IdP が適切に Authenticate されていない Claimant の Identity を Assert する. |
| | Attacker が既存の Assertion を改ざんする. | 侵害を受けた Proxy が Authentication Assertion の AAL を変更する. |
| Assertion 漏洩 | Assertion が第三者に閲覧可能になる. | Network モニタリングにより Subscriber の Address of Record が部外者に暴露される. |
| IdP による Assertion 否認 | IdP が後になって Transaction に署名していないと主張する. | ユーザーが RP で不正なクレジットカード Transaction に関与し, IdP は彼らをログインさせていないと主張する. |
| Subscriber による Assertion 否認 | Subscriber が Transaction を実行していないと主張する. | ユーザー同意 (e.g., 契約) の不履行. |
| Assertion リダイレクト | Assertion が意図しないコンテキストで利用される. | 侵害を受けたユーザーエージェントが Assertino を Attacker に渡し, Attacker がどこか別の場所でそれを利用する. |
| Assertion 再利用 | Assertion が同じ RP に複数回利用される. | 傍受された Assertion が, Attacker 自身の Session を Authenticate するために利用される. |
| Assertion 置換 | Attacker が意図されていない Subscriber の為に Assertion を利用する. | IdP と RP の間での Session Hijacking Attack. |

<!--
| **Federation Threats/Attacks**  | **Description**  | **Examples** |
|---------------------------------|------------------|--------------|
| Assertion Manufacture or Modification | The attacker generates a false assertion | Compromised IdP asserts identity of a claimant who has not properly authenticated |
| | The attacker modifies an existing assertion | Compromised proxy that changes AAL of an authentication assertion |
| Assertion Disclosure | Assertion visible to third party | Network monitoring reveals subscriber address of record to an outside party |
| Assertion Repudiation by the IdP | IdP later claims not to have signed transaction | User engages in fraudulent credit card transaction at RP, IdP claims not to have logged them in |
| Assertion Repudiation by the Subscriber | Subscriber claims not to have performed transaction | User agreement (e.g., contract) cannot be enforced |
| Assertion Redirect | Assertion can be used in unintended context | Compromised user agent passes assertion to attacker who uses it elsewhere |
| Assertion Reuse | Assertion can be used more than once with same RP | Intercepted assertion used by attacker to authenticate their own session |
| Assertion Substitution | Attacker uses an assertion intended for a different subscriber | Session hijacking attack between IdP and RP |
-->

### 8.2 Federation Threat Mitigation Strategies

上記の脅威を緩和するのに役立つメカニズムを Table 8-2 に示す.

<!-- Mechanisms that assist in mitigating the above threats are identified in Table 8-2. -->

<div class="text-center" markdown="1">

**Table 8-2 Mitigating Federation Threats**

</div>

| **Federation Threat/Attack** | **Threat Mitigation Mechanisms** | **Normative Reference(s)** |
|------------------------------|----------------------------------|---|
| Assertion 偽造 / 改ざん | IdP が Assertion に暗号論的に署名を施し, RP がそれを検証する. | [4.1](#key-mgmt), [6](#assertions) |
| | Assertion を Authenticated Protected Channel 経由で IdP を Authenticate した状態で送信する. | [7.1](#back-channel), [7.2](#front-channel) |
| | 推測不能でランダムな識別子を Assertion に含める. | [6.2.1](#assertion-id) |
| Assertion 漏洩 | Assertion を Authenticated Protected Channel 経由で RP を Authenticate した状態で送信する. | [7.1](#back-channel), [7.2](#front-channel) |
| | Assertion を特定 RP に対して暗号化する. (双方向の Authenticated Protected Channel で実現可能) | [6.2.3](#encrypted-assertion) |
| IdP による Assertion 否認 | IdP が否認防止 (non-repudiation) 可能な鍵で Assertion に暗号論的に署名を施し, RP がそれを検証する. | [6.2.2](#signed-assertion) |
| Subscriber による Assertion 否認 | Holder-of-Key Assertion を発行する. 提示された鍵所有証明 (Proof of Posession) が Subscriber の関与を立証する. | [6.1.2](#holderofkey) |
| Assertion リダイレクト | 署名対象のコンテンツ内に, Assertion 発行先の RP ("audience") の Identity を含める. RP は自身が意図された受信者であることを検証する. | [6](#assertions), [7.1](#back-channel), [7.2](#front-channel) |
| Assertion 再利用 | Assertion の有効期限を短くし, 署名対象のコンテンツ内に発行日時を含める. RP はその正当性を検証する. | [6](#assertions), [7.1](#back-channel), [7.2](#front-channel) |
| | RP は任意の設定可能な時間内において消費した Assertion をトラックし, 渡された Assertion が1回以上利用されていないことを保証する. | [6.2.1](#assertion-id) |
| Assertion 置換 | Assertion に Assertion リクエストの参照や RP のリクエストに暗号論的に紐づけられたその他の nonce が含まれることを保証する. | [6](#assertions) |
| | Assertion を, Back-Channel モデルなどのように, リクエストと同じ Authenticated Protected Channel で送信する. |[7.1](#back-channel)|

<!--
| **Federation Threat/Attack** | **Threat Mitigation Mechanisms** | **Normative Reference(s)** |
|------------------------------|----------------------------------|---|
| Assertion Manufacture or Modification | Cryptographically sign the assertion at IdP and verify at RP | [4.1](#key-mgmt), [6](#assertions) |
| | Send assertion over an authenticated protected channel authenticating the IdP | [7.1](#back-channel), [7.2](#front-channel) |
| | Include a non-guessable random identifier in the assertion | [6.2.1](#assertion-id) |
| Assertion Disclosure | Send assertion over an authenticated protected channel authenticating the RP | [7.1](#back-channel), [7.2](#front-channel) |
| | Encrypt assertion for a specific RP (may be accomplished by use of a mutually authenticated protected channel) | [6.2.3](#encrypted-assertion) |
| Assertion Repudiation by the IdP | Cryptographically sign the assertion at the IdP with a key that supports non-repudiation; verify signature at RP | [6.2.2](#signed-assertion) |
| Assertion Repudiation by the Subscriber | Issue holder-of-key assertions; proof of possession of presented key verifies subscriber's participation | [6.1.2](#holderofkey) |
| Assertion Redirect | Include identity of the RP ("audience") for which the assertion is issued in its signed content; RP verifies that they are intended recipient | [6](#assertions), [7.1](#back-channel), [7.2](#front-channel) |
| Assertion Reuse | Include an issuance timestamp with short validity period in the signed content of the assertion; RP verifies validity | [6](#assertions), [7.1](#back-channel), [7.2](#front-channel) |
| | RP keeps track of assertions consumed within a configurable time window to ensure that a given assertion is not used more than once. | [6.2.1](#assertion-id) |
| Assertion Substitution | Ensure that assertions contain a reference to the assertion request or some other nonce that was cryptographically bound to the request by the RP | [6](#assertions) |
| | Send assertions in the same authenticated protected channel as the request, such as in the back-channel model |[7.1](#back-channel)|
-->
