AIStateExporter

A Unity Editor-only export tool for project state.
It collects scene hierarchy, components, script asset paths & GUIDs, dependencies, diffs, and more — making it easy to share your Unity project state with AI tools.

⸻

✨ Features

Core
	•	App / Build Info
ProductName / Version / Unity Version / Platform / Scene / ColorSpace / RenderPipeline / ScriptingBackend
	•	Hierarchy Export
Scene hierarchy tree (depth & node limit)
Tag / Layer / Active state / Prefab asset path & GUID
	•	Components / Scripts
Component list
MonoBehaviour → script asset path & GUID
	•	Value Peek (optional)
Public fields/properties of int, float, bool, string, Vector types
	•	Packages Summary
Extract dependencies from Packages/manifest.json

Extended
	•	Diff Export
Show differences (+/-) compared to last export
	•	Dependency List
External assets referenced in the scene (Prefab, Material, ScriptableObject, etc.)
	•	Script Stats / Unused Check
	•	Number of scripts / total lines of code
	•	List unused scripts not referenced by scenes or prefabs
	•	Export Formats
	•	Markdown (default)
	•	JSON (summary)
	•	CSV (object/component counts)
	•	ZIP (large outputs)
	•	Runtime Snapshot (RuntimeSnapshot.cs)
FPS / GC memory / GPU / CPU / Scene name etc., copyable at runtime with hotkey (F12)

⸻

📂 Folder Structure

Assets/IGNORANZ PROJECT/AIStateExporter/
├─ Editor/
│  ├─ AIStateExporter.cs          // Main UI (EditorWindow)
│  ├─ AIStateExporter_Utils.cs    // Common utilities
│  ├─ AIStateExporter_Diff.cs     // Diff export
│  ├─ AIStateExporter_Depend.cs   // Dependency analysis
│  ├─ AIStateExporter_Script.cs   // Script stats / unused check
│  └─ AIStateExporter_Formats.cs  // JSON/CSV/ZIP export
└─ Runtime/
   └─ RuntimeSnapshot.cs          // Runtime snapshot


⸻

🚀 Usage

Editor Export
	1.	From Unity menu: Tools > AI Export > Open Exporter
	2.	Check sections you want to include
	3.	Refresh to preview → Copy to clipboard, Save to file

Diff Mode
	•	Enable Include Diff to see differences against the last export

Runtime Snapshot
	•	Place RuntimeSnapshot in your scene
	•	During Play Mode, press F12 to copy runtime stats

⸻

📝 Example Output

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

⚙️ Notes
	•	Editor-only (excluded from builds)
	•	Value peek only supports lightweight types (not Mesh/Texture/Audio data)
	•	For large scenes, adjust Max Nodes or Hard Char Limit
	•	When sharing externally, always enable Redact Paths / GUIDs

⸻

📜 License

MIT License
(But be mindful of sensitive project information before sharing exports)