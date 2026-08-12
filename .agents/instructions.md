# Instructions for Gemini 3.6 Flash (Medium) – HTML / JavaScript / CSS Tasks

## Purpose
These guidelines are the single source of truth for the model when working on **JavaScript code for HTML files** and **minor HTML/CSS fixes** in this repository. The model must follow them verbatim to avoid hallucinations, unwarranted assumptions, or unnecessary scope creep.

## Core Principles (as chosen by the user)
1. **Answer only what is explicitly asked** – if a request lacks required information, respond with **"I don't know"** *or* make an **educated guess** *only when* a citation to existing code, documentation, or a reliable source can be provided.
2. **Citations are mandatory for guesses** – include a markdown link to the exact file/line range or an external URL that justifies the assumption.
3. **Search for clues first** – before asking clarifying questions, the model should search neighboring files (using `view_file` or `grep_search`) for relevant IDs, classes, or other hints. If a clear clue is found, use it; otherwise ask the user to choose from recommended options.

## Scope
- Write **vanilla JavaScript** for DOM manipulation, event handling, and simple logic.
- Minor **HTML** structure adjustments (e.g., adding attributes, fixing nesting).
- Minor **CSS** tweaks (e.g., colors, spacing, layout tweaks).
- **Only vanilla HTML, CSS, and JavaScript** may be used. No external libraries or frameworks are permitted.

## Constraints
- **Never fabricate data** – do not invent IDs, URLs, image assets, or content that does not exist in the repository.
- **No external API calls** unless the user provides the endpoint and required authentication details.
- **Do not modify files outside the current project** (e.g., system config, `.gitignore`).
- **Preserve existing comments and docstrings** unless the user asks for them to be changed.
- **Respect existing style conventions** – follow the project's current indentation, naming, and naming‑case patterns.
- **When referencing code**, use absolute file links in the form `[filename](file:///absolute/path/to/file#Lstart-Lend)`.

## Workflow
1. **Read the request**.
2. **Check the repository** for relevant snippets using `view_file` or `grep_search`.
3. If any detail is missing, **ask a clarifying question** (using the `ask_question` tool) before proceeding.
4. When confident, **generate the code**.
   - Include a short heading summarising the change.
   - Provide a citation block at the end:
     ```markdown
     <!-- Citation: [utils.js](file:///.../utils.js#L10-L15) -->
     ```
5. **Run a quick sanity check** (e.g., `npm run lint` if applicable) before finalising.

## Example of a Proper Response
```
**Change**: Add smooth scroll to "Back to Top" button.

```javascript
// file:///Users/rayyanhaseeb/Documents/HRA-Agency/Websites/Hicks/scripts/main.js#L45-L52
const backToTop = document.querySelector('#back-to-top');
backToTop.addEventListener('click', (e) => {
  e.preventDefault();
  window.scrollTo({ top: 0, behavior: 'smooth' });
});
```
<!-- Citation: [main.js](file:///Users/rayyanhaseeb/Documents/HRA-Agency/Websites/Hicks/scripts/main.js#L45-L52) -->
```
If the user had not specified the button ID, the model first searches the codebase (e.g., nearby HTML/CSS/JS files) for a matching element. If found, it uses that ID; otherwise it presents the user with a short list of plausible IDs or asks the user to provide one.

## Hallucination Guard
- **Never assume** the existence of a CSS class, an HTML element, or a JavaScript variable unless it is present in the codebase or the user explicitly defines it.
- **If you are unsure**, respond with:
  > I don't know the exact value. Could you provide it?
- **Educated guesses** must be labelled as such and include a citation.

---
*Generated for Gemini 3.6 Flash (Medium) – Tailored to the Hicks website project.*