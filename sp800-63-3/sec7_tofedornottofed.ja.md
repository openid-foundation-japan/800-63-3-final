<a name="sec7"></a>

<div class="breaker"></div>

## 7 <a name="toFedorNotToFed"></a> Federation Considerations

_This section is informative._

本ガイドラインおよび付随する Vol. は, 各機関が選択する Authentication および Identity Proofing アーキテクチャーに関しては不問である. しかしながら, 機関や個々のアプリケーションローカルで Identity サービスを構築するよりも, Identity Federation を利用した方がより効率的かつ効果的になるようなシナリオが存在する. 以下に Federation が利用可能であればそれを有望な選択肢として考慮すべきシナリオをまとめる. なおこのリストは Federation とローカルの Identity アーキテクチャーの経済的メリットデメリットを考慮したものではない.

<!-- This guideline and its companion volumes are agnostic to the authentication and identity proofing architecture an agency selects. However, there are scenarios an agency may encounter that make identity federation potentially more efficient and effective than establishing identity services local to the agency or individual applications. The following list details scenarios where, if any apply, the agency may consider federation a viable option. This list does not take into consideration any economic benefits or weaknesses of federation vs. localized identity architectures. -->

Authenticator を Federate すべきケース:

<!-- Federate authenticators when: -->

1. 潜在的ユーザーがすでに必要な AAL 以上を満たす Authenticator を持っている.
2. 想定される全てのユーザーコミュニティーをカバーするために複数の Credential フォームファクターが必要である.
3. 機関が Authentication 管理 (e.g., アカウントリカバリー, Authenticator 発行, ヘルプデスク) のためのインフラストラクチャーを保持していない.
4. RP 実装を変更することなく, 時間経過によりプライマリーな Authenticator を追加したりアップグレードしたいという要望がある.
5. サポートすべき複数の環境がある. Federation プロトコルは Network ベースであり, 多様なプラットフォームや言語による実装が可能である.
6. 潜在的ユーザーが複数のコミュニティーに所属し, それぞれが独自に既存の Identity インフラストラクチャーを保持している.

<!-- 1. Potential users already have an authenticator at or above required AAL.
2. Multiple credential form factors are required to cover all possible user communities.
3. Agency does not have infrastructure to support authentication management (e.g., account recovery, authenticator issuance, help desk).
4. There is a desire to allow primary authenticators to be added and upgraded over time without changing the RP's implementation.
5. There are different environments to be supported, as federation protocols are network-based and allow for implementation on a wide variety of platforms and languages.
6. Potential users come from multiple communities, each with its own existing identity infrastructure. -->

Attribute を Federate すべきケース:

<!-- Federate attributes when: -->

1. ステークホルダーがサービスに Access するために, Pseudonymity が必須, 必要, 実現可能ないしは重要である.
2. サービスへの Access に部分的な Attribute リストのみが必要である.
3. サービスへの Access に少なくとも1つ以上の Attribute Reference のみが必要である.
4. 当該機関は必要な Attribute の権威ある情報元や発行元ではない.
5. Attribute は (Access 判断など) 一時的な利用のためだけに必要であり, 機関は当該データをローカルに永続化する必要はない.

<!-- 1. Pseudonymity is required, necessary, feasible, or important to stakeholders accessing the service.
2. Access to the service only requires a partial attribute list.
3. Access to the service only requires at least one attribute reference.
4. The agency is not the authoritative source or issuing source for required attributes.
5. Attributes are only required temporarily during use (such as to make an access decision), such that agency does not need to locally persist the data. -->
