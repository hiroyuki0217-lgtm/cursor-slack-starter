# Cursor 優先の技術作業ハンドオフ

実務は既存 Bot、**技術作業（調査・実装・テスト・PR）は Cursor / Cloud Agents** を基本にする。  
この文書は、mari と Grok Bot が Cursor を最大限使うための指示正本である。

既存の S01〜S05 固定本文、`mari-source-handoff`、C01 を含む既存 Skill、Routine、全 Bot 配布は変更しない。  
Bot への適用は、統括（mari）または本人が **個別に** Remember / 依頼文へ載せる。一斉配布はしない。

## 置き場（本人確定）

| 置き場 | 役割 | ここに置くもの | 置かないもの |
|--|--|--|--|
| **Obsidian** | 記録 | 判断理由、経緯、学び、失敗と改善、運用メモのログ | 納品物の正本、連絡の本文だけ |
| **Notion** | 成果物 | 完成した手順・テンプレ・納品ページ、参照できる成果 | 雑多な経緯ログ、連絡の往復そのもの |
| **Slack** | 連絡共有 | 依頼、メンション、進捗の短い共有、リンク渡し | 成果物の全文、長期の記録本文 |

このファイル（repo）は Cursor 受け側の技術正本。運用の**成果物**は Notion に置き、**記録**は Obsidian、**連絡**は Slack。

## Slack 運用（現状の制約）

`#home_top` などチャンネルで **自分の名義で返せるのは mari と Cursor だけ**。  
個人 Grok Bot はチャンネルスレッドから他 Bot へ渡せない。返信を同じスレッドに戻す公式経路は Team Bot 接続時のみ。Team Bot / 追加契約は、本人が課金・権限を承認するまで前提にしない。

### 誰がどこで動くか

| 場所 | 動かす相手 | やること |
|--|--|--|
| **Slack** | 本人・mari・Cursor | 連絡共有。実装は `@Cursor`。部署 Bot をスレッドに呼ばない |
| **Grok Bot アプリ / DM / グループ** | 各 Bot | 運用・定期・専門実務。Slack 名義での返信は期待しない |
| **Cloud Agents** | Cursor | 調査・実装・テスト・PR。Bot からも直接起動してよい |

### 流れ（これが基本）

1. **Slack に来た実装** → mari または本人が `@Cursor` → Cloud Agent がスレッドに要約・PR  
2. **Bot 側で実装が必要** → Bot は Slack を経由せず **Cloud Agents を直接起動** → run/PR URL を Bot チャットへ。Slack に出す必要があれば **mari が1行で共有**  
3. **Bot の作業結果をチームに見せる** → 成果物は Notion、連絡は Slack（mari 経由）。Bot 本人を Slack に立たせない  
4. **Cursor が Bot に仕事を振る** → Slack チャンネルからはしない。必要なら本人/mari が Bot アプリ側へ指示

### Slack でやらないこと

- 個人 Grok Bot を `@` して実装や中継を期待する  
- Cursor に「Slack から Alfred / try へ渡して同じスレッドに戻す」を頼む  
- Team Bot 未接続のまま「各 Bot が社員のように Slack 返信」する前提で設計する  

## 判定（15秒）

次のいずれかに当てはまる作業は、Bot 自身で長くやらず **すぐ Cursor へ渡す**。

- リポジトリのコードを読む・直す・足す
- ビルド・テスト・型チェック・lint
- PR / ブランチ / CI の作成・確認
- 実装の計画を固めてから Cloud Agents に投げる
- 「動くものを検証してから返す」が必要な開発作業

Bot に残すもの:

- 受付・方針・振り分け・要約
- 定期監視・定型オペ・画面運用（コード変更を伴わない）
- Cursor 起動後の進捗確認と、依頼元への短い報告

## mari 用（統括）

実装案件を受けたら、自分で実装せず Cursor に渡す。

```text
【振り分け】技術作業 → Cursor / Cloud Agents
【やること】目的・受け入れ条件・禁止事項を短く付けて @Cursor または Cloud Agents を起動
【あなた】判断と進捗要約だけ返す。コード本体は書かない
【Botへ】部署Botがコードに入りそうなら、この正本の「Bot用」を個別に思い出させ、Cursorへ渡させる
【触るな】S01〜S05、mari-source-handoff、C01、Routine、全Bot配布、課金・権限
```

Slack 最短例:

```text
@Cursor
目的: （1行）
受け入れ: （箇条書き）
制約: 既存Skill/Routine/Bot配布・課金・権限は触らない
PRまで進めて。進捗はスレッドに要約だけ。
```

## Bot 用（特にここを厚く）

コーディングが必要になった瞬間に、自分で粘らず Cloud Agents / `@Cursor` を使う。

```text
Remember（技術作業）:
- コード・テスト・PR・実装計画が必要なら、自分で長く書かず Cursor Cloud Agents へ直接委任する
- Slack チャンネルでは自分が名義返信できない前提。実装の Slack 共有が必要なら run/PR URL を mari または本人へ渡し、mari が Slack に1行出す
- 委任文には必ず含める: 目的 / 受け入れ条件 / 対象repoまたはリンク / 禁止（Skill固定文・Routine・Bot配布・課金・権限）
- 委任したら run URL または PR URL を待ち、依頼元へ要約だけ返す
- 同じタスクの既存 Cloud Agent run があれば新規起動せず接続する
- 運用・定期・画面だけの仕事は自分が続ける。実装が混ざったら実装分だけ Cursor へ切る
```

Bot が Cursor へ渡すときの文面:

```text
【Cloud Agent / @Cursor 依頼】
目的:
受け入れ条件:
- 
対象: repo / ブランチ / 関連リンク
やってよい: 調査、実装、テスト、PR
やるな: S01〜S05固定文、mari-source-handoff、C01、既存Skill/Routine変更、全Bot配布、課金・権限、Locked use
完了後: PR URL と要約を返す
```

## やってはいけない（勿体無い使い方）

- Bot がエディタや長いパッチで実装を完結させようとする
- mari が仕様議論のまま実装まで抱える
- Cursor に方針だけ聞いて、実装・テスト・PR を付けない
- チャンネルから個人 Grok Bot へ実装を中継して同じスレッド復帰を期待する（公式上、Team Bot 以外は不可）

## 公式の起動経路

- Slack: `@Cursor` で Cloud Agent 起動 — https://cursor.com/docs/integrations/slack
- Grok Bot → Cloud Agents 委任 — https://cursor.com/docs/grok-bot/teams
- Web: https://cursor.com/agents

## 未検証の扱い

この文書の存在は、全 Bot 適用済みでも、枠の削減実績でもない。  
適用した Bot・実委任の有無・削減量は、その都度区別して記録する。
