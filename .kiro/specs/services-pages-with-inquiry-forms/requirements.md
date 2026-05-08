# Requirements Document

## Introduction

This document specifies the requirements for adding Avecas services to the Rycene VLSI website. The feature will introduce a Services section with dedicated pages for each service category, complete with marketing content and inquiry forms. The implementation will follow the existing single-page application (SPA) architecture using view switching, glassmorphism design, and dark theme aesthetics.

## Glossary

- **SPA (Single-Page Application)**: A web application that dynamically rewrites the current page rather than loading entire new pages from the server
- **View**: A distinct section of the SPA that can be shown or hidden using the view switching mechanism
- **Service_Category**: A top-level service offering (e.g., Semiconductor Design, Embedded Solutions)
- **Service_Page**: A dedicated view displaying marketing content and inquiry form for a specific service category
- **Inquiry_Form**: A web form allowing users to request information about a specific service
- **Success_Popup**: A modal dialog displayed after successful form submission
- **View_Switcher**: The JavaScript function (`switchView`) that manages navigation between different views
- **Glassmorphism**: A design style using frosted glass effects with backdrop blur and transparency
- **Services_Navigation**: The navigation UI element that provides access to all service categories
- **Form_Field**: An individual input element within the inquiry form (text input, email, textarea, etc.)
- **Demo_Mode**: A non-production state where forms display success messages without actual data submission

## Requirements

### Requirement 1: Services Navigation Section

**User Story:** As a website visitor, I want to access different service categories from a navigation section, so that I can explore the services offered by Avecas.

#### Acceptance Criteria

1. THE Website SHALL display a Services navigation section in the main navigation area
2. THE Services_Navigation SHALL include links or buttons for all seven service categories: Semiconductor Design, Embedded Solutions, Software Solutions, Product Engineering Services, Staffing & Resource Augmentation, Consulting & Advisory, and Training & Skill Development
3. WHEN a user clicks on a service category link, THE View_Switcher SHALL navigate to the corresponding Service_Page
4. THE Services_Navigation SHALL follow the existing glassmorphism design pattern with dark theme styling
5. THE Services_Navigation SHALL be responsive and accessible on mobile devices

### Requirement 2: Service Page Views

**User Story:** As a website visitor, I want to view detailed information about each service category, so that I can understand what services are available and how they can benefit me.

#### Acceptance Criteria

1. THE Website SHALL create seven distinct Service_Page views, one for each service category
2. WHEN a Service_Page is displayed, THE View_Switcher SHALL hide all other views following the existing SPA pattern
3. THE Service_Page SHALL include a back navigation button that returns to the home view
4. THE Service_Page SHALL display marketing content describing the specific service category
5. THE Service_Page SHALL follow the existing design system including glassmorphism effects, dark theme, and animated backgrounds
6. THE Service_Page SHALL be responsive and render correctly on mobile, tablet, and desktop devices
7. THE Service_Page SHALL use the existing CSS classes and styling patterns (glass-card, btn-glass, etc.)

### Requirement 3: Service Marketing Content

**User Story:** As a website visitor, I want to read compelling marketing content about each service, so that I can make informed decisions about which services meet my needs.

#### Acceptance Criteria

1. THE Service_Page SHALL display a service title using the existing typography scale (text-3xl or larger)
2. THE Service_Page SHALL include a service description explaining the value proposition
3. WHERE a service category has sub-categories (e.g., Semiconductor Design has Front-End Design, Back-End Design, etc.), THE Service_Page SHALL list and describe each sub-category
4. THE Service_Page SHALL use the existing interactive-text-block or glass-card components for content presentation
5. THE Service_Page SHALL include relevant icons or visual elements consistent with the existing design
6. THE Service_Page SHALL maintain readability with appropriate text contrast and spacing

### Requirement 4: Inquiry Form Structure

**User Story:** As a potential customer, I want to submit an inquiry about a service, so that I can request more information or discuss my project needs.

#### Acceptance Criteria

1. THE Service_Page SHALL include an Inquiry_Form below the marketing content
2. THE Inquiry_Form SHALL include the following Form_Fields: Full Name (text input), Email Address (email input), Phone Number (text input), Company Name (text input), and Message (textarea)
3. THE Inquiry_Form SHALL display a form title indicating it is for the specific service category
4. THE Inquiry_Form SHALL use the existing form-input CSS class for consistent styling
5. THE Inquiry_Form SHALL include a submit button styled with the btn-glass-primary class
6. THE Inquiry_Form SHALL mark required fields with visual indicators (asterisk or label text)
7. THE Inquiry_Form SHALL follow the existing glassmorphism form design pattern

### Requirement 5: Form Validation

**User Story:** As a potential customer, I want the form to validate my input, so that I can correct any errors before submission.

#### Acceptance Criteria

1. WHEN a user submits the Inquiry_Form with empty required fields, THE Inquiry_Form SHALL display validation error messages
2. WHEN a user enters an invalid email format, THE Inquiry_Form SHALL display an email validation error message
3. THE Inquiry_Form SHALL use HTML5 validation attributes (required, type="email") for client-side validation
4. THE Inquiry_Form SHALL prevent form submission when validation fails
5. THE Inquiry_Form SHALL provide clear, user-friendly error messages
6. WHEN validation errors occur, THE Inquiry_Form SHALL maintain the user's entered data

### Requirement 6: Form Submission in Demo Mode

**User Story:** As a website visitor, I want to see a success confirmation when I submit an inquiry form, so that I know my request was received (demo mode).

#### Acceptance Criteria

1. WHEN a user submits a valid Inquiry_Form in Demo_Mode, THE Website SHALL display a Success_Popup
2. THE Inquiry_Form SHALL NOT send data to Google Sheets or any external service in Demo_Mode
3. THE Inquiry_Form SHALL simulate a successful submission with a brief delay (e.g., 500-1000ms) to mimic network request
4. WHEN the form is submitting, THE Inquiry_Form SHALL display a loading indicator on the submit button
5. WHEN the form is submitting, THE Inquiry_Form SHALL disable the submit button to prevent duplicate submissions

### Requirement 7: Success Popup Display

**User Story:** As a website visitor, I want to see a clear success message after submitting an inquiry, so that I have confirmation that my request was received.

#### Acceptance Criteria

1. THE Success_Popup SHALL appear as a modal overlay centered on the screen
2. THE Success_Popup SHALL display a success message thanking the user for their inquiry
3. THE Success_Popup SHALL include the service category name in the success message
4. THE Success_Popup SHALL include a close button to dismiss the popup
5. THE Success_Popup SHALL follow the existing modal design pattern with glassmorphism styling
6. WHEN the Success_Popup is displayed, THE Website SHALL prevent background scrolling
7. WHEN the user clicks the close button, THE Success_Popup SHALL hide and reset the Inquiry_Form

### Requirement 8: Success Popup Interaction

**User Story:** As a website visitor, I want to easily close the success popup, so that I can continue browsing the website.

#### Acceptance Criteria

1. WHEN a user clicks the close button, THE Success_Popup SHALL hide with a smooth fade-out transition
2. WHEN a user clicks outside the Success_Popup content area (on the backdrop), THE Success_Popup SHALL hide
3. WHEN a user presses the Escape key, THE Success_Popup SHALL hide
4. WHEN the Success_Popup closes, THE Inquiry_Form SHALL reset all Form_Fields to empty values
5. WHEN the Success_Popup closes, THE Website SHALL restore background scrolling

### Requirement 9: View Switching Integration

**User Story:** As a website visitor, I want seamless navigation between service pages and other website sections, so that I can easily explore the entire website.

#### Acceptance Criteria

1. THE View_Switcher SHALL register all seven Service_Page views in the existing view management system
2. WHEN a Service_Page is activated, THE View_Switcher SHALL add the view ID to the browser history
3. WHEN a user uses browser back/forward buttons, THE View_Switcher SHALL navigate to the appropriate Service_Page
4. THE View_Switcher SHALL scroll to the top of the page when switching to a Service_Page
5. THE View_Switcher SHALL close any open mobile navigation menus when switching views
6. THE View_Switcher SHALL maintain the existing view switching behavior for all other views (home, details, enroll, contact, privacy, terms, refund)

### Requirement 10: Responsive Design

**User Story:** As a mobile user, I want the service pages and inquiry forms to work well on my device, so that I can access services information on any screen size.

#### Acceptance Criteria

1. WHEN the viewport width is less than 768px, THE Service_Page SHALL display content in a single column layout
2. WHEN the viewport width is less than 768px, THE Inquiry_Form SHALL stack Form_Fields vertically with full width
3. WHEN the viewport width is less than 768px, THE Services_Navigation SHALL adapt to mobile navigation patterns (hamburger menu or dropdown)
4. THE Service_Page SHALL use responsive typography that scales appropriately for mobile devices
5. THE Success_Popup SHALL be responsive and display correctly on mobile devices
6. THE Service_Page SHALL maintain touch-friendly button sizes (minimum 44x44px) on mobile devices

### Requirement 11: Performance and Animations

**User Story:** As a website visitor, I want smooth animations and fast page transitions, so that I have a pleasant browsing experience.

#### Acceptance Criteria

1. WHEN switching to a Service_Page, THE View_Switcher SHALL complete the transition within 300ms
2. THE Service_Page SHALL use CSS transitions for hover effects on buttons and cards
3. THE Service_Page SHALL apply the existing animation libraries (GSAP, AOS) for content entrance animations
4. THE Service_Page SHALL optimize animations for mobile devices to maintain 60fps performance
5. THE Success_Popup SHALL animate in with a fade and scale effect
6. THE Success_Popup SHALL animate out with a fade effect when closing

### Requirement 12: Accessibility

**User Story:** As a user with accessibility needs, I want the service pages and forms to be accessible, so that I can navigate and use them with assistive technologies.

#### Acceptance Criteria

1. THE Service_Page SHALL use semantic HTML elements (header, main, section, form, button)
2. THE Inquiry_Form SHALL associate labels with Form_Fields using for/id attributes or aria-label
3. THE Success_Popup SHALL trap keyboard focus within the modal when open
4. THE Success_Popup SHALL return focus to the triggering element when closed
5. THE Service_Page SHALL provide sufficient color contrast (WCAG AA minimum) for all text
6. THE Services_Navigation SHALL be keyboard navigable with visible focus indicators
7. THE Inquiry_Form SHALL provide error messages that are announced to screen readers

### Requirement 13: Service Category Content Specification

**User Story:** As a content manager, I want clear specifications for each service category's content, so that I can ensure all required information is included.

#### Acceptance Criteria

1. THE Semiconductor_Design Service_Page SHALL include content for seven sub-categories: Front-End Design, Back-End Design, Analog Design, Design for Testability (DFT), IP & SoC Design Services, EDA & CAD Services, and Post-Silicon & Technology Engineering
2. THE Embedded_Solutions Service_Page SHALL include content for four sub-categories: Embedded Hardware, Embedded Software, Verification & Validation, and Edge AI & DSP
3. THE Software_Solutions Service_Page SHALL include content for Web & Mobile App Development services
4. THE Product_Engineering_Services Service_Page SHALL include content for PoC Development, Prototype to Production, Cost & Performance Optimization, Product Lifecycle Management, and Sustenance & Maintenance Engineering
5. THE Staffing_Resource_Augmentation Service_Page SHALL include content for Onsite & Offshore Resources, VLSI/Embedded/Software Consultants, Flexible Engagement Models, and Dedicated Offshore Development Centers
6. THE Consulting_Advisory Service_Page SHALL include content for Semiconductor & VLSI Consulting, Embedded Product Roadmap Planning, Digital Transformation & Cloud Advisory, Cost Optimization & Design Migration, and IP Licensing & Technology Partnerships
7. THE Training_Skill_Development Service_Page SHALL include content for VLSI Design & Verification Training, Embedded Systems & IoT Training, Software Development & AI/ML Training, Corporate Training Programs, and Internship & University Partnerships

### Requirement 14: Future Google Sheets Integration Preparation

**User Story:** As a developer, I want the inquiry forms structured to easily integrate with Google Sheets in the future, so that form submissions can be stored without major refactoring.

#### Acceptance Criteria

1. THE Inquiry_Form SHALL use a form element with a unique ID for each service category
2. THE Inquiry_Form SHALL include a hidden field indicating the service category name
3. THE Inquiry_Form SHALL structure Form_Fields with name attributes matching the expected Google Sheets column names
4. THE Inquiry_Form submission handler SHALL be implemented as a separate function that can be easily modified to add Google Sheets integration
5. THE Inquiry_Form submission handler SHALL include a placeholder for the Google Sheets script URL (commented out in Demo_Mode)
6. THE Inquiry_Form SHALL follow the same submission pattern as the existing enrollment form (using fetch API)

### Requirement 15: Error Handling

**User Story:** As a website visitor, I want clear feedback if something goes wrong with my form submission, so that I know what to do next.

#### Acceptance Criteria

1. IF the form submission fails in Demo_Mode (simulated error), THEN THE Website SHALL display an error message to the user
2. THE error message SHALL be displayed in a visually distinct style (e.g., red border or background)
3. THE error message SHALL provide actionable guidance (e.g., "Please try again" or "Check your connection")
4. WHEN an error occurs, THE Inquiry_Form SHALL re-enable the submit button
5. WHEN an error occurs, THE Inquiry_Form SHALL maintain the user's entered data
6. THE error message SHALL be accessible to screen readers
