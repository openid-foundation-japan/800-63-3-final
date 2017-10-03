<div class="breaker"></div>
<a name="purpose"></a>

## 1 Purpose

*This section is informative.*

本リコメンデーションと付随ドキュメント [SP 800-63](sp800-63-3.html), [SP 800-63A](sp800-63a.html), [SP 800-63B](sp800-63b.html) では, Credential Service Provider (CSP) が Digital Authentication を実装する際の技術的ガイドラインを示す.

<!-- This recommendation and its companion documents, [SP 800-63](sp800-63-3.html), [SP 800-63A](sp800-63a.html), and [SP 800-63B](sp800-63b.html), provide technical guidelines to credential service providers (CSPs) for the implementation of digital authentication. -->

本ドキュメント SP 800-63C では, Federated Identity システムにおける Identity Provider (IdP) と Relying Party (RP) に対する要件を示す. Federation を利用すると, ある一つの IdP が, 独立して個別管理された複数の RP に対して, Assertion を通じて, Authentication と (オプションで) Subscriber の Attribute を提供することができる. 同様に RP が複数の IdP を利用することもできる.

<!-- This document, SP 800-63C, provides requirements to identity providers (IdPs) and relying parties (RPs) of federated identity systems. Federation allows a given IdP to provide authentication and (optionally) subscriber attributes to a number of separately-administered RPs through the use of assertions. Similarly, RPs may use more than one IdP. -->

<div class="breaker"></div>
<a name="introduction"></a>

## 2 Introduction

*This section is informative.*

Federation は Network 接続されたシステム間で Authentication および Subscriber Attribute の情報を伝達可能にするプロセスです. Federation シナリオでは Verifier ないし CSP は Identity Provider / IdP と呼ばれ, RP は IdP が提供する情報を受け取り利用する主体となる.

<!-- Federation is a process that allows for the conveyance of authentication and subscriber attribute information across networked systems. In a federation scenario, the verifier or CSP is referred to as an identity provider, or IdP. The RP is the party that receives and uses the information provided by the IdP. -->

Federated Identity システムは, 上記タスクを完遂するために Assertion を利用する. Assertion は, IdP から RP に当てた Subscriber に関する情報を含んだステートメントである. Federation 技術は, 一般的に RP と IdP が異なる主体であり, 異なる管理下にある場合に利用される. RP は Assertion に含まれる情報を利用して Subscriber を識別し, RP が管理下に置くリソースに Subscriber が Access する際の Authorization 決定を行う. Assertion は通常 Subscriber の識別子を含み, 過去の RP とのインタラクションと Subscriber を紐づけることを可能にする. Assertion はさらに Attribute Value や Attribute Reference を含み, RP での Authorization 決定の際に Subscriber についてのより詳しい特徴を伝えることもある. より大規模な Federation プロトコルにおいては, Attribute が Assertion の外でやり取りされることもある. こういった Attribute Value や Attribute Reference は, Attribute Based Access Control (ABAC) における Access 権限の決定に使われたり, トランザクションを促進 (e.g., 配送先住所) したりする.

<!-- Federated identity systems use assertions to accomplish this task. Assertions are statements from an IdP to an RP that contain information about a subscriber. Federation technology is generally used when the RP and the IdP are not a single entity or are not under common administration. The RP uses the information in the assertion to identify the subscriber and make authorization decisions about their access to resources controlled by the RP. An assertion typically includes an identifier for the subscriber, allowing association of the subscriber with their previous interactions with the RP. Assertions may additionally include attribute values or attribute references that further characterize the subscriber and support the authorization decision at the RP. Additional attributes may also be available outside of the assertion as part of the larger federation protocol. These attribute values and attribute references are often used in determining access privileges for Attribute Based Access Control (ABAC) or facilitating a transaction (e.g., shipping address). -->

Federated Identity シナリオでは, Subscriber は RP に対して直接 Authenticate するわけではない. その代わり, Federation プロトコルを定義し, 通常は RP からのリクエストに応じたレスポンスとして, IdP が Subscriber に紐づいた識別子に対する Assertion を生成する手段をもうける. IdP は ([SP 800-63B, Section 7](sp800-63b.html#sec7) に述べた Session 管理を使うかもしれないが) Subscriber を責任を持って Authenticate する. このプロセスにより, Subscriber は個々の RP に対して独立した Credential を所有・管理することなく, 複数の RP からサービスを受けることができる. また *Single Sign On* も可能となり, Subscriber はひとたび IdP に対して Authenticate すれば, それ以降複数の RP からサービスを受けることもできる.

<!-- In a federated identity scenario, the subscriber does not authenticate directly to the RP. Instead, the federation protocol defines a mechanism for an IdP to generate an assertion for the identifier associated with a subscriber, usually in response to a request from the RP. The IdP is responsible for authenticating the subscriber (though it may use session management as described in [SP 800-63B, Section 7](sp800-63b.html#sec7)). This process allows the subscriber to obtain services from multiple RPs without the need to hold or maintain separate credentials at each. This process can also be used to support *single sign on*, where subscribers authenticate once to an IdP and subsequently obtain services from multiple RPs. -->

Federation には, セキュリティーとプライバシーに関する繊細な要件があり, 注意深い考慮を必要とする, 比較的複雑なマルチパーティープロトコルが必要である. 特定の Federation 構造を評価する際は, 構成要素間のインタラクションに分解すると有益かもしれない. 一般的に, Subscriber と IdP の間の Authentication は SP 800-63B で述べた Authentication 方式に基づいて行われ, IdP と RP の間のインタラクションは SP 800-63A で述べた手順により確立された Attribute およびその他の Self-asserted Attribute を伝達するものとなる. したがって, 本ドキュメントで提示される多くの要件は, これら2つのドキュメントの該当する要件と何らかの関係を有す.

<!-- Federation requires relatively complex multiparty protocols that have subtle security and privacy requirements and require careful consideration. When evaluating a particular federation structure, it may be instructive to break it down into its component interactions. Generally speaking, authentication between the subscriber and the IdP will be based on the authentication mechanisms presented in SP 800-63B, while interactions between the IdP and RP will convey attributes established using procedures in SP 800-63A and other self-asserted attributes. Many of the requirements presented in this document, therefore, have some relationship with corresponding requirements in those two documents. -->

下表は, 本ドキュメントのどのセクションが Normative (規範) であり, どのセクションが Informative (参考) であるかを示している.

<!-- The following table states which sections of the document are normative and which are informative: -->

|Section Name|Normative/Informative|
|----|:--:|
|1. Purpose|Informative|
|2. Introduction|Informative|
|3. Definitions and Abbreviations|Informative|
|4. Federation Assurance Level (FAL)|Normative|
|5. Federation|Normative|
|6. Assertion|Normative|
|7. Assertion Presentation|Normative|
|8. Security|Informative|
|9. Privacy Considerations|Informative|
|10. Usability Considerations|Informative|
|11. Examples|Informative|
|12. References|Informative|
