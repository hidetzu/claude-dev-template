# Spec + Roadmap Driven Development

⚠ **An exception, recorded in the top-level README §3.** ⚠ **It has run in one project, not two,
and that project is not public.** ⚠ **What travelled is the shape — the document set, the
Roadmap → Theme → Steering model, and the four commands. ⚠ The project's own documents stayed
behind.**

⚠ **It is not wired into the rest of this template.** ⚠ **The skills and rules at the top level
do not read `doc/` or `.steering/`, and nothing here reads them.** Adopting one does not adopt
the other.

---

## コンセプト

- Spec 駆動
- Roadmap 駆動
- Theme（Epic）ベース
- Steering による実装設計

## モデル

```
Roadmap → RoadmapItem → Theme → Steering
```

## なぜ必要か

- Spec 駆動だけでは時間軸が弱い
- Agile だけでは設計が弱い

## 解決

- Roadmap で時間軸
- Theme で機能
- Steering で実装

## ディレクトリ構造

```
doc/                              永続ドキュメント。「何を作るか」「どう作るか」
  product-requirements.md         スケルトン。プロダクト要求
  roadmap.md                      スケルトン。フェーズと Theme
  functional-design.md            ⚠ プロジェクトが書く。機能設計
  architecture.md                 ⚠ プロジェクトが書く。技術仕様
  repository-structure.md         ⚠ プロジェクトが書く。ディレクトリと役割
  glossary.md                     ⚠ プロジェクトが書く。ユビキタス言語
  development-guidelines.md       ⚠ プロジェクトが書く。開発フローと規約、ビルド・テストのコマンド
.steering/
  <YYYYMMDD>-<title>/             Theme ごとの作業単位。/new-theme が作る
    requirements.md               要求定義
    design.md                     設計
    tasklist.md                   タスクリスト
.claude/commands/
  new-theme.md                    Theme のステアリングを作る
  spec-review.md                  ステアリング 3 ファイルをレビューする
  impl-review.md                  実装をステアリングに照らしてレビューする
  doc-sync.md                     実装後に doc/ の更新要否を判定する
```

## 流れ

1. `doc/roadmap.md` に Theme を置く
2. `/new-theme <YYYYMMDD>-<title> <概要>` でステアリングを作る
3. `/spec-review .steering/<dir>/` で実装前にレビューする
4. 実装する
5. `/impl-review <branch>` で設計との整合を見る
6. `/doc-sync .steering/<dir>/` で永続ドキュメントを追従させる

## 使い方

`doc/` と `.claude/commands/` をプロジェクトにコピーし、`FILL IN` をすべて埋める。
⚠ **「プロジェクトが書く」とした 5 本は、ここには置いていない。** ⚠ **中身がプロジェクトにしか
書けないため。** コマンドはこの 5 本を読む前提なので、最初に見出しだけでも作っておく。
