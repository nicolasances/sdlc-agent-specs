# Slicing Strategy for Frontend

## Guiding Principle

The guiding principles for slicing an idea into Features for a frontend follows the MVP philosophy: each Feature should deliver a complete, end-to-end user experience, even if it's minimal.

## Methodology

To slice an idea into Features for the frontend, follow these steps:

1. **Understand the User Journey**: Take the idea and map out the user journey. Identify the key interactions and touchpoints that the user will have with the product.
2. **Identify the Main Screens**: Based on the user journey, identify the main screens or components that will be involved. Each screen or component can potentially be a separate Feature. 
    - If screens have been defined in a design tool and are available in a wireframe or prototype, use those as a reference. 
    - Check the documentation for any existing screens or components that have been defined, and see if they align with the user journey.
3. **Define the Features**: For each main screen or component, define a Feature that delivers a complete user experience for that screen. This means that the Feature should include all necessary interactions, presentation logic, data fetching, and state management to make the screen functional. 

**Example of a good Feature for frontend:**
- In a User Profile screen, a Feature could be "Display User Information". This Feature would include fetching the user's data from the API, handling loading and error states, and rendering the user's name, profile picture, and other relevant information.
- In a Dashboard screen, a Feature could be "Show Recent Activity". This Feature would involve fetching the user's recent activity data, handling loading and error states, and rendering a list of recent actions or notifications.

## Output Format
Each Feature for a frontend should be documented in a markdown file (.md) with the following format:

```markdown
# [Feature Name]

## 1. Purpose & Scope
[A description of the feature, why it's needed and what it does]

**Out of scope**: 
- [Thing deliberately excluded]
- [Thing deliberately excluded]

## 2. Key User Stories
[Frame user stories from the end user's perspective, naming the operation or capability they need, not the technical implementation. Use the format: "As a [type of user], I want to [perform some action] so that [achieve some goal]."]

| # | As a User I want to .. | so that .. |
|---|------------------------|------------|

## 3. Interfaces
[Describe the screens, components, or interactions this feature belongs to, introduces, or modifies. Include any relevant design references, such as references to wireframes or prototypes. Explain how the feature fits into the overall user experience and how it interacts with other features or components. Describe how it fits into the specific screens or components defined in the design documentation, if applicable.]

**Screen:** [Name of the screen this feature belongs to, as defined in the design documentation]

**Components:** [List of components this feature belongs to, as defined in the design documentation]

| Component Name | Description | Expected Behavior |
|----------------|-------------|-------------------|

**Additional Notes:** [Any additional notes about the interfaces, such as edge cases, error states, or interactions with other features or components.]

## 4. Business Logic
[Describe the rules, flows, algorithms, and invariants that govern this feature's behavior. This includes any client-side logic that is necessary to support the user interactions and interfaces described above. Use one bullet per rule; be specific enough that a developer can implement it without guessing.]

## 5. Technical Decisions
[Surface any technical or architectural decision that you are making in the design of this feature, especially if it deviates from standard practices or if there are multiple viable approaches that are significantly different from each other.]

| # | Decision | Rationale |
|---|----------|-----------|

## 6. Success Criteria
[Define clear success criteria for this feature, which can be used to determine when the implementation is complete and meets the requirements. This could include specific user interactions that must work, performance benchmarks, or any other measurable outcomes that indicate the feature is functioning as intended.]

| # | Criterion | Notes |
|---|-----------|-------|

## 7. Open Questions
[Surface any open questions that you have about the design of this feature, especially if they impact the user experience or the technical implementation. These could be questions about edge cases, error handling, performance considerations, or anything else that is not yet fully defined.]

| # | Question | Notes |
|---|----------|-------|

```

---