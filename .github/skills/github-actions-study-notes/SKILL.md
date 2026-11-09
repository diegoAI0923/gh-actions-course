---
name: github-actions-study-notes
description: Formats and annotates rough Git and GitHub Actions study notes appended to the bottom of not-your-typical-readme.md. Use when the user asks to format, explain, organize, or document recently appended study notes in this repository.
---

# GitHub Actions Study Notes

Maintain `not-your-typical-readme.md` as the GitHub Actions certification study journal.

## Workflow

1. Read the complete study notes file and identify the newest rough material the user appended at its bottom.
2. Read enough repository context to accurately explain the commands, configuration, or workflow being documented.
3. Replace only that newly appended rough material with a structured, readable study entry. Preserve all prior content, including existing headings, explanations, links, and templates.
4. Use this format when the material supports it:

   ````md
   ## [Topic or workflow name]

   **Concept:** [The Git or GitHub Actions concept being practiced.]

   **Context:** [Why this work was performed.]

   ```sh
   [A copyable command.]
   ````

   > [A concise explanation of what the command does and why it matters.]

   **Observed result:** [The relevant output, behavior, or repository state.]

   **Key takeaway:** [The certification-relevant idea.]

   **References:** [Relevant course or GitHub documentation links.]
   ```

5. Use one fenced `sh` block per shell command or closely related command sequence. Follow each block with a concise Markdown blockquote that explains it. Use an appropriately labeled fenced block, such as `yaml`, for workflow configuration.
6. Include only fields supported by the appended material. Do not invent command output, workflow runs, course links, or results. Ask for clarification when critical context is missing.
7. Run `git diff --check` after editing and report the formatted section and validation result.

## Preservation rules

- Treat the user’s bottom-of-file addition as the only editable input unless they explicitly request a broader change.
- Do not reformat or remove previous entries.
- Keep commands copyable: do not place explanatory comments inside a command block unless the user supplied them.
- Do not run documented commands merely to produce notes unless the user explicitly requests execution.

## Invocation examples

- `Format the study notes I just appended to @not-your-typical-readme.md.`
- `Use the GitHub Actions study notes skill to explain and organize the new bottom-of-file notes.`
