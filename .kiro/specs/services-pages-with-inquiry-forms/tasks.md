# Implementation Plan: Services Pages with Inquiry Forms

## Overview

Add seven dedicated Avecas service pages to the existing `index.html` SPA. All changes are inline: new CSS in the `<style>` block, new HTML inside `<main>`, new JavaScript in the `<script>` block. The implementation follows the existing view-switching architecture, glassmorphism design system, and introduces a shared inquiry form handler with a single reusable success modal.

## Tasks

- [x] 1. Add CSS for services feature components
  - Insert the following new rule-sets into the existing `<style>` block (after the last existing rule):
    - `.services-dropdown-item` and its `:hover` state (dropdown link styling)
    - `.service-hero-icon` (64×64 rounded icon container for service hero sections)
    - `@keyframes modalScaleIn` and `.animate-modal-in` (success modal entrance animation)
    - `.inquiry-error-msg` (red-tinted error message box)
    - `.service-card-accent-cyan`, `.service-card-accent-purple`, `.service-card-accent-orange` (top border accent lines for sub-category cards)
  - _Requirements: 2.5, 2.7, 3.5, 7.5, 11.5, 15.2_

- [x] 2. Add `servicesData` array and shared JS functions
  - [x] 2.1 Define `const servicesData` array in the `<script>` block (before `DOMContentLoaded`)
    - Include all 7 service objects with `id`, `title`, `icon`, `description`, `accentColor`, and `subCategories` array
    - Semiconductor Design (cyan, 7 sub-categories per Req 13.1)
    - Embedded Solutions (purple, 4 sub-categories per Req 13.2)
    - Software Solutions (cyan, 1 sub-category per Req 13.3)
    - Product Engineering Services (orange, 5 sub-categories per Req 13.4)
    - Staffing & Resource Augmentation (purple, 4 sub-categories per Req 13.5)
    - Consulting & Advisory (cyan, 5 sub-categories per Req 13.6)
    - Training & Skill Development (orange, 5 sub-categories per Req 13.7)
    - _Requirements: 13.1, 13.2, 13.3, 13.4, 13.5, 13.6, 13.7_

  - [x] 2.2 Implement `window.serviceInquirySubmit(formId, serviceName)` function
    - Call `form.checkValidity()` / `form.reportValidity()` for early exit on invalid input
    - Capture original button text, set `disabled = true` and spinner HTML (loading state)
    - In demo mode: `setTimeout(800ms)` → call `showServiceSuccessModal(serviceName)`, `form.reset()`, restore button
    - Include commented-out production `fetch` block with `scriptURL` placeholder and `.catch(() => showServiceErrorMessage(formId))`
    - _Requirements: 5.1, 5.2, 5.3, 5.4, 6.1, 6.2, 6.3, 6.4, 6.5, 14.4, 14.5, 14.6_

  - [ ]* 2.3 Write property test: submit button enters loading state (Property 9)
    - **Property 9: Submit button enters loading state during submission**
    - **Validates: Requirements 6.4, 6.5**
    - Use `fc.constantFrom(...servicesData)` — for any service form with valid data, immediately after `serviceInquirySubmit` is called the submit button must be `disabled` and contain a loading indicator

  - [x] 2.4 Implement `showServiceSuccessModal(serviceName)` function
    - Set `#service-modal-service-name` text content to `"Service: " + serviceName`
    - Remove `hidden` class from `#service-inquiry-modal`
    - Set `document.body.style.overflow = 'hidden'`
    - _Requirements: 7.1, 7.2, 7.3, 7.6_

  - [ ]* 2.5 Write property test: success modal shows correct service name (Property 7)
    - **Property 7: Success modal shows correct service name**
    - **Validates: Requirements 7.2, 7.3**
    - Use `fc.string({ minLength: 1 })` — for any service name string, after `showServiceSuccessModal(name)` the modal must not have `hidden` class and `#service-modal-service-name` text must include the name

  - [x] 2.6 Implement `showServiceErrorMessage(formId)` function
    - Find or create `.inquiry-error-msg` div inside the form
    - Set `role="alert"` and error text
    - Remove `hidden` class from the error element
    - _Requirements: 15.1, 15.2, 15.3, 15.6_

- [x] 3. Update `allViews` array in `switchView()` to include all 7 service view IDs
  - Locate the `allViews` array inside `switchView` and append:
    `'semiconductor-design', 'embedded-solutions', 'software-solutions', 'product-engineering', 'staffing-augmentation', 'consulting-advisory', 'training-development'`
  - Ensure the view IDs match the `id` attribute format used in the HTML divs (`view-{id}`)
  - _Requirements: 9.1, 9.4, 9.6_

  - [ ]* 3.1 Write property test: view exclusivity on navigation (Property 1)
    - **Property 1: View exclusivity on navigation**
    - **Validates: Requirements 2.2, 9.1**
    - Use `fc.constantFrom(...servicesData.map(s => s.id))` — after `switchView(service.id)`, `#view-{service.id}` must not have `hidden-view` class and every other view in `allViews` must have `hidden-view` class

- [x] 4. Add Services dropdown to desktop navigation
  - Insert a `<div class="relative group" id="services-nav-wrapper">` containing the `#services-nav-btn` button and `#services-dropdown` panel between the "Team & Mission" nav button and the "Contact Us" button in the desktop `<nav>`
  - The dropdown panel uses `class="hidden group-hover:block absolute ..."` with `aria-haspopup="true"` on the trigger button
  - Leave the dropdown panel body empty — it will be populated by JS on `DOMContentLoaded`
  - _Requirements: 1.1, 1.2, 1.4, 12.6_

- [x] 5. Add Services collapsible section to mobile navigation
  - Inside `#mobile-dropdown`, add a `<div>` containing `#services-mobile-toggle` button and `#services-mobile-submenu` (initially `hidden`)
  - The toggle button shows a chevron icon (`#services-mobile-chevron`) that rotates when expanded
  - Leave the submenu body empty — it will be populated by JS on `DOMContentLoaded`
  - _Requirements: 1.1, 1.2, 1.5, 10.3_

- [x] 6. Add all 7 service page view HTML divs inside `<main>`
  - Place each div after the existing `#view-refund` div and before `</main>`
  - Each div: `<div id="view-{id}" class="hidden-view pt-24 pb-12 min-h-screen">`
  - Each view contains (in order):
    1. Back to Home button: `onclick="switchView('home')"` styled with `btn-glass btn-glass-secondary`
    2. Service hero section: `.service-hero-icon` with the service's Font Awesome icon, `<h1>` with `text-3d-steel` class, description paragraph
    3. Sub-categories grid: `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6` of `glass-card` divs, each with `.service-card-accent-{color}` top border, icon, title, and description
    4. Inquiry form section: heading "Get in Touch — {Service Title}", then `<form id="inquiry-{id}">` with all required fields (see field spec in design), submit button calling `serviceInquirySubmit('inquiry-{id}', '{title}')`
  - Include `input[type="hidden"][name="service"]` pre-filled with the service title in each form
  - Mark required fields (`fullName`, `email`, `message`) with `required` attribute and `<span class="text-red-400 ml-1">*</span>` in labels
  - Use `for`/`id` attribute pairs on all `<label>` / `<input>` pairs
  - _Requirements: 2.1, 2.3, 2.4, 2.5, 2.6, 2.7, 3.1, 3.2, 3.3, 3.4, 3.5, 4.1, 4.2, 4.3, 4.4, 4.5, 4.6, 4.7, 5.3, 12.1, 12.2, 14.1, 14.2, 14.3_

  - [ ]* 6.1 Write property test: service page renders title and description (Property 3)
    - **Property 3: Service page renders title and description**
    - **Validates: Requirements 3.1, 3.2**
    - Use `fc.constantFrom(...servicesData)` — for any service, the corresponding view element must contain the service's `title` and `description` text in its innerHTML

  - [ ]* 6.2 Write property test: all sub-categories are rendered (Property 4)
    - **Property 4: All sub-categories are rendered**
    - **Validates: Requirements 3.3, 13.1–13.7**
    - Use `fc.constantFrom(...servicesData.filter(s => s.subCategories.length > 0))` — every sub-category `title` must appear in the corresponding view element's innerHTML

  - [ ]* 6.3 Write property test: inquiry form fields are present for every service (Property 5)
    - **Property 5: Inquiry form fields are present for every service**
    - **Validates: Requirements 4.1, 4.2, 14.1–14.3**
    - Use `fc.constantFrom(...servicesData)` — `#inquiry-{id}` must contain `input[type="text"][name="fullName"]`, `input[type="email"][name="email"]`, `input[name="phone"]`, `input[name="company"]`, `textarea[name="message"]`, and `input[type="hidden"][name="service"]` with value equal to the service title

  - [ ]* 6.4 Write property test: form title includes service name (Property 6)
    - **Property 6: Form title includes service name**
    - **Validates: Requirements 4.3**
    - Use `fc.constantFrom(...servicesData)` — the inquiry form section heading within `#view-{id}` must contain the service's `title` string

  - [ ]* 6.5 Write property test: back button navigates home (Property 2)
    - **Property 2: Back button navigates home**
    - **Validates: Requirements 2.3**
    - Use `fc.constantFrom(...servicesData)` — each service view must contain at least one button/link that calls `switchView('home')`, resulting in `#view-home` visible and `#view-{id}` hidden

- [x] 7. Add shared success modal HTML (`#service-inquiry-modal`)
  - Insert the modal div after the last existing modal element and before `</body>`
  - Structure: outer `div.modal.hidden` → `.modal-backdrop` + inner content panel with `.animate-modal-in`
  - Inner panel contains: green check icon circle, "Thank You!" heading, static text, `#service-modal-service-name` paragraph (populated by JS), response time note, and `.modal-close-btn` button
  - _Requirements: 7.1, 7.4, 7.5, 8.1, 11.5_

- [x] 8. Checkpoint — verify static structure
  - Ensure all 7 `#view-{id}` divs are present in the DOM
  - Ensure `#service-inquiry-modal` is present
  - Ensure `#services-nav-wrapper` and `#services-mobile-toggle` are present
  - Ensure all 7 form IDs (`inquiry-semiconductor-design`, etc.) exist
  - Ask the user if any questions arise before proceeding.

- [x] 9. Wire up navigation and modal interactions on `DOMContentLoaded`
  - [x] 9.1 Populate desktop dropdown and mobile submenu from `servicesData`
    - Iterate `servicesData`, create a `<button class="services-dropdown-item">` per service for `#services-dropdown`
    - Each button calls `switchView(service.id)` and closes the mobile menu if open
    - Duplicate the same buttons into `#services-mobile-submenu`
    - _Requirements: 1.2, 1.3, 9.5_

  - [x] 9.2 Wire mobile services submenu toggle
    - Add click listener to `#services-mobile-toggle`
    - Toggle `hidden` class on `#services-mobile-submenu`
    - Toggle `rotate-180` class on `#services-mobile-chevron`
    - _Requirements: 1.5, 10.3_

  - [x] 9.3 Wire modal close interactions for `#service-inquiry-modal`
    - Add click listener to `.modal-close-btn` inside the modal: add `hidden` class, restore `document.body.style.overflow`
    - Add click listener to `.modal-backdrop` inside the modal: same close behavior
    - Add `keydown` listener for `Escape` key: close modal if it is currently visible
    - After closing, reset the inquiry form that was last submitted (track via a module-level variable set in `serviceInquirySubmit`)
    - _Requirements: 7.7, 8.1, 8.2, 8.3, 8.4, 8.5, 12.3, 12.4_

  - [ ]* 9.4 Write property test: modal close resets form and restores scroll (Property 8)
    - **Property 8: Modal close resets form and restores scroll**
    - **Validates: Requirements 8.1, 8.2, 8.4, 8.5**
    - Use `fc.constantFrom(...servicesData)` — after the close action is triggered, `#service-inquiry-modal` must have `hidden` class, `document.body.style.overflow` must not be `"hidden"`, and all input/textarea values in the associated form must be empty strings

- [x] 10. Final checkpoint — end-to-end validation
  - Verify the HTML file is valid (no unclosed tags introduced by the new additions)
  - Verify all 7 service views are reachable via `switchView` and the nav dropdown
  - Verify the inquiry form demo flow: fill required fields → submit → loading state → success modal → close → form reset
  - Verify mobile layout: services submenu expands/collapses, single-column sub-category grid at 375px
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional and can be skipped for a faster MVP
- All code changes go inline into `index.html` — no new files are created
- The `servicesData` array is the single source of truth for both navigation and page content
- Property tests use **fast-check** with **Jest + jsdom**; run with `jest --testPathPattern=services`
- The Google Sheets `fetch` call is present but commented out; activating it requires only replacing `scriptURL` and uncommenting the block in `serviceInquirySubmit`
- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation before wiring everything together
