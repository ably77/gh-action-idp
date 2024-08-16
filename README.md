# Github Action IDP

A demo around using IDP concepts, Platform Engineering, and GitOps to enhance the developer experience


### Useful curl commands:

Deploy a Sample Service in `team-a` namespace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/deploy-sample-service.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a"
    }
  }'
```

Deploy a Sample Service in `team-b` namespace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/deploy-sample-service.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a"
    }
  }'
```

Apply a Workspace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/apply-workspace.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "namespaces": "team-a,team-b"
    }
  }'
```

Apply a Delegate Route owned by `team-a` to expose `sample-service-team-a` in the `team-a` namespace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/apply-delegate-route.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a",
      "matchers": "/",
      "destination_kind": "SERVICE",
      "destination_name": "sample-service-team-a",
      "destination_port": "8080",
      "destination_namespace": "team-a"
    }
  }'
```

Apply a Delegate Route owned by `team-a` to expose `httpbin` in the `gh-action-idp` namespace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/apply-delegate-route.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a",
      "matchers": "get,ip",
      "destination_kind": "SERVICE",
      "destination_name": "httpbin",
      "destination_port": "8000",
      "destination_namespace": "gh-action-idp"
    }
  }'
```

Apply a Delegate Route owned by `team-b` to expose `sample-service-team-b` in the `team-b` namespace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/apply-delegate-route.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-b",
      "matchers": "/",
      "destination_kind": "SERVICE",
      "destination_name": "sample-service-team-b",
      "destination_port": "8080",
      "destination_namespace": "team-b"
    }
  }'
```

Delete all Delegate Routes owned by `team-a`
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/delete-delegate-route.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a"
    }
  }'
```

Delete all Delegate Routes owned by `team-b`
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/delete-delegate-route.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-b"
    }
  }'
```

Delete Workspace
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/delete-workspace.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp"
    }
  }'
```

Delete `team-a` Sample Service
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/delete-sample-service.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-a"
    }
  }'
```

Delete `team-b` Sample Service
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token ${GITHUB_PAT}" \
  https://api.github.com/repos/ably77/gh-action-idp/actions/workflows/delete-sample-service.yaml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "workspace_name": "gh-action-idp",
      "team_name": "team-b"
    }
  }'
```
