---
title: aaaEncrypt discos em uma VM do Linux no Azure | Microsoft Docs
description: "Como tooencrypt de discos virtuais em uma VM Linux para segurança aprimorada usando Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Como tooencrypt de discos virtuais em uma VM do Linux
Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados. Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure. Você controla essas chaves criptográficas e pode auditar seu uso. Este artigo fornece detalhes sobre como tooencrypt de discos virtuais em uma VM do Linux usando Olá 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção base a seguir comandos tooencrypt de discos virtuais na sua VM. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#overview-of-disk-encryption).

Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login). Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.

Primeiro, habilite o provedor do Azure Key Vault hello dentro de sua assinatura do Azure com [registro de provedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá *eastus* local:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Criar um cofre de chaves do Azure com [keyvault az criar](/cli/azure/keyvault#create) e habilitar Olá Cofre de chaves para uso com criptografia de disco. Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create). Olá, exemplo a seguir cria uma chave chamada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). identificadores de entidade de serviço Olá Olá autenticação e troca de chaves de criptografia do Cofre de chaves. saudação de exemplo a seguir lê valores Olá Olá entidade de serviço Id e a senha para uso em comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

senha Olá é somente de saída quando você cria Olá entidade de serviço. Se desejar, exibir e registro Olá senha (`echo $sp_password`). Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).

Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy). Olá exemplo a seguir, hello ID de entidade de serviço é fornecido de saudação que precedem o comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Crie uma VM com [az vm create](/cli/azure/vm#create) e anexe um disco de dados de 5 GB. Somente determinadas imagens do marketplace dão suporte à criptografia de disco. Olá, exemplo a seguir cria uma VM denominada `myVM` usando um **CentOS 7.2n** imagem:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM usando Olá `publicIpAddress` mostrado na saída Olá Olá precede o comando. Criar uma partição e sistema de arquivos, em seguida, montar o disco de dados hello. Para obter mais informações, consulte [conectar tooa novo disco de VM do Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Feche a sessão SSH.

Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable). Olá, exemplo a seguir usa Olá `$sp_id` e `$sp_password` variáveis de saudação anterior `ad sp create-for-rbac` comando:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Levará algum tempo para Olá toocomplete de processo de criptografia de disco. Monitorar o status de saudação do processo de saudação com [Mostrar de criptografia de vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Olá status mostra **EncryptionInProgress**. Aguarde até que o status de Olá Olá OS relatórios de disco **VMRestartPending**, em seguida, reiniciar a VM com [reinicialização de vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Olá processo de criptografia de disco é finalizado durante o processo de inicialização hello, então, aguarde alguns minutos antes de verificar o status de saudação do encryption novamente com **Mostrar de criptografia de vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

status de saudação agora devem relatar disco Olá SO e discos de dados como **criptografado**.

## <a name="overview-of-disk-encryption"></a>Visão geral da criptografia de disco
Discos virtuais em VMs do Linux são criptografados em repouso usando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Não há nenhuma taxa para criptografar discos virtuais no Azure. As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2. Você mantém o controle dessas chaves criptográficas e pode auditar seu uso. Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM. Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.

processo de saudação de criptografia de uma VM é o seguinte:

1. Crie uma chave de criptografia em um Cofre de chaves do Azure.
2. Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.
3. chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, criar um serviço do Active Directory do Azure principal com as permissões adequadas hello.
4. Emita Olá comando tooencrypt seus discos virtuais, especificação de entidade de serviço do Active Directory do Azure hello e adequado toobe chave criptográfica usada.
5. solicitações do principais de serviço do Active Directory do Azure Olá Olá chave de criptografia necessária do Cofre de chaves do Azure.
6. discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.

## <a name="encryption-process"></a>Processo de criptografia
Criptografia de disco se baseia em Olá componentes adicionais a seguir:

* **Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello.
  * Se houver um, você pode usar um Cofre de Chaves do Azure existente. Você não tem toodedicate discos tooencrypting um cofre de chaves.
  * limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.
* **Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada.
  * Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.
  * entidade de serviço Olá fornece um mecanismo seguro toorequest e emitido chaves de criptografia apropriadas hello. Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
Requisitos e cenários com suporte para criptografia de disco:

* saudação do servidor Linux SKUs - Red Hat Enterprise Linux, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Ubuntu a seguir.
* Todos os recursos (como o Cofre de chaves, a conta de armazenamento e VM) devem estar no hello mesma região do Azure e assinatura.
* VMs Standard das séries A, D, DS, G e GS.

Criptografia de disco não é suportada em Olá os seguintes cenários:

* VMs de camada básica.
* Máquinas virtuais criadas usando o modelo de implantação clássico hello.
* Desabilitação da criptografia de disco do OS em VMs do Linux.
* Atualizando chaves de criptografia de saudação em uma VM Linux já criptografados.

## <a name="create-azure-key-vault-and-keys"></a>Criar o Azure Key Vault e as chaves
Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login). Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myKey* e *myVM*.

primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas. Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços. Para criptografia de disco virtual, use o Cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais.

Habilitar provedor de Azure Key Vault hello dentro de sua assinatura do Azure com [registro de provedor az](/cli/azure/provider#register) e criar um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá `eastus` local:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região. Criar um cofre de chaves do Azure com [keyvault az criar](/cli/azure/keyvault#create) e habilitar Olá Cofre de chaves para uso com criptografia de disco. Especifique um nome exclusivo de Key Vault para *keyvault_name* da seguinte maneira:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software. Usar um HSM requer um Cofre de Chaves premium. Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software. toocreate adicionar um cofre de chaves, premium em Olá anterior etapa `--sku Premium` toohello comando. Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão.

Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello. Criar uma chave de criptografia em seu Key Vault com [az keyvault key create](/cli/azure/keyvault/key#create). Olá, exemplo a seguir cria uma chave chamada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Criar hello entidade de serviço do Active Directory do Azure
Quando discos virtuais são criptografados ou descriptografados, especifique um conta toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves. Essa conta, uma entidade de serviço do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM. Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.

Crie uma entidade de serviço usando o Azure Active Directory com [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). saudação de exemplo a seguir lê valores Olá Olá entidade de serviço Id e a senha para uso em comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

senha de saudação é exibida apenas quando você cria hello entidade de serviço. Se desejar, exibir e registro Olá senha (`echo $sp_password`). Você pode listar suas entidades de serviço com [az ad sp list](/cli/azure/ad/sp#list) e exibir informações adicionais sobre uma entidade de serviço específica com [az ad sp show](/cli/azure/ad/sp#show).

toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory tooread principal Olá as chaves de serviço. Defina permissões em seu Key Vault com [az keyvault set-policy](/cli/azure/keyvault#set-policy). Olá exemplo a seguir, hello ID de entidade de serviço é fornecido de saudação que precedem o comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Criar máquina virtual
tooactually criptografar alguns discos virtuais, permite criar uma máquina virtual e adicionar um disco de dados. Criar um tooencrypt VM com [criar vm az](/cli/azure/vm#create) e anexar um disco de dados de 5 Gb. Somente determinadas imagens do marketplace dão suporte à criptografia de disco. Olá, exemplo a seguir cria uma VM denominada *myVM* usando um **CentOS 7.2n** imagem:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM usando Olá `publicIpAddress` mostrado na saída Olá Olá precede o comando. Criar uma partição e sistema de arquivos, em seguida, montar o disco de dados hello. Para obter mais informações, consulte [conectar tooa novo disco de VM do Linux toomount Olá](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Feche a sessão SSH.


## <a name="encrypt-virtual-machine"></a>Criptografar máquina virtual
discos virtuais do tooencrypt hello, você reúne todos os componentes anteriores do hello:

1. Especifique Olá entidade de serviço do Active Directory do Azure e a senha.
2. Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.
3. Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.
4. Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.

Criptografe sua VM com [az vm encryption enable](/cli/azure/vm/encryption#enable). Olá, exemplo a seguir usa Olá `$sp_id` e `$sp_password` variáveis de saudação anterior `ad sp create-for-rbac` comando:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Levará algum tempo para Olá toocomplete de processo de criptografia de disco. Monitorar o status de saudação do processo de saudação com [Mostrar de criptografia de vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

saudação de saída é similar toohello truncada de exemplo a seguir:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Aguarde até que o status de Olá Olá OS relatórios de disco **VMRestartPending**, em seguida, reiniciar a VM com [reinicialização de vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Olá processo de criptografia de disco é finalizado durante o processo de inicialização hello, então, aguarde alguns minutos antes de verificar o status de saudação do encryption novamente com **Mostrar de criptografia de vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

status de saudação agora devem relatar disco Olá SO e discos de dados como **criptografado**.


## <a name="add-additional-data-disks"></a>Adicionar discos de dados adicionais
Depois que você criptografou os discos de dados, você pode posteriormente adicionar discos virtuais adicionais tooyour VM e também criptografá-los. Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte maneira:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Execute novamente Olá comando tooencrypt Olá os discos virtuais da seguinte maneira:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre como gerenciar o Cofre de Chaves do Azure, incluindo a exclusão de chaves criptográficas e cofres, consulte [Gerenciar Cofres de Chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).
