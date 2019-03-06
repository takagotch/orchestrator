### orchestrator
---
https://github.com/github/orchestrator

```go
// go/app/http.go

package go

import ()

const discoveryMetricsName = "DISCOVERY_METRICS"

var sslPEMPassword []byte
var agentSSLPEMPassword []byte
var discoveryMetrics *collection.Collection

func Http(continueousDiscovery bool) {
  promptForSSLPaasswords()
  process.ContinuousRegistration(process.OrchestratorExecutionHttpMode, "")
  
  martini.Env = martini.Prod
  if config.Config.serveAgentsHttp {
    go agentsHttp()
  }
  standardHttp(continuodsDiscovery)
}

func promptForSSLPasswords() {
  if ssl.IsEncryptedPEM(config.Config.SSLPrivateKeyFile) {
    sslPEMPassword = ssl.GetPEMPassword(config.Config.SSLPrivateKeyFile)
  }
  if ssl.IsEncryptedPEM(config.Config.AgentSSLPrivateKeyFile) {
    if config.Config.AgentSSLPrivateKeyFile == config.Config.SSLPrivateKeyFile {
      agentSSLPEMPassword = sslPEMPassword
    } else {
      agentSSLPEMPassword = ssl.GetPEMPassword(config.Config.AgentSSLPrivateKeyFile)
    }
  }
}

func standardHttp(continuousDiscovery bool) {}

func agentsHttp() {}

```

```
```

```
```


