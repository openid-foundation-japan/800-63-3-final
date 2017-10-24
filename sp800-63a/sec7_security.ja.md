<a name="sec7"></a>

<div class="breaker"></div>

## 7 Threats and Security Considerations

_This section is informative._

Enrollment プロセスにおいては, なりすまし, およびインフラストラクチャー提供者に対する不正アクセスと提供者自身の不正行為, という2つの脅威カテゴリーが一般的に存在する. インフラストラクチャーに対する脅威は従来のコンピューターセキュリティー制御策 (e.g., 侵入防止, 記録保持, 独立監査) により対応可能であるため, それらは本ドキュメントのスコープ外とし, 本セクションではなりすましの脅威に焦点を当てる. セキュリティー制御策に関する詳細は [SP 800-53](#SP800-53) *Recommended Security and Privacy Controls for Federal Information Systems and Organizations* を参照のこと.

<!-- There are two general categories of threats to the enrollment process: impersonation, and either compromise or malfeasance of the infrastructure provider. This section focuses on impersonation threats, as infrastructure threats are addressed by traditional computer security controls (e.g., intrusion protection, record keeping, independent audits) and are outside the scope of this document. For more information on security controls, see [SP 800-53](#SP800-53), *Recommended Security and Privacy Controls for Federal Information Systems and Organizations*. -->

Enrollment プロセスにおける脅威としては, なりすましに加え, Identity Proofing, Authenticator の紐付け, Credential 発行の各段階における通信メカニズムに対する脅威が挙げられる. [Table 7-1](#63aSec7-Table1) に Enrollment と Identity Proofing に関連する脅威をまとめる.

<!-- Threats to the enrollment process include impersonation attacks and threats to the transport mechanisms for identity proofing, authenticator binding, and credential issuance. [Table 7-1](#63aSec7-Table1) lists the threats related to enrollment and identity proofing. -->

<a name="63aSec7-Table1"></a>

<div class="text-center" markdown="1">

**Table 7-1 Enrollment and Identity Proofing Threats**

</div>


| **Activity** | **Threat/Attack** | **Example** |
|--------------|-------------------|-------------|
| Enrollment | Identity Proofing Evidence の偽造 | Applicant が偽造運転免許証を利用して不正な Identity を主張する. |
| | 他人の Identity の不正利用 | Applicant が他人に紐づくパスポートを利用する. |
| | Enrollment 否認 | Subscriber が Enrollment を拒否し, 自身は CSP に対して登録していないと主張する. |

<!--
|**Activity**   |     **Threat/Attack**  | **Example** |
|---------------|------------------------|------------------|
|Enrollment | Falsified identity proofing evidence | An applicant claims an incorrect identity by using a forged driver's license.|
| | Fraudulent use of another's identity | An applicant uses a passport associated with a different individual.
| | Enrollment repudiation | A subscriber denies enrollment, claiming that they did not enroll with the CSP.|
-->

### 7.1 Threat Mitigation Strategies

Enrollment における脅威は, なりすましを困難にしたり, なりすましの検出率を向上させることで, 抑止することができる. 推奨案では, おもになりすましを困難にする手法について扱うが, だれがなりすましを行なったかを証明するのに役立つ手段と手順も規定する. 各レベルにおいて, Claimed Identity が存在すること, Applicant が Claimed Identity の所有者であること, Applicant が後日 Enrollment を否認できないことを確かなものにする方法が採用される. Assurance Level が上がるにつれ, カジュアル, システマチック, および内部犯によるなりすましに対する抵抗力が高まる. [Table 7-2](#63aSec7-Table2) に Enrollment および発行プロセスにおける脅威への対策に関する戦略をまとめる.

<!-- Enrollment threats can be deterred by making impersonation more difficult to accomplish or by increasing the likelihood of detection. This recommendation deals primarily with methods for making impersonation more difficult; however, it does prescribe certain methods and procedures that may help prove who perpetrated an impersonation. At each level, methods are employed to determine that a person with the claimed identity exists, that the applicant is the person entitled to the claimed identity, and that the applicant cannot later repudiate the enrollment. As the level of assurance increases, the methods employed provide increasing resistance to casual, systematic, and insider impersonation. [Table 7-2](#63aSec7-Table2) lists strategies for mitigating threats to the enrollment and issuance processes. -->

<a name="63aSec7-Table2"></a>

<div class="text-center" markdown="1">

**Table 7-2 Enrollment and Issuance Threat Mitigation Strategies**

</div>

| **Activity** | **Threat/Attack** | **Mitigation Strategy** |**Normative Reference(s)**|
|--------------|-------------------|-------------------------|--------------------------|
| Enrollment | Identity Proofing Evidence の偽造 | CSP が提示されたエビデンスの物理セキュリティー機能を確認する. | [4.4.1.3](#4-4-1-3), [4.5.3](#4-5-3), [5.2.2](#evidence_validation) |
| | | CSP がエビデンス発行元やその他の Authoritative Source に対してエビデンスに記載された個人の詳細を確認する. | [4.4.1.3](#4-4-1-3), [4.5.3](#4-5-3), [4.5.6](#4-5-6) [5.2.2](#evidence_validation) |
| | 他人の Identity の不正利用 | CSP がエビデンス発行元やその他の Authoritative Source から取得した情報と照らし合わせ, Applicant の Identity Evidence と Biometrics を検証する. | [4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7), [5.3](#verify) |
| | | Applicant が提供した非政府発行のドキュメント (e.g., Applicant 名義で Applicant の現住所が記載された電気代の請求書や, クレジットカードの請求書) を検証し, Applicant の Identity に対する確信を高める. | [4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7), [5.3](#verify) |
| | Enrollment 否認 | CSP が Subscriber の Biometric を保存する. | [4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7) |

<!--
| **Activity** | **Threat/Attack** | **Mitigation Strategy** |**Normative Reference(s)**|
|--------------|-------------------|-------------------------|------------------------|
| Enrollment | Falsified identity proofing evidence | CSP validates physical security features of presented evidence.|[4.4.1.3](#4-4-1-3), [4.5.3](#4-5-3), [5.2.2](#evidence_validation)|
| | | CSP validates personal details in the evidence with the issuer or other authoritative source.|[4.4.1.3](#4-4-1-3), [4.5.3](#4-5-3), [4.5.6](#4-5-6) [5.2.2](#evidence_validation)|
| | Fraudulent use of another's identity | CSP verifies identity evidence and biometric of applicant against information obtained from issuer or other authoritative source.|[4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7), [5.3](#verify)|
| | |Verify applicant-provided non-government-issued documentation (e.g., electricity bills in the name of the applicant with the current address of the applicant printed on the bill, or a credit card bill) to help achieve a higher level of confidence in the applicant's identity.|[4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7), [5.3](#verify)|
| | Enrollment repudiation | CSP saves a subscriber's biometric. |[4.4.1.7](#4-4-1-7), [4.5.7](#4-5-7)
-->