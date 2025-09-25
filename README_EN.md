# AIStateExporter

A **Unity Editor-only export tool** for development state.  
It generates text summaries of scene hierarchy, components, script paths & GUIDs, dependencies, and diffs — making it ideal for sharing the state of your project with AI assistants.

---

### ✨ Features

#### Basic
- **App / Build Info**  
  ProductName / Version / Unity Version / Platform / Scene / ColorSpace / RenderPipeline / ScriptingBackend
- **Hierarchy Export**  
  Hierarchy tree (max depth / node limit) with Tag / Layer / Active state / Prefab asset path & GUID
- **Components / Scripts**  
  Component list, with MonoBehaviour → script asset path & GUID
- **Field Preview (optional)**  
  int / float / bool / string / Vector public fields & properties
- **Package Summary**  
  Summarizes dependencies from `Packages/manifest.json`

#### Extended
- **Diff Export**: show added/removed differences compared to the last export  
- **Dependency List**: assets referenced in the scene (Prefab, Material, ScriptableObject, etc.)  
- **Script Stats / Unused Check**  
  - Total script count & line count  
  - Unused scripts not referenced in scenes or prefabs  
- **Multiple Output Formats**  
  - Markdown (default)  
  - JSON (summary)  
  - CSV (object & component counts)  
  - ZIP (for large output)  
- **Runtime Snapshot (RuntimeSnapshot.cs)**  
  Capture FPS / GC memory / GPU / CPU / Scene name while running, copied via hotkey (**F12**)  

---

### 📂 Folder Structure

```plaintext
Assets/
└─ IGNORANZ PROJECT/
   └─ AIStateExporter/
      ├─ Editor/
      │  ├─ AIStateExporter.cs          // Main UI (EditorWindow)
      │  ├─ AIStateExporter_Utils.cs    // Common utilities
      │  ├─ AIStateExporter_Diff.cs     // Diff export
      │  ├─ AIStateExporter_Depend.cs   // Dependency analysis
      │  ├─ AIStateExporter_Script.cs   // Script stats & unused check
      │  └─ AIStateExporter_Formats.cs  // JSON/CSV/ZIP output
      └─ Runtime/
         └─ RuntimeSnapshot.cs          // Runtime snapshot
```

---

### 🚀 Usage

#### Editor Export
1. Open from Unity menu **Tools > AI Export > Open Exporter**  
2. Check the sections you want  
3. **Refresh** for preview → **Copy** to clipboard, or **Save** to file  

#### Diff Mode
- Enable **Include Diff** to show differences (+/-) compared to the last export  

#### Runtime Snapshot
- Place `RuntimeSnapshot` in the scene  
- Press **F12** while running to copy runtime info  

---

### 📝 Example Output

```plaintext
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
```

---

### ⚙️ Notes
- **Editor only** (not included in build)  
- Field preview supports only lightweight types (Mesh, Texture, AudioClip contents are excluded)  
- For large scenes, adjust **Max Nodes** or **Hard Char Limit**  
- When sharing externally, always enable **Redact Paths / GUIDs**  

---

### 📜 License

MIT License  
(Handle confidential project information responsibly.)
