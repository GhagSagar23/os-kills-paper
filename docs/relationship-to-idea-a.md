# Relationship to Idea A

Idea C overlaps with [[idea-a::lessons-learned]] L2 (OEM kills) and L5 (permission revocations). The core observations are captured in Idea A's Lessons Learned section.

## What would make Idea C standalone

A large-enough deployed device fleet (hundreds of devices, not ~30) with per-event OEM/OS metadata in the permission log. At current scale, the data is anecdotal. Revisit when deployment reaches statistical significance.

## Instrumentation to keep

Ensure the production app logs per-event metadata: OEM, OS version, kill cause (Doze/OEM policy/user revocation/reboot), recovery mechanism outcome. This data feeds a future standalone paper.

## Status

Parked. See [[idea-a::oem-compatibility]] for current OEM findings.

Links: [[idea-a::lessons-learned]], [[idea-a::oem-compatibility]]
