# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Itinerary Planner — a personal travel planning system built on Claude Code skills and agents. All trip data is stored as version-controlled Markdown files. No paid APIs required.

## Architecture

- **Skills** (`.claude/skills/`): User-invocable commands (`/plan-trip`, `/research-destination`, `/build-itinerary`, `/add-booking`, `/trip-summary`, `/map-trip`)
- **Agents** (`.claude/agents/`): Specialized subagents for research and itinerary building (run as forked contexts using Sonnet)
- **Trip data** (`trips/<trip-name>/`): Plain Markdown files organized into `overview.md`, `research/`, `itinerary/`, and `bookings/`

## Conventions

- All trip data files are Markdown (`.md`)
- Trip folder names use kebab-case (e.g., `tokyo-2026`)
- Day files are zero-padded: `day-01.md`, `day-02.md`, etc.
- Budget levels: `budget`, `mid-range`, `luxury`
- Agents use WebSearch and WebFetch for all research — no external API keys needed
- For directions/distances, agents search the web rather than calling a Maps API

## Workflow

1. `/plan-trip` — Create trip folder structure and overview
2. `/research-destination` — Research destinations (delegates to travel-researcher agent)
3. `/build-itinerary` — Build day-by-day plans (delegates to itinerary-builder agent)
4. `/add-booking` — Record flights, hotels, activities
5. `/trip-summary` — View trip overview and status
6. `/map-trip` — Generate a KML map for Google My Maps (one layer per day)
