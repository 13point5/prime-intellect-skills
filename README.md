# Prime Intellect Skills

A collection of skills and guidelines for working with Prime Intellect's platform and tools.

## Overview

This repository contains documentation and reference materials for Prime Intellect's ecosystem. Each skill provides detailed API references, usage examples, and best practices for specific components of the Prime Intellect platform.

## Skills

### 🚀 [Prime Intellect API](./skills/prime-intellect-api/SKILL.md)

Complete API reference for Prime Intellect's GPU cloud platform. Includes documentation for:

- **Availability** - Check GPU, cluster, and disk availability and pricing
- **Pods** - Create, manage, and monitor GPU instances
- **Disks** - Network-attached storage management
- **SSH Keys** - Manage SSH keys for pod access
- **Inference** - Language model inference API for chat completions
- **Sandboxes** - Lightweight container environments
- **Images** - Custom Docker image management
- **Evals** - Evaluation management for model benchmarking
- **User** - User information and team management

### 🔜 Coming Soon

- **CLI** - Command-line interface documentation and usage guides
- **Verifiers** - Verification tools and workflows
- **Prime-RL** - Reinforcement learning framework documentation

## Structure

```
prime-intellect-guidelines/
├── README.md
└── skills/
    ├── prime-intellect-api/
    │   ├── SKILL.md          # Main skill definition and overview
    │   ├── availability.md   # GPU/cluster/disk availability API
    │   ├── pods.md            # Pod management API
    │   ├── disks.md           # Disk management API
    │   ├── ssh-keys.md        # SSH key management API
    │   ├── inference.md       # Inference API
    │   ├── sandboxes.md       # Sandbox API
    │   ├── images.md          # Custom image management API
    │   ├── evals.md           # Evaluation API
    │   └── user.md            # User and team API
    ├── cli/                   # (Coming soon)
    ├── verifiers/             # (Coming soon)
    └── prime-rl/              # (Coming soon)
```

## Usage

Each skill directory contains a `SKILL.md` file that serves as the main entry point, providing:

- Skill metadata (name, description)
- Quick reference guides
- Links to detailed documentation files

The individual documentation files contain:

- API endpoint specifications
- Request/response examples
- Authentication requirements
- Usage patterns and best practices

## Contributing

When adding new skills:

1. Create a new directory under `skills/`
2. Add a `SKILL.md` file with skill metadata and overview
3. Create individual documentation files as needed
4. Update this README with the new skill

## Resources

- [Prime Intellect Website](https://primeintellect.ai)
- [API Documentation](https://docs.primeintellect.ai/api-reference/introduction)
- [OpenAPI Interactive Explorer](https://api.primeintellect.ai/docs)

## License

MIT License
