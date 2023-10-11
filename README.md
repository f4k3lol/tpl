# tpl

Данный чарт представляет собой чарт-шаблон с значениями по-умолчанию, который можно использовать как зависимость

https://hub.docker.com/r/f4k3lol/tpl

```yaml
dependencies:
  - name: tpl
    version: 0.11.0
```


## Переменные

|Key|Type|Default|Description|
|-|-|-|-|
| **Общие переменные** |
| kind | string | "Deployment" | Тип шаблона. Может быть `Deployment` или `StatefulSet`
| replicaCount | int | 1 | Кол-во реплик в replicaset
| imagePullSecrets | list | [] | imagePullSecrets для контейнеров пода
| nameOverride | string | "" | переопределяет имя чарта
| fullNameOverride | string | "" | переопределяет имя инстанса чарта
| podAnnotations | object | {} | Аннотации пода в формате k: v
| enableServiceLinks | bool | false | enableServiceLinks пода
| nodeSelector | object | {} | nodeSelector пода
| topologySpreadConstraints | list | [] | topologySpreadConstraints пода
| tolerations | list | [] | tolerations пода
| affinity | object | {} | affinity пода
| extraValues | object | {} | по умолчанию не используется, может быть использовано при шаблонизации чартов (`{{ .Values.extraValues.x }}`). Может быть применено в `containers.*.configs`
| extraManifests | list | [] | дополнительные k8s манифесты в raw-виде
| terminationGracePeriodSeconds | int | null | terminationGracePeriodSeconds пода
| **Deployment переменные** | используются только при `kind == "Deployment"` |
| autoscaling | object | см. ниже | настройки hpa пода
| autoscaling.enabled | bool | false | флаг для включения hpa
| autoscaling.minReplicas | int | 1 | hpa minReplicas
| autoscaling.maxReplicas | int | 20 | hpa maxReplicas
| autoscaling.behavior | object | {} | hpa behavior
| autoscaling.metrics | list | [] | hpa metrics
| strategy | object | см. ниже | настройки strategy деплоймента
| strategy.type | string | RollingUpdate | тип strategy
| **StatefulSet переменные** | используются только при `kind == "StatefulSet"` |
| defaultVolumeClaimTemplateSpec | object | {} | Описание дефолтов для поля spec каждого volumeClaimTemplate (`volumeClaimTemplates.[*].spec`)
| volumeClaimTemplates | list | [] | Описание volumeClaimTemplates
| serviceName | string | "" | statefulset serviceName, имя сервиса, используемое в statefulset
| minReadySeconds | int | 0 | statefulset minReadySeconds
| podManagementPolicy | string | "OrderedReady" | statefulset podManagementPolicy
| updateStrategy | object | см. ниже | statefulset updateStrategy
| updateStrategy.type | string | "RollingUpdate" | statefulset updateStrategy.type
| persistentVolumeClaimRetentionPolicy | object | см. ниже | statefulset persistentVolumeClaimRetentionPolicy
| persistentVolumeClaimRetentionPolicy.whenDeleted | string | "Retain" | statefulset persistentVolumeClaimRetentionPolicy.whenDeleted
| persistentVolumeClaimRetentionPolicy.whenScaled | string | "Retain" | statefulset persistentVolumeClaimRetentionPolicy.whenScaled
| **Переменные с описанием приложения** |
| defaultContainer | object | см. [values.yaml](/values.yaml) | описание дефолтов контейнера, которые будут применяться к каждому обозначенному контейнеру в `containers:`
| defaultService | object | см. [values.yaml](/values.yaml) | описание дефолтов сервиса, которые будут применяться к каждому обозначенному сервису в `services:`
| defaultIngress | object | см. [values.yaml](/values.yaml) | описание дефолтов ингресса, которые будут применяться к каждому обозначенному ингрессу в `services.*.ingresses:`
| containers | object | см. [example.yaml](/example.yaml) | описание контейнеров пода в формате `name: spec` - обязательно нужен хотя бы 1 контейнер
| services | object | см. [example.yaml](/example.yaml) | описание сервисов в формате `name: spec`
