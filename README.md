# Fitter Jobs for ["It Life Berlin"](https://t.me/it_life_berlin)

# CronJobs

1. **dev_to.json** - ["0 9 * * *"] - every day 9AM
2. **steam_sales.json** - ["15 9 * * *"] - every day 9:15AM

# Example cronjob

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: fitter-dev-to-cronjob
spec:
  schedule: "0 9 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: pi
              image: ghcr.io/pxyup/fitter:v1.0.18-linux-arm64
              env:
                - name: BOT_TOKEN
                  value: "BOT_TOKEN"
                - name: CHAT_ID
                  value: "CHAT_ID"
                - name: CONFIG_URL
                  value: "https://raw.githubusercontent.com/PxyUp/it_life_berlin_fitter/refs/heads/master/dev_to.json"
              args: ["-url=https://raw.githubusercontent.com/PxyUp/it_life_berlin_fitter/refs/heads/master/dev_to.json", "--verbose", "--log-level=debug"]
          restartPolicy: Never
      backoffLimit: 4
```