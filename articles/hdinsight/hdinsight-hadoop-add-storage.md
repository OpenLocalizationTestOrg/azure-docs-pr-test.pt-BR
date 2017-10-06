---
title: contas de armazenamento do Azure adicionais aaaAdd tooHDInsight | Microsoft Docs
description: Saiba como tooadd adicionais de armazenamento do Azure contas tooan cluster de HDInsight existente.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Adicionar tooHDInsight de contas de armazenamento adicional

Saiba como toouse script ações tooadd mais armazenamento do Azure contas tooHDInsight. Olá, as etapas neste documento adicionam um cluster de HDInsight baseados em Linux existente do armazenamento conta tooan.

> [!IMPORTANT]
> informações de saudação neste documento são sobre como adicionar armazenamento adicional tooa cluster após ele ter sido criado. Para saber mais sobre como adicionar contas de armazenamento durante a criação do cluster, veja [Configurar clusters no HDInsight com Hadoop, Spark, Kafka e muito mais](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Como ele funciona

Esse script usa Olá parâmetros a seguir:

* __Nome da conta de armazenamento do Azure__: nome Olá Olá conta tooadd toohello HDInsight do cluster de armazenamento. Depois de executar o script hello, HDInsight pode ler e gravar dados armazenados nesta conta de armazenamento.

* __Chave de conta de armazenamento do Azure__: uma chave que concede a conta de armazenamento de toohello de acesso.

* __-p__ (opcional): se for especificado, a chave de Olá não é criptografado e é armazenado no arquivo de Core-site.XML hello como texto sem formatação.

Durante o processamento, o script hello executa Olá ações a seguir:

* Se hello conta de armazenamento já existe na configuração de Core-site.XML Olá para cluster hello, Olá script será encerrado e nenhuma ação adicional é executadas.

* Verifica se a conta de armazenamento Olá existe e pode ser acessada usando a chave de saudação.

* Criptografa a chave de saudação usando credenciais de cluster hello.

* Adiciona Olá armazenamento conta toohello Core-site.XML arquivo.

* Para e reinicia os serviços de saudação Oozie, YARN, MapReduce2 e HDFS. Parar e iniciar esses serviços permitem toouse Olá nova conta de armazenamento.

> [!WARNING]
> Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente.

## <a name="hello-script"></a>script Hello

__Local do script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Requisitos__:

* script Hello deve ser aplicada em Olá __nós de cabeçalho__.

## <a name="toouse-hello-script"></a>script de saudação toouse

Esse script pode ser usado em Olá portal do Azure, Azure PowerShell, ou Olá 1.0 da CLI do Azure. Para obter mais informações, consulte Olá [usando a ação de script de clusters HDInsight baseados em Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.

> [!IMPORTANT]
> Ao usar etapas Olá fornecidas no documento de personalização hello, use Olá tooapply informações a seguir este script:
>
> * Substitua qualquer ação de script de exemplo URI hello URI para esse script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Substitua quaisquer parâmetros de exemplo com o nome de conta de armazenamento do Azure hello e chave Olá conta toobe toohello adicionado do cluster de armazenamento. Se usar hello portal do Azure, esses parâmetros devem ser separados por um espaço.
> * Você não precisa toomark esse script como __Persisted__, como ele atualizações de configuração do Ambari Olá para cluster Olá diretamente.

## <a name="known-issues"></a>Problemas conhecidos

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Contas de armazenamento não exibidas no Portal do Azure ou nas ferramentas

Ao exibir hello HDInsight cluster no hello portal do Azure, selecionando Olá __contas de armazenamento__ entrada em __propriedades__ não mostra as contas de armazenamento adicionadas por esta ação de script. Azure PowerShell e a CLI do Azure não exibem conta de armazenamento adicional da saudação ou.

informações de armazenamento de saudação não são exibidas porque o script hello apenas modifica a configuração de Core-site.XML de saudação para cluster hello. Essas informações não são usadas ao recuperar informações de cluster hello usando APIs de gerenciamento do Azure.

informações de conta de armazenamento tooview adicionado cluster toohello usando esse script, use Olá API REST do Ambari. Olá tooretrieve comandos a seguir ao Use essas informações para seu cluster:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Definir `$clusterName` toohello nome do cluster do HDInsight hello. Definir `$storageAccountName` toohello nome hello da conta de armazenamento. Quando solicitado, insira o logon de cluster da saudação (administrador) e a senha.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Definir `$PASSWORD` toohello senha da conta de logon (admin) de cluster. Definir `$CLUSTERNAME` toohello nome do cluster do HDInsight hello. Definir `$STORAGEACCOUNTNAME` toohello nome hello da conta de armazenamento.
>
> Este exemplo usa [ondulação (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve e análise de dados JSON.

Ao usar esse comando, substitua __CLUSTERNAME__ com o nome de saudação do cluster do HDInsight hello. Substituir __senha__ com a senha de logon de saudação HTTP para o cluster hello. Substituir __STORAGEACCOUNT__ com nome Olá Olá da conta de armazenamento adicionada usando a ação de script. Informações retornadas deste comando será exibida semelhante toohello texto a seguir:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Esse texto é um exemplo de uma chave criptografada, que é usada tooaccess Olá conta de armazenamento.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Não é possível tooaccess armazenamento depois de alterar a chave

Se você alterar a chave de saudação para uma conta de armazenamento, HDInsight não pode acessar a conta de armazenamento hello. HDInsight usa uma cópia armazenada em cache de chave em Olá Core-site.XML para cluster hello. Essa cópia armazenada em cache deve ser a nova chave de saudação toomatch atualizado.

Executado novamente ação de script hello __não__ atualizar chave hello, conforme o script hello verifica toosee se já existe uma entrada para a conta de armazenamento hello. Se já houver uma entrada, ele não fará alterações.

toowork alternativa para esse problema, você deve remover a entrada existente Olá Olá conta de armazenamento. Use Olá entrada existente de saudação de tooremove de etapas a seguir:

1. Em um navegador da web, abra a saudação da interface do usuário do Ambari Web para seu cluster HDInsight. Olá URI é https://CLUSTERNAME.azurehdinsight.net. Substituir __CLUSTERNAME__ com nome de saudação do cluster.

    Quando solicitado, insira o usuário de logon do hello HTTP e a senha para seu cluster.

2. Na lista de saudação de serviços esquerda Olá da página hello, selecione __HDFS__. Em seguida, selecione Olá __configurações__ guia no Centro de saudação da página de saudação.

3. Em Olá __filtro...__  campo, digite um valor de __fs.azure.account__. Isso retorna as entradas para as contas de armazenamento adicional que foram adicionadas toohello cluster. Há dois tipos de entradas; __keyprovider__ e __key__. Conter nome Olá Olá da conta de armazenamento como parte do nome da chave hello.

    Olá, a seguir está exemplos de entradas para uma conta de armazenamento denominada __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Depois de ter identificado chaves Olá Olá conta de armazenamento é necessário tooremove, use Olá vermelho '-' toohello ícone à direita da saudação entrada toodelete-lo. Em seguida, usar Olá __salvar__ botão toosave suas alterações.

5. Depois que as alterações foram salvas, use conta de armazenamento de Olá Olá script ação tooadd e o novo cluster de toohello do valor de chave.

### <a name="poor-performance"></a>Desempenho ruim

Se a conta de armazenamento Olá estiver em uma região diferente cluster do HDInsight hello, você pode enfrentar desempenho insatisfatório. Acessar os dados de um região diferente envia tráfego de rede fora hello Azure data center regional e em Olá internet pública, que pode apresentar latência.

> [!WARNING]
> Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá uma região diferente.

### <a name="additional-charges"></a>Custos adicionais

Se a conta de armazenamento Olá é em uma região diferente de Olá cluster HDInsight, você pode perceber encargo adicional na sua cobrança do Azure. Um encargo de saída é aplicado quando os dados saem de um data center regional. Essa taxa será aplicada mesmo que o tráfego de saudação é destinado para outro data center do Azure em uma região diferente.

> [!WARNING]
> Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá uma região diferente.

## <a name="next-steps"></a>Próximas etapas

Você aprendeu como contas de armazenamento adicional tooadd tooan cluster de HDInsight existente. Para saber mais sobre as ações de script, confira [Personalizar clusters HDInsight com base em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)
