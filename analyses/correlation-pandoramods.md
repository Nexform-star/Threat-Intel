# Threat Intelligence Correlation Report: Shared Infrastructure

## 1. Objective

Compare two apparently unrelated GitHub projects to determine whether they share technical infrastructure or distributed artifacts.

## 2. Projects

### Project A
- Repository: `aerisgrace29/Duel-Forge-Bot`
- Theme: Yu-Gi-Oh! Master Duel

### Project B
- Repository: `andreibalakin18-ai/anime-shop-sim-clerk-brain`
- Theme: Anime Shop Simulator

## 3. Shared Infrastructure

Both projects reference:

`pandoramods.top`

This domain was previously identified during the static analysis of Project A as part of its download infrastructure.

## 4. Shared Artifact

The same file was identified across all three projects.

| Project | Repository                                      | SHA-256  |
| ------- | ----------------------------------------------- | -------- |
| A       | `aerisgrace29/Duel-Forge-Bot`                   | `1f8584740529424e2cb07cd56287e2919d6995249750589324c55cde42da4150` |
| B       | `andreibalakin18-ai/anime-shop-sim-clerk-brain` | `1f8584740529424e2cb07cd56287e2919d6995249750589324c55cde42da4150` |
| C       | `zaltvcloud/di2-apex-trainer`                   | `1f8584740529424e2cb07cd56287e2919d6995249750589324c55cde42da4150` |

The SHA-256 value is identical across all three samples, indicating that the files have identical content.

This provides a strong technical correlation between the three distribution chains. Combined with the shared `pandoramods.top` infrastructure and similar web/redirect structures, the projects appear to rely on the same distributed artifact and infrastructure.

This finding establishes a technical relationship between the samples, but does not by itself establish that the repositories are operated by the same individual or organization.

## 5. Structural Similarities

The two projects also present similarities in their repository/web structure.

Observed similarities:
- similar project presentation;
- similar web structure;
- shared external domain;
- shared distributed artifact.

## 6. Technical Correlation

The combination of a shared external domain and an identical file provides a strong technical correlation between the two distribution chains.

This establishes a relationship between the infrastructure/artifacts used by the projects.

It does not, by itself, establish that the repositories are operated by the same individual or organization.

## 7. Conclusion

The investigation identified multiple technical links between the two projects, most notably the shared `pandoramods.top` infrastructure and the identical file identified through SHA-256 comparison.

These findings support further investigation of the shared infrastructure and historical repository contents.

Three apparently unrelated projects were found to share the same external infrastructure, web distribution structure, and identical file based on SHA-256 comparison.

## 8. Limitations

This analysis is based on publicly available repository content and static comparison.

No attribution to a specific individual or organization is made solely from these findings.
