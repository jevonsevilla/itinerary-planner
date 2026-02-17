# /trip-summary

Display a read-only summary of an existing trip's status.

## Usage

```
/trip-summary <trip-name>
```

**Parameters:**
- `trip-name` (required): The existing trip folder name (e.g., `tokyo-2026`)

## Instructions

1. Parse `$ARGUMENTS` to extract `trip-name`
2. Verify that `trips/<trip-name>/overview.md` exists — if not, tell the user to run `/plan-trip` first
3. Read all trip files and compile a summary. This is **read-only** — do not modify any files.

### Summary Sections

**Trip Overview**
- Read `trips/<trip-name>/overview.md` and display destination, dates, duration, budget level

**Traveler Profile** _(skip this section silently if the overview has no Interests, Special Requests, or Dietary & Accessibility sections)_
- **Group**: Display group type and ages (if present)
- **Interests**: List stated interests
- **Special requests**: List any special requests
- **Dietary & accessibility**: List any restrictions or needs

**Research Status**
- Use Glob to find files in `trips/<trip-name>/research/`
- List destinations researched, or note if none yet

**Itinerary Status**
- Use Glob to find files in `trips/<trip-name>/itinerary/`
- If itinerary exists: show a one-line highlight per day (read each day file's Theme section)
- If no itinerary: note it's not yet built

**Booking Status**
- Read each file in `trips/<trip-name>/bookings/`
- Summarize: number of flights, hotels, activities booked
- Show total booked cost per category

**Budget Summary**
- Read the Budget Tracker from overview.md
- Show estimated vs. booked vs. remaining

**Action Items**
- Based on what's missing, suggest next steps:
  - No research? → `/research-destination`
  - No itinerary? → `/build-itinerary`
  - Missing bookings? → `/add-booking`
  - Everything done? → "Trip is fully planned!"

### Output Format

Display the summary directly in the conversation as formatted Markdown. Do NOT write any files.
