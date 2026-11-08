# Developer Cookbook — L_RETICULUM
**Stack:** Python 3.11, rns 0.x (Reticulum), PAX 27B, AIOSS_FORMAT
**Domain:** Reticulum: cryptography-based mesh networking for Anticloud sovereign communications

## Reticulum mesh inference
```python
from l_reticulum import ReticulumPAXBridge

bridge = ReticulumPAXBridge(
    config_dir="./reticulum_config/",
    pax_model="./pax-27b-q4.gguf",
    aioss_chain="./reticulum.aioss"
)

bridge.start()
print(f"Reticulum address: {bridge.identity.hexhash}")

for request in bridge.inference_requests():
    response = bridge.pax_inference(request.query, request.schema)
    request.reply(response.compressed_json)
    print(f"Served {request.source_hash[:8]}: {response.summary}")
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
