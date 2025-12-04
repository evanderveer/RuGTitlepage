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
- **Automatic system font detection** - uses Georgia from system fonts if available
- Helpful error messages when fonts are missing

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

### Fonts Required
- **Georgia font family** (automatically detected from system or local directory)

  The package will search for Georgia fonts in this order:
  1. **System fonts** (recommended) - Windows, macOS, or Linux font directories
  2. **Local `./fonts/` directory** (fallback) - for custom installations

  If using local fonts, place these files in `./fonts/`:
  - `Georgia-Regular.ttf`
  - `Georgia-Italic.ttf`
  - `Georgia-Bold.ttf`
  - `Georgia-BoldItalic.ttf`

### TeX Engine
- **Required**: XeLaTeX (for correct Georgia font loading)
- **Fallback**: pdfLaTeX (for testing only - will use incorrect font)

## Installation

### Option 1: Using System Fonts (Recommended)

1. **Ensure Georgia font is installed on your system**
   - **Windows**: Georgia is typically pre-installed with Windows
   - **macOS**: Georgia may be installed, or install it from Font Book
   - **Linux**: Install the `ttf-mscorefonts-installer` package

2. Place `RuGtitlepage.sty` and `logo.eps` in your thesis directory

3. Include the package in your LaTeX document:
   ```latex
   \usepackage{RuGtitlepage}
   ```

The package will automatically detect and use the Georgia font from your system.

### Option 2: Using Local Fonts (Fallback)

If Georgia is not available system-wide, or you need a specific version:

1. Place `RuGtitlepage.sty` in your thesis directory
2. Create a `fonts/` subdirectory
3. Copy Georgia font files to `fonts/`:
   - `Georgia-Regular.ttf`
   - `Georgia-Italic.ttf`
   - `Georgia-Bold.ttf`
   - `Georgia-BoldItalic.ttf`
4. Ensure `logo.eps` is in your thesis directory
5. Include the package:
   ```latex
   \usepackage{RuGtitlepage}
   ```

The package will automatically fall back to the local fonts if system fonts aren't found.

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

### Minimal Installation (Using System Fonts)
```
titlepage/
├── RuGtitlepage.sty          # Main package file
├── README.md                  # This file
├── titlepage.tex              # Example usage document
├── logo.eps                   # University logo (EPS format)
└── logo-eps-converted-to.pdf  # University logo (PDF format)
```

### With Local Fonts (Optional Fallback)
```
titlepage/
├── RuGtitlepage.sty          # Main package file
├── README.md                  # This file
├── titlepage.tex              # Example usage document
├── logo.eps                   # University logo (EPS format)
├── logo-eps-converted-to.pdf  # University logo (PDF format)
└── fonts/                     # Optional: only if Georgia not in system fonts
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

## Error Messages and Warnings

### Package Errors

The package provides clear error messages for common issues:

#### Missing Font Files
If Georgia font is not available on your system or in the local directory, you'll see:
```
! Package RuGtitlepage Error: Georgia font not found
Searched locations:
- System fonts (not found)
- ./fonts/ directory (not found)

On Windows: C:/Windows/Fonts/
On macOS: /Library/Fonts/ or ~/Library/Fonts/
On Linux: /usr/share/fonts/ or ~/.fonts/
```

The package searches system fonts first, then falls back to checking the local `./fonts/` directory.

#### Wrong TeX Engine
If you compile with pdfLaTeX instead of XeLaTeX, you'll see a warning:
```
Package RuGtitlepage Warning: You are not using XeLaTeX.
The Georgia font will NOT be loaded.
For correct formatting, compile with XeLaTeX:
latexmk -xelatex yourfile.tex
```

**Note:** This is a warning, not an error. Compilation will continue but with incorrect fonts.

## Troubleshooting

### Logo Not Found

**Error:** `! LaTeX Error: File 'logo.eps' not found.`

**Solution:** Ensure `logo.eps` is in the same directory as your `.tex` file, or provide the full path:

```latex
% In RuGtitlepage.sty, line 175, change:
\includegraphics[width=6cm]{/path/to/logo.eps}
```

### Font Not Found

**Error:**
```
! Package RuGtitlepage Error: Georgia font not found
```

**Solution:**

**Recommended: Install Georgia system-wide**

1. **Windows**:
   - Georgia is typically pre-installed
   - If missing, obtain from Windows installation media or Microsoft Office
   - Install to `C:/Windows/Fonts/`

2. **macOS**:
   - Open Font Book
   - Install Georgia font family
   - Fonts should be in `/Library/Fonts/` or `~/Library/Fonts/`

3. **Linux**:
   ```bash
   sudo apt-get install ttf-mscorefonts-installer
   ```
   Or manually install to `~/.fonts/` or `/usr/share/fonts/`

**Alternative: Use local fonts directory**

1. Create `./fonts/` directory in your thesis folder
2. Copy Georgia font files to `./fonts/`:
   - `Georgia-Regular.ttf`
   - `Georgia-Italic.ttf`
   - `Georgia-Bold.ttf`
   - `Georgia-BoldItalic.ttf`

**Font Search Order:**
The package automatically searches:
1. System fonts (via fontspec's automatic detection)
2. Local `./fonts/` directory (manual fallback)

If Georgia is found in system fonts, you'll see:
```
Package RuGtitlepage Info: Georgia font loaded from system fonts
```

If loaded from local directory:
```
Package RuGtitlepage Info: Georgia font loaded from ./fonts/ directory
```

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
