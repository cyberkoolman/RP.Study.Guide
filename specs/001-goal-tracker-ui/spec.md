# Feature Specification: doit - Goal Tracking Web App

**Feature Branch**: `001-goal-tracker-ui`  
**Created**: 2026-02-14  
**Status**: Draft  
**Input**: User description: "initial page setup - this application should be a goal tracking web app called 'doit'. There should be two columns - a left one where current goals are shown, along with how many days left the user has to achieve the goal, and a right one where completed goals are. Each goal can be 'checked' using a checkbox, and then either moved to the completed column or permanently deleted. To add new goals, a user can click on a button to open a new goal form in a modal (title and end date fields). Goals reaching their end date (within 3 days) are highlighted. Let's use a modern light theme with fun pastel colours."

**⚠️ NOTE**: This project does not include automated testing. Acceptance scenarios below are for manual verification only.

## User Scenarios & Manual Verification *(mandatory)*

### User Story 1 - View Active Goals (Priority: P1)

Users need to see their active goals at a glance with clear visibility of how much time remains to achieve each goal.

**Why this priority**: This is the core value proposition of the app. Without the ability to view goals and their deadlines, the app provides no value. This is the foundational MVP feature.

**Independent Verification**: Open the app and verify active goals appear in the left column with goal titles and days remaining displayed clearly. Users should immediately understand their goal status without additional clicks.

**Acceptance Scenarios**:

1. **Given** the user has active goals, **When** they open the app, **Then** all active goals are displayed in the left column
2. **Given** an active goal has an end date, **When** the goal is displayed, **Then** the days remaining until the end date is shown next to the goal title
3. **Given** there are no active goals, **When** the user opens the app, **Then** an empty state with helpful guidance is shown in the left column
4. **Given** multiple active goals exist, **When** displayed, **Then** goals are ordered logically (by end date, showing most urgent first)

---

### User Story 2 - Add New Goals (Priority: P2)

Users need a simple way to create new goals with a title and target completion date.

**Why this priority**: After viewing goals, the next critical capability is creating them. Without this, users can't populate the system with their objectives. This completes the basic input functionality.

**Independent Verification**: Click the add goal button, fill out the modal form with a title and end date, submit, and verify the new goal appears in the active goals column with correct days remaining calculation.

**Acceptance Scenarios**:

1. **Given** the user is on the main page, **When** they click the "Add Goal" button, **Then** a modal opens with a form containing title and end date fields
2. **Given** the add goal modal is open, **When** the user enters a title and selects an end date, **Then** both fields accept input correctly
3. **Given** the user has filled the form, **When** they submit, **Then** the modal closes and the new goal appears in the active goals column
4. **Given** the user has submitted a goal, **When** the goal is displayed, **Then** the days remaining is correctly calculated from today to the end date
5. **Given** the modal is open, **When** the user clicks outside the modal or a cancel button, **Then** the modal closes without creating a goal

---

### User Story 3 - Complete or Delete Goals (Priority: P3)

Users need to manage goals by either marking them as completed (to track accomplishments) or permanently deleting them (to remove mistakes or abandoned goals).

**Why this priority**: Goal management is essential for keeping the list relevant and accurate. Users need control over their goal lifecycle. This completes the CRUD operations and enables users to maintain a clean, current goal list.

**Independent Verification**: Check a goal's checkbox, verify the option appears to either complete or delete, execute each action, and confirm goals move to completed column or are permanently removed respectively.

**Acceptance Scenarios**:

1. **Given** an active goal is displayed, **When** the user clicks its checkbox, **Then** the checkbox becomes checked and options to complete or delete become available
2. **Given** a goal checkbox is checked and "complete" is selected, **When** confirmed, **Then** the goal moves from the active column to the completed column on the right
3. **Given** a goal checkbox is checked and "delete" is selected, **When** confirmed, **Then** the goal is permanently removed from both columns
4. **Given** a goal is in the completed column, **When** displayed, **Then** it shows the goal title and completion indicator (no days remaining needed)
5. **Given** multiple goals are checked, **When** an action is taken, **Then** only the intended goal is affected (no batch operations)

---

### User Story 4 - Urgent Goal Highlighting (Priority: P4)

Users need visual alerts when goals are approaching their deadline so they can prioritize urgent items.

**Why this priority**: This enhances usability by proactively drawing attention to time-sensitive goals. While valuable, the app is functional without this feature, making it a lower priority enhancement.

**Independent Verification**: Create a goal with an end date within 3 days, verify it displays with visual highlighting (color, border, or other indicator) that distinguishes it from non-urgent goals.

**Acceptance Scenarios**:

1. **Given** a goal has 3 or fewer days remaining, **When** displayed in the active column, **Then** it is visually highlighted (e.g., pastel red/orange background or border)
2. **Given** a goal has more than 3 days remaining, **When** displayed, **Then** it appears in the normal style without highlighting
3. **Given** a goal's deadline approaches, **When** the days remaining decreases to 3 or less, **Then** the highlighting automatically appears
4. **Given** today is the goal's end date, **When** displayed, **Then** it shows "0 days remaining" with the strongest highlighting

---

### Edge Cases

- What happens when a goal's end date is in the past (overdue goals)?
- How does the system handle very long goal titles (truncation or wrapping)?
- What happens when there are many completed goals (scrolling, pagination, or collapse)?
- How does the app behave on first launch with no goals at all?
- What if a user tries to create a goal with an end date in the past?
- How are dates handled across timezone boundaries?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST display active goals in a left column with goal title and days remaining visible
- **FR-002**: System MUST display completed goals in a right column separate from active goals
- **FR-003**: System MUST calculate and display days remaining as the difference between today's date and the goal's end date
- **FR-004**: Users MUST be able to add new goals via a button that opens a modal form
- **FR-005**: New goal form MUST collect goal title (text field) and end date (date picker)
- **FR-006**: System MUST allow users to check/uncheck goals using a checkbox interface
- **FR-007**: Checked goals MUST present user with two options: complete (move to completed column) or delete (permanent removal)
- **FR-008**: Completed goals MUST be moved from active column to completed column and persist there
- **FR-009**: Deleted goals MUST be permanently removed with no recovery option
- **FR-010**: Goals with 3 or fewer days remaining MUST be visually highlighted to indicate urgency
- **FR-011**: System MUST use a modern light theme with fun pastel colors for the interface
- **FR-012**: System MUST persist goals so they remain available when the user returns to the app
- **FR-013**: Active goals MUST be ordered by urgency (soonest deadline first)

### Key Entities

- **Goal**: Represents a user objective with a deadline
  - Title: descriptive name of the goal
  - End Date: target completion date
  - Status: active or completed
  - Days Remaining: calculated value from current date to end date

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can create a new goal and see it appear in the active column in under 15 seconds
- **SC-002**: Users can immediately identify urgent goals (3 days or less) through visual highlighting without reading text
- **SC-003**: Users can complete or delete a goal in under 10 seconds with clear visual feedback
- **SC-004**: The interface works seamlessly on mobile (375px), tablet (768px), and desktop (1440px) viewports
- **SC-005**: All interactive elements (buttons, checkboxes, modal) provide immediate visual feedback on interaction
- **SC-006**: First-time users can understand the app's purpose and primary actions without instructions
- **SC-007**: Goals persist across browser sessions (page refresh does not lose data)

## Assumptions *(optional)*

- Goals are personal to a single user (no sharing or collaboration features needed)
- All dates use the user's local timezone
- Goals are text-based only (no attachments, images, or rich formatting)
- Completed goals remain indefinitely (no auto-archiving or cleanup)
- The app supports modern browsers (no IE11 compatibility required)
- Data persistence uses browser storage (localStorage or similar client-side storage)
- Days remaining calculation uses calendar days, not business days
- No authentication or user accounts needed for initial version (single-user, browser-based)

**⚠️ NOTE**: This project does not include automated testing. Acceptance scenarios below are for manual verification only.

## User Scenarios & Manual Verification *(mandatory)*

<!--
  IMPORTANT: User stories should be PRIORITIZED as user journeys ordered by importance.
  Each user story/journey must be INDEPENDENTLY VERIFIABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that delivers value.
  
  Assign priorities (P1, P2, P3, etc.) to each story, where P1 is the most critical.
  Think of each story as a standalone slice of functionality that can be:
  - Developed independently
  - Verified independently (manual testing)
  - Deployed independently
  - Demonstrated to users independently
-->

### User Story 1 - [Brief Title] (Priority: P1)

[Describe this user journey in plain language]

**Why this priority**: [Explain the value and why it has this priority level]

**Independent Verification**: [Describe how this can be verified independently - e.g., "Can be fully verified by [specific manual action] and delivers [specific value]"]

**Acceptance Scenarios**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]
2. **Given** [initial state], **When** [action], **Then** [expected outcome]

---

### User Story 2 - [Brief Title] (Priority: P2)

[Describe this user journey in plain language]

**Why this priority**: [Explain the value and why it has this priority level]

**Independent Verification**: [Describe how this can be verified independently]

**Acceptance Scenarios**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]

---

### User Story 3 - [Brief Title] (Priority: P3)

[Describe this user journey in plain language]

**Why this priority**: [Explain the value and why it has this priority level]

**Independent Verification**: [Describe how this can be verified independently]

**Acceptance Scenarios**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]

---

[Add more user stories as needed, each with an assigned priority]

### Edge Cases

<!--
  ACTION REQUIRED: The content in this section represents placeholders.
  Fill them out with the right edge cases.
-->

- What happens when [boundary condition]?
- How does system handle [error scenario]?

## Requirements *(mandatory)*

<!--
  ACTION REQUIRED: The content in this section represents placeholders.
  Fill them out with the right functional requirements.
-->

### Functional Requirements

- **FR-001**: System MUST [specific capability, e.g., "allow users to create accounts"]
- **FR-002**: System MUST [specific capability, e.g., "validate email addresses"]  
- **FR-003**: Users MUST be able to [key interaction, e.g., "reset their password"]
- **FR-004**: System MUST [data requirement, e.g., "persist user preferences"]
- **FR-005**: System MUST [behavior, e.g., "log all security events"]

*Example of marking unclear requirements:*

- **FR-006**: System MUST authenticate users via [NEEDS CLARIFICATION: auth method not specified - email/password, SSO, OAuth?]
- **FR-007**: System MUST retain user data for [NEEDS CLARIFICATION: retention period not specified]

### Key Entities *(include if feature involves data)*

- **[Entity 1]**: [What it represents, key attributes without implementation]
- **[Entity 2]**: [What it represents, relationships to other entities]

## Success Criteria *(mandatory)*

<!--
  ACTION REQUIRED: Define measurable success criteria.
  These must be technology-agnostic and measurable.
-->

### Measurable Outcomes

- **SC-001**: [Measurable metric, e.g., "Users can complete account creation in under 2 minutes"]
- **SC-002**: [Measurable metric, e.g., "System handles 1000 concurrent users without degradation"]
- **SC-003**: [User satisfaction metric, e.g., "90% of users successfully complete primary task on first attempt"]
- **SC-004**: [Business metric, e.g., "Reduce support tickets related to [X] by 50%"]
