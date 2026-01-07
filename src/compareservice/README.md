# Compare Service

## Purpose
Compare Service compares 2–3 products by ID and returns a side-by-side payload pulled from the product catalog service.

## Local run
```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
PORT=8080 PRODUCT_CATALOG_SERVICE_ADDR=localhost:3550 python compareservice.py
```

## Docker build/run
```bash
docker build -t compareservice:dev .
docker run -p 8080:8080 \
  -e PORT=8080 \
  -e PRODUCT_CATALOG_SERVICE_ADDR=host.docker.internal:3550 \
  compareservice:dev
```

## Kubernetes/Skaffold
```bash
skaffold dev
# or
skaffold run
```

Check the service:
```bash
kubectl get pods
kubectl port-forward svc/compareservice 8080:80
```

## API usage examples
```bash
curl -X POST localhost:8080/compare \
  -H 'Content-Type: application/json' \
  -d '{"product_ids":["OLJCESPC7Z","66VCHSJNUP"]}'
```

The OpenAPI specification is served at `http://localhost:8080/openapi.yaml` and stored locally at `openapi.yaml`.

## Testing
```bash
pytest -q
```

This runs the compareservice unit tests (if present) and reports any failures.

## Acceptance criteria
- README provides a reproducible local/Docker/Kubernetes runbook and curl examples.
- Commands run as written.
