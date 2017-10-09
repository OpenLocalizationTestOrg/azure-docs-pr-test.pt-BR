tooadd um grupo de recursos de tooa de marca, use **conjunto de grupos do azure**. Se o grupo de recursos de saudação não tem marcas existentes, passe na marca de saudação.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Marcações são atualizadas como um todo. Se você quiser tooadd um grupo de recursos de tooa marca que tem marcas existentes, passe todas as marcas de saudação. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Marcas não são herdadas pelos recursos em um grupo de recursos. tooadd um recurso de tooa de marca, use **conjunto de recursos do azure**. Passe Olá número de versão de API Olá tipo de recurso que você está adicionando marca hello. Se você precisar de versão de API de saudação tooretrieve, use Olá comando com o provedor de recursos Olá para o tipo de saudação que você está definindo a seguir:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Nos resultados de hello, procure por tipo de recurso de saudação desejado.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Agora, forneça essa versão de API, nome do grupo de recursos, nome do recurso, tipo de recurso e valor da marca como parâmetros.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Marcações existem diretamente em recursos e grupos de recursos. marcas existentes do toosee hello, obter um grupo de recursos e seus recursos com **Mostrar de grupo do azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Que retorna metadados sobre o grupo de recursos hello, incluindo qualquer tooit marcas aplicadas.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

Exibir marcas Olá para um recurso específico usando **Mostrar recurso do azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve todos os recursos de saudação com um valor de marca, use:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve todos os grupos de recursos de saudação com um valor de marca, use:

```azurecli
azure group list -t Dept=Finance
```

Você pode exibir as marcas existentes Olá em sua assinatura com hello comando a seguir:

```azurecli
azure tag list
```
