# Documentation

## 1. Runbooks

* Action-only operational guides
* Designed for use during outages
* No theory, no opinions, no explanations
* Written for high-stress scenarios

Use this when:

* Something is broken
* You already know what failed
* You need fast, repeatable recovery steps

## 2. Architectural Decision Records (ADR)

* Long-term, immutable design decisions
* Capture why, not just what
* Used in interviews and design reviews

Use this when:

* Choosing Proxmox, storage backend, networking model
* Making decisions you would defend months later

## 3. Incidents

* Factual record of failures
* Blameless, timestamped, evidence-driven
* No opinions or emotions

Use this when:

* Something actually breaks (intentionally or accidentally)
* You need a historical record

## 4. Decisions

* Tactical, short-term decisions
* Often made during incidents or builds
* Separate from architecture

Use this when:

* You choose a workaround
* You make a temporary call under pressure

## 5. Incident Response

* Focuses on your thinking and actions
* Shows senior-level response behavior
* Goldmine for interviews

Use this when:

* You respond to an incident

* You want to improve how you react under stress

## How these work together (this is important)

A single failure should generate multiple documents:

1. **Incident** – What broke
2. **Incident Response** – How you handled it
3. **Decision** – Tactical choices made
4. **Runbook** – Future prevention
5. **ADR** (only if architecture changes)

This mirrors real production environments.