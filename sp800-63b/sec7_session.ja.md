<a name="sec7"></a>

## 7 Session 管理

*This section is normative.*

一度 Authentication イベントが行われると、Subscriber が複数のインタラクションをまたぐアプリケーションを Authentication イベントを繰り返す必要なく継続して使用し続けられることはしばしば望まれる。 この要件は、 Authentication イベントがネットワーク経由で調整したいくつかのコンポーネントやパーティを巻き込む Federation シナリオ ( [SP 800-63C](sp800-63c.html) で説明される) に特に当てはまる。

この振る舞いを容易にするため、* Session * は、ある Authentication イベントへの応答によって開始されてもよい (MAY) 。そしてその Session はそれが終了されるときまで維持される。 Session は、活動がないときのタイムアウト、明示的なログアウトイベント、その他の理由など、様々な理由により終了されることがある (MAY) 。 Session は、 Reauthentication イベント ( [Section 7.2](#sessionreauthn) で説明される ) を通して維持されてもよい (MAY) 。ユーザーは、初回の Authentication イベントの一部または全部を繰り返すことによってセッションを再確立する。

Session 管理は 頻繁な Credential の提示よりも望ましい。 Credential を頻繁に提示することのユーザビリティの低さは、しばしばロック解除用 Credential のキャッシュなどの回避策に対するインセンティブを生み出し、 Authentication イベントの新鮮さを無効にする。

### 7.1 Session Bindings

Session は、 Subscriber が動作しているソフトウェア &mdash; ブラウザー、アプリケーション、オペレーティング システム (つまり Session Subject) &mdash; と、 Subscriber がアクセスする RP や CSP (つまり Session ホスト) の間に発生する。 Session シークレットは、 Subscriber のソフトウェアとアクセスされているサービスの間で共有されることとする (SHALL) 。 このシークレットは、Session の 2 つのエンドをバインドし、 Subscriber が経時的にサービスを使用し続けることを許可する。 シークレットは、Subscriber のソフトウェアによって直接提示されることとする (SHALL) 。または、シークレットの所有は暗号化メカニズムによって証明されることとする (SHALL) 。

Session のバインドに使用されるシークレットは、 Session ホストによって Authentication イベントへの直接の応答の中で生成されることとする (SHALL) 。 Session はその生成がトリガーされた Authentication イベントの AAL プロパティ 継承するべきである (SHOULD) 。 Session は Authentication イベントよりも低い AAL で考えられてもよい (MAY) が、 Authentication イベントよりも高い AAL では考えないこととする (SHALL NOT ) 。

Session のバインドに使用されるシークレットは :

1. インタラクションの間に、通常は Authentication の直後に Session ホストによって生成されることとする (SHALL) 。
2. 承認されたランダムビットジェネレーター [[SP 800-90Ar1]](#SP800-90Ar1) によって生成され、少なくとも64ビットの Entropy を含むこととする (SHALL) 。
3. Subscriber のログアウト時に、 Session Subject によって消去または無効にされることとする (SHALL) 。
4. ユーザーがログアウトするとき、またはシークレットの期限が切れたとみなされるとき、Subscriber エンドポイントから消去されるべきである (SHOULD) 。
5. Cross-site Scripting (XSS) 攻撃によるローカルストレージ暴露の可能性があるため、HTML5 ローカル ストレージなどの安全でない場所に配置されるべきでない (SHOULD NOT) 。
6. Authenticated Protected Channel を使用してデバイスから送信、または受信されることとする (SHALL) 。
7. [Section 4.1.4](#aal1reauth)、[4.2.4](#aal2reauth)、[4.3.4](#aal3reauth) の AAL にふさわしい時間の後は、タイムアウトすることとし、受け付けられてはならないこととする (SHALL) 。
8. ホストと Subscriber のエンドポイント間の安全でないコミュニケーションでは有効にしないこととする (SHALL NOT) 。 Authenticated Session は、Authentication の後、HTTPSからHTTPへというような安全でないトランスポートにフォールバックしないこととする (SHALL NOT) 。

URL か POST 内容は Session identifier を含むこととする (SHALL) 。Session identifier は、 Session の外側で行われたアクションが Protected Session に影響しないことを保証することを RP によって検証されることとする (SHALL) 。

経時的に Session を管理するためにはいくつかのメカニズムがある。 次のセクションでは、各例のテクノロジー特有の追加要件と考慮事項に沿って、それぞれの例を示す。 追加の有用なガイダンスとして、 OWASP *Session Management Cheat Sheet* [[OWASP-session]](#OWASP-session) がある。

#### 7.1.1. ブラウザー クッキー

ブラウザー クッキーは、サービスにアクセスする Subscriber のための Session の作成と追跡において、有力なメカニズムである。

クッキーは :

1. セキュアな (HTTPS) Session のみでアクセス可能なようにタグ付けされることとする (SHALL) 。
2. ホスト名とパスの最小で実際的なセットにアクセス可能であることとする (SHALL) 。
3. JavaScript (HttpOnly) からアクセス不可となるようにタグ付けされるべきである (SHOULD) 。
4. Sessionの有効な期間、またそのすぐ後に有効期限切れとなるようタグ付けされるべきである (SHOULD) 。 この要件はクッキーの蓄積を制限することを目的としているが、強制的な Session タイムアウトへの依存はしないこととする (SHALL NOT) 。

#### 7.1.2 Access Tokens

Access Token — OAuth に見られるような — はアプリケーションが Authentication イベントの後、Subscriber のために一連のサービスに Access することを許可するために使用される。 OAuth Access Token の存在は、他のシグナルがない場合、RP によって Subscriber の存在として解釈されないこととする (SHALL NOT) 。 OAuth Access Token 、および関連付けられた Refresh Token は、Authentication Session が終了され、Subscriber そのアプリケーションから去ったあとでも、有効であってもよい (MAY) 。

#### 7.1.3 デバイスの識別

Subscriber とサービス間の Session の制定には、安全なデバイス識別の他の方法 &mdash; 相互 TLS や Token Binding 、その他のメカニズムを含み、これに限らない &mdash; が使用されてもよい (MAY) 。

### 7.2 <a name="sessionreauthn">Reauthentication</a>

認証された Session の継続性は、Authentication の際に Verifier によって発行され、セッション中に任意に更新される Session シークレット の所有に基づくすることとする (SHALL) 。 Session の性質は以下を含むアプリケーションに依存する :

1. Web ブラウザー Session と "Session" クッキー
2. Session シークレットを保持するモバイルアプリケーションのインスタンス

Session シークレットは非永続的であることとする (SHALL) 。つまり、関連するアプリケーションのリスタートやホストデバイスのリブートを超えて残置されないこととする (SHALL NOT) 。

Session の 定期的な Reauthentication は、認証された Session において、Subscriber が継続して存在していること (すなわち Subscriber がログアウトせずに立ち去っていないこと) を確認するために実行されることとする (SHALL) 。

Session は、Session シークレット単独の提示に基づいて、セクション [4.1.3](#aal1reauth), [4.2.3](#aal2reauth) そして [4.3.3](#aal3reauth) (AALに応じる) のガイドラインを超えて拡張されないこととする (SHALL NOT) 。 Reauthentication のタイムリミットは、Session が 満了する前に、[表 7-1](#63bSec7-Table1)で指定された Authentication Factor を Subscriber に促すことで延長されることとする (SHALL) 。 

タイムアウトやその他のアクションによって Session が終了されたとき、ユーザーは再度の Authenticate によって新しい Session の確立を要求されることとする (SHALL) 。

<a name="63bSec7-Table1"></a>

<div class="text-center">
  <p>
    <strong>表 7-1 AAL Reauthentication 要件</strong>
  </p>
</div>

| AAL | 要件                                  |
| --- | ----------------------------------- |
| 1   | 任意の 1 つのファクターの提示                    |
| 2   | Memorized Secret または Biometrics の提示 |
| 3   | 全てのファクターの提示                         |

> ノート: AAL2では、Session シークレットは *something you have* であり、また追加の Authentication Factor が Session を継続するために要求されるため、 物理的な Authenticator でない、Memorized Secret または Biometrics が必須とされる。

#### 7.2.1 Federation または Assertion からの Reauthentication

CSP と RP を接続するために [SP 800-63C](sp800-63c.html) のセクション5で説明されている Federation プロトコルを使用するとき、Session 管理と Reauthentication は特別な考慮事項が適用される。 Federation プロトコルは CSP と RP の間の Authentication イベントを執り行うが、それらの間に Session を確立しない。 CSP と RP は、しばしば別々の Session 管理技術を採用しているので、これらのセッション間にはどんな相関も仮定しないこととする (SHALL NOT) 。 したがって、RP の Session が満了し RP が再認証を必要とするとき、CSP の Session が満了しておらず、ユーザーの Reauthentication なしに CSP でこの Session から新しい Assertion が生成される可能性は十分にある。

Federation プロトコルによる Reauthentication を必要とする RP は、— 可能な場合はプロトコル内で — CSPへの許容可能な最大の Authentication 経過時間を指定することとし (SHALL)、その期間内に Authentication が行われていない場合、CSP は Subscriber を Reauthentication することとする (SHALL) 。 CSP は、RP が、Assertion が Reauthentication に十分かを決定でき且つ次の Reauthentication イベントの時間を決定するために、 Authentication イベントの時間を RP へ伝えることとする (SHALL) 。