<a name="sec9"></a>

## 9 プライバシーの考慮事項

<!-- ## 9 Privacy Considerations -->

*これらのプライバシーに関する考慮事項はセクション 4 のガイダンスを補足する．This section is informative.*

<!-- *These privacy considerations supplement the guidance in Section 4. This section is informative.* -->

### 9.1 プライバシー Risk Assessment

<!-- ### 9.1 Privacy Risk Assessment -->

[セクション 4.1.5](#aal1records), [4.2.5](#aal2records), [4.3.5](#aal3records) は CSP にレコード保有のためのプライバシー Risk Assessment を行わせることを必要とする．このようなプライバシー Risk Assessment が含まれる :

<!-- [Sections 4.1.5](#aal1records), [4.2.5](#aal2records), and [4.3.5](#aal3records) require the CSP to conduct a privacy risk assessment for records retention. Such a privacy risk assessment would include: -->

1. レコード保有が Subscriber に侵害や権限のない情報へのアクセスなどの問題を引き起こす可能性
2. そのような問題が発生した場合のインパクト

<!-- 1. The likelihood that the records retention could create a problem for the subscriber, such as invasiveness or unauthorized access to the information.
2. The impact if such a problem did occur. -->

CSP はリスク受容，リスク軽減，リスク共有など，特定されたプライバシーリスクをとった場合に起こることを合理的に正当化できるべきである． Subscriber の同意を得ることはリスク共有の形と見なされ，Subscriber が共有されたリスクを適切に評価し，受け入れる能力があることが合理的に期待される場合にのみ適している．

<!-- CSPs should be able to reasonably justify any response they take to identified privacy risks, including accepting the risk, mitigating the risk, and sharing the risk. The use of subscriber consent is a form of sharing the risk, and therefore appropriate for use only when a subscriber could reasonably be expected to have the capacity to assess and accept the shared risk. -->

### 9.2 プライバシー コントロール

<!-- ### 9.2 Privacy Controls -->

[セクション 4.4](#aal_privacy) は CSP が適切に調整されたプライバシーコントロールを採用することを必要とする． [SP 800-53](#SP800-53) は，CSP が Authentication メカニズムをデプロイするときに検討するべき一連のプライバシーコントロールを提供する． これらのコントロールは，成功し，信頼できるデプロイメントのための通知や救済策，その他の重要な考慮事項をカバーする．

<!-- [Section 4.4](#aal_privacy) requires CSPs to employ appropriately-tailored privacy controls. [SP 800-53](#SP800-53) provides a set of privacy controls for CSPs to consider when deploying authentication mechanisms. These controls cover notices, redress, and other important considerations for successful and trustworthy deployments. -->

### 9.3 使用制限

<!-- ### 9.3 Use Limitation -->

[セクション 4.4](#aal_privacy) は，Authentication 以外のいかなる目的，詐欺の緩和，または法律や法的手続きにおいて，CSP が明確な通知を提供し Subscriber からの追加の用途についての同意を取得しない限り，Authentication プロセス中に収集され保持される Authenticator についての情報の使用を禁止する． そのような情報の使用は，収集の本来の目的に限定されていることが保証されるよう注意が払われるべきである． 提案されたエージェンシーの使用がこのスコープに該当するが疑問がある場合は，あなたの SAOP に相談してほしい． [セクション 4.4](#aal_privacy) で述べられているように，Subscriber による追加の要件の受諾は，Authentication サービスを提供する条件としないこととする．

<!-- [Section 4.4](#aal_privacy) prohibits CSPs from using information about authenticators that is collected and maintained in the authentication process for any purpose other than authentication, related fraud mitigation, or to comply with law or legal process, unless the CSP provides clear notice and obtains consent from the subscriber for additional uses. Care should be taken to ensure that the use of such information is limited to its original purpose for collection. Consult your SAOP if there are questions about whether proposed agency uses fall within this scope. As stated in [Section 4.4](#aal_privacy), acceptance by the subscriber of additional uses SHALL NOT be a condition of providing authentication services. -->

### 9.4 <a name="agency-privacy"></a>Agency-Specific Privacy Compliance

<!-- ### 9.4 <a name="agency-privacy"></a>Agency-Specific Privacy Compliance -->

[セクション 4.4](#aal_privacy) は，連邦政府の CSP に関する特定の遵守義務をカバーする． プライバシーリスクを評価，軽減し，Authenticator を発行または維持する PII のコレクションが PIA を実施するための *Privacy Act of 1974* [Privacy Act](#PrivacyAct) や *E-Government Act of 2002* [E-Gov](#E-Gov) 要件をトリガーするかどうかなど，コンプライアンス要件について助言するように，Digital Authentication システム開発の最初期段階にあなたのエージェンシーの SAOP を参画させることが重要である． たとえば，Biometrics の集中保有に関して， Privacy Act requirements がトリガーされ，Authentication に必要なその他の属性や PII の収集，維持のために，新規または既存の Privacy Act 記録のシステムによってカバーされる必要があるかもしれない． SAOP は PIA が必要かどうかを判断する際， 同様にエージェンシーを支援することができる．

<!-- [Section 4.4](#aal_privacy) covers specific compliance obligations for federal CSPs. It is critical to involve your agency's SAOP in the earliest stages of digital authentication system development in order to assess and mitigate privacy risks and advise the agency on compliance requirements, such as whether or not the collection of PII to issue or maintain authenticators triggers the *Privacy Act of 1974* [Privacy Act](#PrivacyAct) or the *E-Government Act of 2002* [E-Gov](#E-Gov) requirement to conduct a PIA. For example, with respect to centralized maintenance of biometrics, it is likely that the Privacy Act requirements will be triggered and require coverage by either a new or existing Privacy Act system of records due to the collection and maintenance of PII and any other attributes necessary for authentication. The SAOP can similarly assist the agency in determining whether a PIA is required. -->

これらの考慮事項は Authentication だけのために Privacy Act SORN や PIA を開発するための要件として読まれるべきでない． 多くの場合，全体を網羅する Digital Authentication プロセスの PIA と SORN を下書きすることや，エージェンシーがオンラインで確立しているサービスやベネフィットを議論する，より大きなプログラマティック PIA の一部として Digital Authentication を含めることが最も理にかなっている．

<!-- These considerations should not be read as a requirement to develop a Privacy Act SORN or PIA for authentication alone. In many cases it will make the most sense to draft a PIA and SORN that encompasses the entire digital authentication process or include the digital authentication process as part of a larger programmatic PIA that discusses the service or benefit to which the agency is establishing online. -->

多くの Digital Authentication コンポーネントのために，SAOP がそれぞれ個別のコンポーネントの認識と理解を持つことが重要である． たとえば，他のプライバシー成果物は連携された CSP や RP のサービスを提供または使用するエージェンシーに適用可能であってもよい (例 : データ使用規約，コンピュータマッチング規約) ． SAOP は追加要件の適用を判断する際にエージェンシーを支援できる． また，Digital Authentication の個別のコンポーネントを完全に理解することは，コンプライアンスプロセスまたはほかの手段によって，SAOP が徹底的にプライバシーリスクを評価，軽減することを可能にする．

<!-- Due to the many components of digital authentication, it is important for the SAOP to have an awareness and understanding of each individual component. For example, other privacy artifacts may be applicable to an agency offering or using federated CSP or RP services (e.g., Data Use Agreements, Computer Matching Agreements). The SAOP can assist the agency in determining what additional requirements apply. Moreover, a thorough understanding of the individual components of digital authentication will enable the SAOP to thoroughly assess and mitigate privacy risks either through compliance processes or by other means. -->
