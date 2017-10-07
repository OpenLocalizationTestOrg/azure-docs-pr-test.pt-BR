---
title: aaaEncrypt discos em uma VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Como tooencrypt discos em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Criptografar discos em uma VM do Linux usando Olá 1.0 da CLI do Azure
Para conformidade e segurança aprimorados da máquina virtual (VM), os discos virtuais no Azure podem ser criptografados em repouso. Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure. Você controla essas chaves criptográficas e pode auditar seu uso. Este artigo fornece detalhes sobre como tooencrypt de discos virtuais em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção base a seguir comandos tooencrypt de discos virtuais na sua VM. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#overview-of-disk-encryption).

Você precisa Olá [1.0 mais recente de CLI do Azure](../../xplat-cli-install.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `myKeyVault` e `myVM`.

Primeiro, habilitar o provedor do Azure Key Vault hello dentro de sua assinatura do Azure e criar um grupo de recursos. Olá, exemplo a seguir cria um nome de grupo de recursos `myResourceGroup` em Olá `WestUS` local:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Crie um Cofre de chaves do Azure. Olá, exemplo a seguir cria um cofre de chaves denominado `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Crie uma chave de criptografia em seu Cofre de chaves e habilite-a para criptografia de disco. Olá, exemplo a seguir cria uma chave chamada `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Crie um ponto de extremidade usando o Active Directory do Azure para manipular a autenticação hello e troca de chaves de criptografia do Cofre de chaves. Olá `--home-page` e `--identifier-uris` não é necessário toobe real endereço roteável. Para mais alto nível de segurança hello, segredos de cliente devem ser usados em vez de senhas. Olá CLI do Azure atualmente não é possível gerar segredos de cliente. Segredos de cliente só podem ser gerados no hello portal do Azure. Olá, exemplo a seguir cria um ponto de extremidade do Azure Active Directory denominado `myAADApp` e usa uma senha de `myPassword`. Especifique sua própria senha da seguinte maneira:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Saudação de Observação `applicationId` mostrado na saída de saudação da saudação precede o comando. Essa ID de aplicativo é usado em Olá etapas a seguir:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Adicione um tooan de disco de dados existente de VM. Olá, exemplo a seguir adiciona um disco de dados tooa VM denominada `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Examine os detalhes de saudação para sua chave de Cofre de chaves e hello que você criou. Você precisa Olá chave, ID de Cofre de chave e URI URL na etapa final hello. Olá exemplo a seguir examina Olá detalhes para um cofre de chaves denominado `myKeyVault` e a chave denominada `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Criptografe seus discos da seguinte maneira, digitando seus próprios nomes de parâmetro completamente:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Olá CLI do Azure não fornece detalhados erros durante o processo de criptografia hello. Para obter informações adicionais de solução de problemas, examine `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Como Olá precede o comando tem muitas variáveis e talvez não obtenha muito indicação como toowhy Olá processo falhar, um exemplo completo de comandos seria o seguinte:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Por fim, examine o status da criptografia Olá novamente tooconfirm que os discos virtuais agora foram criptografados. Olá, exemplo a seguir verifica o status de saudação de uma VM denominada `myVM` em Olá `myResourceGroup` grupo de recursos:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Visão geral da criptografia de disco
Discos virtuais em VMs do Linux são criptografados em repouso usando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Não há nenhuma taxa para criptografar discos virtuais no Azure. As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2. Você mantém o controle dessas chaves criptográficas e pode auditar seu uso. Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM. Um ponto de extremidade do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves criptográficas, enquanto as VMs são ligadas e desligadas.

processo de saudação de criptografia de uma VM é o seguinte:

1. Crie uma chave de criptografia em um Cofre de chaves do Azure.
2. Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.
3. chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, crie um ponto de extremidade usando o Azure Active Directory com as permissões adequadas hello.
4. Emita Olá comando tooencrypt seus discos virtuais, especificando o ponto de extremidade do hello Active Directory do Azure e adequado toobe chave criptográfica usada.
5. o ponto de extremidade do Hello Active Directory do Azure solicita chave de criptografia necessária saudação do Cofre de chaves do Azure.
6. discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.

## <a name="supporting-services-and-encryption-process"></a>Suporte a serviços e processo de criptografia
Criptografia de disco se baseia em Olá componentes adicionais a seguir:

* **Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello.
  * Se houver um, você pode usar um Cofre de Chaves do Azure existente. Você não tem toodedicate discos tooencrypting um cofre de chaves.
  * limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.
* **Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada.
  * Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.
  * aplicativo Hello é mais de um ponto de extremidade para Olá Cofre de chaves e toorequest de serviços de máquina Virtual e obter emitido chaves de criptografia apropriadas hello. Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Criar hello Azure Key Vault e chaves
toocomplete Olá restante deste guia, você precisa Olá [mais recente do Azure CLI 1.0](../../xplat-cli-install.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:

```azurecli
azure config mode arm
```

Ao longo de exemplos de comando hello, substitua todos os parâmetros de exemplo com seus próprios nomes, o local e valores de chave. Olá, exemplos a seguir usam uma convenção de `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.

primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas. Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços. Para criptografia de disco virtual, use o Cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais.

Habilitar hello Azure Key Vault provedor na sua assinatura do Azure, em seguida, criar um grupo de recursos. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUS` local:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região. Olá, exemplo a seguir cria um cofre de chaves do Azure denominado `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software. Usar um HSM requer um Cofre de Chaves premium. Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software. toocreate adicionar um cofre de chaves, premium em Olá anterior etapa `--sku Premium` toohello comando. Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão.

Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello. Crie uma chave de criptografia dentro de seu Cofre de Chaves e habilite-a para uso com criptografia de disco virtual. Olá, exemplo a seguir cria uma chave chamada `myKey` e, em seguida, permite que ele para criptografia de disco:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Criar o aplicativo do Active Directory do Azure hello
Quando discos virtuais são criptografados ou descriptografados, você deve usar um ponto de extremidade toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves. Esse ponto de extremidade, um aplicativo do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM. Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.

Como você não estiver criando um aplicativo completo do Active Directory do Azure, Olá `--home-page` e `--identifier-uris` parâmetros no exemplo a seguir de saudação não precisarem toobe real endereço roteável. Olá exemplo a seguir também especifica um segredo baseada em senha, em vez de gerar chaves de dentro de saudação portal do Azure. Neste momento, a geração de chaves não pode ser feita de saudação CLI do Azure.

Crie seu próprio aplicativo do Azure Active Directory. Olá, exemplo a seguir cria um aplicativo chamado `myAADApp` e usa uma senha de `myPassword`. Especifique sua própria senha da seguinte maneira:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Anote Olá `applicationId` que é retornado na saída de saudação do hello precede o comando. Essa ID de aplicativo é usado em alguns Olá restantes etapas. Em seguida, crie um nome de entidade de serviço (SPN) para que o aplicativo hello é acessível em seu ambiente. toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory aplicativo tooread Olá chaves.

Crie Olá SPN e defina as permissões apropriadas Olá da seguinte maneira:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Adicione um disco virtual e examine o status da criptografia
tooactually criptografar alguns discos virtuais, permite adicionar uma tooan de disco existente de VM. Adicione um tooan de disco de dados de 5Gb existente VM da seguinte maneira:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

discos virtuais Olá atualmente não são criptografados. Revise o status de criptografia atual Olá da VM da seguinte maneira:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Criptografar discos virtuais
toonow criptografar discos virtuais hello, você reúne todos os componentes anteriores do hello:

1. Especifique a senha e o aplicativo do Active Directory do Azure hello.
2. Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.
3. Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.
4. Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.

Permite analisar os detalhes de saudação de sua chave de Cofre de chaves do Azure e hello criado, o que for necessário Olá ID cofre da chave, URI e, em seguida, chave de URL na etapa final hello:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Criptografar seus discos virtuais usando a saída de saudação do hello `azure keyvault show` e `azure keyvault key show` comandos da seguinte maneira:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Olá comando anterior tiver muitas variáveis, hello é um exemplo completo de comandos de saudação para referência:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Olá CLI do Azure não fornece detalhados erros durante o processo de criptografia hello. Para obter informações adicionais de solução de problemas, examine `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` no hello VM que está criptografando.

Finalmente, permite examinar o status da criptografia Olá novamente tooconfirm que os discos virtuais agora foram criptografados:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Adicionar discos de dados adicionais
Depois que você criptografou os discos de dados, você pode posteriormente adicionar discos virtuais adicionais tooyour VM e também criptografá-los. Quando você executa Olá `azure vm enable-disk-encryption` comando, a versão da sequência usando Olá Olá incremento `--sequence-version` parâmetro. Esse parâmetro de versão de sequência permite tooperform operações repetidas com hello mesma VM.

Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte maneira:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Executar novamente o hello comando tooencrypt Olá discos virtuais, neste momento adicionando Olá `--sequence-version` parâmetro e valor Olá incremento do nosso primeiro execute da seguinte maneira:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre como gerenciar o Cofre de Chaves do Azure, incluindo a exclusão de chaves criptográficas e cofres, consulte [Gerenciar Cofres de Chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).
