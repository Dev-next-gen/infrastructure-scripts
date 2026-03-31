# infrastructure-scripts

> Battle-tested infrastructure scripts for AI compute deployments. Accumulated from managing ~300 GPU clusters and freelance AI infrastructure work.

## Scripts

### ROCm Setup

```bash
# Full ROCm 6.x installation on Ubuntu 22.04
./rocm/install-rocm.sh --version 6.0 --gpus "rx7900xtx"

# Verify all GPUs detected
./rocm/verify-gpus.sh

# Configure optimal environment variables
source ./rocm/env-setup.sh
```

### Multi-GPU LLM Server

```bash
# Launch llama.cpp with all detected AMD GPUs
./llm/launch-multi-gpu.sh   --model /models/qwen2.5-72b-q4_k_m.gguf   --ctx 131072   --flash-attn

# Auto-split model across available GPUs
./llm/auto-split.sh --model-size 72b --vram-per-gpu 24
```

### Server Hardening

```bash
# Minimal hardening for AI inference servers
./security/harden-server.sh --profile inference

# Firewall setup (inference server)
./security/setup-firewall.sh --allow-ports "8080,8081,9090"
```

### Monitoring Setup

```bash
# Install Prometheus + Grafana + GPU exporter
./monitoring/setup-stack.sh

# GPU metrics exporter for AMD
./monitoring/amd-gpu-exporter.sh --port 9400
```

## MultiAMDGPU Dev

Quick setup for multi-GPU development environments:

```bash
./amd/multiamgpu-dev-setup.sh --gpus 5 --driver rocm6
```

## Directory Structure

```
infrastructure-scripts/
├── rocm/
│   ├── install-rocm.sh
│   ├── verify-gpus.sh
│   └── env-setup.sh
├── llm/
│   ├── launch-multi-gpu.sh
│   ├── auto-split.sh
│   └── benchmark.sh
├── security/
│   ├── harden-server.sh
│   └── setup-firewall.sh
├── monitoring/
│   ├── setup-stack.sh
│   └── amd-gpu-exporter.sh
└── amd/
    └── multiamgpu-dev-setup.sh
```

## License

MIT — Léo Camus / [NextGen Labs](https://nextgen-labs.net)
