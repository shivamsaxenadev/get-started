# Local Reverse Geocoder

This application provides a reverse geocoder service using the [tomayac/local-reverse-geocoder](https://github.com/tomayac/local-reverse-geocoder) Docker image.

## Configuration

The application can be configured by modifying the ConfigMap values in `configmap.yaml` or by updating the `configMapGenerator` section in `kustomization.yaml`. The following configuration parameters are available:

| Parameter      | Description                                      | Default |
| -------------- | ------------------------------------------------ | ------- |
| REPLICAS       | Number of replicas to run                        | 2       |
| CPU_REQUEST    | CPU resource request                             | 100m    |
| CPU_LIMIT      | CPU resource limit (empty string means no limit) | ""      |
| MEMORY_REQUEST | Memory resource request                          | 128Mi   |
| MEMORY_LIMIT   | Memory resource limit                            | 256Mi   |

Additionally, the application is configured with the following environment variables:

| Variable | Description                           | Value |
| -------- | ------------------------------------- | ----- |
| PORT     | Port on which the application listens | 80    |

## Usage

The service is exposed within the cluster at `local-reverse-geocoder.local-reverse-geocoder.svc.cluster.local`.

Example API usage:

```
# Access within the cluster
curl -X POST "http://local-reverse-geocoder.local-reverse-geocoder.svc.cluster.local/geocode" \
  -H "Content-Type: application/json" \
  -d '{"latitude": 40.7128, "longitude": -74.0060}'
```

## Exposing the Service

The service is configured as a ClusterIP type, which means it's only accessible from within the cluster. If you need to expose this service externally, you can create an Ingress resource or modify the Service type to LoadBalancer or NodePort.
