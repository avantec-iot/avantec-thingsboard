# ta652fc_w_thermostat.json

* 使用 thingsboard.cloud 版本。

* demo.thingsboard.io 与 thingsboard.cloud 基本相同。以下部分有差异。

   ```json
   ...
     "provisionType": "CHECK_PRE_PROVISIONED_DEVICES",
   ...
    "provisionConfiguration": {
      "type": "CHECK_PRE_PROVISIONED_DEVICES",
      "provisionDeviceSecret": "TA652FC-W-TB_PROVISION-SECRET"
    },
   ...
   "provisionDeviceKey": "TA652FC-W-TB_PROVISION-KEY",
   ```

* 192.168.21.206 与 thingsboard.cloud 基本相同，如下一段有差异


   ```json
  "defaultDashboardId": {
    "entityType": "DASHBOARD",
    "id": "752954a0-8697-11ed-a9b3-4f7e77852806"
  },
   ```

