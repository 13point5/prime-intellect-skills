# Images API

Custom Docker image management for pods.

## Endpoints

### GET List User Images
```
GET /api/v1/images
```

Lists all custom images owned by the user.

### POST Initiate Image Build
```
POST /api/v1/images/build/initiate
```

Initiates a new image build process.

### POST Start Image Build
```
POST /api/v1/images/build/{build_id}/start
```

Starts the actual build after initiation.

### GET Build Status
```
GET /api/v1/images/build/{build_id}/status
```

Check the status of an ongoing build.

### GET List Image Builds
```
GET /api/v1/images/builds
```

Lists all image builds (completed and in progress).

### DELETE User Image
```
DELETE /api/v1/images/{image_id}
```

## Using Custom Images with Pods

1. Build and upload your custom image
2. When creating a pod, set:
   ```json
   {
     "pod": {
       "image": "custom_template",
       "customTemplateId": "your_image_id"
     }
   }
   ```

## Pre-built Images

Available images (no custom build needed):
- `ubuntu_22_cuda_12` - Base Ubuntu with CUDA 12
- `cuda_12_4_pytorch_2_5` - PyTorch 2.5 with CUDA 12.4
- `cuda_12_6_pytorch_2_7` - PyTorch 2.7 with CUDA 12.6
- `stable_diffusion` - Stable Diffusion setup
- `axolotl` - Axolotl fine-tuning
- `vllm_llama_8b/70b/405b` - vLLM with Llama models
- `prime_rl` - Reinforcement learning environment

## Template Validation

### POST Check Docker Image
```
POST /api/v1/templates/check-image
```

Validates a Docker image before building.

### GET List Registry Credentials
```
GET /api/v1/templates/registry-credentials
```

Lists saved container registry credentials.
