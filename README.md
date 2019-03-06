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

func agentsHttp() {
  m := martini.Classic()
  m.Use(gzip.All())
  m.Use(render.Renderer())
  if config.Config.AgentsUseMutualTLS {
    m.Use(ssl.VerifyOUs(config.Config.AgentSSLValidOUs))
  }
  
  log.Info("Starting agents listener")
  
  agent.AgentsAPI.URLPrefix = config.Config.URLPrefix
  http.AgentsAPI.RegisterRequests(m)
  
  if config.Config.AgentsUseSSL {
  
  } else {
    log.Info("Starting agent HTTP listener")
    if err := nethttp.ListenAndServe(config.Config.AgentsServerPort, m); err != nil {
    　　log.Fatale(err)
    }
  }
  log.Info("Agent server started")
}

```

```
```

```
```


