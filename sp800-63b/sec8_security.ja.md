<a name="sec8"></a>

## 8 脅威とセキュリティに関する考慮事項
<!-- ## 8 Threats and Security Considerations -->

*This section is informative.*

### 8.1 Authenticator の脅威
<!-- ### 8.1 Authenticator Threats -->

Authenticator を制御できる Attacker は Authenticator の所有者のように偽装することができる。 Authenticator への脅威は、Authenticator を構成する Authentication 要素の種類ごとの Attack に基づいて分類されることができる :
<!-- An attacker who can gain control of an authenticator will often be able to masquerade as the authenticator's owner. Threats to authenticators can be categorized based on attacks on the types of authentication factors that comprise the authenticator: -->

* *Something you know* は攻撃者に開示されることがある。 Attacker は Memorized Secret を推測するかもしれない。 Authenticator が Shared Secret である場合、Attacker は CSP または Verifier への Access を得てシークレットの値を入手する、または、その値のハッシュに対して辞書 Attack を行うことができるだろう。 Attacker は、PIN やパスコードの入力を観察したり、PIN やパスコードが書かれた記録やジャーナルエントリを見つけたり、またはシークレットをキャプチャーするために不正なソフトウェア (例：キーボードロガー) をインストールしたりするかもしれない。 さらに、Attacker は Verifier によってメンテナンスされている Password データベースに対する Offline Attack によってシークレットを特定するかもしれない。
<!-- * *Something you know* may be disclosed to an attacker. The attacker might guess a memorized secret. Where the authenticator is a shared secret, the attacker could gain access to the CSP or verifier and obtain the secret value or perform a dictionary attack on a hash of that value. An attacker may observe the entry of a PIN or passcode, find a written record or journal entry of a PIN or passcode, or may install malicious software (e.g., a keyboard logger) to capture the secret. Additionally, an attacker may determine the secret through offline attacks on a password database maintained by the verifier. -->

* *Something you have* は紛失、破損、所有者から盗難される、または Attacker によって複製されることがある。 たとえば、所有者のコンピューターへの Access を得た Attacker は、ソフトウェアの Authenticator をコピーするかもしれない。 ハードウェアの Authenticator は、盗難されたり、いじられたり、複製されるかもしれない。 Out-of-band のシークレットは、Attacker によって傍受され、彼らの Session を Authenticate するために利用されるかもしれない。
<!-- * *Something you have* may be lost, damaged, stolen from the owner, or cloned by an attacker. For example, an attacker who gains access to the owner's computer might copy a software authenticator. A hardware authenticator might be stolen, tampered with, or duplicated. Out-of-band secrets may be intercepted by an attacker and used to authenticate their own session. -->

* *Something you are* は複製されることがある。たとえば、Attacker は Subscriber の指紋のコピーを得たり、レプリカを製作するかもしれない。
<!-- * *Something you are* may be replicated. For example, an attacker may obtain a copy of the subscriber's fingerprint and construct a replica. -->

このドキュメントは Subscriber が Verifier に対して虚偽の Authenticate を試みようとしている Attacker と共謀してないことを前提としている。 この前提に立って、Digital Authentication に使用される Authenticator への脅威はいくつかの例とともに [ 表 8-1](#63bSec8-Table1) にリストされる。
<!-- This document assumes that the subscriber is not colluding with an attacker who is attempting to falsely authenticate to the verifier. With this assumption in mind, the threats to the authenticator(s) used for digital authentication are listed in [Table 8-1](#63bSec8-Table1), along with some examples. -->

<a name="63bSec8-Table1"></a>

<div class="text-center" markdown="1">

**表 8-1 - Authenticator の脅威**
<!-- **Table 8-1  Authenticator Threats** -->

</div>


| **Authenticator の脅威/攻撃**  | **説明**  | **例**  |
| ------------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Assertion の製造または変更**  | Attacker が偽の Assertion を生成する  | 危殆化した CSP が 正しくAuthenticate されていない Claimant の Identity を主張する  |
| | Attacker が既存の Assertion を変更する  | Authentication Assertion の AAL を変更する危殆化したプロキシ  |
| **盗難**  | 物理的な Authenticator が Attacker によって盗難される  | ハードウェア暗号化デバイスが盗難される  |
| | | OTP デバイスが盗難される  |
| | | ルックアップシークレット Authenticator が盗難される  |
| | | 携帯電話が盗難される  |
| **複製**  | Subscriber の Authenticator が、本人の知識ごと、または知識なしに複製される  | Password が書かれた紙が開示される  |
|  |  | 電子ファイルに格納されている Password がコピーされる  |
|  |  | ソフトウェア PKI Authenticator (Private Key) がコピーされる  |
|  |  | ルックアップシークレット Authenticator がコピーされる  |
|  |  | 偽造された Biometric Authenticator が製造される  |
| **盗聴**  | Subscriber が認証を行っているときに、 Authenticator Secret または Authenticator Output が攻撃者に暴露される  | キーボードエントリーを監視して Memorized secret を取得する  |
|  |  | キーストロークをロギングするソフトウェアによって、Memorized secret または Authenticator の出力を横取りする  |
|  |  | PIN パッドデバイスから PIN がキャプチャされる  |
|  |  | ハッシュされた Password が取得され、Attacker に別の Authentication で使用される (*pass-the-hash Attack*)  |
|  | Out of band シークレットが、通信チャネルの危殆化によって Attacker に傍受される  | Out of band シークレットが暗号化されていないWi-Fiで送信され、Attacker に受信される  |
| **オフライン クラッキング**  | Authenticator が、Authentication メカニズムの外側で解析メソッドによって明らかにされる  | Software PKI authenticator が、Private Key の復号に使用する正しい Password を識別するための辞書 Attack を受ける  |
| **サイドチャネル Attack**  | Authenticator Secret が、 Authenticator の物理的特性を利用して明らかにされる。  | 鍵がハードウェア Cryptographic Authenticator の差分電力解析によって明らかにされる  |
|  |  | Authenticator への無数の試行の応答時間の解析によって、 Cryptographic Authenticator シークレットが抽出される  |
| **Phishing または Pharming** | Attacker が Verifier や RP であると考えるように Subscriber をだますことで、Authenticator Output がキャプチャされる  | Subscriber が Verifier に偽装した Web サイトに入力することで、Password が明らかにされる  |
|  |  | 銀行 Subscriber が、銀行担当者に見せかけたフィッシャーからのメールに返信することで、Memorized Secret が明らかにされる  |
|  |  | Subscriber が DNS スプーフィングを介して偽の Verifier Webサイトにアクセスしてしまうことで、Memorized Secret が明らかにされる  |
| **Social Engineering**  | Attacker が、Subscriber 自身がAuthenticator Secret または Authenticator Output を明らかにするように説き伏せるために Subscriber と信頼関係を構築する | Subscriber の上司の代理として Password を聞いてきた同僚に対して Subscriber が Memorized Secret を明らかにする  |
|  |  | システム管理者を装った Attacker からの電話問い合わせによって、Subscriber が Memorized Secret を明らかにする  |
|  |  | Attacker が、犠牲者の携帯電話を Attacker にリダイレクトするようにモバイルオペレーターをやりこめることで、SMS経由の Out-of-band シークレットが Attacker に受信される |
| **オンラインでの推測**  | Attacker が Verifier にオンラインで接続し、その Verifier のコンテキストで有効な Authenticator Output を推測しようと試行する  | Memorized Secret を推測するためにオンライン辞書 Attack が利用される  |
|  |  | 正当な Claimant に登録された OTP デバイスの Authenticator Output を推測するために、オンラインでの推測が使用される  |
| **エンドポイントの危殆化**  | エンドポイント上の不正なコードが、接続された Authenticator への Remote Access を Subscriber 同意なしにプロキシする。  | エンドポイントに接続された Cryptographic Authenticator が、Remote から Attacker の Authenticate に使用される  |
|  | エンドポイント上の不正なコードが、Verifier が意図していない Authentication を引き起こす  | Authentication が、Subscriber ではなく Attacker のために行われる  |
|  |  | エンドポイント上の不正なアプリが SMS 経由で送信された Out-of-band シークレットを読みだし、Attacker がシークレットを Authenticate に使用する  |
|  | エンドポイント上の不正なコードが、 Multi-Factor ソフトウェア Cryptographic Authenticator を危殆化させる  | 不正なコードが Authentication をプロキシする、またはエンドポイントから Authenticator の鍵をエクスポートする  |
| **認証されていない Binding**  | Attacker が彼らの管理下の Authenticator を Subscriber のアカウントにバインドさせる  | Attacker が Subscriber への経路の途中で Authenticator やプロビジョニングキーを傍受する  |

<!--
 | **Authenticator Threat/Attack**  | **Description**  | **Examples** |
|------------------------------------|------------------|--------------|
| **Assertion Manufacture or Modification** | The attacker generates a false assertion | Compromised CSP asserts identity of a claimant who has not properly authenticated |
| | The attacker modifies an existing assertion | Compromised proxy that changes AAL of an authentication assertion |
| **Theft** | A physical authenticator is stolen by an Attacker. | A hardware cryptographic device is stolen. |
| | | An OTP device is stolen. |
| | | A look-up secret authenticator is stolen. |
| | | A cell phone is stolen. |
| **Duplication** | The subscriber's authenticator has been copied with or without their knowledge. | Passwords written on paper are disclosed.
| | | Passwords stored in an electronic file are copied. |
| | | Software PKI authenticator (private key) copied. |
| | | Look-up secret authenticator copied. |
| | | Counterfeit biometric authenticator manufactured. |
| **Eavesdropping** | The authenticator secret or authenticator output is revealed to the attacker as the subscriber is authenticating. | Memorized secrets are obtained by watching keyboard entry. |
| | | Memorized secrets or authenticator outputs are intercepted by keystroke logging software. |
| | | A PIN is captured from a PIN pad device. |
| | | A hashed password is obtained and used by an attacker for another authentication (*pass-the-hash attack*). |
| | An out-of-band secret is intercepted by the attacker by compromising the communication channel. | An out-of-band secret is transmitted via unencrypted Wi-Fi and received by the attacker. |
| **Offline Cracking** | The authenticator is exposed using analytical methods outside the authentication mechanism. | A software PKI authenticator is subjected to dictionary attack to identify the correct password to use to decrypt the private key. |
| **Side Channel Attack** | The authenticator secret is exposed using physical characteristics of the authenticator. | A key is extracted by differential power analysis on a hardware cryptographic authenticator. |
| | | A cryptographic authenticator secret is extracted by analysis of the response time of the authenticator over a number of attempts. |
| **Phishing or Pharming** | The authenticator output is captured by fooling the subscriber into thinking the attacker is a verifier or RP. | A password is revealed by subscriber to a website impersonating the verifier.
| | | A memorized secret is revealed by a bank subscriber in response to an email inquiry from a phisher pretending to represent the bank. |
| | | A memorized secret is revealed by the subscriber at a bogus verifier website reached through DNS spoofing.
| **Social Engineering** | The attacker establishes a level of trust with a subscriber in order to convince the subscriber to reveal their authenticator secret or authenticator output. | A memorized secret is revealed by the subscriber to an officemate asking for the password on behalf of the subscriber's boss. |
| | | A memorized secret is revealed by a subscriber in a telephone inquiry from an attacker masquerading as a system administrator. |
| | | An out of band secret sent via SMS is received by an attacker who has convinced the mobile operator to redirect the victim's mobile phone to the attacker. |
| **Online Guessing** | The attacker connects to the verifier online and attempts to guess a valid authenticator output in the context of that verifier. | Online dictionary attacks are used to guess memorized secrets. |
| | | Online guessing is used to guess authenticator outputs for an OTP device registered to a legitimate claimant. |
| **Endpoint Compromise** | Malicious code on the endpoint proxies remote access to a connected authenticator without the subscriber's consent. | A cryptographic authenticator connected to the endpoint is used to authenticate remote attackers. |
| | Malicious code on the endpoint causes authentication to other than the intended verifier. | Authentication is performed on behalf of an attacker rather than the subscriber.
| | | A malicious app on the endpoint reads an out-of-band secret sent via SMS and the attacker uses the secret to authenticate.
| | Malicious code on the endpoint compromises a multi-factor software cryptographic authenticator. | Malicious code proxies authentication or exports authenticator keys from the endpoint.
| **Unauthorized Binding** | An attacker is able to cause an authenticator under their control to be bound to a subscriber's account. | An attacker intercepts an authenticator or provisioning key en route to the subscriber.
 -->

### 8.2 脅威を軽減するストラテジー
<!-- ### 8.2 Threat Mitigation Strategies -->
[表 8-2](#63bSec8-Table2) は、上記で説明された脅威の軽減を支援するメカニズムをまとめたものである。
<!-- Related mechanisms that assist in mitigating the threats identified above are summarized in [Table 8-2](#63bSec8-Table2). -->

<a name="63bSec8-Table2"></a>

<div class="text-center" markdown="1">

**表 8-2 - Authenticator の脅威を軽減する**
<!-- **Table 8-2 Mitigating Authenticator Threats** -->

</div>


| **Authenticator の脅威/攻撃**  | **脅威を軽減するメカニズム**  | **規約の参照**  |
| ------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **盗難**  | Memorized Secret または Biometrics によってアクティブにされる必要がある Multi-Factor Authenticator を使用する | [4.2.1](#aal2types), [4.3.1](#aal3types)  |
|  | Memorized Secret または Biometrics を含む Authenticator を組み合わせて使用する  | [4.2.1](#aal2types), [4.3.1](#aal3types)  |
| **複製**  | Authentication シークレットの抽出や複製が長期的に困難な Authenticator を使用する  | [4.2.2](#aal2req), [4.3.2](#aal3req), [5.1.7.1](#sfcda)  |
| **盗聴**  | 特にキー ロガーなどのマルウェアに感染していないか、エンドポイントがセキュリティを確保できているか、使用する前に確かめる  | [4.2.2](#aal2req)  |
|  | 信頼されていないワイヤレスネットワークを、暗号化されていないセカンダリの out-of-band の Authentication チャネルとして使用することを避ける | [5.1.3.1](#ooba)  |
|  | 認証され、保護されたチャネル経由で Authenticate を行う (例 : ブラウザーウィンドウのロックアイコンを確認する)  | [4.1.2](#aal1req), [4.2.2](#aal2req), [4.3.2](#aal3req)  |
|  | *pass-the-hash* のようなリプレイ Attack に耐性のある Authentication プロトコルを使用する  | [5.2.8](#replay)  |
|  | 信頼された入力と信頼された表示機能の Authentication エンドポイントを使用する  | [5.1.6.1](#sfcsa), [5.1.8.1](#mfcsa)  |
| **オフライン クラッキング**  | 高い Entropy の Authenticator Secret で Authenticator を使用する  | [5.1.2.1](#lusa), [5.1.4.1](#sfotpa), [5.1.5.1](#mfotpa), [5.1.7.1](#sfcda), [5.1.9.1](#mfcda) |
|  | 鍵付きハッシュを含む、ソルト付き、ハッシュ化された状態で Memorized Secret を保存する  | [5.1.1.2](#memsecretver), [5.2.7](#verifier-secrets)  |
| **サイドチャネル Attack**  | シークレットの値に関係なく消費電力とタイミングが一定に保たれるように設計された Authenticator アルゴリズムを使用する  | [4.3.2](#aal3req)  |
| **Phishing または Pharming** | Verifier Impersonation への防御が提供される Authenticator を使用する。  | [5.2.5](#verifimpers)  |
| **Social Engineering**  | カスタマーサービスエージェントなどの第三者による Social Engineering のリスクを引き起こす Authenticator の使用を避ける  | [6.1.2.1](#bindexisting), [6.1.2.3](#replacement)  |
| **オンラインでの推測**  | 高い Entropy の出力を生成する Authenticator を使用する  | [5.1.2.1](#lusa), [5.1.7.1](#sfcda), [5.1.9.1](#mfcda)  |
|  | アクティベーションの試行に繰り返し失敗した後にはロックアップする Authenticator を使用する  | [5.2.2](#throttle)  |
| **エンドポイントの危殆化**  | Subscriber の物理的なアクションを必要とするハードウェア Authenticator を使用する  | [5.2.9](#intent)  |
|  | ソフトウェアベースの鍵は Restricted-Access ストレージで保持する  | [5.1.3.1](#ooba), [5.1.6.1](#sfcsa), [5.1.8.1](#mfcsa)  |
| **認証されていない Binding**  | Authenticator と 関連する鍵のプロビジョニングには MitM に体制のあるプロトコルを使用する  | [6.1](#binding)  |

<!--
| **Authenticator Threat/Attack** | **Threat Mitigation Mechanisms** | **Normative Reference(s)** |
|---------------------------------|----------------------------------|-------|
| **Theft** | Use multi-factor authenticators that need to be activated through a memorized secret or biometric.| [4.2.1](#aal2types), [4.3.1](#aal3types) |
| | Use a combination of authenticators that includes a memorized secret or biometric. | [4.2.1](#aal2types), [4.3.1](#aal3types) |
| **Duplication** |  Use authenticators from which it is difficult to extract and duplicate long-term authentication secrets. | [4.2.2](#aal2req), [4.3.2](#aal3req), [5.1.7.1](#sfcda) |
| **Eavesdropping** | Ensure the security of the endpoint, especially with respect to freedom from malware such as key loggers, prior to use. | [4.2.2](#aal2req) |
| | Avoid use of non-trusted wireless networks as unencrypted secondary out-of-band authentication channels. | [5.1.3.1](#ooba) |
| | Authenticate over authenticated protected channels (e.g., observe lock icon in browser window). | [4.1.2](#aal1req), [4.2.2](#aal2req), [4.3.2](#aal3req) |
| | Use authentication protocols that are resistant to replay attacks such as *pass-the-hash*. | [5.2.8](#replay) |
| | Use authentication endpoints that employ trusted input and trusted display capabilities. | [5.1.6.1](#sfcsa), [5.1.8.1](#mfcsa) |
| **Offline Cracking** | Use an authenticator with a high entropy authenticator secret. | [5.1.2.1](#lusa), [5.1.4.1](#sfotpa), [5.1.5.1](#mfotpa), [5.1.7.1](#sfcda), [5.1.9.1](#mfcda) |
| | Store memorized secrets in a salted, hashed form, including a keyed hash. | [5.1.1.2](#memsecretver), [5.2.7](#verifier-secrets) |
| **Side Channel Attack** | Use authenticator algorithms that are designed to maintain constant power consumption and timing regardless of secret values. | [4.3.2](#aal3req)
| **Phishing or Pharming** | Use authenticators that provide verifier impersonation resistance. | [5.2.5](#verifimpers) |
| **Social Engineering** | Avoid use of authenticators that present a risk of social engineering of third parties such as customer service agents. | [6.1.2.1](#bindexisting), [6.1.2.3](#replacement) |
| **Online Guessing** | Use authenticators that generate high entropy output. | [5.1.2.1](#lusa), [5.1.7.1](#sfcda), [5.1.9.1](#mfcda) |
| | Use an authenticator that locks up after a number of repeated failed activation attempts. | [5.2.2](#throttle) |
| **Endpoint Compromise** | Use hardware authenticators that require physical action by the subscriber. | [5.2.9](#intent) |
| | Maintain software-based keys in restricted-access storage. | [5.1.3.1](#ooba), [5.1.6.1](#sfcsa), [5.1.8.1](#mfcsa) |
| **Unauthorized Binding** | Use MitM-resistant protocols for provisioning of authenticators and associated keys. | [6.1](#binding) |
 -->

[表 8-1](#63bSec8-Table1) で説明された脅威を軽減するために、いくつかのストラテジーを適用できる :
<!-- Several other strategies may be applied to mitigate the threats described in [Table 8-1](#63bSec8-Table1): -->

* *複数の要素* があると、Attack がより成功しにくくなる。 もし Attacker が Cryptographic Authenticator を盗むことと Memorized Secret の推定の両方を必要とするなら、その両方を達成することはとても困難になり得る。
<!-- * *Multiple factors* make successful attacks more difficult to accomplish. If an attacker needs to both steal a cryptographic authenticator and guess a memorized secret, then the work to discover both factors may be too high. -->

* *物理的なセキュリティメカニズム* は盗難された Authenticator を複製から保護するために採用されることがある。物理的なセキュリティメカニズムは、耐タンパー性の確保、検出、および対応を可能にする。
<!-- * *Physical security mechanisms* may be employed to protect a stolen authenticator from duplication. Physical security mechanisms can provide tamper evidence, detection, and response. -->

* 共有されている辞書に現れない *長い Memorized Secret の使用を要求する* ことは、Attacker にすべての入力可能な値を試させる。
<!-- * *Requiring the use of long memorized secrets* that don't appear in common dictionaries may force attackers to try every possible value. -->

* *システムと Network のセキュリティコントロール* は、Attacker がシステムへの Access を得ることや、不正なソフトウェアをインストールすることを防ぐために使用される。
<!-- * *System and network security controls* may be employed to prevent an attacker from gaining access to a system or installing malicious software. -->

* *定期的なトレーニング* は、いつどのように危殆化 —または危殆化の疑い— を報告するか Subscriber の理解を促したり、また、Attacker の Authentication プロセスを破るための試行を示す振る舞いのパターンを認識したりするために実施される。
<!-- * *Periodic training* may be performed to ensure subscribers understand when and how to report compromise — or suspicion of compromise — or otherwise recognize patterns of behavior that may signify an attacker attempting to compromise the authentication process. -->

* *Out of band テクニック* は、登録されたデバイス (例: 携帯電話) を所有していることの検証に使用される。
<!-- * *Out of band techniques* may be employed to verify proof of possession of registered devices (e.g., cell phones). -->

### 8.3 Authenticator の復旧
<!-- ### 8.3 Authenticator Recovery -->

多くの Authentication メカニズムの弱点は、Subscriber が 1 つまたは複数の Authenticator のコントロールを失い、それらを交換する必要がある場合の手続きである。 多くの場合、Subscriber を Authenticate できる残りの選択肢は限られている。経済的な心配 (例 : コールセンター運営のコスト) から、安価であまりセキュアでないバックアップの Authentication メソッドを使用したいと考えさせる。 Authenticator の復旧は、人がアシストをするという点で、Social Engineering Attack のリスクもある。
<!-- The weak point in many authentication mechanisms is the process followed when a subscriber loses control of one or more authenticators and needs to replace them. In many cases, the options remaining available to authenticate the subscriber are limited, and economic concerns (e.g., cost of maintaining call centers) motivate the use of inexpensive, and often less secure, backup authentication methods. To the extent that authenticator recovery is human-assisted, there is also the risk of social engineering attacks. -->

Authentication 要素の完全性を維持するためには、1 つの要素を使用した Authentication を異なる要素の Authenticator を取得するために活用できないことが必要不可欠である。 たとえば、Memorized Secret は新しいルックアップシークレットのリストを得るために使用できてはならない。
<!-- To maintain the integrity of the authentication factors, it is essential that it not be possible to leverage an authentication involving one factor to obtain an authenticator of a different factor. For example, a memorized secret must not be usable to obtain a new list of look-up secrets. -->

### 8.4 Session Attack
<!-- ### 8.4 Session Attacks -->

上記のディスカッションでは Authentication イベント自体に対する脅威に焦点を当てているが、Authentication イベントに続く Session 上のハイジャック Attack は同様のセキュリティインパクトを持つ可能性がある。 [セクション 7](#sec7) の Session 管理ガイドラインは XSSのような Attack に対して Session の完全性を維持するために必要不可欠である。 さらに、実行可能な内容が含まれていないことを確実にするために、[[OWASP-XSS-prevention]](#OWASP-XSS-prevention)に示されるすべての情報をサニタイズすることが重要である。 これらのガイドラインでは、Session シークレットの漏洩に対してさらなる保護を提供するため、Session シークレットが Mobile Code にアクセスできないようにすることも推奨している。
<!-- The above discussion focuses on threats to the authentication event itself, but hijacking attacks on the session following an authentication event can have similar security impacts. The session management guidelines in [Section 7](#sec7) are essential to maintain session integrity against attacks, such as XSS. In addition, it is important to sanitize all information to be displayed [[OWASP-XSS-prevention]](#OWASP-XSS-prevention) to ensure that it does not contain executable content. These guidelines also recommend that session secrets be made inaccessible to mobile code in order to provide extra protection against exfiltration of session secrets. -->

もう一つの Authentication 後の脅威である Cross-site Request Forgery (CSRF) は、複数の Session を同時に有効にするユーザ傾向の利点を利用する。 有効なURLやリクエストが意図せずまたは悪意を持ってアクティブ化される可能性を防ぐために Web リクエストの中に Session 識別子を埋め込んで検証することが重要である。
<!-- Another post-authentication threat, cross-site request forgery (CSRF), takes advantage of users' tendency to have multiple sessions active at the same time. It is important to embed and verify a session identifier into web requests to prevent the ability for a valid URL or request to be unintentionally or maliciously activated. -->
