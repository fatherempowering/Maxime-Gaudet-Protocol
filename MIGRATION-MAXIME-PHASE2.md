# Maxime Gaudet Phase 2 Migration Notes

This branch prepares the Maxime Gaudet portal only. It does not modify the shared Father Empowering template and does not include the final Phase 2 training or nutrition program yet.

## Source

- Old data key: `faem_mg_v9d`
- Old photo database: `faem_photos_v1`
- Old photo store: `photos`

## Target

- Client slug: `maxime-gaudet`
- New data key: `faem_maxime_gaudet_data_v1`
- New photo database: `faem_maxime_gaudet_photos_v1`
- Training runtime file: `training-program.json`
- Nutrition runtime file: `nutrition-program.json`

## Migration Guarantees

- The old `faem_mg_v9d` localStorage value is never deleted.
- The old `faem_photos_v1` IndexedDB database is never deleted.
- A full raw backup is stored before writing the new data key.
- The data migration is guarded by `faem_maxime_gaudet_legacy_mg_v9d_migrated_v1`.
- The photo migration is guarded by `faem_maxime_gaudet_legacy_photos_migrated_v1`.
- Week 0 is marked completed only for the Maxime portal migration.

## Manual Regression Checklist

1. Open the current old Maxime portal on the same browser/device that contains the existing client data.
2. Confirm the browser has `localStorage.faem_mg_v9d`.
3. Confirm the browser has IndexedDB `faem_photos_v1`.
4. Open the Phase 2 portal URL after uploading this branch.
5. Confirm `localStorage.faem_maxime_gaudet_data_v1` is created.
6. Confirm `localStorage.faem_mg_v9d` still exists unchanged.
7. Confirm `localStorage.faem_maxime_gaudet_legacy_mg_v9d_backup_v1` exists.
8. Confirm `localStorage.faem_maxime_gaudet_legacy_mg_v9d_report_v1` reports `data_migrated`.
9. Confirm Week 0 does not re-open as an incomplete onboarding flow.
10. Confirm old sessions appear in History.
11. Confirm old loads and notes are present in migrated sessions.
12. Confirm check-ins, bodyweight, measurements, and unlocked week are preserved.
13. Confirm photos show for the corresponding migrated weeks.
14. Confirm `faem_photos_v1` still exists after migration.
15. Refresh the app and confirm the migration does not run a second time.

## Rollback

Because the migration is non-destructive, rollback is to restore the previous `index.html` in the GitHub repo. Existing old client data remains under `faem_mg_v9d` and `faem_photos_v1`.
