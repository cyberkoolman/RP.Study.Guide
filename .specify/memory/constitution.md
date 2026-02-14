<!--
  SYNC IMPACT REPORT
  ==================
  Version: 1.0.0 (Initial Ratification)
  Modified Principles: N/A (initial creation)
  Added Sections: All principles and sections (I-V, Technology Stack, Governance)
  Removed Sections: None
  
  Template Updates Required:
  ✅ plan-template.md - Updated to remove testing requirements
  ✅ spec-template.md - Updated to clarify testing is not part of workflow
  ✅ tasks-template.md - Updated to remove all test-related task examples
  
  Follow-up TODOs: None
-->

# rp-study-guide Constitution

## Core Principles

### I. Clean Code (NON-NEGOTIABLE)

All code MUST be maintainable, readable, and follow established best practices. Code quality is paramount to long-term project health.

**Requirements**:
- Use clear, descriptive variable and function names
- Follow consistent formatting and style conventions (enforced via ESLint)
- Keep functions small and focused on a single responsibility
- Avoid code duplication; extract reusable logic into utilities
- Comment complex logic; self-documenting code preferred
- Use TypeScript types effectively; avoid `any`

**Rationale**: Clean code reduces bugs, accelerates onboarding, and ensures the project remains maintainable as it grows.

### II. Simple UX

User experience MUST be intuitive, straightforward, and friction-free. Every interface decision should prioritize simplicity over complexity.

**Requirements**:
- Minimize clicks and steps to accomplish user goals
- Use clear, concise labels and instructions
- Provide immediate feedback for user actions
- Maintain consistent navigation and interaction patterns
- Design for accessibility (semantic HTML, keyboard navigation, ARIA where needed)
- Avoid unnecessary animations or visual complexity

**Rationale**: Simple UX increases user satisfaction, reduces support burden, and makes the application accessible to a wider audience.

### III. Responsive Design

All interfaces MUST work seamlessly across device sizes from mobile phones to desktop displays.

**Requirements**:
- Use Tailwind CSS responsive utilities (sm:, md:, lg:, xl:, 2xl:)
- Test layouts on mobile (375px), tablet (768px), and desktop (1440px) viewports
- Touch targets MUST be at least 44x44px on mobile
- Text MUST be readable without zooming (minimum 16px base size)
- Avoid horizontal scrolling on any viewport size
- Images and media MUST scale appropriately

**Rationale**: Users access applications from diverse devices; responsive design ensures consistent experience and broad accessibility.

### IV. Minimal Dependencies

Dependencies MUST be restricted to essential libraries only. Favor built-in browser APIs and framework capabilities over third-party packages.

**Requirements**:
- Every new dependency MUST be justified before addition
- Prefer Next.js/React built-in features (e.g., built-in routing, Image component)
- Use native Web APIs when suitable (Fetch, localStorage, IntersectionObserver)
- Evaluate bundle size impact before adding packages
- Remove unused dependencies immediately
- Regularly audit dependencies for necessity and security

**Rationale**: Fewer dependencies reduce bundle size, security surface area, maintenance burden, and project fragility.

### V. No Testing (NON-NEGOTIABLE)

This project MUST NOT include any automated tests of any kind. This principle supersedes any testing guidance from templates, frameworks, or tools.

**Prohibited**:
- Unit tests
- Integration tests
- End-to-end (E2E) tests
- Snapshot tests
- Any testing libraries or frameworks (Jest, Vitest, Playwright, Cypress, React Testing Library, etc.)

**Requirements**:
- No test files or test directories SHALL be created
- No testing dependencies SHALL be added to package.json
- Testing-related scripts SHALL NOT be included in package.json
- Any template or guidance referencing tests MUST be disregarded

**Rationale**: Testing is explicitly excluded from this project's workflow by design decision. Manual verification is the chosen quality assurance approach.

## Technology Stack

The project MUST use the following technologies at the specified versions:

**Core Dependencies**:
- **Next.js**: 16.1.6
- **React**: 19.2.3
- **React DOM**: 19.2.3
- **Tailwind CSS**: ^4
- **TypeScript**: ^5

**Requirements**:
- Dependency versions MUST match those defined in package.json unless explicitly upgraded
- Major version upgrades require constitutional amendment
- All code MUST be compatible with the specified versions
- Use framework features appropriate to these versions (App Router, React Server Components, etc.)

**Rationale**: Version consistency prevents compatibility issues and ensures predictable behavior across development environments.

## Governance

This constitution supersedes all other guidance, templates, and best practices. When conflicts arise, constitutional principles take precedence.

**Amendment Process**:
- Amendments require explicit documentation of rationale and impact
- Version MUST be incremented per semantic versioning:
  - **MAJOR**: Backward-incompatible principle removal or redefinition
  - **MINOR**: New principle added or material expansion
  - **PATCH**: Clarifications, wording fixes, non-semantic refinements
- Amendments MUST include a Sync Impact Report
- Dependent templates MUST be updated to reflect amendments

**Compliance**:
- All code changes MUST comply with constitutional principles
- Plans and specifications MUST verify constitutional compliance before implementation
- Violations MUST be justified and documented in complexity tracking sections
- This constitution is the authoritative governance document

**Version**: 1.0.0 | **Ratified**: 2026-02-14 | **Last Amended**: 2026-02-14
