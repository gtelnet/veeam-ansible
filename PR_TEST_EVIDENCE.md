## Test Evidence

### Scope
Validated both answer-file paths and reboot-gating behavior introduced/affected by this PR:

- Non-13.1 path uses existing Jinja2 answer-file template.
- 13.1.0.x path builds answer file from setup media template and injects role-configured properties.
- EM/VBR/Console reboot checks use explicit Windows reboot-pending registry detection where updated.

### Test Matrix

| Scenario | Version | Expected Path | Result |
| --- | --- | --- | --- |
| Fresh VBR install | 13.1.0.411 | Dynamic media-template answer file | ✅ Pass |
| Fresh VBR install | Pre-13.1 (control) | Existing Jinja2 answer file | ✅ Pass |
| EM install/upgrade flow | Matching target versions | Inline reboot-pending detection and conditional reboot | ✅ Pass |
| VBR console install/upgrade flow | Matching target versions | Inline reboot-pending detection and conditional reboot | ✅ Pass |
| VBR upgrade flow | Matching target versions | Inline reboot-pending detection and conditional reboot | ✅ Pass |

### Validation Notes

- 13.1.0.x installs successfully locate setup-provided VbrAnswerFile_install.xml from media and generate a final answer file with role variables applied.
- Non-13.1 behavior remains on the prior templated path.
- Reboot is only triggered when reboot-pending indicators are present.
- No regressions observed in install completion and service-start checks for tested scenarios.
