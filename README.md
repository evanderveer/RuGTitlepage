# RuG Titlepage Package

A LaTeX package for generating PhD thesis title pages formatted according to University of Groningen (RuG - Rijksuniversiteit Groningen) requirements.

## Features

- Automatic title page generation with university branding
- Custom page dimensions (17cm × 24cm)
- Dynamic defense date formatting with automatic day-of-week calculation
- Flexible committee member management (supervisors, co-supervisors, assessment committee)
- Conditional rendering of sections (only shows sections with content)
- Georgia font family integration for formal academic appearance
- XeLaTeX required for correct font rendering (pdfLaTeX fallback for testing only)

## Requirements

### LaTeX Packages
- `microtype` - Typography enhancement
- `graphicx` - Image inclusion (university logo)
- `pgfkeys`, `pgffor` - Programming utilities
- `datetime` - Date/time formatting
- `geometry` - Custom page dimensions
- `iftex` - TeX engine detection
- `fontspec` - Font management (XeTeX only)

### Files Required
- `logo.eps` or `logo.pdf` - University of Groningen logo
- `fonts/` directory containing Georgia font family:
  - `Georgia-Regular.ttf`
  - `Georgia-Italic.ttf`
  - `Georgia-Bold.ttf`
  - `Georgia-BoldItalic.ttf`

### TeX Engine
- **Required**: XeLaTeX (for correct Georgia font loading)
- **Fallback**: pdfLaTeX (for testing only - will use incorrect font)

## Installation

1. Place `RuGtitlepage.sty` in your thesis directory
2. Ensure `logo.eps` and `fonts/` directory are in the same location
3. Include the package in your LaTeX document:

```latex
\usepackage{RuGtitlepage}
```

## Usage

### Basic Example

```latex
\documentclass[11pt]{article}
\usepackage{RuGtitlepage}

\begin{document}

% Configure title page information
\RuGtitle{Your PhD Thesis Title Goes Here}
\RuGrector{Prof. Dr. Rector Name}
\RuGdefensedate{15}{6}{2026}{14}{00}
\RuGcandidate{Your Name}{10}{3}{1990}

% Add committee members
\RuGsupervisor{Prof. Dr. First Supervisor}
\RuGsupervisor{Prof. Dr. Second Supervisor}
\RuGcosupervisor{Dr. Co-Supervisor Name}
\RuGassessor{Prof. Dr. Committee Member 1}
\RuGassessor{Prof. Dr. Committee Member 2}
\RuGassessor{Prof. Dr. Committee Member 3}

% Generate the title page
\makeRuGtitlepage

% Generate the committee page (on a new page)
\newpage
\makeRuGcommittee

\end{document}
```

### Compilation

**Important:** You must compile with XeLaTeX to load the correct Georgia font. Using pdfLaTeX will result in incorrect fonts and is only supported as a fallback for testing purposes.

Compile with XeLaTeX using latexmk (recommended):

```bash
latexmk -xelatex yourfile.tex
```

Or directly with XeLaTeX:

```bash
xelatex yourfile.tex
```

**Note:** Do not use `pdflatex` for final versions - it will not load the Georgia font correctly.

## Commands Reference

### Title Page Configuration

#### `\RuGtitle{title}`
Sets the thesis title.

**Parameters:**
- `title` - The full title of your thesis

**Example:**
```latex
\RuGtitle{Advanced Studies in Quantum Computing and Machine Learning}
```

---

#### `\RuGdefensedate{day}{month}{year}{hour}{minute}`
Sets the defense date with automatic day-of-week calculation.

**Parameters:**
- `day` - Day of the month (1-31)
- `month` - Month number (1-12)
- `year` - Year (e.g., 2026)
- `hour` - Hour in 24-hour format (0-23)
- `minute` - Minute (00-59)

**Example:**
```latex
\RuGdefensedate{15}{6}{2026}{14}{00}
```
**Output:** "Tuesday 15 June 2026 at 14:00 hours"

---

#### `\RuGrector{name}`
Sets the Rector Magnificus name.

**Parameters:**
- `name` - Full name of the Rector Magnificus

**Example:**
```latex
\RuGrector{Prof. Dr. Jouke de Vries}
```

---

#### `\RuGcandidate{name}{day}{month}{year}`
Sets the candidate (PhD student) information.

**Parameters:**
- `name` - Full name of the candidate
- `day` - Birth day (1-31)
- `month` - Birth month (1-12)
- `year` - Birth year

**Example:**
```latex
\RuGcandidate{Jane Smith}{10}{3}{1990}
```
**Output:** "Jane Smith, born on 10 March 1990"

---

### Committee Members

#### `\RuGsupervisor{name}`
Adds a supervisor to the list. Can be called multiple times.

**Parameters:**
- `name` - Full name and title of the supervisor

**Example:**
```latex
\RuGsupervisor{Prof. Dr. John Smith}
\RuGsupervisor{Prof. Dr. Mary Johnson}
```

---

#### `\RuGcosupervisor{name}`
Adds a co-supervisor to the list. Can be called multiple times.

**Parameters:**
- `name` - Full name and title of the co-supervisor

**Example:**
```latex
\RuGcosupervisor{Dr. Robert Brown}
```

---

#### `\RuGassessor{name}`
Adds an assessment committee member to the list. Can be called multiple times.

**Parameters:**
- `name` - Full name and title of the committee member

**Example:**
```latex
\RuGassessor{Prof. Dr. Alice Cooper}
\RuGassessor{Prof. Dr. David Lee}
\RuGassessor{Prof. Dr. Emma Wilson}
```

---

### Page Generation

#### `\makeRuGtitlepage`
Generates the complete title page. Must be called after setting title, rector, defense date, and candidate.

**Example:**
```latex
\makeRuGtitlepage
```

---

#### `\makeRuGcommittee`
Generates the committee members page. Typically called on a new page after the title page.

**Features:**
- Only shows sections that have members
- Proper spacing between sections
- Follows RuG formatting requirements

**Example:**
```latex
\newpage
\makeRuGcommittee
```

## Layout Specifications

### Page Dimensions
- **Paper size:** 17cm × 24cm (custom)
- **Margins:**
  - Left/Right: 1.4cm
  - Top: 2cm
  - Bottom: 1cm

### Vertical Spacing (Title Page)
The title page uses fixed-height minipages for consistent spacing:
- Title: 5.5cm
- "PhD thesis" text: 3.75cm
- Rector/defense information: 4cm
- "by" separator: 3cm
- Candidate information: 2cm

### Typography
- **Font family:** Georgia (serif)
- **Title:** Huge, bold
- **Headings:** Large, bold
- **Body text:** Footnotesize
- **Candidate name:** Large, bold

## File Structure

```
titlepage/
├── RuGtitlepage.sty          # Main package file
├── README.md                  # This file
├── titlepage.tex              # Example usage document
├── logo.eps                   # University logo (EPS format)
├── logo-eps-converted-to.pdf  # University logo (PDF format)
└── fonts/
    ├── Georgia-Regular.ttf
    ├── Georgia-Italic.ttf
    ├── Georgia-Bold.ttf
    └── Georgia-BoldItalic.ttf
```

## Advanced Usage

### Multiple Supervisors

```latex
\RuGsupervisor{Prof. Dr. First Supervisor}
\RuGsupervisor{Prof. Dr. Second Supervisor}
\RuGsupervisor{Prof. Dr. Third Supervisor}
```

### Optional Sections

Sections are automatically hidden if no members are added. For example, if you don't have co-supervisors:

```latex
% Don't call \RuGcosupervisor at all
\RuGsupervisor{Prof. Dr. Main Supervisor}
\RuGassessor{Prof. Dr. Committee Member}

\makeRuGcommittee  % Will only show Supervisors and Assessment Committee
```

### Custom Spacing

To add extra space between title page and committee page:

```latex
\makeRuGtitlepage

\newpage
\vspace{2cm}  % Add extra space at top

\makeRuGcommittee
```

## Technical Details

### Package Architecture

The package uses a declarative configuration pattern:
1. User calls setter commands to configure data (e.g., `\RuGtitle`, `\RuGsupervisor`)
2. Each setter defines an internal command prefixed with `@`
3. Generation commands (`\makeRuGtitlepage`, `\makeRuGcommittee`) assemble the configured elements

### Committee Member Implementation

Committee members are managed using **etoolbox's list commands**:
- `\listadd` - Accumulates members into lists
- `\dolistloop` - Iterates through lists for printing
- `\ifdefempty` - Conditionally renders sections

This approach:
- Handles any number of members
- Avoids trailing separators
- Efficiently manages memory
- Provides clean, maintainable code

## Troubleshooting

### Logo Not Found

**Error:** `! LaTeX Error: File 'logo.eps' not found.`

**Solution:** Ensure `logo.eps` is in the same directory as your `.tex` file, or provide the full path:

```latex
% In RuGtitlepage.sty, line 175, change:
\includegraphics[width=6cm]{/path/to/logo.eps}
```

### Font Not Found

**Error:** `! fontspec error: "font-not-found"`

**Solution:**
1. Ensure you are compiling with **XeLaTeX** (not pdfLaTeX)
2. Verify the `fonts/` directory exists with all Georgia font files
3. Check the relative path in `RuGtitlepage.sty` (line 24-31)
4. Consider using system fonts instead:

```latex
\setmainfont{Georgia}  % Uses system Georgia font
```

**Important:** The Georgia font is only loaded when using XeLaTeX. If you compile with pdfLaTeX, the default Computer Modern font will be used instead, which is incorrect for final submissions.

### Defense Date Format Issues

**Problem:** Day of week is incorrect

**Solution:** Verify the date parameters are in the correct order:
```latex
\RuGdefensedate{day}{month}{year}{hour}{minute}
```

### Committee Members Not Showing

**Problem:** `\makeRuGcommittee` produces an empty page

**Solution:** Ensure you've added at least one member:
```latex
\RuGsupervisor{Prof. Dr. Name}  % Add this before \makeRuGcommittee
```

## Version History

### Current Version
- Dynamic committee member management
- Improved code documentation
- XeTeX compatibility with fallback support
- Automated defense date formatting

## License

This package is provided for use with University of Groningen PhD theses. Please ensure compliance with university regulations and branding guidelines.

## Credits

Developed for the University of Groningen PhD thesis requirements.

## Contact

For issues, questions, or contributions, please contact your thesis supervisor or the university's thesis office.
