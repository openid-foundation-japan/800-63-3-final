<a name="sec9"></a>

<div class="breaker"></div>

## 9 Usability Considerations

_This section is informative._

本セクションでは, Enrollment と Identity Proofing に関連するユーザビリティー上の考慮事項を実装者に周知することを目的とする (典型的な Authenticator の利用と断続的イベントに関するユーザビリティー上の考慮事項については [SP 800-63B, Section 10](sp800-63b.html#sec10) を参照のこと).

<!-- This section is intended to raise implementers' awareness of the usability considerations associated with enrollment and identity proofing (for usability considerations for typical authenticator usage and intermittent events, see [SP 800-63B, Section 10](sp800-63b.html#sec10). -->

[ISO/IEC 9241-11](#ISO9241-11) はユーザビリティーを "特定のユーザーが特定の利用コンテキストにおいて,  有効, 効率的かつ満足できる程度に特定の目的を達成するためにプロダクトを利用できる程度" と定義している. この定義は, 有効性, 効率性, 満足度を達成するために必要な主要因として, ユーザーと目標, 利用コンテキストに着目している. ユーザビリティーを達成するには, これらのキー要素を考慮した全体的アプローチが必要である.

<!-- [ISO/IEC 9241-11](#ISO9241-11) defines usability as the "extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency and satisfaction in a specified context of use." This definition focuses on users, goals, and context of use as the necessary elements for achieving effectiveness, efficiency, and satisfaction. A holistic approach considering these key elements is necessary to achieve usability. -->

Enrollment および Identity Proofing におけるユーザビリティーの包括的ゴールは, ユーザーの負担 (e.g., かかる時間やフラストレーション) や Enrollment における摩擦 (e.g., 完了までのステップ数とトラックされる情報量) を最小化し, スムーズでポジティブな Enrollment プロセスを促進することである. このゴールを達成するため, 組織はまずユーザーに自身をよく知ってもらう必要がある.

<!-- The overarching goal of usability for enrollment and identity proofing is to promote a smooth, positive enrollment process for users by minimizing user burden (e.g., time and frustration) and enrollment friction (e.g., the number of steps to complete and amount of information to track). To achieve this goal, organizations have to first familiarize themselves with their users. -->

Enrollment および Identity Proofing プロセスでは, ユーザーは CSP および自身が Access するオンラインサービスとのインタラクションを行うことになる. ファーストインプレッションがネガティブであれば, それ以降のインタラクションに対するユーザーの印象にも影響しうるため, 組織はプロセス全体を通じてポジティブなユーザーエクスペリエンスを促進する必要がある.

<!-- The enrollment and identity proofing process sets the stage for a user's interactions with a given CSP and the online services that the user will access; as negative first impressions can influence user perception of subsequent interactions, organizations need to promote a positive user experience throughout the process. -->

ユーザビリティーは計画性なく断片的に達成できるものではない. Enrollment および Identity Proofing プロセスに対するユーザビリティー評価を行うことは, 非常に重要である. 代表的なユーザー, 現実的なゴールとタスク, 適切な利用コンテキストのもとでユーザービリティ評価を行うことが重要である. Enrollment および Identity Proofing プロセスは, ユーザーが正しいことをするのは簡単に, 間違ったことをするのは難しく, かつ間違っても簡単に回復できるように設計し実装するべきである.

<!-- Usability cannot be achieved in a piecemeal manner. Performing a usability evaluation on the enrollment and identity proofing process is critical. It is important to conduct usability evaluation with representative users, realistic goals and tasks, and appropriate contexts of use. The enrollment and identity proofing process should be designed and implemented so it is easy for users to do the right thing, hard to do the wrong thing, and easy to recover when the wrong thing happens. -->

ユーザー視点では, Enrollment および Identity Proofing には, Enrollment 事前準備, Enrollment および Proofing Session, Enrollment 完了後アクション, の3つの主要なステップが存在する. これらのステップは単一の Session で起こることもあれば, それぞれがかなり時間的に離れている (e.g., 数日から数週間) こともある.

<!-- From the user's perspective, the three main steps of enrollment and identity proofing are pre-enrollment preparation, the enrollment and proofing session, and post-enrollment actions. These steps may occur in a single session or there could be significant time elapsed between each one (e.g., days or weeks). -->

全般的, および各ステップごとのユーザビリティー上の考慮事項については, 以下の各セクションで述べる.

<!-- General and step-specific usability considerations are described in sub-sections below. -->

**ASSUMPTIONS**

本セクションでは, "ユーザー" は "Applicant" ないし "Subscriber" を意味する.

<!-- In this section, the term "users" means "applicants" or "subscribers." -->

ガイドラインおよび考慮事項はユーザー視点で記述する.

<!-- Guidelines and considerations are described from the users' perspective. -->

アクセシビリティーはユーザビリティーとは異なり, 本ドキュメントの扱うところではない. [Section 508](#Section508) は情報技術の障壁を排除するために制定され, 連邦政府機関に対して, 電子的かつ情報技術を活用し障害者が公開コンテンツにアクセス可能になるよう求めている. アクセシビリティーガイドラインについては Section 508 の法と標準を参照のこと.

<!-- Accessibility differs from usability and is out of scope for this document. [Section 508](#Section508) was enacted to eliminate barriers in information technology and require federal agencies to make their electronic and information technology public content accessible to people with disabilities. Refer to Section 508 law and standards for accessibility guidance. -->

### 9.1 General User Experience Considerations Duuring Enrollment and Identity Proofing

本サブセクションでは, Enrollment プロセスの全ステップに渡って適用可能なユーザビリティー上の考慮事項について述べる. 各ステップごとに固有のユーザビリティー上の考慮事項は Sections [9.2](#sec9_2) から [9.4](#sec9_4) を参照のこと.

<!-- This sub-section provides usability considerations that are applicable across all steps of the enrollment process. Usability considerations specific to each step are detailed in Sections [9.2](#sec9_2) to [9.4](#sec9_4). -->

* ユーザーのフラストレーションを回避するため, Enrollment に必要なプロセスを合理化し, 各ステップを可能な限り明確かつ容易にする.

<!-- * To avoid user frustration, streamline the process required for enrollment to make each step as clear and easy as possible. -->

* どこでどのように技術的支援を受けることができるかを明確に伝える. 例えば, お

* どこでどのようにして技術的な支援を得ることができるかを明確に伝える. 例えば, ユーザーにオンラインセルフサービス機能へのリンクや, ヘルプデスクサポートのためのチャットや電話番号を提供する. 理想的には, 外部からの介入なしにユーザーが自身で Enrollment 準備の疑問を解決できるよう, 十分な情報を提供するべきである.

<!-- * Clearly communicate how and where to acquire technical assistance. For example, provide helpful information such as a link to online self-service feature, chat sessions, and a phone number for help desk support. Ideally, sufficient information should be provided to enable users to answer their own enrollment preparation questions without outside intervention. -->

* 誰が何の目的で彼らのデータを収集するのかを明確に説明する. また, 彼らのデータがたどるパス, 特にどこにデータが格納されるかも示す.

<!-- * Clearly explain who is collecting their data and why. Also indicate the path their data will take, in particular where the data is being stored. -->

* 提示されたすべての情報が使用できることを保証する.
  * すべてのユーザーに提示する資料 (e.g., データ収集通知や記入式フォーム) について, 適切な情報デザインプラクティスに従う.
  * 資料, 典型的には第6学年から第8学年のリテラシーレベルの平易な言葉で記述し, 技術的な専門用語は避けること. 能動態と口語スタイルで, 主なポイントを論理的に順序立て, 混乱を避けるため同義語ではなく同一単語を一貫して使用し, 可動性向上のため可能であれば箇条書きや書式付き文書などを利用すること.
  * フォントスタイル, サイズ, 色, 周囲の背景とのコントラストなどのテキストの読みやすさを考慮する. 最もコントラスト比が高いのは, 白地に黒である. ユーザーの視力レベルは人それぞれであるため, テキストの可読性は重要である. 判読不可能なテキストは, ユーザーの誤認や入力エラーにつながる (e.g., 記入式フォームを埋める際など).
  * 電子的な資料にはサンセリフフォント, 紙の資料にはセリフフォントを使用する.
  * 可能であれば, すぐ混同しがちな文字 (文字 "O" と数字 "0" など) を明確に区別できないフォントは避ける. これは特に Enrollment コードにおいて重要である.
  * テキストがディスプレイに収まる限り, 最小フォントサイズは12ポイントとする.
* 代表的なユーザーに対して各ステップのユーザビリティー評価を行う. ユーザビリティー評価においては, 現実的ゴールとタスクを定め, 適切な利用コンテキストを設定する.

<!--
* Ensure all information presented is usable.
  * Follow good information design practice for all user-facing materials (e.g., data collection notices and fillable forms).
  * Write materials in plain language, typically at a 6th to 8th grade literacy level, and avoid technical jargon. Use active voice and conversational style, logically sequence main points, use the same word consistently rather than synonyms to avoid confusion, and use bullets, numbers, and formatting where appropriate to aid readability.
  * Consider text legibility, such as font style, size, color, and contrast with surrounding background. The highest contrast is black on white. Text legibility is important because users have different levels of visual acuity. Illegible text will contribute to user comprehension errors or user entry errors (e.g., when completing fillable forms).
  * Use sans serif font styles for electronic materials and serif fonts for paper materials.
  * When possible, avoid fonts that do not clearly distinguish between easily confusable characters (such as the letter "O" and the number "0"). This is especially important for enrollment codes.
  * Use a minimum font size of 12 points, as long as the text fits the display.
* Perform a usability evaluation for each step with representative users. Establish realistic goals and tasks, and appropriate contexts of use for the usability evaluation.
-->

### <a name="sec9_2"></a>9.2 Pre-Enrollment Preparation

本セクションでは, 十分な Enrollment の事前準備を促進するための効果的なアプローチについて述べる. これによりユーザーは困難でフラストレーションが溜まる Enrollment Session を避けることができる. ユーザーが Enrollment Session にできるだけ準備万端であれるよう保証することは, Enrollment および Identity Proofing の全体的な成功とユーザビリティーにとって非常に重要である.

<!-- This section describes an effective approach to facilitate sufficient pre-enrollment preparation so users can avoid challenging, frustrating enrollment sessions. Ensuring users are as prepared as possible for their enrollment sessions is critical to the overall success and usability of the enrollment and identity proofing process. -->

そのような準備は, ユーザーが必要な情報 (e.g., 作成が必要な書類について) を適切な時間枠内に利用可能な形式で受け取れる場合にのみ可能となる. これにはどの Identity Evidence が必要となるかを正確にユーザーに伝えることも含まれる. ユーザーは IAL や当該 Identity Evidence が "fair", "strong", "superior" のどれに当てはまるかなどについては一切知る必要はない. 一方で組織は特定のシステムに Access するためにどの IAL が必要かを知っている必要がある.

<!-- Such preparation is only possible if users receive the necessary information (e.g., required documentation) in a usable format in an appropriate timeframe. This includes making users aware of exactly what identity evidence will be required. Users do not need to know anything about IALs or whether the identity evidence required is scored as "fair," "strong," or "superior," whereas organizations need to know what IAL is required for access to a particular system. -->

ユーザーが Enrollment プロセスを進めるかどうか, およびその Session に何が必要になるかについて, 情報に基づいた判断を下せるようにするには, ユーザーに以下の項目を提供すること.

<!-- To ensure users are equipped to make informed decisions about whether to proceed with the enrollment process, and what will be needed for their session, provide users: -->

* 各ステップで何が期待されるかなど, プロセス全体についての情報.
 * ユーザーがそれに応じて計画を立てられるよう, 予想される時間枠についての明確な説明.

<!--
* Information about the entire process, such as what to expect in each step.   
  * Clear explanations of the expected timeframes to allow users to plan accordingly.
-->

* ユーザーに価値命題を理解させるための, Identity Proofing の必要性とメリットに関する説明.

<!-- * Explanation of the need for — and benefits of — identity proofing to allow users to understand the value proposition. -->

* Enrollment 料金が発生する場合は, その額と受け入れ可能な支払い方法についての情報. より多種多様な支払い方法を許容することで, ユーザーは好みの支払い方法を選ぶことができる.

<!-- * Information on the monetary amount and acceptable forms of payment, and if there is an enrollment fee. Offering a larger variety of acceptable forms of payment allows users to choose their preferred payment operation. -->

* ユーザーの Enrollment Session が対面なのか Remote チャネル越しの対面なのか, およびユーザーに選択肢があるかについての情報. 利用可能な Session の選択肢についてのみ情報を提供すること.
  * ユーザーが場所に関する選択肢を持っているかや, 対面ないし Remote チャネル越しの対面 Session に関する必要なロジスティック情報など, 場所に関する情報. 紛失や盗難への被害が増えるため, ユーザーは Identity Evidence を特定の公共空間 (e.g., 銀行 v.s. スーパーマーケット) に持っていくのを嫌がる可能性があることに注意すること.
  * Remote Session に対する技術要件 (e.g., Internet Access 要件) に関する情報.
  * 待機時間を最小限に抑えるために, 対面や Remote チャネル越しの対面での Identity Proofing Session の予約を可能にする. 予約なしでの来場が可能な場合は, 予約がない場合に待ち時間がより長くなる可能性がることをユーザーに明確に伝える.
    * Enrollment Session の予約, リマインダーの設定と, 予約の変更方法に関する明確な手順を伝えること.
    * 予約のリマインダーを提供し, ユーザーが好みのリマインダー形式 (e.g., 郵便, ボイスメール, Email, テキストメッセージ) を指定できるようにすること. ユーザーには, 日付, 時刻, 場所, 必要な Identity Evidence に関する記述などが必要である.
* 利用可能かつ必要な Identity Evidence および Attribute に関して, それぞれが任意か必須か, 完全な Identity Evidence 一式を提供しない場合の影響についての情報. ユーザーは具体的な Identity Evidence の組み合わせ, およびそれぞれの Identity Evidence に関する要件 (e.g., 出生証明書には捺印が必要) についての情報が必要である. 必要な Identity Evidence を取得することが潜在的に困難な可能性もあるため, これは特に重要である.
  * 可能であれば, 必要な Identity Evidence の取得を容易にするツールを実装する.
  * ユーザーに, 未成年や独特なニーズを持つ人々に対する特別な要件を知らせる. 例えば, 公証人, 法定後見人, その他の本人の代理権を法的に証明できる個人などの Trusted Referee を利用する場合に必要な情報 (詳細は [Section 5.3.4](#trustref) を参照).
  * フォームが必要であれば
     * Enrollment Session 開始前および Session 中に記入式フォームを提示すること. ユーザーにプリンターへの Access を要求しないこと.
     * ユーザーがフォームに入力しなければならない情報量を最小化すること. フォームが長くなると, ユーザーは簡単にフラストレーションを感じ, エラーを発生させがちである. 可能であれば事前にフォームを埋めておくこと.

<!--
* Information on whether the user's enrollment session will be in-person or in-person over remote channels, and whether a user can choose. Only provide information relevant to the allowable session option(s).
  * Information on the location(s), whether a user can choose their preferred location, and necessary logistical information for in-person or in-person over remote channels session. Note that users may be reluctant to bring identity evidence to certain public places (bank versus supermarket), as it increases exposure to loss or theft.
  * Information on the technical requirements (e.g., requirements for internet access) for remote sessions.
  * An option to set an appointment for in-person or in-person over remote channels identity proofing sessions to minimize wait times. If walk-ins are allowed, make it clear to users that their wait times may be greater without an appointment.
    * Provide clear instructions for setting up an enrollment session appointment, reminders, and how to reschedule existing appointments.
    * Offer appointment reminders and allow users to specify their preferred appointment reminder format(s) (e.g., postal mail, voicemail, email, text message). Users need information such as date, time, location, and a description of required identity evidence.
* Information on the allowed and required identity evidence and attributes, whether each piece is voluntary or mandatory, and the consequences for not providing the complete set of identity evidence. Users need to know the specific combinations of identity evidence, including requirements specific to a piece of identity evidence (e.g., a raised seal on a birth certificate). This is especially important due to potential difficulties procuring the necessary identity evidence.
  * Where possible, implement tools to make it easier to obtain the necessary identity evidence.
  * Inform users of any special requirements for minors and people with unique needs. For example, provide users with the information necessary to use trusted referees, such as a notary, legal guardian, or some other form of certified individual that can legally vouch for or act on behalf of the individual (see [Section 5.3.4](#trustref)).
  * If forms are required:
     * Provide fillable forms before and at the enrollment session. Do not require users to have access to a printer.
     * Minimize the amount of information users must enter on a form, as users are easily frustrated and more error-prone with longer forms. Where possible, pre-populate forms.
-->

### 9.3 Enrollment and Proofing Session

Enrollment Session に特化したユーザビリティー上の考慮事項としては, 以下のような項目が挙げられる.

<!-- Usability considerations specific to the enrollment session include: -->

* ユーザーに Enrollment Session 開始時に Enrollment Session の手順についてリマインドすること. ユーザーが事前準備段階でそれらを覚えてくることを期待しないように. Enrollment Session が事前準備の直後に開始されない場合, Proofing および Enrollment フェーズ完了にかかる典型的時間枠を明示的にリマインドすることが特に重要である.
  * 対面ないしは Remote チャネル越しの対面でリスケジューリングできるようにすること.
  * 可能な場合は, 利用可能かつ必要な Identity Evidence のチェックリストを提供し, Enrollment コードを含め, ユーザーが Enrollment Session を進めるのに必要な Identity Evidence を確実に持っているようにすること.
  * どの情報が破棄され, どの情報が将来のフォローアップ Session のために保管され, どの Identity Evidence が将来の Session を完了させるために必要となるかをユーザーに通知すること. 理想的には, ユーザーは Identity Proofing Session を途中で終了させるか選択できることが望ましい.
  * 事前の Identity Verification の経験によりユーザーはすでに何らかの期待を持っている可能性があることから, ユーザーに Enrollment Session の結果に関する想定を伝えること (e.g., 運転免許証が対面で手渡される, パスポートが郵送で送られる).
  * ユーザーが Authenticator を Enrollment Session 成功後即時に渡されるのか否か, Authenticator を受け取るための予定を立てなければならないのか, Authenticator を郵送で受け取ればいいのか, またいつ Authenticator が受け取れると期待すれば良いかなどを明確にすること.

<!--
* Remind users at the start of the enrollment session of the enrollment session procedure, without expecting them to remember from the pre-enrollment preparation step. If the enrollment session does not immediately follow pre-enrollment preparation, it is especially important to clearly remind users of the typical timeframe to complete the proofing and enrollment phase.
  * Provide rescheduling options for in-person or in-person over remote channels.
  * Provide a checklist with the allowed and required identity evidence to ensure users have the requisite identity evidence to proceed with the enrollment session, including enrollment codes, if applicable. If users do not have the complete set of identity evidence, they must be informed regarding whether they can complete a partial identity proofing session.
  * Notify users regarding what information will be destroyed, what, if any, information will be retained for future follow-up sessions, and what identity evidence they will need to bring to complete a future session. Ideally, users can choose whether they would like to complete a partial identity proofing session.
  * Set user expectations regarding the outcome of the enrollment session as prior identity verification experiences may drive their expectations (e.g., receiving a driver's license in person, receiving a passport in the mail).
  * Clearly indicate whether users will receive an authenticator immediately at the end of a successful enrollment session, if users have to schedule an appointment to pick it up in person, or if users will receive it in the mail and when they can expect to receive it.
-->

* Enrollment Session 中には, CSP がどのデータを記録するかなど, Identity Proofing 時にユーザーに明示的に通知を行うべきいくつかの要件が課されることになる (通知要件の詳細については [Section 4.2.](#genProofReqs) と [Section 8.](#sec8) を参照). 4.2 の要件 (5) に従って, CSP がユーザーに追加の Attribute に関する同意を求めたり, Attribute を Identity Proofing, Authentication, Authorization, Attribute Assertion 以外の目的で利用することに同意を求めたりすると, そういった行為がユーザーの予期しないことであったり不快感を感じさせるかもしれない. ユーザーがそれらに対してメリットを理解できず, 余計なリスクを感じる場合, ユーザーは同意してプロセスを進めることを嫌がったりためらったりするかもしれない. 追加の要件に関して, ユーザーに明確な通知を行うこと.
* ユーザビリティー視点では KBV は非常に問題が多いため, KBV の利用は避けること. 人間の記憶力には限界があるため, KBV はエラーを引き起こしたりユーザーにフラストレーションを抱かせがちである. KBV を利用する場合は, 以下のユーザビリティー上の考慮事項に従うこと.
  * ユーザーが正しく回答できるよう, KBV の質問には関連性とコンテキストを持たせるべきである.
  * KBV の質問は明確な言い回しにすること. あいまいな表現はユーザーのエラーにつながる可能性がある. 例えば, ユーザーに社会保障残高について質問する場合, 社会保障講座の変動を考慮し期間を明確に指定すること.
  * KBV の質問をするまえに, ユーザーに以下を知らせること.
    * 許容される試行回数と残りの試行回数.
    * KBV の質問が, 次の試行において変化するであろうこと.
    * KBV Session 中, タイムアウト前にインアクティブ状態でタイムアウトが近いことを警告すること.
* Enrollment コードが発行される場合.
    * 事前に Enrollment コードが送られることを, その到着予想時期, コードの有効期間, 送付方法 (e.g., 郵送, SMS, 固定電話, Email) とともにユーザーに通知すること.
    * Enrollment コードをユーザーに送付する際は, その利用手順と有効期限を添えること. 特に [Section 4.4.1.6](#4-4-1-6) にあるように有効期間が短い場合, この情報は特に重要である.
    * QR コードなどの機械可読光学ラベルを発行する場合 ([Section 4.6.](#enrollmentcode) 参照), どうすれば QR コードをスキャンできるかについての情報も添えること (e.g., 利用可能な QR コードアプリケーション).
    * Enrollment コードが期限切れしたり使用前に紛失したりすると, Enrollment プロセスを再び繰り返す必要があることをユーザーに知らせること.
    * 全てのユーザーがこのレベルの技術を使いこなせるわけではないため, 代替オプションをユーザーに提供すること. 例えば, ユーザーはこのアプローチに必要な技術を持ち合わせていないかもしれない.
* Enrollment Session 終了時には以下のようにすること.
  * Enrollment が成功した場合は, ユーザーに成功した Enrollment に関する確認と次のステップに関する情報を送ること (e.g., いつどこで Authenticator を受け取るべきかや, いつ Authenticator が郵送されるかなど).
  * Enrollment が途中で終了 (ユーザーが完全な Identity Evidence セットを持っていなかった, ユーザーがプロセス中断を選択した, Session がタイムアウトしたなど) した場合は, ユーザーに以下を伝えること.
    * どの情報が破棄されるか.
    * もしあれば, どの情報が将来のフォローアップ Session のために保持されるか.
    * どれくらいの期間その情報が保持されるか.
    * 将来の Session ではどの Identity Evidence を持ってくる必要があるか.
  * Enrollment が失敗した場合は, ユーザーに代替の Enrollment Session タイプについての明確な説明を提供すること. 例えば, Remote Proofing を完了できないユーザーに対面の Proofing を提供するなど.
* ユーザーが Enrollment Session 中に Authenticator を受け取る場合は, ユーザーに Authenticator の利用と保管に関する情報を提供すること. 例えば, 利用手順 (特に初回利用時や初期化時に特別な要件がある場合), Authenticator の有効期限, Authenticator の保護方法, Authenticator を紛失したり盗まれた場合の対応方法など.

<!--
* During the enrollment session, there are several requirements to provide users with explicit notice at the time of identity proofing, such as what data will be retained on record by the CSP (see [Section 4.2.](#genProofReqs) and [Section 8.](#sec8) for detailed requirements on notices). If CSPs seek consent from a user for additional attributes or uses of their attributes for any purpose other than identity proofing, authentication, authorization or attribute assertions, per 4.2 requirement (5), make CSPs aware that requesting additional attributes or uses may be unexpected or may make users uncomfortable. If users do not perceive benefit(s) to the additional collection or uses, but perceive extra risk, they may be unwilling or hesitant to provide consent or continue the process. Provide users with explicit notice of the additional requirements.
* Avoid using KBV since it is extremely problematic from a usability perspective. KBV tends to be error-prone and frustrating for users given the limitations of human memory. If KBV is used, address the following usability considerations.
  * KBV questions should have relevance and context to users for them to be able to answer correctly.
  * Phrase KBV questions clearly, as ambiguity can lead to user errors. For example, when asking about a user's social security balance, clearly specify which time period as social security accounts fluctuate.
  * Prior to being asked KBV questions, users must be informed of:
    * The number of allowed attempts and remaining attempt(s).
    * The fact that KBV questions will change on subsequent attempts.
    * During the KBV session, provide timeout inactivity warnings prior to timeout.
* If an enrollment code is issued:
    * Notify users in advance that they will receive an enrollment code, when to expect it, the length of time for which the code is valid, and how it will arrive (e.g., physical mail, SMS, landline telephone, email, or physical mailing address).
    * When an enrollment code is delivered to a user, include instructions on how to use the code, and the length of time for which the code is valid. This is especially important given the short validity timeframes specified in [Section 4.4.1.6](#4-4-1-6).
    * If issuing a machine-readable optical label, such as a QR Code (see [Section 4.6.](#enrollmentcode)), provide users with information on how to obtain QR code scanning capabilities (e.g., acceptable QR code applications).
    * Inform users that they will be required to repeat the enrollment process if enrollment codes expire or are lost before use.
    * Provide users with alternative options as not all users are able to use this level of technology. For example, users may not have the technology needed for this approach to be feasible.
* At the end of the enrollment session,
  * If enrollment is successful, send users confirmation regarding the successful enrollment and information on next steps (e.g., when and where to pick up their authenticator, when it will arrive in the mail).
  * If enrollment is partially complete (due to users not having the complete set of identity evidence, users choosing to stop the process, or session timeouts), communicate to users:
    * what information will be destroyed;
    * what, if any, information will be retained for future follow-up sessions;
    * how long the information will be retained; and
    * what identity evidence they will need to bring to a future session.
  * If enrollment is unsuccessful, provide users with clear instructions for alternative enrollment session types, for example, offering in-person proofing for users that can not complete remote proofing.
* If users receive the authenticator during the enrollment session, provide users information on the use and maintenance of the authenticator. For example, information could include instructions for use (especially if there are different requirements for first-time use or initialization), information on authenticator expiration, how to protect the authenticator, and what to do if the authenticator is lost or stolen.
-->

* 対面の Proofing, および Remote の Enrollment Session 越しに行われる対面の Proofing のどちらにおいても, 追加のユーザビリティー上の考慮事項が適用される.
  * Enrollment Session 開始時に, オペレーターや係員は自身の役割をユーザーに説明すること (e.g., オペレーターないし係員は,  Enrollment Session をとおしてユーザーに付き添うのか, 静かに観察し必要な時だけインタラクションを行うのか).
  * Enrollment Session 開始時に, ユーザーに Session 中に離席してはならないこと, Session をとおして彼らのアクションが可視でなければならないことを伝えること.
  * Enrollment Session 中に Biometrics が収集される場合は, その収集プロセスを完了させる手順についてユーザーに明確に説明すること. この情報はプロセス直前に提供されることが最も望ましい. その場にいるオペレーターからの修正フィードバックが可能な口頭での説明が, 最も効果的である (e.g., Biometrics センサーがどこにあるか, いつ開始されるか, どのようにセンサーとインタラクションすべきか, いつ Biometrics の収集が完了するか).

<!--
* For both in-person and in-person proofing performed over remote channels enrollment sessions, additional usability considerations apply:
  * At the start of the enrollment session, operators or attendants need to explain their role to users (e.g., whether operators or attendants will walk users through the enrollment session or observe silently and only interact as needed).
  * At the start of the enrollment session, inform users that they must not depart during the session, and that their actions must be visible throughout the session.
  * When biometrics are collected during the enrollment session, provide users clear instructions on how to complete the collection process. The instructions are best given just prior to the process. Verbal instructions with corrective feedback from a live operator are the most effective (e.g., instruct users where the biometric sensor is, when to start, how to interact with the sensor, and when the biometric collection is completed).
-->

* Remote Identity Proofing はオンラインで行われるため, 一般的な Web 上のユーザビリティー原則に従うこと. 以下に例を挙げる.
  * ユーザーが Enrollment プロセスを通過できるようにユーザーインターフェースを設計すること.
  * ユーザーが記憶しなければならないことを減らすこと.
  * インターフェースを一貫したものにすること.
  * 順序づけられたステップには明確にラベルをつけること.
  * 開始ポイントを明確にすること.
  * 多様なプラットフォームやデバイスサイズをサポートするように設計すること.
  * ナビゲーションを, 一貫性があり発見しやすく辿りやすいものにすること.

<!--
* Since remote identity proofing is conducted online, follow general web usability principles. For example:
  * Design the user interface to walk users through the enrollment process.
  * Reduce users' memory load.
  * Make the interface consistent.
  * Clearly label sequential steps.
  * Make the starting point clear.
  * Design to support multiple platforms and device sizes.
  * Make the navigation consistent, easy to find, and easy to follow.
-->

###  <a name="sec9_4"></a>9.4 Post-Enrollment

Post-Enrollment とは, Enrollment 直後かつ Authenticator 通常利用前のステップを指す (Authenticator 通常利用と断続的イベントに関するユーザビリティー上の考慮事項については, [SP800-63B](sp800-63b.html) Section 10.1-10.3 を参照). 上述のように, ユーザーは Enrollment Session 終了時に Authenticator の配送 (もしくは受け取り) 手段に関して知らされている.

<!-- Post-enrollment refers to the step immediately after enrollment but prior to typical usage of an authenticator (for usability considerations for typical authenticator usage and intermittent events, see [SP800-63B](sp800-63b.html), Section 10.1-10.3. As described above, users have already been informed at the end of their enrollment session regarding the expected delivery (or pick-up) mechanism by which they will receive their authenticator. -->

Post-Enrollment に関するユーザビリティー上の考慮事項には以下のようなものがある.

<!-- Usability considerations for post-enrollment include: -->

* ユーザーの Authenticator 到着までの待ち時間を最小化すること. 待ち時間が短いほど, ユーザーはすぐに情報システムとサービスに Access できる.

<!-- * Minimize the amount of time that users wait for their authenticator to arrive. Shorter wait times will allow users to access information systems and services more quickly. -->

* Authenticator を受け取るために物理的にある場所に行く必要があるかどうかを知らせること. 既出の予約とリマインダーに関するユーザビリティー上の考慮事項はここでも適用される.

<!-- * Inform users whether they need to go to a physical location to pick up their authenticators. The previously-identified usability considerations for appointments and reminders still apply. -->

* Authenticator と共に, Authenticator の利用と管理に関する情報も提供すること. これには, 利用手順 (特に初回利用時や初期化時に特別な要件がある場合), Authenticator の有効期限, Authenticator の保護方法, Authenticator を紛失したり盗まれた場合の対応方法などが含まれる.

<!-- * Along with the authenticator, give users information relevant to the use and maintenance of the authenticator; this may include instructions for use, especially if there are different requirements for first-time use or initialization, information on authenticator expiration, and what to do if the authenticator is lost or stolen. -->
