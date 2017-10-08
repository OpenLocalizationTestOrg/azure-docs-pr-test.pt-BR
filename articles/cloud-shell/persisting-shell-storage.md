---
title: "arquivos de aaaPersist no Shell de nuvem do Azure (visualização) | Microsoft Docs"
description: Passo a passo de como o Azure Cloud Shell persiste arquivos.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Persistir arquivos no Azure Cloud Shell
Shell de nuvem tira proveito dos arquivos de toopersist de armazenamento de arquivo do Azure entre sessões.

## <a name="set-up-a-clouddrive-file-share"></a>Configurar um compartilhamento de arquivos `clouddrive`
Na inicialização inicial, o Shell de nuvem solicita tooassociate um arquivo novo ou existente compartilhar arquivos toopersist entre sessões.

### <a name="create-new-storage"></a>Criar novo armazenamento

Quando você usa as configurações básicas e seleciona apenas uma assinatura, o Shell de nuvem cria três recursos em seu nome na região Olá suportada mais próximo tooyou:
* Grupo de recursos: `cloud-shell-storage-<region>`
* Conta de armazenamento: `cs<uniqueGuid>`
* Compartilhamento de arquivos:`cs-<user>-<domain>-com-<uniqueGuid>`

![configuração de assinatura de saudação](media/basic-storage.png)

compartilhamento de arquivo Hello monta como `clouddrive` no seu `$Home` directory. Olá compartilhamento de arquivos é também usado toostore uma imagem de 5 GB é criada para você e que automaticamente atualiza e persiste o `$Home` directory. Isso é uma ação única e compartilhamento de arquivo hello monta automaticamente nas sessões subsequentes.

### <a name="use-existing-resources"></a>Usar recursos existentes

Usando Olá opções avançadas, você pode associar recursos existentes. Quando aparece o prompt de configuração de armazenamento hello, selecione **Mostrar configurações avançadas** tooview as opções adicionais. Compartilhamentos de arquivos existentes recebem um toopersist de imagem de usuário de 5 GB a `$Home` directory. menus suspensos de saudação são filtrados para a sua região do Shell de nuvem e para contas de armazenamento com redundância local & com redundância geográfica.

![configuração de grupo de recursos de saudação](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Restringir a criação de recursos com uma política de recursos do Azure
As contas de armazenamento criadas no Cloud Shell são marcadas com `ms-resource-usage:azure-cloud-shell`. Toodisallow usuários criando contas de armazenamento em nuvem Shell, crie um [política de recurso do Azure para marcas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que são disparadas por essa marca específica.

## <a name="how-cloud-shell-works"></a>Como funciona o Cloud Shell
Shell de nuvem persiste arquivos por meio de saudação métodos a seguir:
* Criar uma imagem de disco do seu `$Home` directory toopersist todos os conteúdo no diretório de saudação. imagem de disco de saudação é salvo em seu compartilhamento de arquivo especificado como `acc_<User>.img` em `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, e sincronizará as alterações.

* Montagem do compartilhamento de arquivos especificado como `clouddrive` no diretório `$Home` para que haja interação direta com o compartilhamento de arquivos. `/Home/<User>/clouddrive`está mapeada muito`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Todos os arquivos em seu diretório `$Home` como chaves SSH são persistidos em sua imagem de disco do usuário, que é armazenada no compartilhamento de arquivos montado. Aplique as práticas recomendadas ao persistir informações em seu diretório `$Home` e no compartilhamento de arquivos montado.

## <a name="use-hello-clouddrive-command"></a>Saudação de uso `clouddrive` comando
Com o Shell de nuvem, você pode executar um comando denominado `clouddrive`, que permite que você toomanually atualização Olá compartilhamento de arquivos que tooCloud montado Shell.
![Executando o comando "clouddrive" hello](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Montar um novo`clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Pré-requisitos para montagem manual
Você pode atualizar o compartilhamento de arquivo hello associada com o Shell de nuvem usando Olá `clouddrive mount` comando.

Se você monta um compartilhamento de arquivo, contas de armazenamento Olá devem ser:
* O armazenamento redundante localmente ou compartilhamentos de arquivos do armazenamento com redundância geográfica toosupport.
* Localizadas na região atribuída a você. Quando a integração, região Olá você recebem toois listados no nome do grupo de recursos de saudação `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Regiões de armazenamento com suporte
Hello arquivos do Azure devem residir no hello mesma região que Olá nuvem Shell máquina que estiver montando sejam. Clusters de Shell de nuvem existem atualmente no hello regiões a seguir:
|Área|Região|
|---|---|
|Américas|Leste dos EUA, Centro-Sul dos EUA, Oeste dos EUA|
|Europa|Norte da Europa, Europa Ocidental|
|Pacífico Asiático|Índia Central, Sudeste Asiático|

### <a name="hello-clouddrive-mount-command"></a>Olá `clouddrive mount` comando

> [!NOTE]
> Se você estiver montando um novo compartilhamento de arquivo, uma nova imagem de usuário é criada para sua `$Home` diretório, porque seu anterior `$Home` imagem é mantida no compartilhamento de arquivo hello anterior.

Executar Olá `clouddrive mount` com hello parâmetros a seguir:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview obter mais detalhes, execute `clouddrive mount -h`, conforme mostrado aqui:

![Olá em execução ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Desmontar o `clouddrive`
Você pode desmontar um compartilhamento de arquivos que tooCloud montado Shell a qualquer momento. Depois que o compartilhamento de arquivos é desmontado, será solicitado toomount um novo tooyour anterior de compartilhamento de arquivo próxima sessão.

tooremove um arquivo de compartilhamento do Shell de nuvem:
1. Execute `clouddrive unmount`.
2. Confirmar e confirmar Olá prompts.

O compartilhamento de arquivos continuará tooexist, a menos que você exclua-o manualmente. O Cloud Shell deixará de procurar por esse compartilhamento de arquivos em sessões subsequentes.

tooview obter mais detalhes, execute `clouddrive unmount -h`, conforme mostrado aqui:

![Olá em execução ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> A execução desse comando não excluirá qualquer recurso. Excluir manualmente um grupo de recursos, a conta de armazenamento ou o compartilhamento de arquivos que é mapeado tooCloud Shell excluirá permanentemente seu `$Home` imagem de diretório e outros arquivos em seu compartilhamento de arquivos. Essa ação não pode ser desfeita.

## <a name="list-clouddrive-file-shares"></a>Listar compartilhamentos de arquivos do `clouddrive`
toodiscover o compartilhamento de arquivos está montado como `clouddrive`, execute o seguinte Olá `df` comando. 

tooclouddrive de caminho de arquivo Hello mostra que o nome da conta de armazenamento e compartilhamento de arquivos na URL de saudação. Por exemplo, `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Transferência de arquivos locais tooCloud Shell
Olá `clouddrive` diretório for sincronizado com folha de armazenamento do portal do Azure hello. Use este tooor de arquivos local tootransfer folha do seu compartilhamento de arquivos. Atualizar os arquivos a partir do Shell de nuvem é refletido no armazenamento de arquivo hello GUI quando você atualiza a folha de saudação.

### <a name="download-files"></a>Baixar arquivos

![Lista de arquivos locais](media/download.png)
1. No Olá portal do Azure, acesse o compartilhamento de arquivos montados toohello.
2. Selecione o arquivo de destino de saudação.
3. Selecione Olá **baixar** botão.

### <a name="upload-files"></a>Carregar arquivos

![Arquivos locais toobe carregado](media/upload.png)
1. Acesse o compartilhamento de arquivos montados tooyour.
2. Selecione Olá **carregar** botão.
3. Selecione o arquivo de saudação ou arquivos que você deseja tooupload.
4. Confirme o carregamento de saudação.

Agora você deve ver arquivos Olá acessíveis em sua `clouddrive` diretório no Shell de nuvem.

## <a name="next-steps"></a>Próximas etapas
[Início rápido do Cloud Shell](quickstart.md) <br>
[Saiba mais sobre o armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Saiba mais sobre marcas de armazenamento](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
