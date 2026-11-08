# How to Update — L_RETICULUM
**Platform:** Anticloud | **IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg

## Module: L_RETICULUM
Domain: Reticulum: cryptography-based mesh networking for Anticloud sovereign communications


## Update Procedure
1. Backup current state
2. Test in api-oss-labs sandbox
3. `pip install --upgrade anticloud-l_reticulum`
4. `python -m l_reticulum.tests.smoke`
5. `aioss verify --chain ./l_reticulum.aioss`
6. Monitor 30 min via api-oss-monitor

## Rollback
```bash
pip install anticloud-l_reticulum==<previous>
python -m api_oss_backup restore --archive ./backups/<latest>
```

## Weight Updates
PAX 27B weight updates are signed by Anticloud FZ LLE:
```bash
anticloud tool verify-weights --model ./pax-27b-q4-new.gguf --sig ./pax-27b-q4-new.sig
```
