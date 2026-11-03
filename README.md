# CardiPal

A secure, offline-first desktop companion for structured AI prompt engineering.

## Overview

CardiPal (internally referenced as PromptPal) is a lightweight, privacy-focused Windows desktop utility designed to bridge the gap between raw student drafting and professional AI prompt engineering. Developed in alignment with Mapúa University's co-intelligence framework, it serves as an educational scaffold rather than a basic automation tool.

The application operates entirely offline, providing students and interns with a structured template library, dynamic variable injection, and educational tooltips known as **Coach's Notes**. Through its compact, non-intrusive desktop interface, CardiPal allows users to build and refine prompts alongside their primary tasks while keeping prompt generation and data storage local.

## Visuals and Preview

<!-- Replace the placeholder image paths with actual application screenshots. -->

![Main Capture Screen](docs/images/main-capture-screen.png)
<img width="1725" height="771" alt="image" src="https://github.com/user-attachments/assets/f0b0016b-c32a-4047-bedf-c47ada4bd652" />


*Main Capture Screen – The freeform editor where users can quickly capture rough drafts, code snippets, and notes.*

![Template Library](docs/images/template-library.png)

*Template Library – Categorized templates featuring Coach's Notes, educational guidance, and dynamic variable requirements.*

![Companion Widget View](docs/images/companion-widget.png)

*Companion Widget – CardiPal operating within its fixed 445 × 310 px desktop window.*

## Key Features

- **100% Offline Autonomy:** No cloud dependencies, external API calls, or telemetry. Prompt generation and data storage are handled locally.
- **Template Library and Frameworks:** Categorized institutional templates for writing, analysis, and coding, complete with educational strategy notes.
- **Dynamic Composition Engine:** Automatically injects user-defined variables (e.g., `{{user_input}}`) into selected template structures to generate refined prompts.
- **Non-Intrusive Desktop Interface:** Uses strict CSS Flexbox constraints and a fixed 445 × 310 px window to function as a compact desktop companion.
- **Instant Clipboard Export:** Sends compiled prompts directly to the Windows operating system clipboard for use in external AI tools.
- **Local Data Persistence:** Uses SQLite with Write-Ahead Logging (WAL) and automatic background saving to maintain drafts, workflow states, and user preferences.

## How It Works

CardiPal follows a straightforward four-step workflow:

1. **Input:** Enter a rough draft in the freeform editor or select a structured framework from the Template Library.
2. **Composition:** The application processes the input, validates required variables, and combines the provided information with the selected template.
3. **Export:** Copy the completed prompt directly to the system clipboard and paste it into the preferred AI tool.
4. **Persistence:** CardiPal automatically saves the active draft, workflow state, and user preferences to its local SQLite database.

## Technology Stack

CardiPal is built using a modern, performance-oriented desktop application stack.

| Component | Technology |
|---|---|
| Desktop Framework | Tauri |
| Backend and Systems Logic | Rust |
| Frontend | React, TypeScript |
| Build Tool | Vite |
| Database | SQLite (WAL Mode) |
| Package Manager | npm |
| Styling | CSS |

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
    ├── package-lock.json
    ├── tsconfig.json
    ├── tsconfig.node.json
    ├── vite.config.ts
    ├── README.md
    │
    ├── .vscode/
    │   └── extensions.json
    │
    ├── public/
    │   ├── launcher.png
    │   ├── tauri.svg
    │   └── vite.svg
    │
    ├── src/
    │   ├── App.css
    │   ├── App.tsx
    │   ├── Companion.tsx
    │   ├── main.tsx
    │   ├── types.ts
    │   ├── vite-env.d.ts
    │   │
    │   ├── assets/
    │   │   └── react.svg
    │   │
    │   ├── components/
    │   │   ├── ConfirmModal.tsx
    │   │   ├── PromptEditor.tsx
    │   │   ├── TemplateBuilder.tsx
    │   │   └── TemplateLibrary.tsx
    │   │
    │   ├── data/
    │   │   └── templates.ts
    │   │
    │   ├── hooks/
    │   │   └── useSessionLock.ts
    │   │
    │   └── utils/
    │       ├── builder.ts
    │       ├── builder.test.ts
    │       ├── session.test.ts
    │       ├── shortcut.ts
    │       ├── store.ts
    │       └── window.ts
    │
    └── src-tauri/
        ├── .gitignore
        ├── build.rs
        ├── Cargo.lock
        ├── Cargo.toml
        ├── tauri.conf.json
        │
        ├── capabilities/
        │   ├── companion.json
        │   ├── default.json
        │   └── storage.json
        │
        ├── icons/
        │   ├── 32x32.png
        │   ├── 128x128.png
        │   ├── 128x128@2x.png
        │   ├── Square30x30Logo.png
        │   ├── Square44x44Logo.png
        │   ├── Square71x71Logo.png
        │   ├── Square89x89Logo.png
        │   ├── Square107x107Logo.png
        │   ├── Square142x142Logo.png
        │   ├── Square150x150Logo.png
        │   ├── Square284x284Logo.png
        │   ├── Square310x310Logo.png
        │   ├── StoreLogo.png
        │   ├── icon.icns
        │   ├── icon.ico
        │   └── icon.png
        │
        └── src/
            ├── capture.rs
            ├── lib.rs
            ├── main.rs
            └── store.rs
```

### Important Directories and Files

| Path | Description |
|---|---|
| `src/components/` | Reusable React components for prompt editing, template management, and confirmation dialogs. |
| `src/data/templates.ts` | Built-in institutional templates and prompt frameworks. |
| `src/utils/builder.ts` | Core logic for compiling templates and injecting dynamic variables. |
| `src/utils/store.ts` | Frontend interface for communicating with the local persistence system. |
| `src/utils/window.ts` | Window dimension and layout constraint management. |
| `src-tauri/src/capture.rs` | Backend logic for clipboard operations. |
| `src-tauri/src/store.rs` | SQLite database operations and local persistence. |
| `src-tauri/src/main.rs` | Tauri application initialization and backend commands. |
| `src-tauri/tauri.conf.json` | Desktop application configuration and window settings. |
| `src-tauri/capabilities/` | Tauri permissions and security capabilities. |

## Getting Started

### Prerequisites

To build and run CardiPal from source, ensure that your development environment has the following:

| Requirement | Description |
|---|---|
| Operating System | Windows 10 or Windows 11 |
| Node.js | Version 16 or higher |
| npm | Node.js package manager |
| Rust | Install through [rustup](https://rustup.rs/), including Cargo |
| Visual Studio Build Tools | Visual Studio 2022 with the Desktop development with C++ workload |

**Note:** Additional Tauri-specific dependencies may be required depending on your development environment.

### Installation and Setup

#### 1. Clone the Repository

Open your terminal or command prompt and execute:

```bash
git clone https://github.com/yourusername/cardipal.git
cd cardipal
```

Replace the repository URL with the actual GitHub repository address.

#### 2. Install Dependencies

Install the frontend dependencies using npm:

```bash
npm install
```

#### 3. Run in Development Mode

Start CardiPal using:

```bash
npm run tauri dev
```

This command launches the Vite development server and compiles the Rust backend. Once compilation is complete, the CardiPal desktop window should open automatically.

#### 4. Build for Production

To generate the production application, execute:

```bash
npm run tauri build
```

The resulting Windows application bundles and installer will be generated in the Tauri build output directory, typically under:

```text
src-tauri/target/release/
```

The exact installer location depends on the configured Tauri bundling targets.

## How to Use

### 1. Launch CardiPal

Open CardiPal through its desktop shortcut or executable. The application launches in its fixed 445 × 310 px window.

### 2. Draft or Select a Template

- **Freeform Editor:** Type or paste rough notes, ideas, code snippets, or other content into the Home screen.
- **Template Library:** Browse the available frameworks and select one that matches your task.

### 3. Review Coach's Notes

Hover over the available templates to view their Coach's Notes. These provide educational guidance to help users understand the purpose and appropriate application of each framework.

### 4. Fill in Required Variables

When using a template, provide the required information through the corresponding dynamic input fields.

For example:

```text
{{user_input}}
```

CardiPal uses these values to complete the selected prompt structure.

### 5. Copy the Generated Prompt

Click the copy action to compile the prompt and send the completed text to the system clipboard.

### 6. Paste into Your Preferred AI Tool

Open your preferred browser-based AI platform and paste the generated prompt into its input field.

**Automatic Saving:** CardiPal is designed to save drafts and interface preferences in the background. Manual saving should not be necessary during normal operation.

## Configuration

CardiPal is designed to work out of the box with minimal end-user configuration.

### Database

The local SQLite database (`promptpal.sqlite`) is automatically generated and managed by the application's persistence system upon first launch.

The database uses SQLite Write-Ahead Logging (WAL) to support local database operations.

### User Preferences

Application preferences, including supported interface settings such as Light and Dark themes, are stored locally and restored during subsequent sessions.

### Data Privacy

CardiPal follows an offline-first architecture:

- Prompt composition and template processing happen locally.
- Application data is stored in the local SQLite database.
- No external AI API is required for prompt generation.
- Users independently choose which external AI platform receives their copied prompts.

**Important:** Although CardiPal does not require a cloud service for its core functionality, users should still review the privacy policies of any external AI platform to which they paste their prompts.

## Troubleshooting

### Application Layout Overlaps or Scrolls Horizontally

CardiPal relies on strict Flexbox constraints to maintain its compact interface.

Check that the original CSS layout rules have not been modified, particularly:

- `flex-shrink: 0`
- `overflow-y: auto`
- Fixed container dimensions and layout boundaries

Forcefully resizing the application window through external operating system tools may cause unexpected layout behavior.

### Data Does Not Save After Closing

CardiPal uses SQLite WAL mode and local persistence mechanisms.

If data does not appear after restarting:

1. Verify that the application has read/write permissions for its local database directory.
2. Ensure that the application is not being terminated unexpectedly during a save operation.
3. Check for database access or permission errors.
4. Restart the application and verify whether the saved state is restored.

### Tauri Build Fails on Windows

If the application fails during Rust compilation:

1. Open the Visual Studio Installer.
2. Verify that Visual Studio 2022 Build Tools are installed.
3. Ensure that the **Desktop development with C++** workload is selected.
4. Verify that Rust and Cargo are correctly installed.
5. Retry the development or production build.

## Limitations and Future Improvements

### Current Limitations

- **Operating System:** CardiPal is currently designed and tested for Windows 10 and Windows 11. macOS and Linux are not officially supported.
- **Fixed Window Dimensions:** The 445 × 310 px window dimensions are intentionally maintained to preserve the compact companion widget experience.
- **External AI Processing:** CardiPal focuses on prompt composition and organization. AI-generated responses must be obtained through an external AI platform.

### Future Improvements

- **Database Migrations:** Introduce structured database migration mechanisms to support future schema updates while preserving existing user data.
- **Template Expansion:** Expand the institutional template library to accommodate additional academic, technical, and professional workflows.
- **Educational Enhancements:** Improve Coach's Notes and educational guidance to help users develop better prompt engineering practices.

## Project Context

CardiPal was developed in alignment with Mapúa University's co-intelligence framework, emphasizing responsible AI use, structured problem-solving, and improved AI literacy.

Rather than replacing the user's critical thinking, CardiPal encourages users to organize their thoughts, communicate their objectives clearly, and develop more effective interactions with AI systems.

The application serves as a practical desktop companion for students and interns who want to improve how they formulate, structure, and use AI prompts.

---

**CardiPal** – Structured Thinking. Better Prompts. Smarter AI Interaction.
