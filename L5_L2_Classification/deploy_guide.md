# Deploy Guide — L_RETICULUM
**Tier:** TIER_8_RF_MESH_DEFENSE | **Stack:** Python 3.11, rns 0.x (Reticulum), PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, rns 0.7+. LoRa, serial, TCP, or I2P interface. Any hardware with Python.

## Environment
Any hardware: Raspberry Pi, laptop, mobile. LoRa/serial/TCP interface. Low resource requirements.

## AIOSS Integration
```bash
aioss init --module L_RETICULUM --output ./l_reticulum.aioss
aioss append --chain ./l_reticulum.aioss --payload ./output.bin --module L_RETICULUM
aioss verify --chain ./l_reticulum.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="L_RETICULUM",
    aioss_chain="./L_RETICULUM.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./L_RETICULUM.aioss --verbose
python -m L_RETICULUM.tests.smoke
```
