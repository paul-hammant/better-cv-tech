Single Page Resume/CV technology that's optimized for machine consumption into Applicant Tracking Systems and Job-finder portals
================================================================================================================================

A modern, responsive CV/Resume tech using vanilla JavaScript and the `JSON Resume` schema in a regular HTML page doc. Features interactive modification of 
what's visible, print optimization. AI has mocked up a collection of fictional character examples in this repo.

Key existing technology is the schema from [JsonResume](https://jsonresume.org/) and these example pages embed all the details of a person's resume/CV into 
the page as JSON in that schema. JsonResume normally uses a build concept that web-developers would be familar with. You'd start with the resume in JSON form, 
and build a PDF and a .html page from that. The .html version does not yet **also** embed the JSON as is but it could do if it gets an enhancement. This tech doesn't 
use a build at all, and instead swaps that for in-page rendering using JavaScript. It shares the JSON schema from JsonResume project.

* Applicant Tracking Systems and Job-finder portals would extract the JSON for fastest-possible consumption into their databases
* Humans recruitment staff will look at the HTML page, not knowing the raw data started as JSON within.
* Applicants would need to upload `Their_Name_Resume.html` to the ATS or portal (or email it as an attachment).

Applicant Tracking Systems and Job-finder portals would need a **trivial** change to pull the JSON data out of the .html file. 

## Features

- 📱 **Responsive** - Works perfectly on all devices with adaptive layout
- ✏️ **Interactive Verbosity Reduction** - Toggle edit mode to collapse sections priot to (say) print
- 🖨️ **Print-Ready** - Professional PDF output with clean URL formatting
- 🌍 **International** - Automatic CV/Resume terminology based on filename
- ⚡ **Zero Dependencies** - Pure in-page vanilla JavaScript to view (apart from the "download PDF" feature)
- 📋 **JSON Resume Standard** - Uses official JSON Resume schema v1.0.0 for portability
- 🔗 **Enhanced Print Links** - Shows actual URLs in print mode (e.g., "Project: https://example.com")

Limitation: the style of the resume is fixed, wheras JsonResume's portal details 100+ themes/styles.

## Seeing example Resumes/CVs

1. See [GH Pages site](https://paul-hammant.github.io/better-cv-tech/) to see the gallery of fictional character's CVs/resumes.
2. Or open any individual CV/Resume file directly
3. Click the ✏️ button to enter edit mode for that contrace/expand interactive feature
4. Use 🖨️ button or Ctrl+P to print/save as PDF

## JSON Resume Schema

All CV/Resume files now use the official [JSON Resume Schema v1.0.0](https://jsonresume.org/schema/) format:

```json
{
  "$schema": "https://raw.githubusercontent.com/jsonresume/resume-schema/v1.0.0/schema.json",
  "basics": {
    "name": "Your Name",
    "label": "Your Title",
    "email": "email@example.com",
    "phone": "+1234567890",
    "summary": "Professional summary...",
    "location": { ... },
    "profiles": [ ... ]
  },
  "work": [ ... ],
  "education": [ ... ],
  "skills": [ ... ],
  "languages": [ ... ],
  "interests": [ ... ],
  "awards": [ ... ],
  "certificates": [ ... ],
  "publications": [ ... ],
  "projects": [ ... ],
  "volunteer": [ ... ],
  "references": [ ... ]
}
```

## Creating Your Own CV/Resume

1. Copy any character file (e.g., `Tony_Stark_Resume.html`)
2. Replace the JSON data in the `<script type="application/json" id="cv-data-json">` section
3. Copy `app.json` and `style.css` into the pertinent section, or ask AI to do that for you.
4. Use `_Resume.html` for American format or `_CV.html` for international
5. Follow the JSON Resume schema structure for maximum compatibility

## Markdown Support in JSON

The JSON Resume schema stores text as plain strings, but this implementation supports basic markdown formatting for richer display:

**Supported markdown syntax:**
- `**bold text**` - Renders as bold
- `*italic text*` - Renders as italics  
- `[link text](https://example.com)` - Creates clickable links
- `## Header` - Section headers (rarely used)
- Line breaks with `\n\n` - Paragraph separation

**Fields that support markdown:**
- `basics.summary` - Professional summary
- `work[].summary` and `work[].highlights[]` - Job descriptions and achievements
- `volunteer[].summary` and `volunteer[].highlights[]` - Volunteer descriptions
- `projects[].description` and `projects[].highlights[]` - Project details
- `publications[].summary` - Publication descriptions
- `awards[].summary` - Award descriptions
- `references[].reference` - Reference letters

**Example:**
```json
"summary": "Experienced **Software Engineer** with expertise in *cloud technologies* and [open source](https://github.com) development."
```

**Note:** ATS systems typically extract plain text only, so markdown formatting is primarily for human-readable HTML/PDF output. The raw text remains readable even without markdown processing.

## Interactive Features

### Expand/Collapse of sections

- Click ✏️ to toggle edit mode
- Click + to expand collapsed sections
- Click - to collapse expanded sections
- State is preserved during page interactions - it holds until you close the browser tab.
- Visual feedback with animations and opacity changes

### Print Optimization
- Professional layout with high-quality typography (11pt base, 1.5 line height)
- Proper page margins (0.5 inch) to prevent content cut-off
- High-contrast black text and dark borders for excellent print visibility
- URLs displayed in parentheses for external links
- Smart page break controls to prevent awkward breaks
- Clean formatting optimized for ATS systems and professional printing
- Responsive column layouts that adapt to print
- Works with both Letter (US) and A4 (International) paper sizes

## PDF Download Options

**Enhanced PDF (Default):** One-click PDF downloads with pixel-perfect formatting
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

## Technologies used

- **Vanilla JavaScript** - No frameworks, pure ES6+ code
- **CSS Grid & Flexbox** - Modern responsive layouts
- **CSS Variables** - Consistent theming and easy customization
- **JSON Resume Schema** - Industry standard data format
- **Object State Management** - Robust expand/collapse state tracking
- **Print CSS** - Specialized styles for professional print output

The resulting HTML does don't have a backend, and can be placed on static sites, or be attachments in email. The current generation 
of email tools may preview HTML pages without JavaScript turned on, though I wrote 
[about that needing to change previously](https://paulhammant.com/2014/01/30/its-time-for-email-apps-to-support-javascript/)

## Architecture

- **Single-File Design** - Each CV is self-contained with embedded JSON data
- **Schema Validation** - All data follows JSON Resume v1.0.0 specification
- **State Management** - Object-based state storage separate from DOM
- **Responsive Breakpoints** - Mobile-first design with tablet and desktop optimizations
- **Print Media Queries** - Specialized print layouts with URL display

## Safety

**For Recruiters/HR receiving .html files:**
- These CV/Resume files contain only vanilla JavaScript for rendering and print functionality
- No external network requests are made (except for optional PDF generation CDN libraries)
- All data is embedded as JSON within the HTML file itself
- Safe to open in up-to-date browsers with standard security settings (Javascript can't interact with the PC's file system or OS)
- Professional ATS tools would verify or wholly replace the inline JavaScript
- The JSON data can be extracted programmatically without executing JavaScript

## For Applicants creating CV/Resume files

You're going to be savvy with text editing tools, and JSON as a format - that's the human price of this tech.

- Edit the JSON inside the .html file if you like, or externally first then copy it in.
- Test print/PDF output before sending to ensure professional appearance
- Use descriptive filenames like "FirstName_LastName_Resume.html"

If you're sticking with the .html file as your canonical CV/resume, you're likely going to keep editing it in there, which isn't anywhere 
near as pleasant as editing a Word or Google doc.

### Converting from Word/PDF to HTML Resume

If you have an existing resume in Word or PDF format, you can use AI to help convert it. Here's a suggested prompt:

```
Please help me create an HTML resume using the JSON Resume format.

1. Take Lorem_Ipsum_Resume.html as the template
2. Read the app.js and style.css files 
3. Create a single self-contained HTML file by:
   - Inlining the CSS into a <style> tag in the <head>
   - Inlining the JavaScript into a <script> tag at the bottom
   - Replacing the Lorem Ipsum JSON data with actual content from my resume - details in My_Resume.docx
4. Extract all relevant information from my resume document and format it according to the JSON Resume schema
5. Name the output file: FirstName_LastName_Resume.html (or _CV.html for international format)

Important: Make sure to preserve all dates, URLs, and contact information exactly as they appear in my original resume.
```

**Note:** The Lorem_Ipsum_Resume.html file serves as a complete example showing every field in the JSON Resume schema with placeholder content.

## License

MIT - Use freely for your own CVs/Resumes!

## Credits

This project demonstrates the modernization of Colin Cook's [XML/XSLT-based CV system](https://github.com/colinccook/cv) 
into a responsive, interactive single-page application using vanilla JavaScript. The "Donald Duck" resume data and rendered HTML of the same 
were the starting point, but hours after starting I discovered the excellent JSON-Resume technology so pivoted to that schema rather than an AI 
inferred one from Donald Duck's resume (featured in Colin Cook's final version).
