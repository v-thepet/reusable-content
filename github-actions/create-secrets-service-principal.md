---
ms.topic: include
ms.technology: devops-cicd
ms.manager: mijacobs
ms.author: jukullam
author: juliakm
ms.date: 09/19/2022
---

# [Service principal](#tab/userlevel)

1. In [GitHub](https://github.com/), browse your repository, select **Settings > Secrets > Actions**.

:::image type="content" source="media/select-secrets.png" alt-text="Screenshot of select secrets. ":::

1. Select **New repository secret**.

1. Paste the entire JSON output from the Azure CLI command into the secret's value field. Give the secret the name `AZURE_CREDENTIALS`.
