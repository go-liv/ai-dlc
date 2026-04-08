# Wireframe

**Type:** Skill  
**Agents:** Designer

## Description
Generates text-based wireframes and UI component specifications for application screens. Produces structured visual representations using ASCII/Unicode art and detailed component breakdowns that developers can implement.

## When to Use
- When designing new screens or user flows
- When the Designer needs to present layout options
- Before implementation to align on UI structure
- When documenting component hierarchies and interactions

## Procedure

### 1. Gather Requirements
Understand what needs to be wireframed:
- Screen purpose and user goals
- Key data and actions on the screen
- Target platform (web, mobile, desktop)
- Existing design system or component library in the project

### 2. Research Existing Patterns
Search the codebase for:
- Existing UI components that can be reused
- Current layout patterns and navigation structure
- Design tokens, themes, or style configurations
- Similar screens already implemented

### 3. Create the Wireframe
Produce a text-based wireframe using ASCII/Unicode:

```
┌─────────────────────────────────────────┐
│  Logo            Nav Item 1 | Nav Item 2│
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────┐  ┌──────────────────────┐ │
│  │ Sidebar  │  │ Main Content         │ │
│  │          │  │                      │ │
│  │ • Item 1 │  │ ┌──────┐ ┌──────┐   │ │
│  │ • Item 2 │  │ │Card 1│ │Card 2│   │ │
│  │ • Item 3 │  │ └──────┘ └──────┘   │ │
│  │          │  │                      │ │
│  └──────────┘  └──────────────────────┘ │
│                                         │
├─────────────────────────────────────────┤
│  Footer                                 │
└─────────────────────────────────────────┘
```

### 4. Define Component Specs
For each component in the wireframe, specify:

```markdown
### Component: <Name>
- **Type**: <button | input | card | list | modal | ...>
- **Content**: <What data it displays>
- **Actions**: <What happens on interaction>
- **States**: <default | hover | active | disabled | loading | error>
- **Responsive**: <How it adapts across breakpoints>
```

### 5. Document User Flow
Describe the interaction flow:
```markdown
### Flow: <Flow Name>
1. User sees <initial state>
2. User clicks <element> → <what happens>
3. System responds with <result>
4. User is taken to <next screen or state>
```

## Output Format

```markdown
# Wireframe — <Screen/Feature Name>

## Overview
<Purpose of this screen and target users>

## Layout
<ASCII wireframe>

## Components
### <Component 1>
- Type: ...
- Content: ...
- Actions: ...
- States: ...

### <Component 2>
...

## User Flows
### <Flow 1>
1. ...
2. ...

## Responsive Behavior
- **Desktop (>1024px)**: <layout description>
- **Tablet (768-1024px)**: <layout description>
- **Mobile (<768px)**: <layout description>

## Notes
<Design rationale, accessibility considerations, open questions>
```

## Constraints
- DO NOT produce pixel-perfect designs — wireframes show structure, not visual polish
- DO include responsive behavior for all wireframes
- DO note accessibility considerations (keyboard nav, screen readers, contrast)
- REUSE existing components from the project's design system when one exists
- KEEP wireframes focused on layout and interaction, not styling details
