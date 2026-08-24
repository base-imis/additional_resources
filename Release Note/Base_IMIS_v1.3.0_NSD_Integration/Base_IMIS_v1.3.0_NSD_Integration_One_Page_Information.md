# Base IMIS v1.3.0 - NSD Integration

## One-Page Release Information Sheet

| Item             | Value                                 | Item             | Value            |
| ---------------- | ------------------------------------- | ---------------- | ---------------- |
| **Branch** | `v1.3.0-nsd`                        | **Status** | Draft for review |
| **Commit** | `d3b21b9` - update after final push | **PR **          |                  |

## Release Summary

This release connects the Base IMIS CWIS Dashboard with the National Sanitation Dashboard (NSD). Authorized users can configure the connection, check draft and published years, and push eligible CWIS indicator data from IMIS to NSD.

## User-Facing Changes

- New **NSD Integration Setting** screen under CWIS IMS.
- Configure city, authentication URL, send-data URL, username, and password.
- View draft and published years returned by NSD.
- Push eligible draft-year indicator data.
- Block published years and show clear success/error messages.

## Technical Scope

- **Controllers:** `NsdDashboardController.php`, `NsdSettingController.php`
- **Model/service:** `Nsd.php`, `CwisSettingService.php`
- **Views:** NSD settings, dashboard controls, and sidebar entry
- **Sidebar:** `resources/views/includes/sidebar.blade.php`
- **Routes:** authentication, status, data retrieval, push, and settings
- **Database:** `cwis.nsd_setting` migration and data dictionary update
- **Permissions:** `PermissionsSeeder` plus four role seeders

## Security and Dependencies

- Do not commit NSD credentials, tokens, or production URLs.
- Configured city and endpoints must match the NSD environment.
- The selected year must contain the required CWIS M&E data.

## Release Purpose

Prepare a controlled open-source feature release that can be reviewed, approved, reused, and adapted by other cities or projects.

## Required Deployment Commands

Run the migration first, followed by all five seeders in the order shown below.

| Order | Action                                 | Command                                                                                                      |
| ----: | -------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
|     1 | Migration                              | `php artisan migrate --path=database/migrations/2025_04_28_123002_nsd_setting.php`                         |
|     2 | PermissionsSeeder                      | `php artisan db:seed --class="Database\\Seeders\\PermissionsSeeder"`                                       |
|     3 | GuestSeeder                            | `php artisan db:seed --class="Database\\Seeders\\RolePermissions\\GuestSeeder"`                            |
|     4 | MunicipalityExecutiveSeeder            | `php artisan db:seed --class="Database\\Seeders\\RolePermissions\\MunicipalityExecutiveSeeder"`            |
|     5 | MunicipalityITAdminSeeder              | `php artisan db:seed --class="Database\\Seeders\\RolePermissions\\MunicipalityITAdminSeeder"`              |
|     6 | MunicipalitySanitationDepartmentSeeder | `php artisan db:seed --class="Database\\Seeders\\RolePermissions\\MunicipalitySanitationDepartmentSeeder"` |

## Seeder Files

- `database/seeders/PermissionsSeeder.php`
- `database/seeders/RolePermissions/GuestSeeder.php`
- `database/seeders/RolePermissions/MunicipalityExecutiveSeeder.php`
- `database/seeders/RolePermissions/MunicipalityITAdminSeeder.php`
- `database/seeders/RolePermissions/MunicipalitySanitationDepartmentSeeder.php`

## Key References

- `app/Http/Controllers/Fsm/NsdDashboardController.php`
- `app/Http/Controllers/Fsm/NsdSettingController.php`
- `resources/views/fsm/nsd-setting/`
- `resources/views/cwis/cwis-dashboard/chart-layout/cwis-dash-layout.blade.php`
- `resources/views/includes/sidebar.blade.php`
- `database/migrations/2025_04_28_123002_nsd_setting.php`
- `documentations/code_documents/19 - NSD Api.md`
- `documentations/data_dictionary/data_dictionary.md`
- [**User Manual —** ](documents/User_Manual_Updated_with_NSD_Integration_Feature.pdf)NSD Integrated User Manual

## Before Final GitHub Release

Update the final commit ID, add the pull request link, complete QA and management sign-off, and create the release tag only after approval.
