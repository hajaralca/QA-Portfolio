# Test Plan: Wikipedia Search & Navigation (v1.0)

## 1. Executive Summary
The objective of this test cycle is to validate the core user journey of the Wikipedia web platform: **Discovery, Consumption, and Accessibility.** This plan covers the Search engine logic, Navigation stability, UI responsiveness, and Internationalization (i18n).

## 2. Scope of Testing
### 2.1 In-Scope
* **Search Module:** Functional, edge-case, and negative testing of search input and results.
* **Navigation:** Deep linking, history management, and anchor stability.
* **UI/UX:** Responsiveness, accessibility (WCAG AA), and visual integrity.
* **Internationalization:** Language switching and regional URL routing.

### 2.2 Out-of-Scope
* Article Editing/Editor Tools.
* User Account Management/Login.
* Backend Database Performance (unless affecting UI response).

## 3. Technical Strategy & Environment

### 3.1 Test Infrastructure
| Category | Specification |
| :--- | :--- |
| **Browsers** | Chrome (Latest), Firefox (Latest), Safari (macOS), Edge. |
| **Mobile Hardware** | **iOS:** iPhone 14 (Safari)<br>**Android:** Pixel 7, Samsung Galaxy A54. |
| **Mobile OS/Browsers**| Safari (iOS), Chrome (Android), Samsung Internet (Android) |
| **Viewports** | 320px–420px (Mobile), 768px (Tablet), 1920px (Desktop)|
| **Network Profiles** | 4G (Stable) and Throttled 3G (for latency testing). |
| **Accessibility Tools** | AXE DevTools, Screen Reader (NVDA/VoiceOver). |

### 3.2 Testing Levels
1.  **Smoke Testing:** Critical Search redirects and Mobile Responsiveness.
2.  **Functional Testing:** Execution of all 39 defined test cases.
3.  **Regression Testing:** Verification of Navigation stability after UI changes.

## 4. Prioritized Execution Modules

### Phase 1: Search & Redirect Logic (Highest Risk)
* **Objective:** Ensure users reach correct data regardless of input quality.
* **Key Focus:** Encoding (C++ -> `%2B%2B`), Diacritics (José), and Auto-suggest latency.
* **Critical Metric:** Search-to-Article redirect accuracy.

### Phase 2: Navigation & State Persistence
* **Objective:** Validate the "Web" nature of the app (Links and History).
* **Key Focus:** Broken link spot-checks and Browser Back/Forward stability.
* **Critical Metric:** Zero "404 Not Found" on internal routing.

### Phase 3: Accessibility (A11y) & UI
* **Objective:** Compliance with legal and usability standards.
* **Key Focus:** Keyboard Tab-order and Contrast ratios (WCAG 2.1 AA).
* **Critical Metric:** WCAG 2.1 AA Compliance status.

### Phase 4: Localization (i18n)
* **Objective:** Verify the multi-tenant architecture of language subdomains.
* **Key Focus:** URL domain switching (`en.` to `fr.`).

## 5. Risk Assessment & Mitigation

| Risk | Impact | Mitigation Strategy |
| :--- | :--- | :--- |
| **High Latency in Search** | High | Test search available immediately under throttled network conditions. |
| **Search Injection/XSS** | Critical | Use long input and special characters to monitor for script execution or 500 errors. |
| **Mobile Breakage** | High | Prioritize 320px viewport testing to ensure search bar remains accessible. |

## 6. Entry & Exit Criteria

### 6.1 Entry Criteria
* Build deployed to Staging environment.
* All Search API endpoints reachable.
* Test Data (Articles in various languages) is indexed.

### 6.2 Exit Criteria
* 100% of **Critical** and **High** priority cases passed.
* Zero "Blocker" or "Critical" defects remain open.
* Accessibility audit shows no "Critical" failures.
* All Redirect logic verified on both Desktop and Mobile.

## 7. Deliverables
* **Test Summary Report (TSR):** Pass/Fail ratios per module.
* **Defect Log:** Detailed reports including DOM snapshots and console logs.
* **Accessibility Statement:** Summary of WCAG AA compliance status.