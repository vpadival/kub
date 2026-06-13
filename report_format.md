# Project Report Formatting Guidelines & Specifications

This document outlines the strict formatting standards for generating and editing the project report. It is optimized for both human review and integration into Large Language Model (LLM) prompts for automated document rendering (e.g., via LaTeX, Pandoc, or HTML-to-PDF engines).

---

## 1. Global Document Configurations

Use these rules as the base stylesheet for the entire document:

| Parameter | Value / Specification |
| :--- | :--- |
| **Font Family** | `Times New Roman` (strictly applied to all body and heading elements) |
| **Line Spacing** | `1.5` |
| **Text Alignment** | `Justified` (all paragraph text must be fully justified) |
| **Bullet Point Style** | Circular bullets (`•` / `disc` type list style) |

---

## 2. Page Hierarchy & Layout Rules

The document is divided into four distinct page types, each requiring different headers, footers, and page numbering rules.

### Page Style Definitions Matrix

| Page Type | Header Enabled | Header Content | Footer Enabled | Footer Content (Left) | Footer Content (Right) | Page Number Style | Separator Lines | Page Boundary |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Cover Page** | No | None | No | None | None | None | None | Yes |
| **Certificate Page** | No | None | No | None | None | None | None | Yes |
| **Preliminary Pages**<br>*(Abstract, Index, List of Figures, etc.)* | No | None | Yes | `Dept. of B.E / [Branch Name]` | Roman Numeral (Capital) | `III`, `IV`, `V`, ... | Solid line above footer | Yes |
| **Chapter Pages**<br>*(Chapter 1 onwards)* | Yes* | `[Project Name]` | Yes | `Dept. of B.E / [Branch Name]` | Arabic Numeral | `1`, `2`, `3`, ... | Solid line below header<br>Solid line above footer | No |
| **Citations Page** | No | None | No | None | None | None | None | No |

*\*Exception: The first page of any chapter (the page containing the chapter title) must NOT display a header.*

### Key Navigation & Formatting Rules:
*   **Header Rules**: Applies strictly from the **Chapter 1** page onwards. Contains the project name left-aligned, with a horizontal separator line below it. 
    *   *Critical Exception*: The page containing the beginning of any chapter does not display a header.
*   **Footer Rules**: Applies from the **Abstract** page onwards (excluding the Citations/References page). Contains the Department/Branch Name left-aligned, and the page number right-aligned, with a horizontal separator line above it.
*   **Page Number Transition**:
    *   **Preliminary pages** (Abstract up to Chapter 1): Use uppercase Roman numerals (e.g. `III`, `IV`, `V`, ...). Pages 1 (Cover Page) and 2 (Certificate Page) do not have visible headers or footers and are skipped in visible numbering.
    *   **Chapters**: Restart Arabic numerals (e.g., `1`, `2`, `3`) starting at `1` on the first page of Chapter 1.
*   **Exceptions**: The **Citations / References Page** and the **Cover Page** must not contain any headers, footers, or page numbers.

---

## 3. Typography & Headings Hierarchy

### Chapter Titles
Each new chapter must begin on a fresh page and follow this exact two-line structure:
1.  **Line 1 (Chapter Label)**: Left-aligned, font size `14pt`, **bold**.
    *   *Format*: `Chapter [N]` (where N is the chapter number)
2.  **Line 2 (Chapter Name)**: Centered, font size `16pt`, **bold**, **underlined**. Must be placed on the line immediately following Line 1.
    *   *Format*: `[Chapter Title]`

#### LLM Prompt Example for Chapter Heading:
```markdown
Chapter 1
                   INTRODUCTION
                   ------------
```
*(In HTML/CSS, style this as: Line 1: `text-align: left; font-size: 14pt; font-weight: bold;`; Line 2: `text-align: center; font-size: 16pt; font-weight: bold; text-decoration: underline;`)*

---

## 4. Tables Styling

All tables (including the Table of Contents/Index, List of Figures, and tables within the body) must adhere to the following layout constraints:

*   **Borders**: Solid black borders, `1 point (1pt)` thickness, applied to all gridlines (inner and outer).
*   **Column Headers**:
    *   Horizontal Alignment: Centered
    *   Vertical Alignment: Centered heightwise
*   **Data Cells**:
    *   **Serial Numbers (S.No) & Page Numbers (Pg No.)**: Centered both vertically and horizontally.
    *   **Standard Text / Content Columns**: Centered vertically (height-wise) and left-aligned horizontally (width-wise).

### Specific Table Formats

#### A. Table of Contents (Index)
*   **Columns**: Must contain exactly 3 columns:
    1.  `SL.No` (Serial Number)
    2.  `Content`
    3.  `Page Number`
*   **Width Layout**:
    *   Must occupy almost the entire width of the page.
    *   The width of `SL.No` and `Page Number` columns must be sized to fit the column header name plus a small amount of padding.
    *   The `Content` column must occupy all remaining width.
*   **Content Alignment**:
    *   `Content` cell text must be left-aligned horizontally and centered vertically.
*   **Row Height**: Row heights must dynamically size to fit their text content.

#### B. List of Figures
*   **Columns**: Must contain exactly 3 columns:
    1.  `Fig.No` (Figure Number)
    2.  `Description` (a shortened version of the figure caption)
    3.  `Page Number`
*   **Width Layout**:
    *   The width of `Fig.No` and `Page Number` columns must be sized to fit the column header name plus a small amount of padding.
    *   The `Description` column must occupy all remaining width.
*   **Content Alignment**:
    *   `Description` cell text must be left-aligned horizontally and centered vertically.
*   **Row Height**: Row heights must dynamically size to fit their text content.

---

## 5. Figures & Media

*   **Alignment**: All images and illustrations must be centered.
*   **Captions**:
    *   Must be placed directly below the image and centered.
    *   **Naming Convention**: `Figure [N].[M]: [Caption Text]`
        *   `N` represents the Chapter number.
        *   `M` represents the figure sequence number within that chapter.
    *   *Example*: `Figure 1.2: System Context Diagram`

---

## 6. Citations & References

*   **Page Placement**: The citations page must be a new page at the very end of the document.
*   **Format**: Citations and the end-of-document reference list must strictly follow the **IEEE reference format** (e.g., brackets `[1]` in text, corresponding to numbered references in the final section).
*   **Page Constraints**: The reference pages must have **no header and no footer**.

---

## LLM Parsable Configuration (JSON Schema)

For programmatic document compilation or LLM prompt extraction:

```json
{
  "document_defaults": {
    "font_family": "Times New Roman",
    "line_spacing": 1.5,
    "text_alignment": "justified",
    "list_style": "disc"
  },
  "page_hierarchy": {
    "cover_page": {
      "header_enabled": false,
      "footer_enabled": false,
      "page_boundary": true
    },
    "certificate_page": {
      "header_enabled": false,
      "footer_enabled": false,
      "page_boundary": true
    },
    "preliminary_pages": {
      "header_enabled": false,
      "footer_enabled": true,
      "footer_left": "Dept. of B.E / [Branch Name]",
      "page_number_style": "ROMAN_CAPITAL",
      "start_page_index_visible": 3,
      "start_page_value_roman": "III",
      "separator_above_footer": true,
      "page_boundary": true
    },
    "chapter_pages": {
      "header_enabled_global": true,
      "header_enabled_first_page": false,
      "header_left": "[Project Name]",
      "separator_below_header": true,
      "footer_enabled": true,
      "footer_left": "Dept. of B.E / [Branch Name]",
      "page_number_style": "ARABIC",
      "start_page_value_arabic": 1,
      "separator_above_footer": true,
      "page_boundary": false
    },
    "citations_page": {
      "header_enabled": false,
      "footer_enabled": false,
      "page_boundary": false
    }
  },
  "headings": {
    "chapter_label": {
      "font_size": "14pt",
      "font_weight": "bold",
      "alignment": "left"
    },
    "chapter_name": {
      "font_size": "16pt",
      "font_weight": "bold",
      "text_decoration": "underline",
      "alignment": "center"
    }
  },
  "tables": {
    "border": {
      "color": "#000000",
      "width": "1pt",
      "style": "solid"
    },
    "alignment": {
      "headers": {
        "horizontal": "center",
        "vertical": "center"
      },
      "meta_columns": ["S.No", "SL.No", "Pg No.", "Page Number", "Fig.No"],
      "meta_cells": {
        "horizontal": "center",
        "vertical": "center"
      },
      "content_cells": {
        "horizontal": "left",
        "vertical": "center"
      }
    },
    "special_tables": {
      "table_of_contents": {
        "columns": ["SL.No", "Content", "Page Number"],
        "layout": "full_width",
        "column_widths": {
          "SL.No": "fit_header_padding",
          "Page Number": "fit_header_padding",
          "Content": "remaining_width"
        }
      },
      "list_of_figures": {
        "columns": ["Fig.No", "Description", "Page Number"],
        "layout": "full_width",
        "column_widths": {
          "Fig.No": "fit_header_padding",
          "Page Number": "fit_header_padding",
          "Description": "remaining_width"
        }
      }
    }
  },
  "figures": {
    "alignment": "center",
    "caption": {
      "alignment": "center",
      "prefix_format": "Figure {chapter_number}.{figure_number}:"
    }
  },
  "citations": {
    "style": "IEEE",
    "new_page": true
  }
}
```
