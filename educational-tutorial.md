---
description: Generates a deep-dive educational programming tutorial based on the current project's code, architecture, and technology stack.
---

# Educational Tutorial Generator

This workflow analyzes your entire project to create a comprehensive **Educational Tutorial Document**.
Unlike a standard README, this document focuses on **teaching** the technologies, patterns, and architectural decisions used in your project, using your actual code as the learning material.

## Steps

1.  **Analyze Project Context**
    -   Scan the root directory to identify the **Technology Stack** (Language, Framework, Database, Tools).
    -   Read `AGENTS.md`, `README.md`, `package.json`, `requirements.txt`, `go.mod`, or equivalent dependency files.
    -   Identify the **Architectural Pattern** (e.g., MVC, Microservices, Event-Driven, Serverless).

2.  **Inject Educational Comments**
    -   **Deep Dive Analysis**: Identify complex logic or key architectural patterns in the source code.
    -   **Add Comments**: Modify the source files to add verbose, educational comments.
        -   Start comments with `TUTORIAL:` (or language equivalent).
        -   Explain *why* the code is written that way, not just *what* it does.
        -   Example (Python):
            ```python
            # TUTORIAL: We use a Decorator here to enforce RBAC (Role-Based Access Control)
            # without repeating the 'if user.role == ...' check in every route.
            @require_role('admin')
            ```

3.  **Generate Comprehensive Masterclass Document**
    -   Create a new file: `PROJECT_MASTERCLASS.md` (or a similar appropriate name).
    -   **Introduction**: Explain *what* the project is and *why* this specific stack was chosen.
    -   **Architecture Deep Dive**:
        -   Explain the high-level design.
        -   **Create a Mermaid Diagram** (C4 Context or Container diagram) showing how system parts interact.
        -   **Embed the Diagram**: Follow the `embed-diagrams` skill.
            -   **CRITICAL**: Use a white background for readability on all themes.
                -   If using `mermaid-cli`, adds flag `-b white`.
                -   Include theme directive in mermaid code: `%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffcc00', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff0f0'}}}%%`
            -   Save a static image to `project_docs/assets/<diagram_name>.png`.
            -   Embed it after the mermaid block: `![Description](assets/<diagram_name>.png)`.
    -   **Core Concepts & Best Practices**:
        -   Pick 3-5 key technical concepts used in the code (e.g., "Dependency Injection in FastAPI", "React Hooks for State Management", "Middleware Pattern in Express").
        -   Explain *why* these are best practices.
        -   Cite specific files and lines of code as examples.
    -   **Code Walkthrough**:
        -   Select the most critical/complex file (e.g., the main API entry point, the core business logic reducer).
        -   Provide a "literate programming" style breakdown, explaining blocks of code in plain English.
    -   **Data Flow**:
        -   **Create a Mermaid Sequence Diagram** showing a request/response cycle or a key data process.
        -   **Embed the Diagram**: (As above, with static fallback; remember `-b white`).
    -   **Source Code Deep Dive**:
        -   Direct the user to open source files (like `app.py`) where `TUTORIAL:` comments have been injected.

4.  **Generate Beginner's Pocket Guide (`tutorial.md`)**
    -   Create a second file: `tutorial.md`.
    -   **Style**: "Elemental", high-level, emoji-rich, simple analogies (e.g., "API is a waiter").
    -   **Content**:
        -   **Language Foundations**: Briefly explain the language (e.g., "Python is readable").
        -   **Key Concepts**: Simple explanations of 3-4 concepts (e.g., "Decorators are security guards").
        -   **Project Map**: A simple bulleted list of what each file does.
        -   **How to Run**: The absolute simplest command to start the app.
    -   **Goal**: A less intimidating, "Day 1" guide for absolute beginners to read *before* the Masterclass.

## Usage

Run this workflow in any project root to generate the customized masterclass document.

`@antigravity run educational-tutorial`
