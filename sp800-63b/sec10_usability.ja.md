<a name="sec10"></a>

<div class="breaker"></div>

## 10. Usability の考慮事項

<!-- ## 10 Usability Considerations -->

_This section is informative._

<!-- _This section is informative._ -->

[ISO/IEC 9241-11](#ISO9241) は，Usability を「特定のユーザが特定の使用状況において，有効性，効率，満足をもって特定のゴールを達成するためにある製品を使用できる程度」として定義している．この定義は有効性，効率，満足を達成する鍵となる要素として，ユーザ，そのゴール，使用状況に焦点を当てている． Usability を達成するためには，これらの鍵となる要素を占める全体論的なアプローチが必要である．

<!-- [ISO/IEC 9241-11](#ISO9241) defines usability as the "extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency and satisfaction in a specified context of use." This definition focuses on users, their goals, and the context of use as key elements necessary for achieving effectiveness, efficiency, and satisfaction. A holistic approach that accounts for these key elements is necessary to achieve usability. -->


情報システムにアクセスするユーザのゴールは，意図したタスクを実行することである． Authentication はこのゴールを実現する機能である． しかしユーザの視点からは，Authentication はそれらと意図したタスクの間にある． Authentication の効果的な設計と実装は，正しいことを行うことを簡単にし，謝ったことを行うことを難しくし，誤ったことが起きたとき，回復することを簡単にする．

<!-- A user's goal for accessing an information system is to perform an intended task. Authentication is the function that enables this goal. However, from the user's perspective, authentication stands between them and their intended task. Effective design and implementation of authentication makes it easy to do the right thing, hard to do the wrong thing, and easy to recover when the wrong thing happens. -->

組織はステークホルダーの Digital Authentication エコシステム全体における全体的な影響を認識する必要がある． ユーザは多くの場合，一つか複数の Authenticator をそれぞれ異なる RP に対して採用する． 続いて，彼らはパスワードを覚えたり，どの Authenticator がどの RP のものかを思い出したり，複数の物理的な Authentication デバイスを持ち歩いたりすることに奮闘する． プアーな Usability はしばしば対抗メカニズムや意図しない回避策を生じさせ，結果としてセキュリティ管理の有効性を低下させるため，Authentication の Usability を評価することは極めて重要である．

<!-- Organizations need to be cognizant of the overall implications of their stakeholders' entire digital authentication ecosystem. Users often employ one or more authenticator, each for a different RP. They then struggle to remember passwords, to recall which authenticator goes with which RP, and to carry multiple physical authentication devices. Evaluating the usability of authentication is critical, as poor usability often results in coping mechanisms and unintended work-arounds that can ultimately degrade the effectiveness of security controls. -->

Usability を開発プロセスに取り入れることで，ユーザの Authentication ニーズ と組織のビジネス上のゴールに取り組みながら，セキュアで使いやすいAuthentication ソリューションをリードすることができる．

<!-- Integrating usability into the development process can lead to authentication solutions that are secure and usable while still addressing users' authentication needs and organizations' business goals. -->

デジタルシステムにおける Usability のインパクトは，適切な AAL を決定する際の Risk Assessment の一環として考慮される必要がある． より高い AAL の Authenticator はより良い Usability を提供することがあり，より低い AAL アプリケーションとしての使用を許すべきである．

<!-- The impact of usability across digital systems needs to be considered as part of the risk assessment when deciding on the appropriate AAL. Authenticators with a higher AAL sometimes offer better usability and should be allowed for use for lower AAL applications. -->

Authentication のための Federation を活用することで，多くの Usability の問題を楽にすることができるが，そのようなアプローチは [SP 800-63C](sp800-63c.html) で説明されているような独自のトレードオフを持つ．

<!-- Leveraging federation for authentication can alleviate many of the usability issues, though such an approach has its own tradeoffs, as discussed in [SP 800-63C](sp800-63c.html). -->

このセクションは一般的な Usability の考慮事項と実装方法を提供するが，特定のソリューションを推奨しない． 言及された実装は特定の Usability ニーズに取り組む革新的な技術的アプローチを促進するための例示である． さらに，Usability の考慮事項とその実装は one-size-fits-all のソリューションを予防する多くの要素に対して敏感である． たとえば，デスクトップコンピューティング環境で使っているフォントサイズは，小さな OTP デバイスのスクリーンではテキストを画面の外に出してしまうかもしれない． 選択した Authenticator の Usability 評価を実施することは，実装の極めて重要な要素である． ユーザの代表者，実際的なゴールとタスク，適切な使用状況とともに評価を行うことが重要である．

<!-- This section provides general usability considerations and possible implementations, but does not recommend specific solutions. The implementations mentioned are examples to encourage innovative technological approaches to address specific usability needs. Further, usability considerations and their implementations are sensitive to many factors that prevent a one-size-fits-all solution. For example, a font size that works in the desktop computing environment may force text to scroll off of a small OTP device screen. Performing a usability evaluation on the selected authenticator is a critical component of implementation. It is important to conduct evaluations with representative users, realistic goals and tasks, and appropriate contexts of use. -->

**前提**

<!-- **ASSUMPTIONS** -->

このセクションでは，「ユーザ」という単語は「Claimant」または「Subscriber」を意味する．

<!-- In this section, the term "users" means "claimants" or "subscribers." -->

ガイドラインと考慮事項はユーザ視点から記述される．

<!-- Guidelines and considerations are described from the users' perspective. -->

アクセシビリティは Usability とは異なり，このドキュメントの対象外である． [セクション 508](#Section508) は情報技術のバリアを排除し，連邦政府機関に対して障害を持つ人々がオンラインの公開コンテンツにアクセスできるようにすることを求めるために制定された． アクセシビリティのガイダンスについてはセクション 508 の法律と標準を参照すること．

<!-- Accessibility differs from usability and is out of scope for this document. [Section 508](#Section508) was enacted to eliminate barriers in information technology and require federal agencies to make their online public content accessible to people with disabilities. Refer to Section 508 law and standards for accessibility guidance. -->

### <a name="usabilitycommon"></a> 10.1 Authenticator に共通する Usability の考慮事項

<!-- ### <a name="usabilitycommon"></a> 10.1 Usability Considerations Common to Authenticators -->

Authentication システムの選択や実装を行う際は，ユーザ，そのゴール，使用状況の組み合わせに注意しながら，選択した Authenticator のライフサイクル全体にわたる Usability (例 : 代表的な使用法や断続的なイベント) を検討する．

<!-- When selecting and implementing an authentication system, consider usability across the entire lifecycle of the selected authenticators (e.g., typical use and intermittent events), while being mindful of the combination of users, their goals, and context of use. -->

単一の Authenticator Type では通常，利用人口のすべてを満足させることはできない． したがって，可能な限り — AAL の要件に基づいて — CSPは代わりの Authenticator をサポートし，ユーザが必要に応じて選択できるようにするべきである． 多くの場合，タスクの即時性，知覚されるコストベネフィットのトレードオフ，特定の Authenticator に対する不慣れさが選択に影響を与える． ユーザはその時点での最小の負担またはコストとなる選択肢を選ぶ傾向がある． たとえば，タスクが情報システムへの即時の Access を必要とするとき，ユーザはより多くのステップを必要とする Authenticator を選択するのではなく，新しいアカウントと Password を作成することを好むかもしれない． あるいは，ユーザがすでに Identity プロバイダのアカウントを持っている場合，(適切なAALで承認された) Identity 連携という選択肢を選ぶかもしれない． ユーザはいくつかの Authenticator を他のものよりもよく理解し，また彼らの理解と経験に基づいた異なる信頼レベルを持っている．

<!-- A single authenticator type usually does not suffice for the entire user population. Therefore, whenever possible — based on AAL requirements — CSPs should support alternative authenticator types and allow users to choose based on their needs. Task immediacy, perceived cost benefit tradeoffs, and unfamiliarity with certain authenticators often impact choice. Users tend to choose options that incur the least burden or cost at that moment. For example, if a task requires immediate access to an information system, a user may prefer to create a new account and password rather than select an authenticator requiring more steps. Alternatively, users may choose a federated identity option — approved at the appropriate AAL — if they already have an account with an identity provider. Users may understand some authenticators better than others, and have different levels of trust based on their understanding and experience. -->

ポジティブな Authentication の経験は，望ましいビジネス成果を達成する組織の成功に不可欠である． したがって，ユーザ視点から Authenticator を検討するべきである． 包括的な Authentication Usability のゴールは，ユーザの負担と Authentication の摩擦 (例 : ユーザが Authenticate する回数，関連するステップ，ユーザが追跡しなければならない情報の量) を最小限に抑えることである． シングルサインオンはそのような最小化ストラテジーの一つを例示する．

<!-- Positive user authentication experiences are integral to the success of an organization achieving desired business outcomes. Therefore, they should strive to consider authenticators from the users' perspective. The overarching authentication usability goal is to minimize user burden and authentication friction (e.g., the number of times a user has to authenticate, the steps involved, and the amount of information he or she has to track). Single sign-on exemplifies one such minimization strategy. -->

ほとんどの Authenticator に適用可能な Usability の考慮事項を以下に説明する．後続のセクションでは，特定の Authenticator に固有の Usability の考慮事項について説明する．

<!-- Usability considerations applicable to most authenticators are described below. Subsequent sections describe usability considerations specific to a particular authenticator. -->

すべての Authenticator の代表的な使用法に関する Usability の考慮事項 :

<!-- Usability considerations for typical usage of all authenticators include: -->

* Authenticator の使用と保守に関連する情報を提供する．たとえば Authenticator の紛失や盗難があった場合の対応方法や使用方法 (特に初回の使用や初期化の際に異なる要件がある場合) ．

<!-- * Provide information on the use and maintenance of the authenticator, e.g., what to do if the authenticator is lost or stolen, and instructions for use — especially if there are different requirements for first-time use or initialization. -->

* ユーザが自分の Authenticator をすぐに利用できるようにするため，Authenticator の可用性も考慮されるべきである ． 紛失，破損，その他の元の Authenticator へのネガティブなインパクトに対応するため，代替の Authentication の選択肢が必要であると考える．

<!-- * Authenticator availability should also be considered as users will need to remember to have their authenticator readily available. Consider the need for alternate authentication options to protect against loss, damage, or other negative impacts to the original authenticator. -->

* 可能な限り，AAL の要件に基づいて，ユーザは代替の Authentication の選択肢を提供されるべきである． これによりユーザは，コンテキスト，ゴール，およびタスク (例 : タスクの頻度や即時性) に基づいて Authenticator を選択することができる． 代替の Authentication の選択肢は特定の Authenticator で発生する可用性の問題にも役立つ．

<!-- * Whenever possible, based on AAL requirements, users should be provided with alternate authentication options. This allows users to choose an authenticator based on their context, goals, and tasks (e.g., the frequency and immediacy of the task). Alternate authentication options also help address availability issues that may occur with a particular authenticator. -->

* ユーザ向けテキストの特徴 :
  * 意図されたオーディエンスに対して，平易な言語でユーザ向けテキストを書く (例 : 説明，指示，通知，エラーメッセージなど) ． 専門的な技術用語を避け，通常，第6学年から第8学年の識字レベルで書く．
  * ユーザ向けおよびユーザが入力したテキストについて，フォントのスタイル，サイズ，色，周囲の背景とのコントラストなどを含む可読性を考慮する． 読みづらいテキストはユーザ入力のミスを引き起こす． 可読性を高めるため，以下の使用を検討する :
    * ハイコントラスト．最も高いコントラストは黒上の白である．
    * 電子ディスプレイ用には Sans serif フォント． 印刷用には Serif フォント．
    * 混乱しやすい文字を明確に区別するフォント (例 : 大文字の「O」と数字「0」など ) ．
    * デバイスの画面に収まる限りは，最小フォントサイズを 12 ポイントとする．

<!-- * Characteristics of user-facing text:
  * Write user-facing text (e.g., instructions, prompts, notifications, error messages) in plain language for the intended audience. Avoid technical jargon and, typically, write for a 6th to 8th grade literacy level.
  * Consider the legibility of user-facing and user-entered text, including font style, size, color, and contrast with surrounding background. Illegible text contributes to user entry errors. To enhance legibility, consider the use of:
    * High contrast. The highest contrast is black on white.
    * Sans serif fonts for electronic displays. Serif fonts for printed materials.
    * Fonts that clearly distinguish between easily confusable characters (e.g., the capital letter "O" and the number "0").
    * A minimum font size of 12 points as long as the text fits for display on the device. -->

* Authenticator 入力中のユーザ体験 :
  * マスクされたテキスト入力はエラーを起こしやすいので，入力中にテキストを表示するオプションを提供する． ユーザに対して一度十分に表示された文字はまた非表示にされる． 従来のデスクトップコンピュータよりもモバイルデバイス (例 : タブレットやスマートフォン ) では Memorized Secret を入力するのに時間がかかるため，マスキング遅延時間を決定する際にはデバイスを考慮する． マスキング遅延時間がユーザのニーズと一致していることを確認する．
  * テキスト入力に不足しない時間が与えられていることを確認する (すなわち，入力画面が尚早にタイムアウトしない ) ．与えられたテキスト入力時間がユーザのニーズと一致していることを確認する．
  * ユーザの混乱や不満を軽減するため，入力エラーに対する明確，有意義かつアクション可能なフィードバックを提供する． ユーザが誤ってテキストを入力したことを知らない場合，重大な Usability への影響が生じる．
  * ユーザが Authenticator Output を入力する必要がある Authenticator に対して，少なくとも10回の入力を許す． 入力テキストがより長く複雑になるほど，ユーザ入力エラーの可能性は大きくなる．
  * 残された試行回数について，明確で有意義なフィードバックを提供する． 混乱と不満を軽減するため，レート制限 (すなわち，スロットリング) によって次の試行までどらくらい待たなければならないかを知らせる．

<!-- * User experience during authenticator entry:
  * Offer the option to display text during entry, as masked text entry is error-prone. Once a given character is displayed long enough for the user to see, it can be hidden. Consider the device when determining masking delay time, as it takes longer to enter memorized secrets on mobile devices (e.g., tablets and smartphones) than on traditional desktop computers. Ensure masking delay durations are consistent with user needs.
  * Ensure the time allowed for text entry is adequate (i.e., the entry screen does not time out prematurely). Ensure allowed text entry times are consistent with user needs.
  * Provide clear, meaningful and actionable feedback on entry errors to reduce user confusion and frustration. Significant usability implications arise when users do not know they have entered text incorrectly.
  * Allow at least 10 entry attempts for authenticators requiring the entry of the authenticator output by the user. The longer and more complex the entry text, the greater the likelihood of user entry errors.
  * Provide clear, meaningful feedback on the number of remaining allowed attempts. For rate limiting (i.e., throttling), inform users how long they have to wait until the next attempt to reduce confusion and frustration. -->

* モバイルデバイスでのタッチ領域や表示領域の制限など，フォーム要因の制約の影響を最小限に抑える :
  * 小さなデバイスでのタイピングはフルサイズキーボードでのタイピングよりもはるかにエラーが発生しやすく時間がかかるため，大きなタッチ領域は Usability を向上させる． 画面上のキーボードサイズが小さいほど，画面上のターゲットのサイズに対する入力メカニズム (例 : 指など) のサイズにより，タイプすることがより困難になる．
  * 小さなディスプレイのための優良なユーザインターフェースと情報デザインを追及する．

<!-- * Minimize the impact of form-factor constraints, such as limited touch and display areas on mobile devices:
  * Larger touch areas improve usability for text entry since typing on small devices is significantly more error prone and time consuming than typing on a full-size keyboard. The smaller the onscreen keyboard, the more difficult it is to type, due to the size of the input mechanism (e.g., a finger) relative to the size of the on-screen target.
  * Follow good user interface and information design for small displays. -->

断続的なイベントには，Reauthentication，アカウントロックアウト，有効期限切れ，失効，破損，紛失，盗難，機能しないソフトウェアなどのイベントが含まれる．

<!-- Intermittent events include events such as reauthentication, account lock-out, expiration, revocation, damage, loss, theft, and non-functional software. -->

Authenticator タイプ間の断続的なイベントに関する Usability の考慮事項 :

<!-- Usability considerations for intermittent events across authenticator types include: -->

* ユーザの非アクティブ状態によって Reauthenticate が必要となることを予防するために，非アクティブタイムアウトが起こらないようその直前(例 : 2分など) に活動をトリガーするためのプロンプトを出す．

<!-- * To prevent users from needing to reauthenticate due to user inactivity, prompt users in order to trigger activity just before (e.g., 2 minutes) an inactivity timeout would otherwise occur. -->

* ユーザの操作に関係のない定期的な Reauthentication イベントが必要となる前には，ユーザが作業を保存することを十分な時間 ( 例 : 1時間など ) を以って促す．

<!-- * Prompt users with adequate time (e.g., 1 hour) to save their work before the fixed periodic reauthentication event required regardless of user activity. -->

* どのようにして，どこで技術的な支援を得られるか明確にする． たとえば，オンラインセルフサービス機能へのリンク，チャットセッション，ヘルプデスクサポートのための電話番号などの情報をユーザに提供する． 理想的には，十分な情報が提供された場合は，外部からの介入なしにユーザが断続的なイベントから自分たちで回復できるようになる．

<!-- * Clearly communicate how and where to acquire technical assistance. For example, provide users with information such as a link to an online self-service feature, chat sessions or a phone number for help desk support. Ideally, sufficient information can be provided to enable users to recover from intermittent events on their own without outside intervention. -->

### 10.2 Authenticator Type による Usability の考慮事項

<!-- ### 10.2 Usability Considerations by Authenticator Type -->

ほとんどの Authenticator ( [セクション 10.1](#usabilitycommon) ) に適用可能な前述の一般的な Usability の考慮事項に加えて，以下のセクションでは，特定の Authenticator Type に固有のその他の Usability の考慮事項について説明する．

<!-- In addition to the previously described general usability considerations applicable to most authenticators ([Section 10.1](#usabilitycommon)), the following sections describe other usability considerations specific to particular authenticator types. -->

#### <a name="memorizedsecrets"></a> 10.2.1 Memorized Secret

<!-- #### <a name="memorizedsecrets"></a> 10.2.1 Memorized Secrets -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは，Memorized Secret (一般的に Password や PIN といわれる) を手動で入力する．

<!-- Users manually input the memorized secret (commonly referred to as a password or PIN). -->

典型的な使用法のための Usability の考慮事項 :

<!-- Usability considerations for typical usage include: -->

* Memorized Secret の記憶しやすさ
  * ユーザが覚えておくべき項目が多いほど，思い出すことに失敗する可能性は大きくなる． Memorized Secret が少なくなるほど，特定の RP に必要な特定の Memorized Secret をより簡単に思い出すことができる．
  * 使用頻度の低い Password は記憶負担が大きくなる．

<!-- * Memorability of the memorized secret.
  * The likelihood of recall failure increases as there are more items for users to remember. With fewer memorized secrets, users can more easily recall the specific memorized secret needed for a particular RP.
  * The memory burden is greater for a less frequently used password. -->

* Memorized Secret 入力中のユーザ体験  
  * Passphrase を含む Memorized Secret を入力するためのフィールドにコピーアンドペースト機能をサポートする．

<!-- * User experience during entry of the memorized secret.
  * Support copy and paste functionality in fields for entering memorized secrets, including passphrases. -->

**_断続的なイベント_**

<!-- **_Intermittent Events_** -->

断続的なイベントの Usability の考慮事項は以下を含む :

<!-- Usability considerations for intermittent events include: -->

* ユーザが Memorized Secret を作成または変更するとき :
  * Memorized Secret の作成や変更の方法を情報を明確に伝える．
  * [セクション5.1.1](#reqauthtype) で指定されているように，Memorized Secret の要件を明確に伝える．
  * Passphrase の使用をサポートするには，少なくとも64文字の長さを許容する． ユーザが空白を含む任意の文字を使用して，望み通りの長さで Memorized Secret を作成し記憶を手助けすることを奨励する．
  * Memorized Secret に他の構成ルール ( 例 : 異なる文字タイプの混合) を課さない．
  * ユーザの要求や Authenticator の危殆化の証拠がない限り，Memorized Secret は恣意的な (例 : 定期的な) 変更を必要としない． ( 詳細については [セクション 5.1.1](#reqauthtype) を参照 )

<!-- * When users create and change memorized secrets:
  * Clearly communicate information on how to create and change memorized secrets.
  * Clearly communicate memorized secret requirements, as specified in [Section 5.1.1](#reqauthtype).
  * Allow at least 64 characters in length to support the use of passphrases. Encourage users to make memorized secrets as lengthy as they want, using any characters they like (including spaces), thus aiding memorization.
  * Do not impose other composition rules (e.g. mixtures of different character types) on memorized secrets.
  * Do not require that memorized secrets be changed arbitrarily (e.g., periodically) unless there is a user request or evidence of authenticator compromise. (See [Section 5.1.1](#reqauthtype) for additional information). -->

* 選択された Password を拒否された場合，( 例 : 受け入れられない Password の"ブラックリスト"に含まれる，過去に使用されたなど ) 明確，有意義でアクション可能なフィードバックを提供する．

<!-- * Provide clear, meaningful and actionable feedback when chosen passwords are rejected (e.g., when it appears on a "black list" of unacceptable passwords or has been used previously). -->


#### 10.2.2 ルックアップ シークレット

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは印刷物または電子的な Authenticator を使用して，Verifier の問いかけに応答するために必要な適切なシークレットを探す． たとえば，ユーザはカードにテーブル形式で印刷された数字または文字列のうち，特定のサブセットを提供するように求められる．

<!-- Users use the authenticator — printed or electronic — to look up the appropriate secret(s) needed to respond to a verifier's prompt. For example, a user may be asked to provide a specific subset of the numeric or character strings printed on a card in table format. -->

代表的な使用法のための Usability の考慮事項 :

<!-- Usability considerations for typical usage include: -->

* ルックアップシークレット入力中のユーザ体験
  * プロンプトの複雑さとサイズを考慮する． ユーザが探すように促されるシークレットのサブセットが大きいほど，Usability への影響は大きくなる． Authentication のためのルックアップシークレットの量と複雑さを選択する際には，認知的作業負荷と入力の物理的な難しさの両方を考慮に入れるべきである．

<!-- * User experience during entry of look-up secrets.
  * Consider the prompts' complexity and size. The larger the subset of secrets a user is prompted to look up, the greater the usability implications. Both the cognitive workload and physical difficulty for entry should be taken into account when selecting the quantity and complexity of look-up secrets for authentication. -->

#### 10.2.3 Out-of-Band

<!-- #### 10.2.3 Out-of-Band -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

Out-of-band authentication では，ユーザはプライマリとセカンダリの通信チャネルへの Access を持つ必要がある．

<!-- Out-of-band authentication requires users have access to a primary and secondary communication channel. -->

代表的な使用法のための Usability の考慮事項 :

<!-- Usability considerations for typical usage: -->

* ロックされたデバイス上でシークレットの受信を通知する．ただし Out-of-Band デバイスがロックされている場合，シークレットに Access するにはデバイスへの Authentication が必要とされるべきである．

<!-- * Notify users of the receipt of a secret on a locked device. However, if the out of band device is locked, authentication to the device should be required to access the secret. -->

* 実装に応じて，ユーザがモバイルデバイスにテキストを入力しなければならない場合に特に問題となるフォーム要因の制約を考慮する． より大きなタッチ領域を提供することはモバイルデバイスでシークレットを入力する際の Usability を向上させる．

<!-- * Depending on the implementation, consider form-factor constraints as they are particularly problematic when users must enter text on mobile devices. Providing larger touch areas will improve usability for entering secrets on mobile devices. -->

* より良い Usability の選択肢は，モバイルデバイス上にテキスト入力を必要としない機能を提供することだ ( 例 : ユーザが Out-of-Band シークレットをコピーアンドペースト出来るような画面上でのシングルタップ，コピー機能など ) ． このような機能をユーザに提供することは，プライマリチャネルとセカンダリチャネルが同じデバイス上にある場合に特に役立つ． たとえば，ユーザがスマートフォンで Authentication Secret を転送することは，Out-of-Band アプリケーションとプライマリチャネルを ( もしかすると複数回にわたり ) 前後に切り替える必要があるため，困難である．

<!-- * A better usability option is to offer features that do not require text entry on mobile devices (e.g., a single tap on the screen, or a copy feature so users can copy and paste out-of-band secrets). Providing users such features is particularly helpful when the primary and secondary channels are on the same device. For example, it is difficult for users to transfer the authentication secret on a smartphone because they must switch back and forth—potentially multiple times—between the out of band application and the primary channel. -->

#### 10.2.4 Single-Factor OTP デバイス

<!-- #### 10.2.4 Single-Factor OTP Device -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは Single-Factor OTP デバイスによって生成された OTP に Access する．Authenticator Output は通常デバイスに表示され，ユーザは Verifier のためにそれを入力する．

<!-- Users access the OTP generated by the single-factor OTP device. The authenticator output is typically displayed on the device and the user enters it for the verifier. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* Authenticator Output は少なくとも変更までに1分を許容する．しかし理想的には [セクション 5.1.4.1](#sfotpa) で指定されているように満2分間を許容する． ユーザは Authenticator Output を入力するのに十分な時間を必要とする ( Single-Factor OTP デバイスとその入力画面の間を前後に行き来することを含む ) ．

<!-- * Authenticator output allows at least one minute between changes, but ideally allows users the full two minutes as specified in [Section 5.1.4.1](#sfotpa). Users need adequate time to enter the authenticator output (including looking back and forth between the single-factor OTP device and the entry screen). -->

* 実装に応じた，実装者にとっての追加の Usability の考慮事項は以下のとおり :
  * もし Single-Factor OTP デバイスがそのアウトプットを電子インターフェース ( 例 : USBなど ) を介して提供する場合，ユーザが Authenticator Output を手動で入力する必要がないことが望ましい． しかし，物理的インプットの操作 ( 例 : ボタンを押すなど ) が必要とされる場合，USBポートの位置は Usability の問題となる可能性がある． たとえば，一部のコンピュータの USB ポートはコンピュータの背面にあり，ユーザの手が届きにくくなる．
  * USB ポートのような直接的コンピュータインターフェースの利用が限られる場合は Usability の問題を引き起こすことがある． たとえば，ラップトップコンピュータの USB ポートの数はしばしばとても限られる． これはユーザに対して Single-Factor OTP デバイスのために他の USB 周辺機器の接続解除を強制するかもしれない．

<!-- * Depending on the implementation, the following are additional usability considerations for implementers:
  * If the single-factor OTP device supplies its output via an electronic interface (e.g, USB) this is preferable since users do not have to manually enter the authenticator output. However, if a physical input (e.g., pressing a button) is required to operate, the location of the USB ports could pose usability difficulties. For example, the USB ports of some computers are located on the back of the computer and will be difficult for users to reach.
  * Limited availability of a direct computer interface such as a USB port could pose usability difficulties. For example, the number of USB ports on laptop computers is often very limited. This may force users to unplug other USB peripherals in order to use the single-factor OTP device. -->

#### 10.2.5 Multi-Factor OTP デバイス

<!-- #### 10.2.5 Multi-Factor OTP Device -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは第二の Authentication Factor を通じて Multi-Factor OTP デバイスによって生成された OTP に Access する． 通常 OTP はデバイスに表示され，Verifier のためにそれを手動で入力する． 第二の Authentication Factor は Memorized Secret ，一体型 Biometrics ( 例 : 指紋など ) リーダー，または直接的なコンピュータインターフェース ( 例 : USB ポート ) などの統合的なエントリーパッドに入力することで達成されてもよい． 追加の要素に対する Usability の考慮事項も同様に適用される． — Multi-Factor Authenticator に使用される Memorized Secret については [セクション 10.2.1](#memorizedsecrets)，Biometrics については [Section 10.4](#biomusability) を参照．

<!-- Users access the OTP generated by the multi-factor OTP device through a second authentication factor. The OTP is typically displayed on the device and the user manually enters it for the verifier. The second authentication factor may be achieved through some kind of integral entry pad to enter a memorized secret, an integral biometric (e.g., fingerprint) reader, or a direct computer interface (e.g., USB port). Usability considerations for the additional factor apply as well — see [Section 10.2.1](#memorizedsecrets) for memorized secrets and [Section 10.4](#biomusability) for biometrics used in multi-factor authenticators. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* Authenticator Output の手動入力中のユーザ体験
  * タイムベース OTP の場合は，OTP が表示されている時間に加えて猶予期間を設ける． ユーザは Multi-Factor OTP デバイスとその入力画面の間を前後に行き来することを含む，Authenticator Output を入力するのに十分な時間を必要とする．
  * ユーザが統合的なエントリーパッドを使用するか，モバイルデバイス上に Authenticator Output を入力して Multi-Factor OTP デバイスのロックを解除する必要がある場合は，フォーム要因の制約について考慮する． 小さなデバイスでのタイピングは従来のキーボードよりはるかにエラーが発生しやすく，時間がかかる． 統合的なエントリーパッドとオンスクリーンキーボードが小さくなるほど，タイプすることがより難しくなる． より大きなタッチ領域を提供することは Multi-Factor OTP デバイスのロックを解除する，またはモバイルデバイスで Authenticator Output を入力する際の Usability を向上させる．
  * USB ポートのような直接的コンピュータインターフェースの利用が限られる場合は Usability の問題を引き起こすことがある． たとえば，ラップトップコンピュータの USB ポートの数はしばしばとても限られるため，ユーザに対して Multi-Factor OTP デバイスのために他の USB 周辺機器の接続解除を強制するかもしれない．

<!-- * User experience during manual entry of the authenticator output.
  * For time-based OTP, provide a grace period in addition to the time during which the OTP is displayed. Users need adequate time to enter the authenticator output, including looking back and forth between the multi-factor OTP device and the entry screen.
  * Consider form-factor constraints if users must unlock the multi-factor OTP device via an integral entry pad or enter the authenticator output on mobile devices. Typing on small devices is significantly more error prone and time-consuming than typing on a traditional keyboard. The smaller the integral entry pad and onscreen keyboard, the more difficult it is to type. Providing larger touch areas improves usability for unlocking the multi-factor OTP device or entering the authenticator output on mobile devices.
  * Limited availability of a direct computer interface like a USB port could pose usability difficulties. For example, laptop computers often have a limited number of USB ports, which may force users to unplug other USB peripherals to use the multi-factor OTP device. -->

#### 10.2.6 Single-Factor 暗号ソフトウェア

<!-- #### 10.2.6 Single-Factor Cryptographic Software -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは暗号ソフトウェアキーの所持とコントロールを証明することによって Authenticate する．

<!-- Users authenticate by proving possession and control of the cryptographic software key. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* ユーザがどの Authentication タスクに使用する Cryptographic Key であるかを認識して呼び出す必要があるため，Cryptographic Key にはユーザにとって意味のある適切で説明的な名前がつけられる． これはユーザが，似ている，またはあいまいな名前の複数の Cryptographic Key を扱うことを予防する． より小さなモバイルデバイス上の複数の Cryptographic Key から選択することは，画面サイズが小さくなるために Cryptographic Key の名前が短縮されると特に問題になる．

<!-- * Give cryptographic keys appropriately descriptive names that are meaningful to users since users have to recognize and recall which cryptographic key to use for which authentication task. This prevents users from having to deal with multiple similarly- and ambiguously-named cryptographic keys. Selecting from multiple cryptographic keys on smaller mobile devices may be particularly problematic if the names of the cryptographic keys are shortened due to reduced screen size. -->

#### 10.2.7 Single-Factor 暗号デバイス

<!-- #### 10.2.7 Single-Factor Cryptographic Device -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは Single-Factor 暗号デバイスの所持を証明することで Authenticate する．

<!-- Users authenticate by proving possession of the single-factor cryptographic device. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* Single-Factor 暗号デバイスの操作として物理的インプット ( 例 : ボタンを押すなど ) を必要とする場合， Usability の問題となる可能性がある． たとえば，いくつかの USB ポートはコンピュータの背面にあり，ユーザの手が届きにくい．

<!-- * Requiring a physical input (e.g., pressing a button) to operate the single-factor cryptographic device could pose usability difficulties. For example, some USB ports are located on the back of computers, making it difficult for users to reach. -->

* USB ポートのような直接的コンピュータインターフェースの利用が限られる場合は Usability の問題を引き起こすことがある． たとえば，ラップトップコンピュータの USB ポートの数はしばしばとても限られるため，ユーザに対して Single-Factor 暗号デバイスのために他の USB 周辺機器の接続解除を強制するかもしれない．

<!-- * Limited availability of a direct computer interface like a USB port could pose usability difficulties. For example, laptop computers often have a limited number of USB ports, which may force users to unplug other USB peripherals to use the single-factor cryptographic device. -->

#### 10.2.8 Multi-Factor 暗号デバイス

<!-- #### 10.2.8 Multi-Factor Cryptographic Software -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

Authenticate するために，ユーザはディスク上に格納された Cryptographic Key，またはアクティベーションを必要とするなんらかの"ソフト"メディアの所有とコントロールを証明する． アクティベーションは，Memorized Secret または Biometrics いずれかの第二の Authentication Factor のインプットによるものである． 追加の要素に対する Usability の考慮事項も同様に適用される． — Multi-Factor Authenticator に使用される Memorized Secret については [セクション 10.2.1](#memorizedsecrets)，Biometrics については [Section 10.4](#biomusability) を参照．

<!-- In order to authenticate, users prove possession and control of the cryptographic key stored on disk or some other "soft" media that requires activation. The activation is through the input of a second authentication factor, either a memorized secret or a biometric. Usability considerations for the additional factor apply as well — see [Section 10.2.1](#memorizedsecrets) for memorized secrets and [Section 10.4](#biomusability) for biometrics used in multi-factor authenticators. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* ユーザがどの Authentication タスクに使用する Cryptographic Key であるかを認識して呼び出す必要があるため，Cryptographic Key にはユーザにとって意味のある適切で説明的な名前がつけられる． これはユーザが，似ている，またはあいまいな名前の複数の Cryptographic Key を扱うことを予防する． より小さなモバイルデバイス上の複数の Cryptographic Key から選択することは，画面サイズが小さくなるために Cryptographic Key の名前が短縮されると特に問題になる．

<!-- * Give cryptographic keys appropriately descriptive names that are meaningful to users since users have to recognize and recall which cryptographic key to use for which authentication task. This prevents users from having to deal with multiple similarly- and ambiguously-named cryptographic keys. Selecting from multiple cryptographic keys on smaller mobile devices may be particularly problematic if the names of the cryptographic keys are shortened due to reduced screen size. -->

#### 10.2.9 Multi-Factor 暗号デバイス

<!-- #### 10.2.9 Multi-Factor Cryptographic Device -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

ユーザは Multi-Factor 暗号デバイスの所持と保護された Cryptographic Key のコントロールを証明することで Authenticate する． デバイスは，Memorized Secret または Biometrics いずれかの第二の Authentication Factor によってアクティベートされる． 追加の要素に対する Usability の考慮事項も同様に適用される． — Multi-Factor Authenticator に使用される Memorized Secret については [セクション 10.2.1](#memorizedsecrets)，Biometrics については [Section 10.4](#biomusability) を参照．

<!-- Users authenticate by proving possession of the multi-factor cryptographic device and control of the protected cryptographic key. The device is activated by a second authentication factor, either a memorized secret or a biometric. Usability considerations for the additional factor apply as well — see [Section 10.2.1](#memorizedsecrets) for memorized secrets and [Section 10.4](#biomusability) for biometrics used in multi-factor authenticators. -->

代表的な使用法のための Usability の考慮事項は以下を含む :

<!-- Usability considerations for typical usage include: -->

* ユーザは，認証のあと，Multi-Factor 暗号デバイスを接続したままにすることを必要としない． ユーザはそれが終わったあと，Multi-Factor 暗号デバイスを取り外すことを忘れるかもしれない ( 例 : スマートカードリーダー内にスマートカードを忘れてコンピュータから遠ざかるなど ) ．

  * ユーザは Multi-Factor 暗号デバイスが接続されたままである必要があるのかどうか，知らされることが求められる．

<!-- * Do not require users to keep multi-factor cryptographic devices connected following authentication. Users may forget to disconnect the multi-factor cryptographic device when they are done with it (e.g., forgetting a smartcard in the smartcard reader and walking away from the computer).
  * Users need to be informed regarding whether the multi-factor cryptographic device is required to stay connected or not. -->

* ユーザがどの Authentication タスクに使用する Cryptographic Key であるかを認識して呼び出す必要があるため，Cryptographic Key にはユーザにとって意味のある適切で説明的な名前がつけられる． これはユーザが，似ている，またはあいまいな名前の複数の Cryptographic Key に面することを予防する． スマートフォンのような，より小さなモバイルデバイス上の複数の Cryptographic Key から選択することは，画面サイズが小さくなるために Cryptographic Key の名前が短縮されると特に問題になる．

<!-- * Give cryptographic keys appropriately descriptive names that are meaningful to users since users have to recognize and recall which cryptographic key to use for which authentication task. This prevents users being faced with multiple similarly and ambiguously named cryptographic keys. Selecting from multiple cryptographic keys on smaller mobile devices (such as smartphones) may be particularly problematic if the names of the cryptographic keys are shortened due to reduced screen size. -->

* USB ポートのような直接的コンピュータインターフェースの利用が限られる場合は Usability の問題を引き起こすことがある． たとえば，ラップトップコンピュータの USB ポートの数はしばしばとても限られるため，ユーザに対して Multi-Factor 暗号デバイスのために他の USB 周辺機器の接続解除を強制するかもしれない．

<!-- * Limited availability of a direct computer interface like a USB port could pose usability difficulties. For example, laptop computers often have a limited number of USB ports, which may force users to unplug other USB peripherals to use the multi-factor cryptographic device. -->

### 10.3 ユーザビリティに関する考慮事項のまとめ

<!-- ### 10.3 Summary of Usability Considerations -->

[表10-1](#t10-1) に各 Authenticator Type の 代表的な使用法と断続的なイベントについての Usability の考慮事項 をまとめる． 代表的な使用法についての Usability の考慮事項の多くは，行で示されているように，ほとんどの Authenticator Type に適用される． この表では，Authenticator Type 全体にわたる Usability の共通で多様な特性をハイライトしている． 各列は，各 Authenticator に対処する Usability の属性を簡単に識別できるようにする． ユーザのゴールや使用状況により，特定の属性が他の属性よりも重視されることがある． 可能な限り，代替の Authenticator Type を提供し，ユーザがそれらを選択できるようにする．

<!-- [Table 10-1](#t10-1) summarizes the usability considerations for typical usage and intermittent events for each authenticator type. Many of the usability considerations for typical usage apply to most of the authenticator types, as demonstrated in the rows. The table highlights common and divergent usability characteristics across the authenticator types. Each column allows readers to easily identify the usability attributes to address for each authenticator. Depending on users' goals and context of use, certain attributes may be valued over others. Whenever possible, provide alternative authenticator types and allow users to choose between them. -->

Multi-Factor Authenticator ( 例 : Multi-Factor OTP デバイス，Multi-Factor 暗号ソフトウェア，Multi-Factor 暗号デバイスなど ) はまたそれらの第二要素の Usability の考慮事項 を継承する． Biometrics は Multi-Factor Authentication ソリューションのアクティベーション要素としてのみ許されているため，Biometrics の Usability の考慮事項は 表 10-1 には含まれず，セクション 10.4 で説明される．

<!-- Multi-factor authenticators (e.g., multi-factor OTP devices, multi-factor cryptographic software, and multi-factor cryptographic devices) also inherit their secondary factor's usability considerations. As biometrics are only allowed as an activation factor in multi-factor authentication solutions, usability considerations for biometrics are not included in Table 10-1 and are discussed in Section 10.4. -->

<a name="t10-1"></a>

<div class="text-center" markdown="1">

**表 10-1 Authenticator Type による Usability の考慮事項のまとめ**

<!-- **Table 10-1 Usability Considerations Summary by Authenticator Type** -->

![](sp800-63b/media/use.png)

</div>

### <a name="biomusability"></a> 10.4 Biometrics の Usability の考慮事項

<!-- ### <a name="biomusability"></a> 10.4 Biometrics Usability Considerations -->

このセクションは Biometrics の 一般的な Usability の考慮事項についてのハイレベルオーバービューを提供する． Biometrics Usability のより詳細な説明は *Usability & Biometrics, Ensuring Successful Biometric Systems* [NIST Usability](#use-and-bio) に見つけることができる．

<!-- This section provides a high-level overview of general usability considerations for biometrics. A more detailed discussion of biometric usability can be found in *Usability & Biometrics, Ensuring Successful Biometric Systems* [NIST Usability](#use-and-bio). -->

ほかの Biometrics 様式も存在するが，以下の3つの Biometrics 様式が Authentication のためによく利用される : 指紋，顔，虹彩

<!-- Although there are other biometric modalities, the following three biometric modalities are more commonly used for authentication: fingerprint, face and iris. -->

**_代表的な使用法_**

<!-- **_Typical Usage_** -->

* すべての様式で，ユーザのなじみ深さと熟練がデバイスのパフォーマンスを向上させる．

<!-- * For all modalities, user familiarity and practice with the device improves performance. -->

* デバイスアフォーダンス ( すなわち，ユーザがアクションを実行することを可能にするデバイスの特性 )，フィードバック，および明確な指示は Biometrics デバイスによるユーザの成功にとって極めて重要である． たとえば，生存検出のために必要なアクションについての明確な指示を提供する．

<!-- * Device affordances (i.e., properties of a device that allow a user to perform an action), feedback, and clear instructions are critical to a user's success with the biometric device. For example, provide clear instructions on the required actions for liveness detection. -->

* 理想的には，ユーザは第二の Authentication Factor のために，最も快適な様式を選択することができる． ユーザ人口は，他よりもいくつかの Biometrics 様式をより快適かつなじみ深く感じ，また受け入れるだろう．

<!-- * Ideally, users can select the modality they are most comfortable with for their second authentication factor. The user population may be more comfortable and familiar with — and accepting of — some biometric modalities than others. -->

* Biometrics をアクティベーション要素とするユーザ体験
  * 残された試行回数について，明確で有意義なフィードバックを提供する． たとえば，混乱と不満を軽減するため，レート制限 (すなわち，スロットリング) によって次の試行までに待たなければならない時間を知らせる．

<!-- * User experience with biometrics as an activation factor.
  * Provide clear, meaningful feedback on the number of remaining allowed attempts. For example, for rate limiting (i.e., throttling), inform users of the time period they have to wait until next attempt to reduce user confusion and frustration. -->

* 指紋の Usability の考慮事項:
  * ユーザは最初の Enrollment に使用した指を覚えておく必要がある．
  * 指の湿気の量はセンサーのキャプチャー成功能力に影響する．
  * 指紋採取の品質に影響を及ぼす追加の要素には，年齢，性別，職業がある ( 例 : 化学薬品を取り扱う，または手で広範囲に働くユーザは摩擦隆線が低下している可能性がある ) ．

<!-- * Fingerprint Usability Considerations:
  * Users have to remember which finger(s) they used for initial enrollment.
  * The amount of moisture on the finger(s) affects the sensor's ability for successful capture.
  * Additional factors influencing fingerprint capture quality include age, gender, and occupation (e.g., users handling chemicals or working extensively with their hands may have degraded friction ridges). -->

* 顔の Usability の考慮事項 :
  * 顔認識の精度に影響するため，ユーザは Enrollment の際にアーティファクト ( 例 : 眼鏡など ) を装着したかどうかを覚えておく必要がある．
  * 環境の証明条件の違いは顔認識の精度に影響することがある．
  * 顔の表情は顔認識の精度に影響する ( 例 : 笑顔に対するナチュラルな状態 ) ．
  * 顔のポーズは顔認識の精度に影響する ( 例 : カメラを見下ろす，またはカメラから遠ざかる ) ．

<!-- * Face Usability Considerations:
  * Users have to remember whether they wore any artifacts (e.g., glasses) during enrollment because it affects facial recognition accuracy.
  * Differences in environmental lighting conditions can affect facial recognition accuracy.
  * Facial expressions affect facial recognition accuracy (e.g., smiling versus neutral expression).
  * Facial poses affect facial recognition accuracy (e.g., looking down or away from the camera). -->

* 虹彩の Usability の考慮事項 :
  * カラーコンタクトの装着は虹彩認識精度に影響することがある．
  * 目の手術を受けたユーザは手術後の再登録が必要になることがある．
  * 環境の証明条件の違いは虹彩認識精度，特に特定の虹彩の色に影響することがある．

<!-- * Iris Usability Considerations:
  * Wearing colored contacts may affect the iris recognition accuracy.
  * Users who have had eye surgery may need to re-enroll post-surgery.
  * Differences in environmental lighting conditions can affect iris recognition accuracy, especially for certain iris colors. -->

**_断続的なイベント_**
<!-- **_Intermittent Events_** -->

Biometrics は Multi-Factor Authentication の第二の要素としてのみ許可されているため，第一の要素の断続的なイベントの Usability の考慮事項は引き続き適用される． 認識精度に影響することがある Biometrics 使用の断続的なイベントは以下のものを含んでいるが，これに限らない :

<!-- As biometrics are only permitted as a second factor for multi-factor authentication, usability considerations for intermittent events with the primary factor still apply. Intermittent events with biometrics use include, but are not limited to, the following, which may affect recognition accuracy: -->

* ユーザが登録した指にけがをすると，指紋認識が機能しないことがある．指紋が薄くなったユーザにとっては指紋 Authentication は困難である．
* Authentication のための顔認識の時点と最初の Enrollment の時点の間に経過した時間は，ユーザの顔の経年による自然の変化として認識精度に影響することがある． ユーザの体重の変化もまた要因となる．
* 眼科手術を受けた人は，再登録を行わない限り虹彩認識が機能しないことがある．

<!-- * If users injure their enrolled finger(s), fingerprint recognition may not work. Fingerprint authentication will be difficult for users with degraded fingerprints.
* The time elapsed between the time of facial recognition for authentication and the time of the initial enrollment can affect recognition accuracy as a user's face changes naturally over time. A user's weight change may also be a factor.
* Iris recognition may not work for people who had eye surgery, unless they re-enroll. -->

すべての Biometrics 様式において，断続的なイベントの Usability の考慮事項は以下を含む :

<!-- Across all biometric modalities, usability considerations for intermittent events include: -->

* 代替の Authentication 方法が利用可能で機能している必要がある．Biometrics が機能しない場合，代替の第二要素としてユーザが Memorized Secret を使用できるようにする．
* 技術的な支援のための規定 :
  * どのようにして，どこで技術的な支援を得られるかの情報を明確に伝える． たとえば，オンラインセルフサービス機能へのリンク，ヘルプデスクサポートのための電話番号などの情報をユーザに提供する． 理想的には，外部からの介入なしにユーザが断続的なイベントから自分たちで回復できるだけの十分な情報を提供する．
  * Biometrics センサの感度に影響することがある要因をユーザに通知する ( 例 : センサーの清浄度 ) ．

<!-- * An alternative authentication method must be available and functioning. In cases where biometrics do not work, allow users to use a memorized secret as an alternative second factor.
* Provisions for technical assistance:
  * Clearly communicate information on how and where to acquire technical assistance. For example, provide users information such as a link to an online self-service feature and a phone number for help desk support. Ideally, provide sufficient information to enable users to recover from intermittent events on their own without outside intervention.
  * Inform users of factors that may affect the sensitivity of the biometric sensor (e.g., cleanliness of the sensor). -->
