# WHO Call for Clinical Guideline Experts: applications dashboard

Quarto dashboard summarising applications to the WHO call for Guideline Development Group (GDG) members for three living clinical guidelines: **sepsis**, **diphtheria** and **viral respiratory infection**. Applications are collected through WHO DataForm (LimeSurvey, survey 741739).

> ⚠️ **Data Privacy Notice:** This repository contains the reporting script, theme and survey structure only. It contains **no individual applicant data**. The published dashboard is rendered without names, e-mail addresses, gender or free-text statements.

---

## 📁 Repository Structure

| Directory / File | Description |
| :--- | :--- |
| `gdg_expert_call.qmd` | Quarto dashboard script (overview, map, applicant table, profiles, data checks). |
| `who.scss` | WHO theme (colours, typography). |
| `assets/` | WHO logos and country → ISO3 → WHO region lookup. |
| `index.html` | Published dashboard (public version, no personal data). |
| `data/` | **Not committed.** Local folder for DataForm exports, one dated sub-folder per snapshot. |

---

## 🚀 Workflow Guide

### Step 1: Export data from WHO DataForm

1. Open the survey in **[WHO DataForm V6](https://extranet.who.int/dataformv6/index.php/surveyAdministration/listsurveys)**.
2. Go to **Responses** → **Export**.
3. Export settings:
   * **Format:** CSV (Microsoft Excel and R data file also work)
   * **Completion state:** All responses (needed for the completion rate)
   * **Headings:** Question code *(Full question text also works)*
4. Also export the **survey structure** (`.txt`) once.
5. Save both into a dated folder, e.g. `data/2026-10-18/`. The most recent dated folder is used.

### Step 2: Render the dashboard

Requires **R** and **Quarto**, with:

```r
install.packages(c("data.table", "plotly", "DT", "htmltools", "bslib", "readxl"))
```

**Internal version** (names, e-mails, motivation statements): do not publish.

```bash
quarto render gdg_expert_call.qmd
```

**Public version** for GitHub Pages:

```bash
quarto render gdg_expert_call.qmd -P show_personal:false -o index.html
```

Optional: `-P snapshot:2026-10-18` to render a specific snapshot.

### Step 3: Publish

Commit `index.html` and push. GitHub Pages: **Settings** → **Pages** → deploy from branch `main`, folder `/ (root)`.

---

## Notes

* The call is open (no invitation list), so the dashboard reports the **completion rate** (submitted ÷ started) and **applicants per seat** (20 per GDG) rather than a response rate.
* The form's age option "50–69" overlaps "60–69"; it is displayed as 50–59.
* The world map loads its outlines from `cdn.plot.ly` and needs an internet connection.

## Contributing / updating

Work on a branch and open a Pull Request; do not commit directly to `main`.

## Maintainer

For access requests or questions, contact cmtm@who.int
