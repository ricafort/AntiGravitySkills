When creating major documentation artifacts (like `implementation_plan.md` or `architecture.md`) that contain Mermaid diagrams:

1.  **Ensure Viewer Support (CRITICAL)**:
    -   The user must have a Mermaid viewer installed in VS Code to see the diagrams.
    -   **Run this command** to install the recommended extension:
    // turbo
    ```powershell
    code --install-extension bierner.markdown-mermaid
    ```
    -   **CRITICAL CONFLICT WARNING**: If diagrams still fail to render (e.g., "No diagram type detected"), check for and **UNINSTALL** the official Mermaid extension, as it effectively breaks the preview renderer in VS Code when used alongside other Markdown extensions.

2.  **Use Robust Syntax**:
    -   **DO NOT** use complex `%%{init: ...}%%` directives inside the markdown file, as they often break the preview parser.
    -   Use simple, standard syntax:
        ```mermaid
        graph TD
            A --> B
        ```
    -   Avoid leading newlines or whitespace before `graph` or `sequenceDiagram`.

3.  **Capture Visual (Optional but Recommended)**:
    -   **Preferred Method**: Use `npx @mermaid-js/mermaid-cli` if available to generate a PNG.
        -   Example: `npx -y @mermaid-js/mermaid-cli -i input.mmd -o output.png -b white`
    -   **Fallback**: If `mermaid-cli` fails, ask the user to upload a screenshot.

4.  **Save & Embed**:
    -   Save the image as `project_docs/assets/<diagram_name>.png`.
    -   Embed it in the markdown file immediately after the mermaid code block:
        ```markdown
        ```mermaid
        graph TD
            A-->B
        ```
        ![Diagram Description](assets/diagram_name.png)
        ```

This ensures the documentation remains visual even in viewers that don't support dynamic Mermaid rendering (like standard GitHub previews or VS Code without plugins).
