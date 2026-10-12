# SpeakUp models

Speech-recognition and speaker-embedding model files used by the SpeakUp Android app (on-device, offline).
They are downloaded once by the app (HTTPS, SHA-256-verified) — nothing is sent anywhere.

| File | Size | SHA-256 |
|---|---|---|
| `encoder.onnx` | 945,740,319 | `75bbfa3eed18f31a68154c60e78bad810b21cba3f488d9d25fdacd924876005e` |
| `decoder_joint.onnx` | 72,520,893 | `e978ddf6688527182c10fde2eb4b83068421648985ef23f7a86be732be8706c1` |
| `vocab.txt` | 93,939 | `d58544679ea4bc6ac563d1f545eb7d474bd6cfa467f0a6e2c1dc1c7d37e3c35d` |
| `speaker.onnx` | 26,535,549 | `3955447b0499dc9e0a4541a895df08b03c69098eba4e56c02b5603e9f7f4fcbb` |

Files are attached to the **Releases** page (tag `v1`), not stored in git.

## What these are

- **ASR (`encoder.onnx`, `decoder_joint.onnx`, `vocab.txt`)** — NVIDIA [parakeet-tdt-0.6b-v3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3)
  (25 European languages incl. Dutch), licensed **CC-BY-4.0** © NVIDIA. ONNX export by
  [istupakov/parakeet-tdt-0.6b-v3-onnx](https://huggingface.co/istupakov/parakeet-tdt-0.6b-v3-onnx).
  **Modification:** the encoder's MatMul weights were quantized to 8-bit weight-only (`MatMulNBits`, block size 32, symmetric,
  onnxruntime 1.31); activations stay float. This keeps accuracy close to fp32 (and is much more robust to noisy audio than the
  common dynamic-int8 builds) while running ~10x faster than real time on a phone CPU. The decoder is the unmodified fp32 graph saved as a single file.
- **Speaker embeddings (`speaker.onnx`)** — [WeSpeaker](https://github.com/wenet-e2e/wespeaker) voxceleb ResNet34-LM
  (Apache-2.0), ONNX conversion from [onnx-community/wespeaker-voxceleb-resnet34-LM](https://huggingface.co/onnx-community/wespeaker-voxceleb-resnet34-LM).

Requires ONNX Runtime ≥ 1.31 (8-bit MatMulNBits on ARM).

## License

Model weights: CC-BY-4.0 (attribution to NVIDIA as above; changes indicated above). WeSpeaker: Apache-2.0.
