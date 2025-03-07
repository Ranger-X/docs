---
title: "Viewing the execution log in Yandex Cloud Functions"
description: "You can view the monitoring schedule in Yandex Cloud Functions using the management console. To do this, select the Cloud Functions service, click on the function whose execution log you want to view. In the window that opens, go to the Logs section and specify the period. By default, the period is set in 1 hour. The function execution logs are stored for 14 days. The time in the log is specified in UTC."
---

# Viewing the execution log

Function execution logs are stored for 14 days. The log uses [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

{% list tabs %}

- Management console

    1. Select **{{ sf-name }}** in the [management console]({{ link-console-main }}).
    1. Click the function you want to view the execution log for.
    1. In the window that opens, go to **Logs** and specify the time period. The default time period is 1 hour.

- CLI

    {% include [timeslot](../../../_includes/functions/timeslot.md) %}

    {% include [cli-install](../../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

    {% include [function-list-note](../../../_includes/functions/function-list-note.md) %}

    View the function execution log:

    ```
    yc serverless function logs <function name>
    ```

    Result:

    ```
    2019-07-04 09:27:43     START RequestID: 34dc9533-ed6e-4468-b9f2-2aa082266fad Version: b09i2s85a0c1fisjboft
    2019-07-04 09:27:43     END RequestID: 34dc9533-ed6e-4468-b9f2-2aa082266fad
    2019-07-04 09:27:43     REPORT RequestID: 34dc9533-ed6e-4468-b9f2-2aa082266fad Duration: 538.610 ms Billed Duration: 538.700 ms Memory Size: 128 MB Max Memory Used: 13 MB
    2019-07-04 09:29:25     START RequestID: 5b6a3779-dcc8-44ec-8ee2-2e7f279394ef Version: b09i2s85a0c1fisjboft
    2019-07-04 09:29:26     END RequestID: 5b6a3779-dcc8-44ec-8ee2-2e7f279394ef
    2019-07-04 09:29:26     REPORT RequestID: 5b6a3779-dcc8-44ec-8ee2-2e7f279394ef Duration: 554.904 ms Billed Duration: 555.000 ms Memory Size: 128 MB Max Memory Used: 13 MB
    ...
    ```

    {% note info %}

    If you called a function with a specific tag, you must also specify this tag when viewing the execution log: `yc serverless function logs my-python-function --tag test`.

    {% endnote %}

- Yandex.Cloud Toolkit

    You can view the function execution log using the [Yandex.Cloud Toolkit plugin](https://github.com/yandex-cloud/ide-plugin-jetbrains/blob/master/README.en.md) for the family of IDEs on the [IntelliJ platform](https://www.jetbrains.com/opensource/idea/) from [JetBrains](https://www.jetbrains.com/).

{% endlist %}

Learn more about working with logs in the [{{ cloud-logging-full-name }} documentation](../../../logging/).

