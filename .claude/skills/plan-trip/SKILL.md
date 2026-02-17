# /plan-trip

Create a new trip folder structure with overview and empty booking files.

## Usage

```
/plan-trip <trip-name> [destination] [dates] [budget-level]
```

**Parameters:**
- `trip-name` (required): Kebab-case name for the trip (e.g., `tokyo-2026`)
- `destination` (optional): Primary destination city/country
- `dates` (optional): Travel dates (e.g., `"2026-04-01 to 2026-04-08"`)
- `budget-level` (optional): One of `budget`, `mid-range`, `luxury` (default: `mid-range`)

If optional parameters are not provided, ask the user interactively.

## Instructions

1. Parse the arguments from `$ARGUMENTS`. The format is: `<trip-name> [destination] [dates] [budget-level]`
2. If destination, dates, or budget-level are missing, use `AskUserQuestion` to gather them
3. **Group composition**: Ask the user for:
   - **Group type**: solo, couple, family, or friends
   - **Ages**: approximate ages or age ranges of the travelers (e.g., "30s", "2 adults + toddler", "20s and 30s")
   - The user can skip this step if they have no preference (default: group type = "Not specified", ages = "Not specified")
4. **Interests & preferences**: Ask the user to select from common travel interests (allow multiple selections):
   - Options: Nightlife, Food & Dining, History & Culture, Nature & Hiking, Beaches, Shopping, Art & Museums, Adventure/Sports, Photography, Relaxation/Spa, Architecture, Local Festivals/Events
   - The user can skip this step (default: "No specific preferences — balanced itinerary")
5. **Special requests**: Ask the user for any specific places, experiences, or preferences they want included (free-form text). Examples: "Visit cherry blossom spots", "Overnight stay in Kyoto", "See a sumo match". The user can skip this step (default: "_None_")
6. **Dietary & accessibility**: Ask the user about dietary restrictions, allergies, or accessibility needs (free-form text). Examples: "Vegetarian", "Wheelchair accessible venues", "Nut allergy". The user can skip this step (default: "_None_")
7. Calculate the number of trip days from the date range
8. Create the folder structure under `trips/<trip-name>/`:
   ```
   trips/<trip-name>/
   ├── overview.md
   ├── research/
   ├── itinerary/
   └── bookings/
       ├── flights.md
       ├── hotels.md
       └── activities.md
   ```
9. Generate `overview.md` using the template at `.claude/skills/plan-trip/templates/trip-overview.md`, filling in all variables:
   - `{{GROUP_TYPE}}`: The group type from step 3 (or "Not specified")
   - `{{AGES}}`: The ages from step 3 (or "Not specified")
   - `{{INTERESTS}}`: A bullet list of selected interests from step 4, each as `- [interest]` (or "_No specific preferences — balanced itinerary_")
   - `{{SPECIAL_REQUESTS}}`: A bullet list of special requests from step 5, each as `- [request]` (or "_None_")
   - `{{DIETARY_ACCESSIBILITY}}`: A bullet list of restrictions/needs from step 6, each as `- [item]` (or "_None_")
10. Generate empty booking files using the template at `.claude/skills/plan-trip/templates/booking.md`
11. Display a summary of what was created and suggest next steps:
    - `/research-destination <trip-name> <destination>` to research the destination
    - `/add-booking <trip-name> flight` to add known bookings
