---
title: "aaaConfigure um nome de domínio personalizado para seu ponto de extremidade de armazenamento de BLOBs do Azure | Microsoft Docs"
description: "Use seu próprio ponto de extremidade de armazenamento de Blob de toohello de nome canônico (CNAME) a Olá toomap portal do Azure em uma conta de armazenamento do Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Configurar um nome de domínio personalizado para seu ponto de extremidade de Armazenamento de Blobs

Você pode configurar um domínio personalizado para acessar os dados de blob em sua conta de armazenamento do Azure. Olá ponto de extremidade padrão para armazenamento de Blob é `<storage-account-name>.blob.core.windows.net`. Se você mapear um domínio personalizado e o subdomínio como **www.contoso.com** toohello ponto de extremidade de blob para sua conta de armazenamento, os usuários podem acessar dados em sua conta de armazenamento usando esse domínio de blob.

> [!IMPORTANT]
> O Armazenamento do Azure ainda não dá suporte nativo a HTTPS com domínios personalizados. É possível no momento [usar blobs do hello Azure CDN tooaccess com domínios personalizados via HTTPS](./storage-https-custom-domain-cdn.md).
>

Olá, tabela a seguir mostra alguns URLs de exemplo para dados de blob localizados em uma conta de armazenamento denominada **mystorageaccount**. domínio personalizado Olá registrado para a conta de armazenamento Olá **www.contoso.com**:

| Tipo de recurso | URL padrão | URL de domínio personalizada |
| --- | --- | --- |
| Conta de armazenamento | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| Blob |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Contêiner raiz | http://mystorageaccount.blob.core.windows.net/myblob ou http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob ou http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Mapeamento de domínio direto versus intermediário

Há dois toopoint de maneiras seu ponto de extremidade de blob de toohello de domínio personalizado para sua conta de armazenamento: direcionar CNAME mapeamento e usando Olá *asverify* subdomínio intermediário.

### <a name="direct-cname-mapping"></a>Mapeamento direto de CNAME

Olá primeiro e mais simples, o método é toocreate um registro de nome canônico (CNAME) que mapeia o domínio e subdomínio personalizados diretamente toohello ponto de extremidade de blob. Um registro CNAME é um recurso DNS (sistema) do nome de domínio que mapeia um domínio de destino de tooa de domínio de origem. Nesse caso, o domínio de origem Olá é seu próprio domínio e subdomínio personalizados, por exemplo *www.contoso.com*. o domínio de destino Olá é seu ponto de extremidade de serviço Blob, por exemplo  *mystorageaccount.blob.Core.Windows.NET*.

método direto Hello é abordado em [registrar um domínio personalizado](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Mapeamento intermediário com *asverify*

método segundo Hello também usa os registros CNAME, mas primeiro emprega um subdomínio especial reconhecido pelo tempo de inatividade do Azure tooavoid: **asverify**.

processo de saudação do mapeamento de seu ponto de extremidade de blob do domínio personalizado tooa pode resultar em um breve período de tempo de inatividade para domínio Olá enquanto você estiver registrando-lo no hello [portal do Azure](https://portal.azure.com). Se seu domínio personalizado no momento está dando suporte a um aplicativo com um contrato de nível de serviço (SLA) que requer tempo de inatividade zero, você pode usar o hello Azure *asverify* subdomínio como uma etapa de registro intermediário. Esta etapa intermediária garante que os usuários são tooaccess capaz de seu domínio enquanto o mapeamento de DNS Olá ocorre.

método intermediário Hello é abordado em [registrar um domínio personalizado usando Olá *asverify* subdomínio](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Registrar um domínio personalizado
Use este procedimento tooregister seu domínio personalizado se você tiver sem preocupações sobre domínio Olá sendo usuários tooyour temporariamente indisponível, ou se o seu domínio personalizado não está hospedando atualmente um aplicativo.

Se seu domínio personalizado no momento está dando suporte a um aplicativo que não pode ter qualquer tempo de inatividade, execute o procedimento de saudação descrito no [registrar um domínio personalizado usando Olá *asverify* subdomínio](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure um nome de domínio personalizado, você deve criar um novo registro CNAME no DNS. Olá registro CNAME Especifica um alias para um nome de domínio. Nesse caso, ele mapeia o endereço de saudação do ponto de extremidade de armazenamento de Blob seu domínio personalizado toohello para sua conta de armazenamento.

Normalmente, você pode gerenciar as configurações de DNS do seu domínio no site do registrador de domínios. Cada registro tem um método semelhante, mas um pouco diferentes de especificar um registro CNAME, mas o conceito de saudação é Olá mesmo. Alguns pacotes de registro de domínio básico não oferecem configuração de DNS, portanto, talvez seja necessário tooupgrade seu pacote de registro de domínio antes de criar o registro CNAME hello.

1. Navegue de conta de armazenamento tooyour Olá [portal do Azure](https://portal.azure.com).
1. Em **serviço BLOB** na folha de menu hello, selecione **domínio personalizado** tooopen Olá *domínio personalizado* folha.
1. Faça logon no site do registrador de domínio tooyour e vá para a página toohello para gerenciar DNS. Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.
1. Localize seção Olá para gerenciar CNAMEs. Você pode ter a página de configurações avançadas de tooan toogo e procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
1. Crie um novo registro CNAME e forneça um alias de subdomínio, como **www** ou **photos**. Forneça um nome de host, que é o serviço ponto de extremidade Blob, no formato de saudação **mystorageaccount.blob.core.windows.net** (onde *mystorageaccount* é o nome da saudação da sua conta de armazenamento). Olá toouse de nome de host é exibida no item #1 de saudação *domínio personalizado* folha em Olá [portal do Azure](https://portal.azure.com).
1. Na caixa de texto de saudação Olá *domínio personalizado* folha em Olá [portal do Azure](https://portal.azure.com), digite nome de saudação do seu domínio personalizado, incluindo o subdomínio hello. Por exemplo, se o domínio for **contoso.com** e o alias de subdomínio for **www**, digite **www.contoso.com**. Se o subdomínio for **fotos**, digite **photos.contoso.com**. Olá subdomínio for *necessária*.
1. Selecione **salvar** em Olá *domínio personalizado* folha tooregister seu domínio personalizado. Se o registro de saudação for bem-sucedida, você verá uma notificação no portal de sua conta de armazenamento foi atualizada com êxito.

Depois que o novo registro CNAME se propague através do DNS, os usuários podem exibir dados de blob usando seu domínio personalizado, desde que eles têm permissões apropriadas hello.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Registrar um domínio personalizado usando Olá *asverify* subdomínio
Use este procedimento tooregister seu domínio personalizado se seu domínio personalizado no momento está dando suporte a um aplicativo com um SLA que requer que haja sem tempo de inatividade. Criando um CNAME que aponte de `asverify.<subdomain>.<customdomain>` muito`asverify.<storageaccount>.blob.core.windows.net`, previamente, você pode registrar seu domínio com o Azure. Você pode criar um segundo CNAME que aponte de `<subdomain>.<customdomain>` muito`<storageaccount>.blob.core.windows.net`, no ponto em que o domínio personalizado do tráfego tooyour será direcionado tooyour ponto de extremidade de blob.

Olá **asverify** subdomínio é um subdomínio especial reconhecido pelo Azure. Acrescentando `asverify` subdomínio da própria tooyour, você permite que toorecognize Azure seu domínio personalizado sem modificar o registro DNS Olá para o domínio de saudação. Quando você modifica o registro DNS Olá para domínio hello, será mapeada toohello o ponto de extremidade de blob sem tempo de inatividade.

1. Navegue de conta de armazenamento tooyour Olá [portal do Azure](https://portal.azure.com).
1. Em **serviço BLOB** na folha de menu hello, selecione **domínio personalizado** tooopen Olá *domínio personalizado* folha.
1. Faça logon no site do provedor DNS tooyour e vá para a página toohello para gerenciar DNS. Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.
1. Localize seção Olá para gerenciar CNAMEs. Você pode ter a página de configurações avançadas de tooan toogo e procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
1. Criar um novo registro CNAME e forneça um alias de subdomínio que inclui a saudação *asverify* subdomínio. Por exemplo, **asverify. www** ou **asverify.photos**. Forneça um nome de host, que é o serviço ponto de extremidade Blob, no formato de saudação **asverify.mystorageaccount.blob.core.windows.net** (onde **mystorageaccount** é o nome da saudação da sua conta de armazenamento). Olá toouse de nome de host é exibida no item #2 de saudação *domínio personalizado* folha em Olá [portal do Azure](https://portal.azure.com).
1. Na caixa de texto de saudação Olá *domínio personalizado* folha em Olá [portal do Azure](https://portal.azure.com), digite nome de saudação do seu domínio personalizado, incluindo o subdomínio hello. Não inclua *asverify*. Por exemplo, se o domínio for **contoso.com** e o alias de subdomínio for **www**, digite **www.contoso.com**. Se o subdomínio for **fotos**, digite **photos.contoso.com**. subdomínio Olá é necessário.
1. Selecione Olá **usar a validação de CNAME indireta** caixa de seleção.
1. Selecione **salvar** em Olá *domínio personalizado* folha tooregister seu domínio personalizado. Se o registro de saudação for bem-sucedida, você verá uma notificação informando que sua conta de armazenamento foi atualizada com êxito no portal. Neste ponto, seu domínio personalizado foi verificado pelo Azure, mas domínio tooyour do tráfego ainda não estiver sendo roteado tooyour conta de armazenamento.
1. Retornar o site do provedor DNS tooyour e crie outro registro CNAME que mapeie seu ponto de extremidade de serviço do subdomínio tooyour Blob. Por exemplo, especifique o subdomínio Olá **www** ou **fotos** (sem Olá *asverify*), e Olá hostname como  **mystorageaccount.blob.Core.Windows.NET** (onde **mystorageaccount** é o nome da saudação da sua conta de armazenamento). Com essa etapa, o registro de saudação do seu domínio personalizado está concluído.
1. Por fim, você pode excluir o registro CNAME Olá criado Olá contendo **asverify** subdomínio, pois ele foi necessário apenas como uma etapa intermediária.

Depois que o novo registro CNAME se propague através do DNS, os usuários podem exibir dados de blob usando seu domínio personalizado, desde que eles têm permissões apropriadas hello.

## <a name="test-your-custom-domain"></a>Testar seu domínio personalizado

tooconfirm que seu domínio personalizado está realmente mapeado tooyour ponto de extremidade de serviço de Blob, crie um blob em um contêiner público dentro de sua conta de armazenamento. Em seguida, em um navegador da web, use um URI no hello blob de saudação do tooaccess de formato a seguir:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Por exemplo, você pode usar o hello seguinte URI tooaccess um formulário da web em Olá **meus_formulários** contêiner no hello **photos.contoso.com** subdomínio personalizado:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Cancelar o registro de um domínio personalizado

tooderegister um domínio personalizado para seu ponto de extremidade de armazenamento de Blob, use um dos Olá procedimentos a seguir.

### <a name="azure-portal"></a>Portal do Azure

Execute o seguinte Olá na configuração de domínio personalizado de Olá Olá tooremove portal do Azure:

1. Navegue de conta de armazenamento tooyour Olá [portal do Azure](https://portal.azure.com).
1. Em **serviço BLOB** na folha de menu hello, selecione **domínio personalizado** tooopen Olá *domínio personalizado* folha.
1. Conteúdo de Olá clara da caixa de texto de saudação que contém o nome de domínio personalizado.
1. Selecione Olá **salvar** botão.

Quando o domínio personalizado Olá foi removido com êxito, você verá uma notificação informando que sua conta de armazenamento foi atualizada com êxito no portal.

### <a name="azure-cli-20"></a>CLI do Azure 2.0

Saudação de uso [atualização de conta de armazenamento az](https://docs.microsoft.com/cli/azure/storage/account#update) CLI de comando e especifique uma cadeia de caracteres vazia (`""`) para Olá `--custom-domain` tooremove de valor do argumento um registro de domínio personalizado.

* Formato do comando:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Exemplo de comando:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Saudação de uso [conjunto AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet do PowerShell e especifique uma cadeia de caracteres vazia (`""`) para Olá `-CustomDomainName` tooremove de valor do argumento um registro de domínio personalizado.

* Formato do comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Exemplo de comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Próximas etapas
* [Mapear um ponto de extremidade do domínio personalizado tooan Content Delivery Network (CDN) do Azure](../cdn/cdn-map-content-to-custom-domain.md)
* [Usando blobs do hello Azure CDN tooaccess com domínios personalizados por HTTPS](./storage-https-custom-domain-cdn.md)
