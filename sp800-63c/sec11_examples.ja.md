<div class="breaker"></div>
<a name="examples"></a>

## 11 Examples

*This section is informative.*

以下では3種類の Assertion テクノロジー, SAML Assertion, Kerberos Ticket, OpenID Connect Token, について述べる. このリストには, すべてのありうる Assertion テクノロジーは含まれないが, Federated Identity システムで一般的に利用されているものを代表している.

<!-- Three types of assertion technologies are discussed below: SAML assertions, Kerberos tickets, and OpenID Connect tokens. This list is not inclusive of all possible assertion technologies, but does represent those commonly used in federated identity systems. -->

### 11.1 Security Assertion Markup Language (SAML)

SAML は, Authentication および Attribute 情報を生成し, 信頼関係のある Entity 間で Internet 越しにやりとりする XML ベースのフレームワークである. 本執筆時点で最新の [SAML](#SAML) 仕様は, 2005/03/15 発行の SAML v2.0 である.

<!-- SAML is an XML-based framework for creating and exchanging authentication and attribute information between trusted entities over the internet. As of this writing, the latest specification for [SAML](#SAML) is SAML v2.0, issued 15 March 2005. -->

SAML の構成要素を以下に示す.

<!-- The building blocks of SAML include: -->

- Assertion の構造を定義する Assertion XML Schema.
- Assertion および Artifact ([Section 7.1](#back-channel) で述べたインダイレクトモードで使われる Assertion Reference) をリクエストする際に利用する SAML Protocol.
- 根底となる通信プロトコル (HTTP や SOAP など) を定義し, SAML Assertion の転送に利用する Binding.

<!--
- The Assertions XML schema, which defines the structure of the assertion.
- The SAML Protocols, which are used to request assertions and artifacts (the assertion references used in the indirect model described in [Section 7.1](#back-channel)).
- The Bindings, which define the underlying communication protocols (such as HTTP or SOAP), and can be used to transport the SAML assertions.
-->

上記の3要素により, "Web Browser SSO" といった特定のユースケースに対応した SAML プロファイルが定義される.

<!-- The three components above define a SAML profile that corresponds to a particular use case such as "Web Browser SSO". -->

SAML Assertion は XML Schema にエンコードされ, 3つのタイプのステートメントを伝搬する.

<!-- SAML Assertions are encoded in an XML schema and can carry up to three types of statements: -->

- *Authentication Statement*: Assertion Issuer, Authenticated Subscriber, 有効期間およびその他の Authentication に関する情報を含む. 例えば, ある Authentication Assertion は Subscriber "John" が 2004/06/06 10:32pm にパスワードを使って Authenticate されたことを示すであろう.

<!-- -   *Authentication statements* include information about the assertion issuer, the authenticated subscriber, validity period, and other authentication information. For example, an Authentication Assertion would state the subscriber "John" was authenticated using a password at 10:32pm on 06-06-2004. -->

- *Attribute Statement*: Subscriber に関する特定の追加特性を含む. 例えば, "John" という Subject に対して, "Role" という Attribute に対して "Manager" という値が付与されている, など.

<!-- -   *Attribute statements* contain specific additional characteristics related to the subscriber. For example, subject "John" is associated with attribute "Role" with value "Manager". -->

- *Authorization Statement*: Subscriber が Access 権を持つリソースを示す. こういったリソースとしては, 特定のデバイス, ファイル, 特定の Web サーバー上の情報などが挙げられる. 例えば, "John" という Subject が, "Role" を拠り所として, "Webserver1002" 上で "Read" というアクションを行える, など.

<!-- -   *Authorization statements* identify the resources the subscriber has permission to access. These resources may include specific devices, files, and information on specific web servers. For example, subject "John" for action "Read" on "Webserver1002" given evidence "Role". -->

Authorization Statement は本ドキュメントの扱うところではなく, ここでは議論しない.

<!-- Authorization statements are beyond the scope of this document and will not be discussed. -->

### 11.2 Kerberos Tickets <a name="kerberos"></a>

The Kerberos Network Authentication Service [[RFC 4120]](#RFC4120) was designed to provide strong authentication for client/server applications using symmetric-key cryptography on a local, shared network. Extensions to Kerberos can support the use of public key cryptography for selected steps of the protocol. Kerberos also supports confidentiality and integrity protection of session data between the subscriber and the RP. Even though Kerberos uses assertions, it was designed for use on shared networks and, therefore, is not truly a federation protocol.

Kerberos supports authentication of a subscriber over an untrusted, shared local network using one or more IdPs. The subscriber implicitly authenticates to the IdP by demonstrating the ability to decrypt a random session key encrypted for the subscriber by the IdP. (Some Kerberos variants also require the subscriber to explicitly authenticate to the IdP, but this is not universal.) In addition to the encrypted session key, the IdP also generates another encrypted object called a Kerberos ticket. The ticket contains the same session key, the identity of the subscriber to whom the session key was issued, and an expiration time after which the session key is no longer valid. The ticket is confidentiality and integrity protected by a pre-established key that is shared between the IdP and the RP during an explicit setup phase.

To authenticate using the session key, the subscriber sends the ticket to the RP along with encrypted data that proves that the subscriber possesses the session key embedded within the Kerberos ticket. Session keys are either used to generate new tickets or to encrypt and authenticate communications between the subscriber and the RP.

To begin the process, the subscriber sends an authentication request to the Authentication Server (AS). The AS encrypts a session key for the subscriber using the subscriber's long-term credential. The long-term credential may either be a secret key shared between the AS and the subscriber, or in the PKINIT variant of Kerberos, a public key certificate. Most variants of Kerberos based on a shared secret key between the subscriber and IdP derive this key from a user-generated password. As such, they are vulnerable to offline dictionary attacks by passive eavesdroppers, unless Flexible Authentication Secure Tunneling (FAST) \[[RFC 6113](#RFC6113)\] or some other tunneling and armoring mechanism is used.

In addition to delivering the session key to the subscriber, the AS also issues a ticket using a key it shares with the Ticket Granting Server (TGS). This ticket is referred to as a Ticket Granting Ticket (TGT), since the verifier uses the session key in the TGT to issue tickets rather than to explicitly authenticate the verifier. The TGS uses the session key in the TGT to encrypt a new session key for the subscriber and uses a key it shares with the RP to generate a ticket corresponding to the new session key. The subscriber decrypts the session key and uses the ticket and the new session key together to authenticate to the RP.

When Kerberos authentication is based on passwords, the protocol is known to be vulnerable to offline dictionary attacks by eavesdroppers who capture the initial user-to-KDC exchange. Longer password length and complexity provide some mitigation to this vulnerability, although sufficiently long passwords tend to be cumbersome for users. However, when Kerberos password-based authentication is used in a FAST (or similar) tunnel, a successful Man-in-the-Middle attack is additionally required in order to perform the dictionary attack.

### 11.3 OpenID Connect

OpenID Connect \[[OIDC](#OIDC)\] is an internet-scale federated identity and authentication protocol built on top of the OAuth 2.0 authorization framework and the JSON Object Signing and Encryption (JOSE) cryptographic system.

OpenID Connect builds on top of the OAuth 2.0 authorization protocol to enable the subscriber to authorize the RP to access the subscriber's identity and authentication information. The RP in both OpenID Connect and OAuth 2.0 is known as the client.

In a successful OpenID Connect transaction, the IdP issues an ID Token, which is a signed assertion in JSON Web Token (JWT) format. The client parses the ID Token to learn about the subscriber and primary authentication event at the IdP. This token contains at minimum the following information about the subscriber and authentication event:

 - `iss` - An HTTPS URL identifying the IdP that issued the assertion.
 - `sub` - An IdP-specific subject identifier representing the subscriber.
 - `aud` - An IdP-specific audience identifier, equal to the OAuth 2.0 client identifier of the client at the IdP.
 - `exp` - The timestamp at which the ID Token expires and after which SHALL NOT be accepted the client.
 - `iat` - The timestamp at which the ID Token was issued and before which SHALL NOT be accepted by the client.

In addition to the ID Token, the IdP also issues the client an OAuth 2.0 access token which can be used to access the UserInfo Endpoint at the IdP. This endpoint returns a JSON object representing a set of attributes about the subscriber, including but not limited to their name, email address, physical address, phone number, and other profile information. While the information inside the ID Token is reflective of the authentication event, the information in the UserInfo Endpoint is generally more stable and could be more general purpose. Access to different attributes from the UserInfo Endpoint is governed by the use of a specially-defined set of OAuth scopes, `openid`, `profile`, `email`, `phone`, and `address`. An additional scope, `offline_access`, is used to govern the issuance of refresh tokens, which allow the RP to access the UserInfo Endpoint when the subscriber is not present. Access to the UserInfo Endpoint is structured as an API and may be available when the subscriber is not present. Therefore, access to the UserInfo Endpoint is not sufficient for proving a subscriber's presence and establishing an authenticated session at the RP.
