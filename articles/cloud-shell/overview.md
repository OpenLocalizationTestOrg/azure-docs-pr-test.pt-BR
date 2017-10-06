---
title: "Visão geral do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
description: "Visão geral do hello Shell de nuvem do Azure."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Visão geral do Azure Cloud Shell (versão prévia)
O Azure Cloud Shell é um shell interativo e acessível pelo navegador para o gerenciamento de recursos do Azure.

![](media/overview-pic.png)

## <a name="features"></a>Recursos
### <a name="browser-based-shell-experience"></a>Experiência de shell baseada no navegador
Nuvem Shell permite tooa baseado em navegador de linha de comando experiência de acesso criada com tarefas de gerenciamento do Azure em mente. Aproveite o Shell de nuvem toowork ilimitado de um computador local, de forma que somente a nuvem de saudação pode fornecer.

### <a name="pre-configured-azure-workstation"></a>Estação de trabalho pré-configurada do Azure
O Cloud Shell vem pré-instalado com ferramentas de linha de comando populares e suporte para idiomas, para que você possa trabalhar mais rapidamente.

[Olá completo de ferramentas lista Exibir para o Shell de nuvem do Azure aqui.](features.md#tools)

### <a name="automatic-authentication"></a>Autenticação automática
Shell de nuvem com segurança autentica automaticamente em cada sessão para recursos do acesso instantâneo tooyour por meio de saudação 2.0 do CLI do Azure.

### <a name="connect-your-azure-file-storage"></a>Conectar o armazenamento de arquivos do Azure
Máquinas de Shell de nuvem são temporárias e assim exigem um toobe de compartilhamento de arquivos do Azure montado como `clouddrive` toopersist seu diretório $Home.
Na primeira inicialização Shell nuvem solicita toocreate que um grupo de recursos, conta de armazenamento e compartilhamento de arquivos em seu nome. Essa é uma etapa única e será anexada automaticamente para todas as sessões. 

#### <a name="create-new-storage"></a>Criar novo armazenamento
![](media/basic-storage.png)

Uma conta de LRS (armazenamento com redundância local) pode ser criada em seu nome com um Compartilhamento de Arquivos do Azure que contém uma imagem de disco de 5 GB padrão. compartilhamento de arquivo Hello monta como `clouddrive` para arquivo compartilhar interação com a imagem de disco de saudação que está sendo usado toosync e manter seu diretório $Home. Custos de armazenamento regulares se aplicam.

Três recursos serão criados em seu nome:
1. Um Grupo de Recursos chamado: `cloud-shell-storage-<region>`
2. Uma Conta de Armazenamento chamada: `cs<uniqueGuid>`
3. Um Compartilhamento de Arquivos chamado: `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Todos os arquivos em seu diretório $Home como chaves SSH são mantidos em sua imagem de disco do usuário armazenada no compartilhamento de arquivo montados. Aplica as práticas recomendadas ao salvar arquivos no diretório $Home e compartilhamento de arquivos montado.

#### <a name="use-existing-resources"></a>Usar recursos existentes
![](media/advanced-storage.png)

Uma opção avançada também é fornecida permitindo que você tooassociate existente recursos tooCloud Shell. Quando for apresentado com o prompt de configuração de armazenamento hello, clique em opções adicionais de tooselect "Show advanced settings". As listas suspensas são filtradas para sua região do Cloud Shell atribuída e para contas de armazenamento com redundância local/global.

[Saiba mais sobre o armazenamento do Cloud Shell, atualização de compartilhamentos de arquivos e upload/download de arquivos.] (persisting-shell-storage.md)

## <a name="concepts"></a>Conceitos
* O Cloud Shell é executado em um computador temporário fornecido por sessão e por usuário
* O Cloud Shell atinge o tempo limite após 20 minutos sem atividade interativa
* O Cloud Shell só pode ser acessado com um compartilhamento de arquivos anexado
* É atribuído ao Cloud Shell um computador por conta de usuário
* As permissões são definidas da mesma forma que para um usuário normal do Linux

[Saiba mais sobre todos os recursos do Cloud Shell.](features.md)

## <a name="examples"></a>Exemplos
* Criar ou editar scripts tooautomate gerenciamento do Azure
* Gerenciar recursos simultaneamente por meio do portal do Azure e da CLI do Azure 2.0
* Testar a CLI do Azure 2.0

[Experimente todos esses exemplos no início rápido da nuvem Shell hello.](quickstart.md)

## <a name="pricing"></a>Preços
máquina Olá Shell da nuvem de hospedagem é gratuita, com um pré-requisito de um arquivo do Azure montado compartilhar toopersist seu diretório $Home. Custos de armazenamento regulares se aplicam.

## <a name="supported-browsers"></a>Navegadores com suporte
O Cloud Shell é recomendado para Chrome, Edge e Safari. Embora haja suporte para o Shell de nuvem para Chrome, Firefox, Safari, IE e borda, o Shell de nuvem é configurações do navegador toospecific assunto.

## <a name="troubleshooting"></a>Solucionar problemas
1. Ao usar uma assinatura do Azure Active Directory, não é possível criar armazenamento vencimento tooError: DisallowedOperation 400. tooresolve isso, use uma assinatura do Azure capaz de criar recursos de armazenamento. Assinaturas AD é toocreate não é possível recursos do Azure.

Para ver as limitações conhecidas específicas, visite [Limitações do Cloud Shell](limitations.md).
