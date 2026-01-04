# Application Configuration Patterns (env vars, config files, secrets)

This document explains **how to manage application configuration**, a critical part of DevOps and cloud-native design.

Proper configuration patterns make applications **portable, secure, and easy to manage** across environments.

---

## 1. Why This Topic Matters

* Applications move between **development, staging, and production**
* Configurations often differ per environment (DB credentials, API keys)
* Secrets need special handling to avoid leaks
* Aligns directly with **Twelve-Factor App principles**

---

## 2. Environment Variables

* Store per-environment configuration (DB host, port, credentials)
* Pros:

  * Easy to change without modifying code
  * Works well in containerized apps
* Cons:

  * Can be leaked if mismanaged (logs, scripts)
* Example:

```bash
export DB_HOST=localhost
export DB_USER=admin
export DB_PASS=secret
```

---

## 3. Configuration Files

* Store structured configuration in files (JSON, YAML, INI, TOML)
* Pros:

  * Version-controlled, easy for complex configs
  * Supports default values
* Cons:

  * Requires secure handling if it contains secrets
* Example:

```yaml
database:
  host: localhost
  user: admin
  password: secret
```

---

## 4. Secrets Management

* Store sensitive data in dedicated secret management tools
* Examples: AWS Secrets Manager, HashiCorp Vault, Kubernetes Secrets
* Pros:

  * Centralized, encrypted, auditable
  * Rotatable without redeploying code
* Cons:

  * Requires additional setup and tooling

---

## 5. Best Practices

* Never hard-code secrets in the application
* Use environment variables for non-sensitive configs
* Store sensitive configs in secret stores or encrypted files
* Keep development, staging, and production configs isolated
* Document all configuration patterns for team members

---

## 6. Home Lab Mapping

* Experiment with **env vars** in Docker containers
* Store configs in **files mounted via volumes**
* Test **Kubernetes Secrets** for app credentials
* Practice rotating secrets and updating configs safely

---

## 7. You Should Now Clearly Understand

* Proper configuration patterns **enable portability and security**
* Secrets must be handled **centrally and securely**
* Your lab will give hands-on experience managing configurations across environments
* Understanding this is crucial before deploying microservices and CI/CD pipelines

---

## Next Theory Topic

[**Backend Service Flow (request → logic → DB → response)**](../15-backend-service-flow/README.md)
