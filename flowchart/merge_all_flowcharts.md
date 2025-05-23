# Instructions for Merging All Authentication Flowcharts

## Option 1: Using diagrams.net (draw.io)

1. **Open diagrams.net** in your web browser: https://app.diagrams.net/
2. **Create a new blank diagram** with a large canvas size (File → Page Setup → Custom → Width: 2000px, Height: 3000px)
3. **Import each flowchart file**:
   - File → Import From → Device → Select each .drawio file
   - When prompted, select "Import to new page"
4. **Create a main page** for the complete flowchart
5. **Copy elements from each flow** to the main page and arrange them
6. **Connect the related flows** (e.g., MFA decisions to the MFA flow)
7. **Export** as PNG or PDF for submission

## Option 2: Using Lucidchart

1. **Sign in to Lucidchart**: https://www.lucidchart.com/
2. **Create a new document** with a large canvas
3. **Recreate each flowchart** using Lucidchart's shape library
4. **Arrange and connect** the flows
5. **Export** as PNG or PDF

## Option 3: Quick Solution - Screenshot and Combine

1. **Open each .drawio file** in diagrams.net
2. **Take a screenshot** of each flowchart
3. **Combine the screenshots** in a document or presentation software (Word, PowerPoint, etc.)
4. **Add arrows or connectors** to show relationships between flows
5. **Export** as PDF

## Option 4: Professional Approach - Use a Flowchart Template

1. **Find a professional authentication flowchart template** online
2. **Customize it** with your specific flows and requirements
3. **Ensure all required elements** are included
4. **Export** in high resolution

## Recommended Layout

Arrange the flowcharts in this logical order:

```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│ Email/Password  │  │  Social Sign-In │  │       SSO       │
│     Login       │  │                 │  │                 │
└────────┬────────┘  └────────┬────────┘  └────────┬────────┘
         │                    │                    │
         └──────────┬─────────┴──────────┬─────────┘
                    ▼                    ▼
         ┌─────────────────┐  ┌─────────────────┐
         │       MFA       │  │    Account      │
         │                 │  │    Creation     │
         └─────────────────┘  └────────┬────────┘
                                       │
                             ┌─────────▼────────┐
                             │    Password      │
                             │    Recovery      │
                             └──────────────────┘
```

## Final Checklist

Ensure your merged flowchart includes:
- All six authentication flows
- Proper connections between related flows
- Consistent styling (colors, shapes, fonts)
- Clear labels and decision paths
- A legend explaining the symbols
- High-resolution export for submission
