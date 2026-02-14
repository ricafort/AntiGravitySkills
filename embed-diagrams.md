---
description: How to ensure Markdown documentation with Mermaid diagrams has static image fallbacks.
---

When creating major documentation artifacts (like `implementation_plan.md` or `architecture.md`) that contain Mermaid diagrams:

1.  **Create Assets Directory**: Always ensure a `project_docs/assets` (or relative `assets`) directory exists.
    ```powershell
    mkdir -p project_docs/assets
    ```

2.  **Ensure Readability (CRITICAL)**:
    -   Mermaid diagrams often render poorly in dark mode or static previews.
    -   **ALWAYS** include this theme directive at the top of your mermaid code:
        ```mermaid
        %%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffcc00', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff0f0'}}}%%
        graph TD;
            ...
        ```

3.  **Capture Visual**:
    -   **Preferred Method**: Use `npx @mermaid-js/mermaid-cli` if available.
        -   **MUST** use the `-b white` flag to force a white background.
        -   Example: `npx -y @mermaid-js/mermaid-cli -i input.mmd -o output.png -b white`
    -   **Fallback**: If `mermaid-cli` fails, ask the user to upload a screenshot.

4.  **Save & Embed**:
    -   Save the image as `project_docs/assets/<diagram_name>.png`.
    -   Embed it in the markdown file immediately after the mermaid code block:
        ```markdown
        ```mermaid
        %%{init: ... }%%
        graph TD;
            A-->B;
        ```
        ![Diagram Description](assets/diagram_name.png)
        ```

This ensures the documentation remains visual even in viewers that don't support dynamic Mermaid rendering (like standard GitHub previews or VS Code without plugins).
