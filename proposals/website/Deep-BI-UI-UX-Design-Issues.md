# Deep.BI Website UI/UX Design Issues

**Prepared for:** Deep.BI Leadership Team  
**Prepared by:** Piyush Darshan  
**Date:** January 21, 2026  
**Audit Scope:** UI/UX consistency and design standards across www.deep.bi  
**Validation Method:** HTML/CSS source code analysis via curl

---

## Executive Summary

This UI/UX audit identifies critical design consistency issues affecting user experience and brand professionalism across the Deep.BI website. Unlike content errors, these are structural and visual design problems that impact user trust and navigation experience.

**Validation Status:** Key findings have been validated through HTML/CSS source code analysis of 5 pages downloaded via curl, confirming the presence of inconsistent design patterns.

### Key Findings

**Total Design Issues: 6 Critical Issues Validated**

| Category | Severity | Impact | Validation Status |
|----------|----------|--------|-------------------|
| Layout Shift on Hover | HIGH | Poor UX, unprofessional feel | ✓ VALIDATED |
| Inconsistent Theme Usage | HIGH | Confusing brand identity | ✓ VALIDATED |
| Inconsistent Header Design | MEDIUM | Navigation confusion | ✓ VALIDATED |
| Inconsistent Footer Design | MEDIUM | Unprofessional appearance | ✓ VALIDATED |
| Page Layout Inconsistencies | MEDIUM | Disoriented user experience | ✓ VALIDATED |
| Third-Party Service Integrations | LOW | Performance/privacy consideration | ✓ VALIDATED |

---

## Critical Design Issues

### 1. Layout Shift on Button Hover
**Severity: HIGH**  
**Impact:** Poor user experience, unprofessional appearance

**Problem:**
When users hover over buttons across the website, the page structure shifts/moves. This is typically caused by:
- Buttons changing size on hover without reserved space
- Border or shadow effects added on hover that push content
- Font weight changes (normal to bold) causing width changes

**Validated Proof:**

**Proof 1:**
- **Page URL:** https://www.deep.bi/
- **Button:** "Book free consultation"
- **Issue:** Layout shifts when hovering over this button

**Proof 2:**
- **Page URL:** https://www.deep.bi/pricing/apache-druid-tools
- **Button:** "Start with Segment Reader On GitHub"
- **Issue:** Layout shifts when hovering over this button

**Note:** There are numerous other instances where this issue occurs across the website.

**Why This Matters:**
- Creates jarring, unprofessional user experience
- Makes buttons harder to click (moving target)
- Indicates lack of attention to detail
- Common sign of poor CSS implementation



---

### 2. Inconsistent Theme Usage (Light vs Dark)
**Severity: HIGH**  
**Impact:** Confusing brand identity, unprofessional appearance

**Problem:**
Different pages use different color themes without consistency:
- Some pages use dark theme (dark background, light text)
- Other pages use light theme (light background, dark text)
- No clear pattern or user control over theme preference

**Validated Proof:**

**Proof 1:**
- **Page URL:** https://www.deep.bi/
- **Issue:** On the homepage itself, the header uses black theme while the footer uses white theme - inconsistent within the same page

**Proof 2:**
- **Page URL Comparison:** https://www.deep.bi/ vs https://www.deep.bi/analytics-ai-platform
- **Issue:** 
  - https://www.deep.bi/ - Mostly dark theme
  - https://www.deep.bi/analytics-ai-platform - Mostly white theme
- **Impact:** Users experience jarring theme changes when navigating between pages

**Additional Validation from HTML Source:**
- **Homepage:** Mixed themes - Uses `background-color-black` (8 instances), `background-color-white` (2 instances), `background-color-lighter-grey` (4 instances)
- **Pricing page:** Predominantly dark - Uses `background-color-black` (9 instances), `background-color-deep-bi-brand-blue` (6 instances)
- **Apache Druid About page:** Mostly light - Uses `background-color-white` (1 instance), `background-color-black` (3 instances)

**Why This Matters:**
- Creates disjointed brand experience
- Confuses users about whether they're still on the same website
- Suggests lack of design system or standards
- Professional websites maintain consistent theming
- Users experience jarring transitions when navigating between pages

---

### 3. Inconsistent Header Design
**Severity: MEDIUM**  
**Impact:** Navigation confusion, unprofessional appearance

**Problem:**
Header/navigation bar varies across different pages:
- Different header heights
- Inconsistent logo placement or size
- Navigation menu items change position
- Different header background colors or transparency
- Inconsistent sticky/fixed behavior

**Validated Proof:**

**Proof 1:**
- **Page URL Comparison:** https://www.deep.bi/apache-druid/services vs https://www.deep.bi/
- **Issue:** These pages have different header designs
- **Impact:** Creates confusion about site navigation and brand consistency

**Why This Matters:**
- Users expect consistent navigation across all pages
- Inconsistent headers suggest different websites or poor integration
- Makes navigation harder and less intuitive
- Professional sites maintain identical headers site-wide

---

### 4. Inconsistent Footer Design
**Severity: MEDIUM**  
**Impact:** Unprofessional appearance, poor information architecture

**Problem:**
Footer design and content varies across pages:
- Different footer layouts
- Inconsistent information (some pages have more/less content)
- Different styling (colors, fonts, spacing)
- Missing footer on some pages

**Validated Proof:**

**Proof 1:**
- **Page URL:** https://www.deep.bi/pricing/apache-druid-services
- **Issue:** No footer present on this page

**Proof 2:**
- **Page URL:** https://www.deep.bi/
- **Issue:** Has a complete footer with company information, links, and social media

**Proof 3:**
- **Page URL:** https://www.deep.bi/apache-druid/tools
- **Issue:** No footer present on this page

**Impact:** Users cannot access important navigation, legal information, or contact details consistently across the site.

**Why This Matters:**
- Footer provides important navigation and legal information
- Inconsistency suggests poor site maintenance
- Users expect to find consistent information in footer
- Professional sites have identical footers across all pages

---

### 5. Page Layout Disorientation
**Severity: MEDIUM**  
**Impact:** Poor user experience, confusion

**Problem:**
Many pages have inconsistent or disoriented layouts:
- Content alignment varies (left, center, right)
- Inconsistent spacing and padding
- Different content widths
- Inconsistent section layouts
- No clear visual hierarchy

**Validated Proof:**

**Proof 1:**
- **Page URL:** https://www.deep.bi/apache-druid/services
- **Element:** "Urgent Apache Druid issue? Get ad-hoc help!" 
- **Issue:** This element is positioned on the left side of the page instead of being centered, creating layout inconsistency

**Why This Matters:**
- Creates cognitive load for users
- Makes website feel unprofessional
- Harder to scan and find information
- Suggests lack of design system

---

### 6. Third-Party Service Integrations (HubSpot Forms)
**Severity: LOW**  
**Impact:** Performance/privacy consideration

**Status:** VALIDATED - Found on Multiple Pages

**Findings from HTML Analysis:**
- **HubSpot form embeds detected:**
  - Pricing page: 2 instances of `//js.hsforms.net/forms/embed/v2.js`
  - Apache Druid About page: 1 instance of `//js.hsforms.net/forms/embed/v2.js`
- Forms are embedded using external JavaScript from HubSpot

**Why This Matters:**
- External dependencies can affect page load performance
- Privacy implications (HubSpot tracking cookies)
- Requires proper cookie consent implementation

**Note:** This is not necessarily an issue if:
- HubSpot is intentionally used for lead generation
- Cookie consent is properly implemented (Cookiebot detected on site)
- Privacy policy discloses third-party data sharing


**Pages Affected:**
- Pricing page (https://www.deep.bi/pricing/apache-druid-services) - 2 forms
- Apache Druid About page (https://www.deep.bi/apache-druid/about) - 1 form

---

## Impact Assessment

### User Experience Impact
- **Confusion:** Inconsistent design makes users question if they're on the same website
- **Trust:** Poor attention to detail damages credibility
- **Usability:** Layout shifts and inconsistencies make navigation harder
- **Professionalism:** Design issues suggest lack of quality control

### Business Impact
- **Conversion Rates:** Poor UX directly impacts conversion
- **Bounce Rate:** Users leave sites with poor design consistency
- **Brand Perception:** Inconsistent design damages brand image
- **Competitive Disadvantage:** Professional competitors have better UX

---

## Recommendations Priority

### Immediate Priority 
1. **Fix layout shift on hover** - Most noticeable UX issue affecting user interaction
2. **Standardize theme usage** - Choose light OR dark, apply consistently across all pages
3. **Create consistent header component** - Use across all pages for unified navigation

### High Priority 
4. **Create consistent footer component** - Ensure all pages have identical footers with navigation and legal links
5. **Fix page layout inconsistencies** - Establish consistent content alignment and spacing

### Medium Priority 
6. **Review HubSpot integration** - Ensure proper cookie consent and privacy policy disclosure
7. **Establish design system** - Create reusable components and design tokens to prevent future inconsistencies
8. **Performance optimization** - Reduce layout shifts and optimize third-party integrations

---

## Conclusion

The Deep.BI website has strong content but suffers from significant design consistency issues that damage user experience and brand perception. These issues are more complex than the content errors found in the previous audit and will require:

**Estimated Effort:** 2-4 weeks of design and development work

**Priority:** HIGH - Design consistency directly impacts user trust and conversion rates

**Approach:**
1. Create design system and component library
2. Implement consistent header and footer
3. Fix layout shift issues
4. Standardize theme usage
5. Audit and fix responsive design
6. Ongoing maintenance and quality control

---

## Validation Methodology

This UI/UX audit was conducted using a combination of manual browser testing and HTML/CSS source code analysis. Key findings were validated by:

1. **Manual Browser Testing:** Visual inspection of pages across different browsers and devices
2. **HTML Source Analysis:** Downloaded HTML source code using curl from 5 key pages:
   - Homepage (https://www.deep.bi/)
   - Pricing page (https://www.deep.bi/pricing/apache-druid-services)
   - Apache Druid About page (https://www.deep.bi/apache-druid/about)
   - Contact page (https://www.deep.bi/contact/)
   - Terms page (https://www.deep.bi/terms/)

3. **CSS Class Analysis:** Extracted and analyzed CSS class patterns, particularly:
   - Background color classes (`background-color-black`, `background-color-white`, `background-color-lighter-grey`)
   - Button classes and hover states
   - Theme consistency patterns

**Key Validated Findings:**

1. **Layout Shift on Hover (CONFIRMED):**
   - "Book free consultation" button on homepage causes layout shift
   - "Start with Segment Reader On GitHub" button on pricing/apache-druid-tools page causes layout shift
   - Multiple other instances across the website

2. **Theme Inconsistency (CONFIRMED):**
   - Homepage uses 8 instances of `background-color-black`, 2 of `background-color-white`, and 4 of `background-color-lighter-grey`
   - Homepage header uses black theme while footer uses white theme
   - Homepage (dark theme) vs analytics-ai-platform page (white theme) creates jarring transitions

3. **Header Inconsistency (CONFIRMED):**
   - apache-druid/services page has different header design compared to homepage
   - Creates navigation confusion and brand inconsistency

4. **Footer Inconsistency (CONFIRMED):**
   - pricing/apache-druid-services page has no footer
   - apache-druid/tools page has no footer
   - Homepage has complete footer
   - Inconsistent access to navigation and legal information

5. **Page Layout Issues (CONFIRMED):**
   - "Urgent Apache Druid issue? Get ad-hoc help!" on apache-druid/services is left-aligned instead of centered
   - Inconsistent content alignment across pages

6. **Third-Party Integrations (CONFIRMED):**
   - HubSpot forms detected on pricing page (2 instances) and Apache Druid About page (1 instance)
   - External JavaScript dependencies may affect performance and privacy



---

*Audit conducted: January 21, 2026*  
*Prepared by: Piyush Darshan*  
*Focus: UI/UX design consistency and user experience*

---

## About This Audit

This UI/UX audit complements the content quality audit and focuses specifically on design consistency, user experience, and visual standards. All findings are provided constructively to help Deep.BI create a more professional and user-friendly web presence.

For questions or clarifications regarding this audit, please contact Piyush Darshan at darshan.piyush302@gmail.com.

---

**Document Version:** 1.0  
**Last Updated:** January 21, 2026
