# ゲーム仕様書

記入者：  上田大正
記入日：  9/15
対象バージョン：  

---

## 1. ゲーム概要

### 1.1 ゲームの目的

敵を倒して素材を集め、「爆弾を作り壁を破壊する」というミッションを達成したのち、脱出地点へ到達する


### 1.2 クリア条件

壁破壊、脱出というミッションを達成する


### 1.3 ゲームオーバー条件

PlayerのHPが０になる。


## 2. 画面遷移

### 2.1 シーン一覧

| シーン | 役割 | 遷移先 | 遷移条件 |
|---|---|---|---|
| TitleScene | タイトル画面 | GameScene / Exit| Enter | A  / Esc | B |
| GameScene | ゲーム画面 | ResultScene | MissionCleared時 / GameOver時 |
| ResultScene | 結果画面 | GameScene / TitleScene | Enter | A  / Esc | B |

### 2.2 Restart時の生成・破棄

 Player、Enemy座標/HP
 Inventory
 WorldItem
 Bomb
 MissionState
 BreakableWall
 経過時間
 撃破数



## 3. 操作仕様

| 操作 | キーボード | コントローラー | ゲーム内の効果 |
|---|---|---|---|
| 移動 | wasd/矢印キー | 左スティック | 移動 |
| 攻撃 | Z | A | 前方に攻撃 |
| 回避 | X | B | 高速移動、無敵 |
| インタラクト | E | Y | Missionの進行 |
| Gadget使用 | C | R | Bombの設置 |
| 工作画面 | Q | L | 工作画面を開く |
| ポーズ | Esc | start | ポーズ画面を開く |

## 4. ゲームプレイループ

開始からResultまでを、処理の条件を含めて記入してください。

1. TitleSceneを開き、Startをする
2. GameSceneが生成され、PlayerとEnemyが配置
3. 攻撃/Zで敵を倒す
4. 敵がいた位置にScrapが落ちる
5. Scrapを２個使い、CraftMenuからBombを生成
6. BombをBreakableWallに設置し爆破させる
7. MissionTargetでInteract/EしてMissionStateを進める
8. 出口へ移動しInterectしてMissionClear

## 5. Player仕様

### 5.1 状態一覧

| 状態 | 開始条件 | 終了条件 | 状態中の挙動 |
|---|---|---|---|
| Idle | 入力がない | 入力が入る | 停止 |
| Move | 移動入力が入る | 移動を停止、攻撃回避 | MoveSpeedをもとに移動 |
| Attack | Z/Aが押される/ActionTimerの数値が0 | 0.18f経過 | 前方に攻撃 |
| Dodge | X/Bが押される/ActionTimerの数値が0 | 0.22f経過 | DodgeSpeedをもとに移動、0.3f無敵 |
| Damage | 無敵がない、攻撃を受ける |  | PlayerHP減少 |
| Dead | HPが0になる | ゲーム終了 | GameOver |

### 5.2 攻撃判定

Player前方半径28fの円
Enemyへ１ダメージ


### 5.3 被ダメージと無敵時間

Enemy接触時1ダメージ
Dodge時0.3f、ダメージを受けて1f間無敵


## 6. Enemy／EnemyAI仕様

### 6.1 視覚判定の順序

1. 
2. 
3. 

### 6.2 警戒状態

| 状態 | Awareness条件 | 移動先 | 表示色 |
|---|---|---|---|
| Patrol |  |  |  |
| Suspicious |  |  |  |
| Alert |  |  |  |
| Chase |  |  |  |

### 6.3 AI更新頻度と遠距離時の処理

（ここに記入）


## 7. Item／Inventory／Craft仕様

### 7.1 WorldItemとInventoryの違い

（ここに記入）


### 7.2 Bombレシピ

| 必要素材 | 必要数 | 完成物 | 完成数 |
|---|---:|---|---:|
|  |  |  |  |

### 7.3 工作失敗時の挙動

（ここに記入）


## 8. Bomb／WorldEffect仕様

| 項目 | 値または挙動 |
|---|---|
| Fuse |  |
| Explosion radius |  |
| Damage |  |
| Enemyへの効果 |  |
| BreakableWallへの効果 |  |

## 9. Mission仕様

| MissionState | 進行条件 | 次の状態 |
|---|---|---|
| ReachTarget |  |  |
| ReachExtraction |  |  |
| Cleared |  |  |

## 10. 更新順序

`Gameplay::UpdatePlaying`を基準に記入してください。

1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 

## 11. 生成と削除

### 11.1 フレーム中に要求だけを記録する対象

（ここに記入）


### 11.2 フレーム末尾に確定する理由

（ここに記入）


## 12. クラス責務・所有関係

| クラス | 主な責務 | 所有する対象 | 所有しない連携対象 |
|---|---|---|---|
| GameApplication |  |  |  |
| SceneManager |  |  |  |
| GameScene |  |  |  |
| Gameplay |  |  |  |
| EnemyManager |  |  |  |
| ItemManager |  |  |  |
| CraftSystem |  |  |  |
| CollisionSystem |  |  |  |
| Mission |  |  |  |

## 13. UIデータフロー

（Gameplay、HudViewModel、GameHudの関係を記入）


## 14. デバッグ表示

| 表示項目 | 意味 | 何の確認に使うか |
|---|---|---|
| Enemy count |  |  |
| Updated enemies |  |  |
| Collision candidates |  |  |

## 15. 不明点・確認事項

1. 
2. 
3. 

## 16. 問題点と改善案

| 優先度 | 現在の問題 | 改善案 | 影響範囲 |
|---|---|---|---|
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
