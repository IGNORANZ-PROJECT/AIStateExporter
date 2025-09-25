AIStateExporter

Unity Editor 専用の 制作状態エクスポートツール です。
シーン階層・コンポーネント・スクリプトのパスや GUID、依存関係、差分などをまとめ、AI にプロジェクトの状況を共有するのに最適なテキストを生成します。

⸻

✨ 主な機能

基本
	•	App / Build 情報
ProductName / Version / Unity バージョン / Platform / Scene / ColorSpace / RenderPipeline / ScriptingBackend
	•	Hierarchy 出力
階層ツリー（最大深度・ノード数指定）
Tag / Layer / Active 状態 / Prefab のアセットパス & GUID
	•	Components / Scripts
コンポーネント一覧
MonoBehaviour → スクリプトのアセットパス & GUID
	•	値チラ見（オプション）
int / float / bool / string / Vector 系の public フィールド/プロパティ
	•	Packages 要約
Packages/manifest.json の依存関係を一覧化

拡張
	•	差分エクスポート
前回出力との差分（+/-）を表示
	•	依存関係リスト
シーン内オブジェクトが参照しているアセット（Prefab, Material, ScriptableObject など）
	•	スクリプト規模/未使用チェック
	•	スクリプト数・総行数
	•	シーンや Prefab に存在しない未使用スクリプト一覧
	•	出力形式の拡張
	•	Markdown（標準）
	•	JSON（サマリ）
	•	CSV（オブジェクトとコンポーネント数）
	•	ZIP 保存（大規模出力対応）
	•	実行時スナップショット（RuntimeSnapshot.cs）
FPS / GCメモリ / GPU / CPU / Scene名 などを実行中にホットキー（F12）でコピー

⸻

📂 フォルダ構成

Assets/IGNORANZ PROJECT/AIStateExporter/
├─ Editor/
│  ├─ AIStateExporter.cs          // メインUI（EditorWindow）
│  ├─ AIStateExporter_Utils.cs    // 共通ユーティリティ
│  ├─ AIStateExporter_Diff.cs     // 差分エクスポート
│  ├─ AIStateExporter_Depend.cs   // 依存関係解析
│  ├─ AIStateExporter_Script.cs   // スクリプト規模/未使用チェック
│  └─ AIStateExporter_Formats.cs  // JSON/CSV/ZIP 出力
└─ Runtime/
   └─ RuntimeSnapshot.cs          // 実行時スナップショット


⸻

🚀 使い方

Editor エクスポート
	1.	Unity メニューから Tools > AI Export > Open Exporter を選択
	2.	欲しいセクションをチェック
	3.	Refresh でプレビュー → Copy でクリップボードコピー、Save でファイル保存

差分モード
	•	「Include Diff」を ON にすると、前回出力との差分（追加/削除）が出力されます

実行時スナップショット
	•	シーンに RuntimeSnapshot を配置
	•	プレイ中に F12 を押すとランタイム情報がコピーされます

⸻

📝 出力例

## APP / BUILD
Product: MyUnityGame
Version: 0.1.0
Unity: 2022.3.51f1
Platform: StandaloneWindows64
Scene: MainScene
Now: 2025-09-11 14:37:22
ColorSpace: Linear
RenderPipeline: UniversalRenderPipelineAsset

## HIERARCHY
- BoardRoot  [Active]  (Tag:Untagged, Layer:Default)
  Path: BoardRoot
  * Transform
  * BoardManager
    - script: Assets/Scripts/BoardManager.cs  8f3d...GUID
  * AudioSource
  - Pieces  [Active]  (Tag:Untagged, Layer:Default)
    Path: BoardRoot/Pieces
    * PieceBase
      - script: Assets/Scripts/PieceBase.cs  a12b...GUID
      - moveSpeed: 4.5
      - isEnemy: False

## DEPENDENCIES (references in scene)
- Assets/Materials/BoardMat.mat  1234abcd...

## SCRIPTS (stats / unused)
- Scripts: 145 files
- Total Lines: ~38,200
- Unused:
  - Assets/Scripts/Old/LegacyAI.cs


⸻

⚙️ 注意事項
	•	Editor 専用（ビルドには含まれません）
	•	値チラ見は軽量型のみ対応（Mesh, Texture, AudioClip の中身は非対象）
	•	大規模シーンでは Max Nodes や Hard Char Limit を調整してください
	•	社外共有時は必ず「Redact Paths / GUIDs」を ON にしてください

⸻

📜 ライセンス

MIT License
（ただしプロジェクト内の秘密情報は自己責任で取り扱ってください）