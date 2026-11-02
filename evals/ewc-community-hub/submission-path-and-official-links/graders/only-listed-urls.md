---
type: regex
not_contains: 'https?://(?!(?:github\.com/ewcloud/ewc-community-hub(?:/blob/main/docs/schema-reference/items/v1alpha1\.md|/blob/main/\.github/workflows/validate\.yml)?|europeanweather\.cloud/community-hub|confluence\.ecmwf\.int/x/wyLOIQ|europeanweather\.cloud/get-access|support\.europeanweather\.cloud|confluence\.ecmwf\.int/display/EWCLOUDKB|confluence\.ecmwf\.int/spaces/EWCLOUDKB/pages/414272933/EWC\+Virtual\+Images\+Available|confluence\.ecmwf\.int/x/evWHEw)(?![\w\-/#?=&%]))'
---

Every URL in the answer must be one listed in references/official-links.md (lines 19-27) or the validate.yml workflow link in references/submission.md line 37; the pattern matches any http(s) URL that is not one of them, so zero matches passes. A guessed Confluence page, portal path or repository URL fails.
