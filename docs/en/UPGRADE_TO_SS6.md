# Upgrade to Silverstripe CMS 6

## Core Framework

⚠️ Update core dependencies to Silverstripe CMS 6:
- `silverstripe/framework`: `^5.0` → `^6.0`
- `silverstripe/admin`: `^2.0` → `^3.0`

## Removed Dependencies

⚠️ The following packages have been temporarily removed from `require` and moved to a `yet-to-update` section:

- `sunnysideup/silverstripe-garbage-collector`
- `sunnysideup/silverstripe-unused-file-report`
- `sunnysideup/assets_overview`
- `sunnysideup/remove-orphaned-elementals`
- `sunnysideup/cleanup-tables`
- `sunnysideup/database-share-clean-up`
- `sunnysideup/dataintegritytests`
- `sunnysideup/delete-all-tables`
- `sunnysideup/templateoverview`
- `sunnysideup/resize-all-images`
- `sunnysideup/version-pruner`
- `oddnoc/silverstripe-artefactcleaner`

🔍 **Manual Action Required**: These packages do not yet have Silverstripe 6-compatible stable releases. Monitor each package repository for SS6 compatibility updates and re-add them to your `composer.json` when available. Functionality provided by these modules will not be available until they are updated and re-installed.
