# CardiPal

A secure, offline desktop companion for structured AI prompt engineering.

## Overview

CardiPal is a lightweight, privacy-focused Windows desktop utility designed to bridge the gap between raw student drafting and professional AI prompt engineering. Developed in alignment with Mapúa University's co-intelligence framework, it serves as an educational scaffold rather than a basic automation tool.

The application operates entirely offline, providing students and interns with a structured template library, dynamic variable injection, and educational tooltips known as Coach's Notes. Through its adaptable, non-intrusive desktop interface, CardiPal allows users to build and refine prompts alongside their primary tasks while keeping prompt generation and data storage local.

## Visuals and Preview

<!-- Replace the placeholder image paths with actual application screenshots. -->

**Main Capture Screen**  
*The freeform editor where users can quickly capture rough drafts, code snippets, and notes.*
<p align="center">
  <img src="docs/images/capture_1.png" width="48%" alt="Capture Screen View 1">
  <img src="docs/images/capture_2.png" width="48%" alt="Capture Screen View 2">
</p>

**Template Library**  
*Categorized templates featuring Coach's Notes, educational guidance, and dynamic variable requirements.*
<p align="center">
  <img src="docs/images/library_1.png" width="48%" alt="Template Library View 1">
  <img src="docs/images/library_2.png" width="48%" alt="Template Library View 2">
</p>

**Companion Widget & Full Screen**  
*CardiPal operating as a compact desktop companion, alongside its expanded full-screen mode.*
<p align="center">
  <img src="docs/images/widget_1.png" width="48%" alt="Compact Widget View">
  <img src="docs/images/fullscreen_2.png" width="48%" alt="Full Screen View">
</p>

## Key Features

- **100% Offline Autonomy:** No cloud dependencies, external API calls, or telemetry. Prompt generation and data storage are handled locally.
- **Template Library and Frameworks:** Categorized institutional templates for writing, analysis, and coding, complete with educational strategy notes.
- **Dynamic Composition Engine:** Automatically injects user-defined variables into selected template structures to generate refined prompts.
- **Adaptable Desktop Interface:** Functions beautifully as a compact desktop companion, but is fully resizable based on user preference and snaps to full screen when dragged to the top of the monitor.
- **Instant Clipboard Export:** Sends compiled prompts directly to the Windows operating system clipboard for use in external AI tools.
- **Local Data Persistence:** Uses SQLite with Write-Ahead Logging (WAL) and automatic background saving to maintain drafts, workflow states, and user preferences.

## How It Works

CardiPal follows a straightforward four-step workflow:

1. **Input:** Enter a rough draft in the freeform editor or select a structured framework from the Template Library.
2. **Composition:** The application processes the input, validates required variables, and automatically combines your original text with the selected template.
3. **Export:** Copy the completed prompt directly to the system clipboard and paste it into the preferred AI tool.
4. **Persistence:** CardiPal automatically saves the active draft, workflow state, and user preferences to its local SQLite database.

## Technology Stack

CardiPal is built using a modern, performance-oriented desktop application stack.

| Component | Technology |
| :--- | :--- |
| **Desktop Framework** | Tauri |
| **Backend and Systems Logic** | Rust |
| **Frontend** | React, TypeScript |
| **Build Tool** | Vite |
| **Database** | SQLite (WAL Mode) |
| **Package Manager** | npm |
| **Styling** | CSS |

## Project Structure

The following tree represents the intended workspace and application organization.

```text
PromptPalWorkspace/
├── README.md
├── package.json
├── package-lock.json
├── promptPal.cmd
└── cardipal/
    ├── .gitignore
    ├── index.html
    ├── package.json
    ├── tsconfig.json
    ├── vite.config.ts
    ├── README.md
    ├── .vscode/
    │   └── extensions.json
    ├── public/
    │   ├── launcher.png
    │   └── tauri.svg
    ├── src/
    │   ├── App.css
    │   ├── App.tsx
    │   ├── Companion.tsx
    │   ├── main.tsx
    │   ├── types.ts
    │   ├── components/
    │   │   ├── ConfirmModal.tsx
    │   │   ├── PromptEditor.tsx
    │   │   ├── TemplateBuilder.tsx
    │   │   └── TemplateLibrary.tsx
    │   ├── data/
    │   │   └── templates.ts
    │   ├── hooks/
    │   │   └── useSessionLock.ts
    │   └── utils/
    │       ├── builder.ts
    │       ├── shortcut.ts
    │       ├── store.ts
    │       └── window.ts
    └── src-tauri/
        ├── build.rs
        ├── Cargo.toml
        ├── tauri.conf.json
        ├── capabilities/
        ├── icons/
        └── src/
            ├── capture.rs
            ├── lib.rs
            ├── main.rs
            └── store.rs
```

### Important Directories and Files

| Path | Description |
| :--- | :--- |
| `src/components/` | Reusable React components for prompt editing, template management, and confirmation dialogs. |
| `src/data/templates.ts` | Built-in institutional templates and prompt frameworks. |
| `src/utils/builder.ts` | Core logic for compiling templates and injecting dynamic variables. |
| `src/utils/store.ts` | Frontend interface for communicating with the local persistence system. |
| `src-tauri/src/store.rs` | SQLite database operations and local persistence. |
| `src-tauri/tauri.conf.json` | Desktop application configuration and window settings. |

## Getting Started

### Prerequisites

To build and run CardiPal from source, ensure that your development environment has the following:

| Requirement | Description |
| :--- | :--- |
| **Operating System** | Windows 10 or Windows 11 |
| **Node.js** | Version 16 or higher |
| **npm** | Node.js package manager |
| **Rust** | Install through rustup, including Cargo |
| **Visual Studio Build Tools** | Visual Studio 2022 with the Desktop development with C++ workload |

*Note: Additional Tauri-specific dependencies may be required depending on your development environment.*

### Installation and Setup

**1. Clone the Repository**

Open your terminal or command prompt and execute:
```bash
git clone https://github.com/Rodgerss111/cardi-pal.git
cd cardipal
```

**2. Install Dependencies**

Install the frontend dependencies using npm:
```bash
npm install
```

**3. Run in Development Mode**

Start CardiPal using:
```bash
npm run tauri dev
```
This command launches the Vite development server and compiles the Rust backend. Once compilation is complete, the CardiPal desktop window should open automatically.

**4. Build for Production**

To generate the production application, execute:
```bash
npm run tauri build
```
The resulting Windows application bundles and installer will be generated in the Tauri build output directory, typically under `src-tauri/target/release/`.

## How to Use

**1. Launch CardiPal & Shortcuts**

Open CardiPal through its desktop shortcut, or by clicking the cardinal bird icon in your Windows system tray. You can also quickly summon the app using the configured global keyboard shortcut `Ctrl + Shift + Space` to show the app 'Esc' to hide. The application launches in a compact companion size by default, but you can freely resize it or drag it to the top of your screen to snap it into full-screen mode.

**2. Draft or Select a Template**

- **Freeform Editor:** Type or paste rough notes, ideas, code snippets, or other content into the Home screen.
- **Template Library:** Browse the available frameworks and select one that matches your task.

<p align="center">
  <img src="https://github.com/user-attachments/assets/1447fce0-094a-4f24-8830-cc14c529cba1" width="48%" >
</p>

**3. Review Coach's Notes**

Hover over the available templates to view their Coach's Notes. These provide educational guidance to help users understand the purpose and appropriate application of each framework.
<p align="center">
  <img src="https://github.com/user-attachments/assets/bbe20a79-74b8-4e6e-8df2-5ae703b8e247" width="48%" >
</p>

**4. Automatic Variable Injection**

When using a template, ensure that the placeholder `{{user_input}}` remains in the task section of the template. You do not need to manually replace this text. CardiPal's engine will automatically detect `{{user_input}}` and replace it with your original draft or prompt from the Home screen.
<p align="center">
  <img src="https://github.com/user-attachments/assets/31411e80-7106-48dc-8c2c-d31085fd0808" width="48%" >
</p>
**5. Copy the Generated Prompt**

Click the copy action to compile the prompt and send the completed text to the system clipboard.

**6. Paste into Your Preferred AI Tool**

Open your preferred browser-based AI platform and paste the generated prompt into its input field.
<p align="center">
  <img src="https://github.com/user-attachments/assets/49626330-70d9-47ad-899b-f439a0294570" width="48%" height="327" >
</p>

*Automatic Saving: CardiPal is designed to save drafts and interface preferences in the background. Manual saving should not be necessary during normal operation.*

## Configuration

CardiPal is designed to work out of the box with minimal end-user configuration.

- **Database:** The local SQLite database (`promptpal.sqlite`) is automatically generated and managed by the application's persistence system upon first launch. It uses SQLite Write-Ahead Logging (WAL) to ensure high-performance local database operations.
- **User Preferences:** Application preferences, including supported interface settings such as Light and Dark themes, are stored locally and restored during subsequent sessions.

## Data Privacy

CardiPal follows an offline-first architecture:

- Prompt composition and template processing happen locally.
- Application data is stored in the local SQLite database.
- No external AI API is required for prompt generation.
- Users independently choose which external AI platform receives their copied prompts.

*Important: Although CardiPal does not require a cloud service for its core functionality, users should still review the privacy policies of any external AI platform to which they paste their prompts.*

## Troubleshooting

**Application Layout Issues**

CardiPal relies on CSS Flexbox to maintain its interface. While it is fully resizable, if you experience layout overlapping:

- Check that the original CSS layout rules (such as `flex-shrink: 0` and `overflow-y: auto`) have not been modified in the source code.

**Data Does Not Save After Closing**

CardiPal uses SQLite WAL mode and local persistence mechanisms. If data does not appear after restarting:

1. Verify that the application has read/write permissions for its local database directory.
2. Ensure that the application is not being terminated unexpectedly via task manager during a save operation.
3. Restart the application and verify whether the saved state is restored.

**Tauri Build Fails on Windows**

If the application fails during Rust compilation:

1. Open the Visual Studio Installer.
2. Verify that Visual Studio 2022 Build Tools are installed.
3. Ensure that the Desktop development with C++ workload is selected.
4. Verify that Rust and Cargo are correctly installed.

## Limitations and Future Improvements

**Current Limitations**

- **Operating System:** CardiPal is currently designed and tested for Windows 10 and Windows 11. macOS and Linux are not officially supported.
- **External AI Processing:** CardiPal focuses on prompt composition and organization. AI-generated responses must be obtained through an external AI platform.

**Future Improvements**

- **Database Migrations:** Introduce structured database migration mechanisms to support future schema updates while preserving existing user data.
- **Template Expansion:** Expand the institutional template library to accommodate additional academic, technical, and professional workflows.
- **Educational Enhancements:** Improve Coach's Notes and educational guidance to help users develop better prompt engineering practices.

## Project Context

CardiPal was developed in alignment with Mapúa University's co-intelligence framework, emphasizing responsible AI use, structured problem-solving, and improved AI literacy.

Rather than replacing the user's critical thinking, CardiPal encourages users to organize their thoughts, communicate their objectives clearly, and develop more effective interactions with AI systems. The application serves as a practical desktop companion for students and interns who want to improve how they formulate, structure, and use AI prompts.

---
*CardiPal – Structured Thinking. Better Prompts. Smarter AI Interaction.*
