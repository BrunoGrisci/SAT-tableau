# SAT-tableau

<p align="right">
  <strong>English</strong> |
  <a href="README.pt-BR.md">Português (Brasil)</a>
</p>

**SAT-tableau** is an interactive, browser-based educational webtool for visualizing the tableau proof behind the **Cook-Levin theorem**, namely that **SAT is NP-complete**.

The tool focuses on the reduction from an accepting computation of a **nondeterministic polynomial-time Turing Machine (NDTM)** to a Boolean satisfiability instance. It shows how the tableau variables, the machine transitions, and the SAT formula components fit together.

It is designed for classroom use in **Theory of Computation**, especially when teaching the Cook-Levin theorem through the standard computation-history/tableau construction.

🔗 **GitHub Pages target:** https://brunogrisci.github.io/sat_tableau
🔗 **GitHub repository:** https://github.com/BrunoGrisci/SAT-tableau

---

## ✨ Features

### Core functionality
- Interactive visualization of the Cook-Levin tableau construction for SAT.
- Example NDTM for unary multiples of **2 or 3**:
  - branch `×2` checks whether the input length is even,
  - branch `×3` checks whether the input length is a multiple of three.
- Configurable unary input length, represented as the number of `1`s.
- Correct treatment of accepting and rejecting branches:
  - an input such as `1` has no accepting branch,
  - an input such as `1111` is accepted by the `×2` branch but rejected by the `×3` branch,
  - rejecting selected branches are highlighted in red to show that their assignment cannot satisfy `φaccept`.
- Branch controls show whether each nondeterministic branch currently accepts or rejects.

### Tableau visualization
- A 3D tableau of Boolean variables `x_{i,j,s}`:
  - rows `t_i` represent time/configuration steps,
  - columns `j_i` represent tape/configuration positions,
  - depth represents the possible symbols and states.
- True variables are rendered as readable cells; false variables are shown as small markers in 3D mode.
- A **2D symbol-axis view** flattens the tableau into a square-like projection for lecture explanation.
- In 2D mode, false-variable markers are hidden so they do not obscure the true-cell labels.
- View controls:
  - drag to rotate,
  - shift/middle-button drag to pan,
  - mouse wheel to zoom,
  - reset view,
  - align down the symbol axis.

### Machine and formula panels
- **Machine panel** with:
  - the NDTM graph,
  - highlighted active transition,
  - transition cards for the nondeterministic split, scan transitions, accept transitions, and reject transitions,
  - the unary-input control.
- **Formula panel** with the standard Cook-Levin components:
  - `φcell`: every tableau position contains exactly one symbol,
  - `φstart`: the first row is the initial configuration,
  - `φaccept`: at least one tableau cell contains `qA`,
  - `φmove`: every local window follows a legal machine move.
- Formula blocks show the relevant schema, clause/literal counts, and the currently selected cell, unit, accepting literal, or legal window.
- Clickable tableau selections:
  - choose a cell for `φcell`,
  - choose an initial-row unit for `φstart`,
  - choose an accepting literal for `φaccept`,
  - choose a local 2-row window for `φmove`.
- Connector lines link the active machine/formula explanation to the corresponding tableau location.
- The right-side Machine/Formula panel can be resized by dragging its left separator; the width is persisted locally.

### References and usability
- In-page **References** modal explaining:
  - the roles of Stephen Cook and Leonid Levin,
  - the Karp/Sipser-style tableau proof used by the tool,
  - Richard Karp's 21 NP-complete problems,
  - the difference between the pedagogical tableau encoding and later quasilinear encodings,
  - the main theoretical source: Michael Sipser, *Introduction to the Theory of Computation*.
- 🌙 / ☀️ clear/dark mode toggle.
- English / Brazilian Portuguese toggle.
- Persistent preferences via `localStorage`:
  - theme,
  - language,
  - side-panel width.
- Fully client-side, with no backend and no external UI framework.

---

## 🧠 Pedagogical goals

This tool was built to help students:

- see SAT variables as positions in a computation tableau rather than as abstract symbols only,
- connect the existential nondeterministic accepting branch with satisfiability of the formula,
- understand why a rejecting branch does not itself satisfy `φaccept`,
- inspect the four main Cook-Levin constraints separately,
- relate local tableau windows to Turing Machine transitions,
- understand why checking local consistency is enough to certify a global computation history,
- distinguish the proof idea from implementation-level or optimized encodings.

It is suitable for:

- undergraduate Theory of Computation courses,
- classroom demonstrations with a projector,
- guided discussions of NP-completeness and reductions,
- self-study of the tableau version of the Cook-Levin theorem.

---

## 📄 Input model

The current tool does not import arbitrary machines. It uses a fixed pedagogical NDTM derived from the course material:

- input alphabet: unary strings over `1`,
- input value: the number of `1`s, configurable in the Machine panel,
- accepted language: unary numbers whose length is a multiple of `2` or `3`,
- nondeterministic choice: the first transition chooses either the `×2` branch or the `×3` branch.

The tableau size is derived from the current input length. For each input, the tool rebuilds the trace, updates both branch results, and re-renders the corresponding tableau and formula explanations.

---

## 🌐 Internationalization (i18n)

- Full support for **English** and **Brazilian Portuguese**.
- Header, controls, panels, references, status messages, tooltips, and formula explanations are bilingual.
- Switching language does **not** reset the selected input, branch, focus, tableau view, or side-panel width.

---

## 🛠️ Tech stack

- Vanilla **HTML / CSS / JavaScript**
- No build step
- No external dependencies
- Fully client-side
- Compatible with static hosting such as **GitHub Pages**

Main files:

- `sat_tableau.html`
- `assetsSAT_tableau/styles.css`
- `assetsSAT_tableau/script.js`

To run locally, open `sat_tableau.html` directly in a browser, or serve the folder with any static file server, for example:

```bash
python3 -m http.server 4173
```

Then open:

```text
http://127.0.0.1:4173/sat_tableau.html
```

---

## 🧪 Verification

The project is static and does not require a test framework. During development, the implementation was checked with:

```bash
node --check assetsSAT_tableau/script.js
```

Browser validation was also used to confirm:

- branch acceptance/rejection for different unary inputs,
- red highlights for selected rejecting branches,
- formula focus modes `φcell`, `φstart`, `φaccept`, and `φmove`,
- selectable cells, start units, accepting literals, and move windows,
- machine and formula connector lines,
- 3D rotation, pan, zoom, reset, and 2D symbol-axis view,
- hidden false-variable markers in 2D mode only,
- clear/dark theme switching,
- English/Brazilian Portuguese switching,
- references modal behavior,
- side-panel resizing and persistence.

---

## 🚀 Future work (ideas)

- Support importing or editing arbitrary nondeterministic Turing Machines.
- Add a guided walkthrough mode for the four formula components.
- Add optional display of expanded sample clauses for more tableau positions.
- Add a compact legend for symbol layers and state/tape/boundary classes.
- Export the current tableau assignment or formula summary.
- Add screenshots and short animated examples for the README.

---

## 🎓 Credits

**Developed by**  
**Prof. Bruno Iochins Grisci**  
Departamento de Informática Teórica  
Instituto de Informática – Universidade Federal do Rio Grande do Sul (UFRGS)  
🔗 https://brunogrisci.github.io/  
🔗 https://www.inf.ufrgs.br/site/  
🔗 https://www.ufrgs.br/site/

**Main theoretical reference**
- Michael Sipser, *Introduction to the Theory of Computation*, especially the Cook-Levin theorem and tableau/window construction.

**Historical and proof context**
- Stephen Cook and Leonid Levin: the Cook-Levin theorem.
- Richard Karp: reducibility and the 21 NP-complete problems.
- Karp/Sipser-style tableau proof used as the basis for this visualization.
- Later quasilinear encodings are acknowledged in the references modal but intentionally not developed in this teaching tool.

**Development note**  
This webtool was created with the assistance of **Codex GPT-5.5**.

---

## 📦 License

This project is licensed under the **MIT License**.

You are free to use, modify, and redistribute it for academic and educational purposes, provided proper attribution is given.

See the `LICENSE` file for details.

---

If you use this tool in teaching or research, a citation or link back to the repository is appreciated.

## 📚 Citation

If you use this tool in academic work (papers, theses, technical reports, or teaching material), please cite it as:

```bibtex
@software{Grisci_SAT_tableau,
  author       = {Bruno Iochins Grisci},
  title        = {{SAT-tableau}: An Interactive Visualizer for the Cook-Levin Tableau Construction},
  year         = {2026},
  url          = {https://github.com/BrunoGrisci/SAT-tableau},
  note         = {Educational web-based software},
}
```

---

## 🔄 See also

- **TM → PCP Domino Generator (tm2pcp)**  
  Webtool: https://brunogrisci.github.io/tm2pcp  
  Repository: https://github.com/BrunoGrisci/tm2pcp-webtool

- **PCP → CFG Ambiguity webtool**  
  Web app: https://brunogrisci.github.io/pcp2cfg  
  Repository: https://github.com/BrunoGrisci/pcp2cfg-webtool

- **Executable computability reductions**  
  Repository: https://github.com/BrunoGrisci/reductions-computability
