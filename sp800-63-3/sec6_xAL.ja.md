<a name="sec6"></a>

<div class="breaker"></div>

## 6 <a name="CYOA"></a>Selecting Assurance Levels

_This section is normative._

Risk Assessment の結果は最適なレベル選択における第一の要素となる. 本セクションでは Risk Assessment の結果を, リスクと無関係なその他の要素と合わせて, どのように最も有益な xAL 選択を行うかについて詳説する.

<!-- The risk assessment results are the primary factor in selecting the most appropriate levels. This section details how to apply the results of the risk assessment with additional factors unrelated to risk to determine the most advantageous xAL selection. -->

第一に, Risk Assessment 影響プロファイル を, [Table 6-1](#63Sec6-Table6-1) にある各 Assurance Level に関連する影響プロファイルと比較する. 必要な Assurance Level を決定するには, Risk Assessment により得られた全カテゴリーにおける潜在的影響に合致ないしは超越する影響プロファイルを見つけること.

<!-- First, compare the risk assessment impact profile to the impact profiles associated with each assurance level, as shown in [Table 6-1](#63Sec6-Table6-1) below. To determine the required assurance level, find the lowest level whose impact profile meets or exceeds the potential impact for every category analyzed in the risk assessment. -->

<a name="63Sec6-Table6-1"></a>
<div class="text-center" markdown="1">
**Table 6-1 Maximum Potential Impacts for Each Assurance Level**
</div>

<table>

 <tr>

 <td></td>
    <td style="text-align: center" colspan="3"><strong>Assurance Level</strong></td>
  </tr>
  <tr>

  <th>影響カテゴリー</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
  </tr>
  <tr>
    <td>不便, 苦痛, または社会的地位やレピュテーションの毀損</td>
    <td>Low</td>
    <td>Mod</td>
    <td>High</td>
  </tr>
  <tr>
    <td>経済的損失または機関の負債</td>
    <td>Low</td>
    <td>Mod</td>
    <td>High</td>
  </tr>
   <tr>
    <td>機関のプログラムや公共の利益への損害</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  <tr>
  <tr>
    <td>Authorize のないセンシティブ情報の公開</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  </tr>
    <td>個人の安全</td>
    <td>N/A</td>
    <td>Low</td>
    <td>Mod/High</td>
  </tr>

  </tr>
  <tr>
    <td>民事または刑事上の違反</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  </tr>

</table>

<!-- <table>

 <tr>

 <td></td>
    <td style="text-align: center" colspan="3"><strong>Assurance Level</strong></td>
  </tr>
  <tr>

  <th>Impact Categories</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
  </tr>
  <tr>
    <td>Inconvenience, distress or damage to standing or reputation</td>
    <td>Low</td>
    <td>Mod</td>
    <td>High</td>
  </tr>
  <tr>
    <td>Financial loss or agency liability</td>
    <td>Low</td>
    <td>Mod</td>
    <td>High</td>
  </tr>
   <tr>
    <td>Harm to agency programs or public interests</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  <tr>
  <tr>
    <td>Unauthorized release of sensitive information</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  </tr>
    <td>Personal Safety</td>
    <td>N/A</td>
    <td>Low</td>
    <td>Mod/High</td>
  </tr>

  </tr>
  <tr>
    <td>Civil or criminal violations</td>
    <td>N/A</td>
    <td>Low/Mod</td>
    <td>High</td>
  </tr>

</table> -->

リスクを分析するにあたり, 機関は, 何らかの失敗を引き起こしたり人・組織に損害を及ぼす可能性を含む, 予想される Authenticatino 失敗の直接的および間接的な結果のすべてを考慮しなければならない (SHALL). 潜在的な影響の定義には, 意味がコンテキストに依存する "相当" または "軽微" のような相対的な用語が含まれる. 機関はこういった被害の相対的重要性を決定するために, 影響を受ける人や主体のコンテキストや性質を考慮すべきである (SHOULD). 時間が経つにつれて, 機関はこれらの問題に関する実践的な経験を得ることとなり, これらの用語の意味はより明確になるであろう. 機関のプログラムや公共の利益に対する被害の分析はコンテキストに強く依存するため, 機関はこれらの問題を注意深く考慮すべきである (SHOULD).

<!-- In analyzing risks, the agency SHALL consider all of the expected direct and indirect results of an authentication failure, including the possibility that there will be more than one failure, or harms to more than one person or organization. The definitions of potential impacts contain some relative terms, like "serious" or "minor," whose meaning will depend on context. The agency SHOULD consider the context and the nature of the persons or entities affected to decide the relative significance of these harms. Over time, the meaning of these terms will become more definite as agencies gain practical experience with these issues. The analysis of harms to agency programs or other public interests depends strongly on the context; the agency SHOULD consider these issues with care. -->

IAL, AAL, FAL の各 Assurance Level 値はそれぞれ異なる可能性もある. 例えばある機関が, ユーザーにより Personal Health Information (PHI) といった形で Personal Information が提出される "health tracker" アプリケーションを構築したとする. [EO 13681](#EO13681) には "デジタルアプリケーションを通じて, 市民に対して Personal Data への Access を可能にする全機関は, Multi-factor Authentication を採用する必要がある" と定められており, 当該機関は AAL2 ないしは AAL3 で MFA を実装する必要がある.

<!-- It is possible that the assurance levels may differ across IAL, AAL, and FAL. For example, suppose an agency establishes a "health tracker" application in which users submit personal information in the form of personal health information (PHI). In line with the terms of [EO 13681](#EO13681) requiring "that all agencies making personal data accessible to citizens through digital applications require the use of multiple factors of authentication," the agency is required to implement MFA at AAL2 or AAL3. -->

また EO 13681 は, Personal Information が公開される場合, 各機関が "必要に応じて有効な Identity Proofing プロセス" を行うことを要求している. これは (必要な AAL に合致するよう) IAL2 や IAL3 での Proofing が必要であるということを意味しない. 上記の例では, 機関のシステムはユーザーの実際の Identity を知る必要もないかもしれない. このケースでは, "有効な Proofing プロセス" というのは Proofing を一切行わないこととなり, 機関は IAL1 を選択することになるであろう. これによりHealth Tracker システムのユーザーは Pseudonymous な状態でいることができる.

<!-- EO 13681 also requires agencies employ "an effective identity proofing process, as appropriate" when personal information is released. This does not mean that proofing at IAL2 or IAL3 (to match the required AAL) is necessary. In the above example, there may be no need for the agency system to know the actual identity of the user. In this case, an "effective proofing process" would be to not proof at all, therefore the agency would select IAL1. This allows the user of the health tracker system to be pseudonymous. -->

ユーザーが Pseudonymous な状態である一方で, 機関 Authentication においては AAL2 や AAL3 を選択するべきである. さもないと悪意ある主体が正規ユーザーのアカウントを侵害し, 当該ユーザーの PHI に Access 可能となってしまう.

<!-- Despite the user being pseudonymous, the agency should still select AAL2 or AAL3 for authentication because a malicious actor could gain access to the user's PHI by compromising the account. -->

> Note: 機関は上表で求められている以上の Assurance Level を許容することもできる. 例えば Federated Transaction では, IAL2 と評価されたアプリケーションにおいて IAL3 の Identity を受け入れることも可能である. これは Authenticator に対しても同様であり, RP が必要とするより強固な Authenticator を利用することも可能である. ただし RP は, こういったことが　CSP によって適切なプライバシー保護がなされている Federated シナリオのみで発生し, RP が要求し Subscriber が Authorize した Attribute のみが RP に提供され, 過度な Personal Information が Credential や Assertion から漏れることがないよう保証する必要がある. 詳細は [SP 800-63C の Privacy Considerations](sp800-63c.html#privacy) を参照のこと.

<!-- > Note: An agency can accept a higher assurance level than those required in the table above. For example, in a federated transaction, an agency can accept an IAL3 identity if their application is assessed at IAL2. The same holds true for authenticators: stronger authenticators can be used at RPs that have lower authenticator requirements. However, RPs will have to ensure that this only occurs in federated scenarios with appropriate privacy protections by the CSP such that only attributes that have been requested by the RP and authorized by the subscriber are provided to the RP and that excessive personal information does not leak from the credential or an assertion. See the [privacy considerations in SP 800-63C](sp800-63c.html#privacy) for more details. -->

<!---->

> Note: 単一のアプリケーションにおいて異なる IAL, AAL, FAL を設定可能ということは, 本ドキュメントがもはや総合的な LOA という概念をサポートしていないということである. LOA 決定のための "Low Watermark" アプローチはもはや通用しない. IAL1 かつ AAL2 のアプリケーションを, IAL2 かつ AAL2 のアプリケーションよりセキュアでないとかプライバシー強度が低いとみなすべきではない. これらのアプリケーションの差異は, 必要とされる Proofing の程度のみであり, それはアプリケーションのセキュリティーやプライバシーには影響しないかもしれない. 一方でもし機関が誤った xAL 選択を行うと, セキュリティーやプライバシーに大きな影響を及ぼす可能性がある.

<!-- > Note: The upshot of potentially having a different IAL, AAL, and FAL within a single application stems from the fact that this document no longer supports the notion of an overall LOA &mdash; the "low watermark" approach to determining LOA no longer applies. An application with IAL1 and AAL2 should not be considered any less secure or privacy-enhancing than an application with IAL2 and AAL2. The only difference between these applications is the amount of proofing required, which may not impact the security and privacy of each application. That said, if an agency incorrectly determines the xAL, security and privacy could very well be impacted. -->

### <a name="IAL_CYOA"></a> 6.1 Selecting IAL

[Figure 6-1](#63Sec6-Figure1) に示す IAL の決定木は, Risk Assessment の結果と Identity Proofing サービスに関する追加の考慮事項を組み合わせ, 各機関がデジタルサービスの提供に最適な Identity Proofing 要件を決定する際の一助となる.

<!-- The IAL decision tree in [Figure 6-1](#63Sec6-Figure1) combines the results from the risk assessment with additional considerations related to identity proofing services to allow agencies to select the most appropriate identity proofing requirements for their digital service offering. -->

IAL 選択の実施は, 当該デジタルサービス提供者が Proofing を行わなければならないということを意味するものではない. 機関が Federate できるかどうかは [Section 7](#toFedorNotToFed) に詳しく述べる.

<!-- The IAL selection does not mean the digital service provider will need to perform the proofing themselves. More information on whether an agency can federate is provided in [Section 7](#toFedorNotToFed). -->

<a name="63Sec6-Figure1"></a>
<div class="text-center" markdown="1">
<img src="sp800-63-3/media/IAL_CYOA.png" alt="IAL Choose Your Own" style="width:1000px;height:1093px;;min-width: 1000px;min-height:1093px;"/>

**Figure 6-1 Selecting IAL**
</div>


<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63-3/media/ial-step1.png" alt="IAL Step 1"/></td>
  </tr>
  <tr>
    <td>
      最初にこの問いに答えることで, Risk Assessment と IAL 選択はショートカットできる. サービスがデジタル Transaction 実行に際していかなる Personal Information も必要としない場合, システムは IAL1 で運用可能である.
    </td>
    <!-- <td>The risk assessment and IAL selection can be short circuited by answering this question first. If the service does not require any personal information to execute any digital transactions, the system can operate at IAL1.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/ial-step2.png" alt="IAL Step 2"/></td>
  </tr>
  <tr>
    <td>
      RP は Personal Information が必要であれば, 確認済かつ検証済な Attribute が必要か, Self-asserted な Attribute が許容可能かを判断する必要がある. ひとつでも確認済かつ検証済な Attribute が必要な場合は, IAL2 か IAL3 の Proofing を行なった上で Attribute を受け入れる必要があるであろう. Self-asserted な Attribute のみでデジタルサービスを提供可能であれば, IAL 選択はショートカットして IAL1 に落ち着くことができる.
    </td>
    <!-- <td>If personal information is needed, the RP needs to determine if validated and verified attributes are required, or if self-asserted attributes are acceptable. If even a single validated and verified attribute is needed, then the provider will need to accept attributes that have been IAL2 or IAL3 proofed. Again, the selection of IAL can be short circuited to IAL1 if the agency can deliver the digital service with self-asserted attributes only.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/ial-step3.png" alt="IAL Step 3"/></td>
  </tr>
  <tr>
    <td>
      この段階では, 機関はある程度の Proofing が必要であることは理解していることになる. Step 3 は, IAL2 と IAL3 のどちらが最適な選択かを決定するために, Identity Proofing が失敗した際の潜在的影響に着目している. 機関が陥る可能性のある主な Idetity Proofing 失敗は, 偽造された Identity を真として受け入れてしまうことである. これによりサービスや利益を間違った人物や不適格な人物に提供してしまうことになる. さらに, Proofing が必要ない場合や必要以上に多くの情報を収集してしまった場合, それ自体がリスクとなりうる. 従って必要がないのに検証済 Attribute を取得することも, Identity Proofing の失敗であるとみなされる. このステップでは, サービス提供の為に Personal Information が必要であるかどうか察知し, 機関が Step 1 および 2 に誤って回答していないかどうかを検知すべきである. 片方にはネガティブな影響がない場合でも, もう一方には著しい被害が及ぶ可能性もあるため, リスクは組織およびユーザーの両方の視点で考慮すべきである. 機関の Risk Management プロセスはこのステップから開始されるべきである.
    </td>
    <!-- <td>At this point, the agency understands that some level of proofing is required. Step 3 is intended to look at the potential impacts of an identity proofing failure to determine if IAL2 or IAL3 is the most appropriate selection. The primary identity proofing failure an agency may encounter is accepting a falsified identity as true, therefore providing a service or benefit to the wrong or ineligible person. In addition, proofing, when not required, or collecting more information than needed is a risk in and of itself. Hence, obtaining verified attribute information when not needed is also considered an identity proofing failure. This step should identify if the agency answered Step 1 and 2 incorrectly, realizing they do not need personal information to deliver the service. Risk should be considered from the perspective of the organization and to the user, since one may not be negatively impacted while the other could be significantly harmed. Agency risk management processes should commence with this step.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/ial-step4.png" alt="IAL Step 4"/></td>
  </tr>
  <tr>
    <td>
      Step 4 では, 機関が要求する Personal Information が最終的に Identity の特定につながるかどうかを決定する. この問いは言い換えれば, 機関がデジタルサービスに Access する Subject の完全な Identity を知る必要があり, 2-3 の Attribute が確認済かつ検証済みであったとしても Pseudonymous Access が不可能かどうかということである. 機関が Subject を特定する必要がある場合, IAL 選択プロセスは終了可能である. しかしながら機関は, Step 5 が価値あるものかどうか検討すべきである. Claim (訳注: draft 段階では "Attribute Claim" と呼ばれていた "Attribute Reference" のこと) の受け入れにより, 必要以上の Personal Information の収集や保存のリスクを軽減することができる.
    </td>
    <!-- <td>Step 4 is intended to determine if the personal information required by the agency will ultimately resolve to a unique identity. In other words, the agency needs to know the full identity of the subject accessing the digital service, and pseudonymous access, even with a few validated and verified attributes, is not possible. If the agency needs to uniquely identify the subject, the process can end. However, the agency should consider if Step 5 is of value to them, as the acceptance of claims will reduce exposure to the risk of over collecting and storing more personal information than is necessary.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/ial-step5.png" alt="IAL Step 5"/></td>
  </tr>
  <tr>
    <td>
      Step 5 はデジタルサービスが完全な Attribute Value への Access なしに提供可能かどうかにフォーカスしている. これはすべての Attribute が Claim として受け渡されなければならないという意味ではなく, 機関が必要と判断する個人の各 Attribute に着目し, どれは Claim で十分であり, どれは完全な Value でないといけないかを判断するよう求めるものである. Federated な環境ではデジタルサービス提供者は Attribute 情報を最初から管理下に置いていないため, Claim 受け取りに最適である. アプリケーションがすべての必要な Identity Proofing を自身で実行するのであれば, すべての Value がすでにデジタルサービス提供者の管理下にあるため, Claim 受け渡しは意味がない可能性もある.
    </td>
    <!-- <td>Step 5 focuses on whether the digital service can be provided without having access to full attribute values. This does not mean all attributes must be delivered as claims, but this step does ask the agency to look at each personal attribute they have deemed necessary, and identify which can suffice as claims and which need to be complete values. A federated environment is best suited for receiving claims, as the digital service provider is not in control of the attribute information to start with. If the application also performs all required identity proofing, claims may not make sense since full values are already under the digital service provider's control.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/ial-step6.png" alt="IAL Step 6"/></td>
  </tr>
  <tr>
    <td>
      もし機関が Step 6 にたどり着いたとすれば, Claim を利用すべきである. このステップにたどり着いたということは, デジタルサービスの提供に完全な Attribute Value が必要でないと判断されたということであり, デジタルサービスは Federated Attribute Reference を CSP (もしくは複数の CSPs) から受け取るのに最適であると判断される.
    </td>
    <!-- <td>If the agency has reached Step 6, claims should be used. This step identifies the digital service as an excellent candidate for accepting federated attribute references from a CSP (or multiple CSPs), since it has been determined that complete attribute values are not needed to deliver the digital service.</td> -->
  </tr>
  </table>
</div>

> Note: 機関は最適な Proofing プロセスを選択する際に, 自身のサービス対象のユーザー層も考慮すべきである. IAL 選択の機能ではないものの, ある種の Proofing プロセスはある種のユーザー層に対して他のプロセスより適切である可能性がある. 対象ユーザー層により高い Proofing 成功率を高められるため, この種の分析は機関にメリットをもたらすであろう.

<!-- > Note: Agencies should also consider their constituents' demographics when selecting the most appropriate proofing process. While not a function of IAL selection, certain proofing processes may be more appropriate for some demographics than others. Agencies will benefit as this type of analysis ensures the greatest opportunity for their constituents to be proofed successfully. -->

### <a name="AAL_CYOA"></a> 6.2 Selecting AAL

[Figure 6-2](#63Sec6-Figure2) に示す AAL の決定木は, Risk Assessment の結果と Authentication に関する追加の考慮事項を組み合わせ, 各機関がデジタルサービスの提供に最適な Authentication 要件を決定する際の一助となる.

<!-- The AAL decision tree in [Figure 6-2](#63Sec6-Figure2) combines the results from the risk assessment with additional considerations related to authentication to allow agencies to select the most appropriate authentication requirements for their digital service offering. -->

AAL 選択の実施は, 当該デジタルサービス提供者が自身で Authenticator を発行しなければならないということを意味するものではない. 機関が Federate できるかどうかは Section 7 に詳しく述べる.

<!-- The AAL selection does not mean the digital service provider will need to issue authenticators themselves. More information on whether the agency can federate is provided in [Section 7](#toFedorNotToFed). -->

<a name="63Sec6-Figure2"></a>
<div class="text-center" markdown="1">
<img src="sp800-63-3/media/AAL_CYOA.png" alt="AAL Choose Your Own" style="width:1000px;height:958px;;min-width: 1000px;min-height:958px;"/>

**Figure 6-2 Selecting AAL**
</div>

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63-3/media/aal-step1.png" alt="AAL Step 1"/></td>
  </tr>
  <tr>
    <td>
      Step 1 では Authentication 失敗の潜在的影響に着目する. これはつまり, Authorize されていないユーザーが正規のユーザーアカウントに Access できた場合, 何が起こるかということである. 片方にはネガティブな影響がない場合でも, もう一方には著しい被害が及ぶ可能性もあるため, リスクは組織およびユーザーの両方の視点で考慮すべきである. 機関の Risk Management プロセスはこのステップから開始されるべきである.
    </td>
    <!-- <td>Step 1 asks agencies to look at the potential impacts of an authentication failure. In other words, what would occur if an unauthorized user accessed one or more valid user accounts? Risk should be considered from the perspective of the organization and to a valid user, since one may not be negatively impacted while the other could be significantly harmed. Agency risk management processes should commence with this step.</td> -->
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/aal-step2.png" alt="AAL Step 2"/></td>
  </tr>
  <tr>
    <td>
      Personal Information にオンラインでアクセス可能な場合は, MFA が必要となる. この決定木の他のパスではすでに MFA が必要な AAL が確定しているため, Personal Information に関して問われるのはこの段階のみとなる. Risk Assessment 実施に際しては, 全ての AAL で Personal Information の公開に関して検討すべきである. このステップで重要な点は, Personal Information をオンラインで収集しない場合, AAL2 以上を要求するために Personal Information を確認・検証する必要はないということである. Self-asserted Personal Information の公開時も MFA によるアカウント保護は必要である. Self-asserted な情報は偽造可能だが, ほとんどのユーザーはデジタルサービスの恩恵を受けるため正しい情報を提供するであろう. したがって Self-asserted データは適切に保護しなければならない.
    </td>
    <!-- <td>MFA is required when any personal information is made available online. Since the other paths in this decision tree already drive the agency to an AAL that requires MFA, the question of personal information is only raised at this point. That said, personal information release at all AALs should be considered when performing the risk assessment. An important point at this step is that the collection of personal information, if not made available online, does not need to be validated or verified to require an AAL of 2 or higher. Release of even self-asserted personal information requires account protection via MFA. Even though self-asserted information can be falsified, most users will provide accurate information to benefit from the digital service. As such, self-asserted data must be protected appropriately.</td> -->

  </tr>

  </table>
</div>

### <a name="FAL_CYOA"></a> 6.3 Selecting FAL

The FAL decision tree in [Figure 6-3](#63Sec6-Figure3) combines the results from the risk assessment with additional considerations related to federation to allow agencies to select the most appropriate requirements for their digital service offering.

<a name="63Sec6-Figure3"></a>
<div class="text-center" markdown="1">
<img src="sp800-63-3/media/FAL_CYOA.png" alt="FAL Choose Your Own" style="width:1000px;height:983px;;min-width: 1000px;min-height:983px;"/>

**Figure 6-3 Selecting FAL**
</div>

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63-3/media/fal-step1.png" alt="FAL Step 1"/></td>
  </tr>
  <tr>
   <td>Step 1 asks agencies to look at the potential impacts of a federation failure. In other words, what would occur if an unauthorized user could compromise an assertion? Examples of compromise include use of assertion replay to impersonate a valid user or leakage of assertion information information through the browser. Risk should be considered from the perspective of the organization and to the subscriber, since one may not be negatively impacted while the other could be significantly harmed. Agency risk management processes should commence with this step.</td>
  </tr>
  <tr>
    <td><img src="sp800-63-3/media/fal-step2.png" alt="FAL Step 2"/></td>
  </tr>
  <tr>

   <td>FAL2 is required when any personal information is passed in an assertion. Personal information release at all FALs should be considered when performing the risk assessment. FAL2 or higher is required when any personal information is contained in an assertion, as the audience and encryption requirements at FAL1 are not sufficient to protect personal information from being released. Release of even self-asserted personal information requires assertion protection via FAL2. Even though self-asserted information can be falsified, most users will provide accurate information to benefit from the digital service. However, when personal information is available to the RP via an authorized API call, such information need not be included in the assertion itself. Since the assertion no longer includes personal information, it need not be encrypted and this FAL requirement does not apply.</td>

  </tr>
  <tr>
    <td><img src="sp800-63-3/media/fal-step3.png" alt="FAL Step 3"/></td>
  </tr>
  <tr>
   <td>RPs should use a back-channel presentation mechanism as described in [SP 800-63C Section 7.1](sp800-63c.html#back-channel) where possible as such mechanisms allow for greater privacy and security. Since the subscriber handles only an assertion reference and not the assertion itself, there is less chance of leakage of attributes or other sensitive information found in the assertion to the subscriber's browser or other programs. As the RP directly presents the assertion reference to the IdP, the IdP can often take steps to identify and authenticate the RP during this step. Further, as the RP fetches the assertion directly from the IdP over an authenticated protected channel, there are fewer opportunities for an attacker to inject an assertion into an RP.</td>
  </tr>

  </table>
</div>

All FALs require assertions to have a baseline of protections, including signatures, expirations, audience restrictions, and others enumerated in [SP 800-63C](sp800-63c.html#assertions). When taken together, these measures make it so that assertions cannot be created or modified by an unauthorized party, and that an RP will not accept an assertion created for a different system.

### 6.4 Combining xALs

This guideline introduces a model where individual xALs can be selected without requiring parity to each other. While options exist to select varying xALs for a system, in many instances the same level will be chosen for all xALs.

The ability to combine varying xALs offers significant flexibility to agencies, but not all combinations are possible due to the nature of the data collected from an individual and the authenticators to protect that data. [Table 6-2](#63sec6-Table2) details valid combinations of IAL and AAL to ensure personal information remains protected by MFA.

<a name="63sec6-Table2"></a>

<div class="text-center" markdown="1">

**Table 6-2 Acceptable Combinations of IAL and AAL**

</div>


| | AAL1 | AAL2 | AAL3 |
|:-:|:-:|:-:|:-:|
| **IAL1: Without personal data** | Allowed | Allowed | Allowed |
| **IAL1: With personal data** | **NO** | Allowed | Allowed |
| **IAL2** |  **NO** | Allowed | Allowed |
| **IAL3** |  **NO** | Allowed | Allowed |

> Note: Per Executive Order 13681 [[EO 13681]](#EO13681), the release of personal data requires protection with MFA, even if the personal data is self-asserted and not validated. When the transaction does not make personal data accessible, authentication may occur at AAL1, although providing an option for the user to choose stronger authentication is recommended. In addition, it may be possible at IAL1 to self-assert information that is not personal, in which case AAL1 is acceptable.
