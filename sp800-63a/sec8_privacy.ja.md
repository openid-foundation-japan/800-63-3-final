<a name="sec8"></a>

<div class="breaker"></div>

## <a name="privacy-section-header"></a> 8 Privacy Considerations

_This section is informative._

以下のプライバシーに関する考慮事項は, [Section 4.2](#genProofReqs) の General Requirements に関する情報を提供する.

<!-- These privacy considerations provide information regarding the General Requirements set forth in [Section 4.2](#genProofReqs). -->

### 8.1 Collection and Data Minimization

[Section 4.2 requirement 2](#4.2-r2) では, Identity Resolution, Validation および Verification に対する適用可能なベストプラクティスに基づいて, Claimed Identity の存在確認および Claimed Identity と Applicant の関連付けに必要な PII のみの収集を許可している. 不必要な PII を収集すると, なぜ Identity Proofing に利用されない情報が収集されているのかという混乱を生じさせる. これは侵害や不要な懸念を与え, Applicant の信頼を損ねることにつながる可能性がある. さらに, PII を保持すると, Unauthorized Access や不正利用に対して脆弱になる可能性もある. データ最小化により PII の量を減少させそのようなリスクを軽減することは, Identity Proofing プロセスにおける信頼を促進することとなろう.

<!-- [Section 4.2 requirement 2](#4.2-r2) permits the collection of only the PII necessary to validate the existence of the claimed identity and associate the claimed identity to the applicant, based on best available practices for appropriate identity resolution, validation, and verification. Collecting unnecessary PII can create confusion regarding why information not being used for the identity proofing service is being collected. This leads to invasiveness or overreach concerns, which can lead to loss of applicant trust. Further, PII retention can become vulnerable to unauthorized access or use. Data minimization reduces the amount of PII vulnerable to unauthorized access or use, and encourages trust in the identity proofing process. -->

#### 8.1.1 Social Security Numbers

[Section 4.2 requirement 13](#4.2-r13) では, Identity Resolution がその他の Attribute や Attribute の組み合わせによって達成不可能であり, SSN が Identity Resolution に必要でない限り, CSP が SSN を収集することを禁じている. SSN への過度な信頼は, 誤用を招き, なりすましなどにより Applicant に損害を与えかねない. しかし, こと連邦政府機関の RP にとっては, SSN により Subscriber を既存のレコードに関連づけることができ, Identity Resolution が達成されるケースもある. したがって, 本ドキュメントは SSN を識別子として捉え, その利用に関して適切な措置を行う.
> Note: 高 IAL のエビデンス要件においては, SSN や Social Security Card を Identity Evidence として受け入れることを禁止している.

<!-- [Section 4.2 requirement 13](#4.2-r13) does not permit the CSP to collect the SSN unless it is necessary for performing identity resolution, when resolution cannot be accomplished by collection of another attribute or combination of attributes. Overreliance on the SSN can contribute to misuse and place the applicant at risk of harm, such as through identity theft. Nonetheless, the SSN may achieve identity resolution for RPs in particular federal agencies that use SSNs to correlate a subscriber to existing records. Thus, this document recognizes the role of the SSN as an identifier and makes appropriate allowance for its use. -->
<!-- > Note: Evidence requirements at the higher IALs preclude using the SSN or the Social Security Card as acceptable identity evidence. -->

Identity Proofing を目的として SSN を収集する前に, 各組織は SSN を収集する際の法的義務, 第三者のプロセスやシステムとの相互運用性のために SSN を利用する必要性, または運用要件を考慮する必要がある. 運用要件は, システムやプロセス, 形式が, コストや許容不可能なリスク要因により置き換え不可能であることにより示されるかもしれない. なお, 運用上の必要性は, 使い勝手や変更したくないという意思によって正当化されるものではない.

<!-- Prior to collecting the SSN for identity proofing, organizations need to consider any legal obligation to collect the SSN, the necessity of using the SSN for interoperability with third party processes and systems, or operational requirements. Operational requirements can be demonstrated by an inability to alter systems, processes, or forms due to cost or unacceptable levels of risk. Operational necessity is not justified by ease of use or unwillingness to change. -->

連邦政府機関に対する [Executive Order (EO) 9397] (#9397) の初期の要件である, 当該機関で働く個人, 取引関係にある個人, ないしは取引関係にある他組織に属する個人の識別の主要手段として SSN を利用すべしという要件は廃止された. したがって, EO 9397 はもはやそれ単体をもって SSN 収集が必要であるという権威として参照することはできない.

<!-- For federal agencies, the initial requirement in [Executive Order (EO) 9397] (#9397) to use the SSN as a primary means of identification for individuals working for, with, or conducting business with their agency, has since been eliminated. Accordingly, EO 9397 cannot be referenced as the sole authority establishing the collection of the SSN as necessary. -->

連邦政府機関は, Office of Management and Budget Policy に従って SSN の収集および不必要な利用を削減する義務を考慮に入れ, あらゆる SSN 収集に関する意思決定をレビューする必要がある.

<!-- Federal agencies need to review any decision to collect the SSN relative to their obligation to reduce the collection and unnecessary use of SSNs under Office of Management and Budget policy. -->

### <a name="consent"></a>8.2 Notice and Consent

[Section 4.2 requirement 3](4.2-r3) requires the CSP provide explicit notice to the applicant at the time of collection regarding the purpose for collecting and maintaining a record of the attributes necessary for identity proofing, including whether such attributes are voluntary or mandatory in order to complete the identity proofing transactions, and the consequences for not providing the attributes.

An effective notice will take into account user experience design standards and research, and an assessment of privacy risks that may arise from the collection. Various factors should be considered, including incorrectly inferring that applicants understand why attributes are collected, that collected information may be combined with other data sources, etc. An effective notice is never only a pointer leading to a complex, legalistic privacy policy or general terms and conditions that applicants are unlikely to read or understand.

### 8.3 Use Limitation

[Section 4.2 requirement 4](#4.2-r4) does not permit the CSP to use attributes collected and maintained in the identity proofing process for any purpose other than identity proofing, authentication, authorization, or attribute assertions, related fraud mitigation, or to comply with law or legal process unless the CSP provides clear notice and obtains consent from the subscriber for additional uses.

Consult your SAOP if there are questions about whether proposed uses fall within the scope of these permitted uses. This notice should follow the same principles as described in [Section 8.2 Notice and Consent](#consent) and should not be rolled up into a legalistic privacy policy or general terms and conditions. Rather if there are uses outside the bounds of these explicit purposes, the subscriber should be provided with a meaningful way to understand the purpose for additional uses, and the opportunity to accept or decline. The CSP cannot make acceptance by the subscriber of additional uses a condition of providing identity proofing services.

### 8.4. Redress

[Section 4.2 requirement 5](#4.2-r5) requires the CSP to provide effective mechanisms for redressing applicant complaints or problems arising from the identity proofing, and make the mechanisms easy for applicants to find and access.

The Privacy Act requires federal CSPs that maintain a system of records to follow procedures to enable applicants to access and, if incorrect, amend their records. Any Privacy Act Statement should include a reference to the applicable SORN(s), which provide the applicant with instructions on how to make a request for access or correction. Non-federal CSPs should have comparable procedures, including contact information for any third parties if they are the source of the information.

CSPs should make the availability of alternative methods for completing the process clear to users (e.g., in person at a customer service center, if available) in the event an applicant is unable to establish their identity and complete the registration process online.

> Note: If the ID proofing process is not successful, CSPs should inform the applicant of the procedures to address the issue but should not inform the applicant of the specifics of why the registration failed (e.g., do not inform the applicant, "Your SSN did not match the one that we have on record for you"), as doing so could allow fraudulent applicants to gain more knowledge about the accuracy of the PII.


### 8.5 Privacy Risk Assessment

[Section 4.2 requirement 7](#4.2-r7) and [10](#4.2-r13) require the CSP to conduct a privacy risk assessment. In conducting a privacy risk assessment, CSPs should consider:

1. The likelihood that the action it takes (e.g., additional verification steps or records retention) could create a problem for the applicant, such as invasiveness or unauthorized access to the information; and
2. The impact if a problem did occur. CSPs should be able to justify any response it takes to identified privacy risks, including accepting the risk, mitigating the risk, and sharing the risk. The use of applicant consent should be considered a form of sharing the risk, and therefore should only be used when an applicant could reasonably be expected to have the capacity to assess and accept the shared risk.

### 8.6 Agency Specific Privacy Compliance

[Section 4.2 requirement 12](#4.2-r12) covers specific compliance obligations for federal CSPs. It is critical to involve your agency's SAOP in the earliest stages of digital authentication system development to assess and mitigate privacy risks and advise the agency on compliance requirements, such as whether or not the PII collection to conduct identity proofing triggers the Privacy Act of 1974 [[Privacy Act]](#PrivacyAct) or the E-Government Act of 2002 [[E-Gov]](#E-Gov)requirement to conduct a Privacy Impact Assessment. For example, with respect to identity proofing, it is likely that the Privacy Act requirements will be triggered and require coverage by either a new or existing Privacy Act system of records due to the collection and maintenance of PII or other attributes necessary to conduct identity proofing.

The SAOP can similarly assist the agency in determining whether a PIA is required. These considerations should not be read as a requirement to develop a Privacy Act SORN or PIA for identity proofing alone; in many cases it will make the most sense to draft a PIA and SORN that encompasses the entire digital authentication process or include the digital authentication process as part of a larger programmatic PIA that discusses the program or benefit the agency is establishing online access to.

Due to the many components of digital authentication, it is important for the SAOP to have an awareness and understanding of each individual component. For example, other privacy artifacts may be applicable to an agency offering or using proofing services such as Data Use Agreements, Computer Matching Agreements, etc. The SAOP can assist the agency in determining what additional requirements apply. Moreover, a thorough understanding of the individual components of digital authentication will enable the SAOP to thoroughly assess and mitigate privacy risks either through compliance processes or by other means.
