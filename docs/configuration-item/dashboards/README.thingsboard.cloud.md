# ta652fc_w_thermostat_list.json

* 以 192.168.21.206 为准。
* 192.168.21.206 与 thingsboard.cloud 基本相同，如下一段有差异，可能是前者有些问题
   ?????
* demo.thingsboard.io 与 thingsboard.cloud 基本相同。以下部分有差异。

   ```json
   ...
   "fixedTimewindow": {
      "startTimeMs": 1672655374059,
      "endTimeMs": 1672741774059
   },
   ...
   "targetDashboardId": "3dfa5bf0-8b47-11ed-a522-53ac05faa748",
   ...
   ```

# ta652fc_w_thermostat__for_mobile_app_.json

* 使用 thingsboard.cloud 版本。

* demo.thingsboard.io 与 thingsboard.cloud 基本相同。timewindow部分都有差异。

   ```json
   ...
   "timewindow": {
      "displayValue": "",
      "selectedTab": 0,
      "realtime": {
         "realtimeType": 1,
         "interval": 1000,
         "timewindowMs": 60000,
         "quickInterval": "CURRENT_DAY"
      },
      "history": {
         "historyType": 0,
         "interval": 1000,
         "timewindowMs": 60000,
         "fixedTimewindow": {
            "startTimeMs": 1679882021328,
            "endTimeMs": 1679968421328
         },
         "quickInterval": "CURRENT_DAY"
      },
      "aggregation": {
         "type": "AVG",
         "limit": 2500
      }
   ...
   ```

* 192.168.21.206 与 thingsboard.cloud 基本相同，如下一段有差异，可能是前者有些问题

   ```json
   "entityAliases": {
      "39e9ec11-bd6b-c6c0-4cdf-cc54e491c25b": {
        "id": "39e9ec11-bd6b-c6c0-4cdf-cc54e491c25b",
        "alias": "TA652FC-W",
        "filter": {
          "type": "stateEntity",
          "resolveMultiple": false,
          "stateEntityParamName": null,
          "defaultStateEntity": {
            "entityType": "DEVICE",
            "id": "c58b8420-4a99-11ed-88cf-3bc720ab387f"
          }
        }
      },
      "323f24e7-0464-49db-4eca-23d1103b993b": {
        "id": "323f24e7-0464-49db-4eca-23d1103b993b",
        "alias": "Current thermostat",
        "filter": {
          "type": "stateEntity",
          "resolveMultiple": false,
          "stateEntityParamName": null,
          "defaultStateEntity": null
        }
      }
    },
    ```


# ta652fh_w_thermostat_list.json

* 以 192.168.21.206 为准。
* 192.168.21.206， demo.thingsboard.io 与 thingsboard.cloud 三者基本相同。仅timewindow部分都有差异。

# ta652fh_w_thermostat__for_mobile_app_.json

* 192.168.21.206， demo.thingsboard.io 与 thingsboard.cloud 三者基本相同。仅timewindow部分都有差异。

# firmware.json

* 使用 192.168.21.206 版本。

# thermostat.json

* 192.168.21.206 与 thingsboard.cloud 各不相同。 不清楚谁是最新的，可能前者还在继续修改。
