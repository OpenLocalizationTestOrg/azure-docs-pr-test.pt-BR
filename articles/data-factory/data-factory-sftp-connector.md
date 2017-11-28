---
title: aaaMove dados do servidor SFTP usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados de um local ou um servidor SFTP de nuvem usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="761cf-103">Mover dados de um servidor SFTP usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="761cf-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="761cf-104">Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um tooa de servidor SFTP no local/em nuvem suporte para armazenamento de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="761cf-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="761cf-105">Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.</span><span class="sxs-lookup"><span data-stu-id="761cf-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="761cf-106">Fábrica de dados atualmente suporta apenas mover armazena dados de um servidor de SFTP tooother dados, mas não para mover dados de outros dados armazena o servidor SFTP tooan.</span><span class="sxs-lookup"><span data-stu-id="761cf-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="761cf-107">Ele dá suporte a servidores SFTP tanto locais quanto na nuvem.</span><span class="sxs-lookup"><span data-stu-id="761cf-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="761cf-108">Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="761cf-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="761cf-109">Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="761cf-110">Cenários com suporte e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="761cf-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="761cf-111">Você pode usar dados SFTP conector toocopy de **ambos os servidores SFTP e SFTP local na nuvem**.</span><span class="sxs-lookup"><span data-stu-id="761cf-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="761cf-112">**Básico** e **parâmetros SshPublicKey** tipos de autenticação com suporte ao conectar-se o servidor SFTP toohello.</span><span class="sxs-lookup"><span data-stu-id="761cf-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="761cf-113">Ao copiar dados de um servidor SFTP local, você precisa instalar um Gateway de gerenciamento de dados no ambiente do local de saudação/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="761cf-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="761cf-114">Consulte [Data Management Gateway](data-factory-data-management-gateway.md) para obter detalhes sobre o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="761cf-115">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para instruções passo a passo de configuração de gateway hello e usá-lo.</span><span class="sxs-lookup"><span data-stu-id="761cf-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="761cf-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="761cf-116">Getting started</span></span>
<span data-ttu-id="761cf-117">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem SFTP usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="761cf-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="761cf-118">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="761cf-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="761cf-119">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="761cf-120">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="761cf-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="761cf-121">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="761cf-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="761cf-122">Para exemplos de JSON toocopy dados do servidor SFTP tooAzure armazenamento de Blob, consulte [exemplo JSON: copiar dados de blob de tooAzure servidor SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="761cf-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="761cf-123">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="761cf-123">Linked service properties</span></span>
<span data-ttu-id="761cf-124">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooFTP vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="761cf-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="761cf-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="761cf-125">Property</span></span> | <span data-ttu-id="761cf-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="761cf-126">Description</span></span> | <span data-ttu-id="761cf-127">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="761cf-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="761cf-128">type</span><span class="sxs-lookup"><span data-stu-id="761cf-128">type</span></span> | <span data-ttu-id="761cf-129">propriedade do tipo Hello deve ser definida muito`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="761cf-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="761cf-130">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-130">Yes</span></span> |
| <span data-ttu-id="761cf-131">host</span><span class="sxs-lookup"><span data-stu-id="761cf-131">host</span></span> | <span data-ttu-id="761cf-132">Nome ou endereço IP do servidor SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="761cf-133">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-133">Yes</span></span> |
| <span data-ttu-id="761cf-134">porta</span><span class="sxs-lookup"><span data-stu-id="761cf-134">port</span></span> |<span data-ttu-id="761cf-135">Porta na qual Olá SFTP server está escutando.</span><span class="sxs-lookup"><span data-stu-id="761cf-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="761cf-136">valor padrão de saudação é: 21</span><span class="sxs-lookup"><span data-stu-id="761cf-136">hello default value is: 21</span></span> |<span data-ttu-id="761cf-137">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-137">No</span></span> |
| <span data-ttu-id="761cf-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="761cf-138">authenticationType</span></span> |<span data-ttu-id="761cf-139">Especifique o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="761cf-139">Specify authentication type.</span></span> <span data-ttu-id="761cf-140">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="761cf-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="761cf-141">Consulte também[usando a autenticação básica](#using-basic-authentication) e [usando SSH autenticação de chave pública](#using-ssh-public-key-authentication) seções em mais propriedades e exemplos JSON, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="761cf-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="761cf-142">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-142">Yes</span></span> |
| <span data-ttu-id="761cf-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="761cf-143">skipHostKeyValidation</span></span> | <span data-ttu-id="761cf-144">Especifique se tooskip validação de chave do host.</span><span class="sxs-lookup"><span data-stu-id="761cf-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="761cf-145">Não.</span><span class="sxs-lookup"><span data-stu-id="761cf-145">No.</span></span> <span data-ttu-id="761cf-146">Olá valor padrão: false</span><span class="sxs-lookup"><span data-stu-id="761cf-146">hello default value: false</span></span> |
| <span data-ttu-id="761cf-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="761cf-147">hostKeyFingerprint</span></span> | <span data-ttu-id="761cf-148">Especifique a impressão digital de saudação da chave de host hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="761cf-149">Sim se hello `skipHostKeyValidation` é definido toofalse.</span><span class="sxs-lookup"><span data-stu-id="761cf-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="761cf-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="761cf-150">gatewayName</span></span> |<span data-ttu-id="761cf-151">Nome da saudação Data Management Gateway tooconnect tooan local do servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="761cf-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="761cf-152">Sim se estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="761cf-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="761cf-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="761cf-153">encryptedCredential</span></span> | <span data-ttu-id="761cf-154">Servidor SFTP saudação do tooaccess credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="761cf-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="761cf-155">Gerado automaticamente quando você especificar a autenticação básica (nome de usuário + senha) ou parâmetros SshPublicKey (nome de usuário + caminho da chave privado ou conteúdo) no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="761cf-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="761cf-156">Não.</span><span class="sxs-lookup"><span data-stu-id="761cf-156">No.</span></span> <span data-ttu-id="761cf-157">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="761cf-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="761cf-158">Usando a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="761cf-158">Using basic authentication</span></span>

<span data-ttu-id="761cf-159">Definir toouse a autenticação básica, `authenticationType` como `Basic`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:</span><span class="sxs-lookup"><span data-stu-id="761cf-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="761cf-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="761cf-160">Property</span></span> | <span data-ttu-id="761cf-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="761cf-161">Description</span></span> | <span data-ttu-id="761cf-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="761cf-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="761cf-163">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="761cf-163">username</span></span> | <span data-ttu-id="761cf-164">Usuário que possui o servidor do acesso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="761cf-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="761cf-165">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-165">Yes</span></span> |
| <span data-ttu-id="761cf-166">Senha</span><span class="sxs-lookup"><span data-stu-id="761cf-166">password</span></span> | <span data-ttu-id="761cf-167">Senha do usuário da saudação (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="761cf-167">Password for hello user (username).</span></span> | <span data-ttu-id="761cf-168">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="761cf-169">Exemplo: autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="761cf-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="761cf-170">Exemplo: autenticação Básica com credencial criptografada</span><span class="sxs-lookup"><span data-stu-id="761cf-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="761cf-171">Usando a autenticação de chave pública SSH</span><span class="sxs-lookup"><span data-stu-id="761cf-171">Using SSH public key authentication</span></span>

<span data-ttu-id="761cf-172">Definir toouse SSH autenticação de chave pública, `authenticationType` como `SshPublicKey`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:</span><span class="sxs-lookup"><span data-stu-id="761cf-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="761cf-173">Propriedade</span><span class="sxs-lookup"><span data-stu-id="761cf-173">Property</span></span> | <span data-ttu-id="761cf-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="761cf-174">Description</span></span> | <span data-ttu-id="761cf-175">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="761cf-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="761cf-176">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="761cf-176">username</span></span> |<span data-ttu-id="761cf-177">Usuário que tem acesso toohello SFTP servidor</span><span class="sxs-lookup"><span data-stu-id="761cf-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="761cf-178">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-178">Yes</span></span> |
| <span data-ttu-id="761cf-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="761cf-179">privateKeyPath</span></span> | <span data-ttu-id="761cf-180">Especifique o caminho absoluto toohello arquivo de chave privada pode acessar o gateway.</span><span class="sxs-lookup"><span data-stu-id="761cf-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="761cf-181">Especifique a saudação `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="761cf-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="761cf-182">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="761cf-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="761cf-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="761cf-183">privateKeyContent</span></span> | <span data-ttu-id="761cf-184">Uma cadeia de caracteres serializada de conteúdo da chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="761cf-185">Olá Assistente para cópia pode ler o arquivo de chave privada hello e extrair o conteúdo da chave privada Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="761cf-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="761cf-186">Se você estiver usando qualquer outra ferramenta/SDK, use a propriedade de privateKeyPath de saudação em vez disso.</span><span class="sxs-lookup"><span data-stu-id="761cf-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="761cf-187">Especifique a saudação `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="761cf-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="761cf-188">Senha</span><span class="sxs-lookup"><span data-stu-id="761cf-188">passPhrase</span></span> | <span data-ttu-id="761cf-189">Especifique Olá senha/frase toodecrypt Olá privada chave de acesso de se o arquivo de chave Olá estiver protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="761cf-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="761cf-190">Sim, se o arquivo de chave privada Olá é protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="761cf-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="761cf-191">O conector SFTP somente suporta a chave OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="761cf-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="761cf-192">Verifique se que o arquivo de chave está no formato adequado hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="761cf-193">Você pode usar a ferramenta Putty tooconvert *.ppk tooOpenSSH formato.</span><span class="sxs-lookup"><span data-stu-id="761cf-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="761cf-194">Exemplo: autenticação de SshPublicKey usando o filePath da chave privada</span><span class="sxs-lookup"><span data-stu-id="761cf-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="761cf-195">Exemplo: autenticação de SshPublicKey usando o conteúdo da chave privada</span><span class="sxs-lookup"><span data-stu-id="761cf-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="761cf-196">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="761cf-196">Dataset properties</span></span>
<span data-ttu-id="761cf-197">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="761cf-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="761cf-198">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="761cf-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="761cf-199">Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="761cf-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="761cf-200">Ele fornece informações de tipo de conjunto de dados toohello específico.</span><span class="sxs-lookup"><span data-stu-id="761cf-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="761cf-201">Olá typeProperties seção um conjunto de dados do tipo **FileShare** conjunto de dados tiver Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="761cf-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="761cf-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="761cf-202">Property</span></span> | <span data-ttu-id="761cf-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="761cf-203">Description</span></span> | <span data-ttu-id="761cf-204">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="761cf-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="761cf-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="761cf-205">folderPath</span></span> |<span data-ttu-id="761cf-206">Subpasta toohello mais recente para o caminho.</span><span class="sxs-lookup"><span data-stu-id="761cf-206">Sub path toohello folder.</span></span> <span data-ttu-id="761cf-207">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="761cf-208">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="761cf-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="761cf-209">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="761cf-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="761cf-210">Sim</span><span class="sxs-lookup"><span data-stu-id="761cf-210">Yes</span></span> |
| <span data-ttu-id="761cf-211">fileName</span><span class="sxs-lookup"><span data-stu-id="761cf-211">fileName</span></span> |<span data-ttu-id="761cf-212">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="761cf-213">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="761cf-214">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="761cf-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="761cf-215">Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="761cf-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="761cf-216">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-216">No</span></span> |
| <span data-ttu-id="761cf-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="761cf-217">fileFilter</span></span> |<span data-ttu-id="761cf-218">Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="761cf-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="761cf-219">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="761cf-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="761cf-220">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="761cf-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="761cf-221">Exemplo 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="761cf-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="761cf-222">fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="761cf-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="761cf-223">Essa propriedade não tem suporte com HDFS.</span><span class="sxs-lookup"><span data-stu-id="761cf-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="761cf-224">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-224">No</span></span> |
| <span data-ttu-id="761cf-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="761cf-225">partitionedBy</span></span> |<span data-ttu-id="761cf-226">partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="761cf-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="761cf-227">Por exemplo, folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="761cf-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="761cf-228">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-228">No</span></span> |
| <span data-ttu-id="761cf-229">formato</span><span class="sxs-lookup"><span data-stu-id="761cf-229">format</span></span> | <span data-ttu-id="761cf-230">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="761cf-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="761cf-231">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="761cf-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="761cf-232">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="761cf-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="761cf-233">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="761cf-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="761cf-234">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-234">No</span></span> |
| <span data-ttu-id="761cf-235">compactação</span><span class="sxs-lookup"><span data-stu-id="761cf-235">compression</span></span> | <span data-ttu-id="761cf-236">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="761cf-237">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="761cf-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="761cf-238">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="761cf-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="761cf-239">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="761cf-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="761cf-240">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-240">No</span></span> |
| <span data-ttu-id="761cf-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="761cf-241">useBinaryTransfer</span></span> |<span data-ttu-id="761cf-242">Especifique se deve usar o modo de transferência Binário.</span><span class="sxs-lookup"><span data-stu-id="761cf-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="761cf-243">True para o modo binário e ASCII false.</span><span class="sxs-lookup"><span data-stu-id="761cf-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="761cf-244">Valor padrão: True.</span><span class="sxs-lookup"><span data-stu-id="761cf-244">Default value: True.</span></span> <span data-ttu-id="761cf-245">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="761cf-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="761cf-246">Não</span><span class="sxs-lookup"><span data-stu-id="761cf-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="761cf-247">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="761cf-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="761cf-248">Usando a propriedade partionedBy</span><span class="sxs-lookup"><span data-stu-id="761cf-248">Using partionedBy property</span></span>
<span data-ttu-id="761cf-249">Como mencionado na seção anterior hello, você pode especificar um folderPath dinâmico, o nome de arquivo para dados de série temporal com partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="761cf-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="761cf-250">Você pode fazer isso com macros de fábrica de dados hello e variável de sistema Olá SliceStart, SliceEnd que indicam Olá período lógico para uma fatia de dados fornecido.</span><span class="sxs-lookup"><span data-stu-id="761cf-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="761cf-251">toolearn sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar Pipelines](data-factory-create-pipelines.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="761cf-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="761cf-252">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="761cf-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="761cf-253">Neste exemplo {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="761cf-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="761cf-254">Olá SliceStart refere-se toostart tempo da fração de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="761cf-255">Olá folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="761cf-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="761cf-256">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="761cf-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="761cf-257">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="761cf-257">Sample 2:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="761cf-258">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="761cf-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="761cf-259">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="761cf-259">Copy activity properties</span></span>
<span data-ttu-id="761cf-260">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="761cf-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="761cf-261">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="761cf-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="761cf-262">Por outro lado, Olá as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="761cf-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="761cf-263">Para a atividade de cópia, propriedades de tipo hello variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="761cf-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="761cf-264">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="761cf-264">Supported file and compression formats</span></span>
<span data-ttu-id="761cf-265">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="761cf-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="761cf-266">Exemplo JSON: Copiar dados de blob de tooAzure servidor SFTP</span><span class="sxs-lookup"><span data-stu-id="761cf-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="761cf-267">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="761cf-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="761cf-268">Eles mostram como fonte de dados toocopy de SFTP tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="761cf-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="761cf-269">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="761cf-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="761cf-270">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="761cf-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="761cf-271">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="761cf-272">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="761cf-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="761cf-273">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="761cf-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="761cf-274">Um serviço vinculado do tipo [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="761cf-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="761cf-275">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="761cf-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="761cf-276">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="761cf-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="761cf-277">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="761cf-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="761cf-278">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="761cf-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="761cf-279">exemplo Hello copia dados de um servidor SFTP tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="761cf-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="761cf-280">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="761cf-281">**Serviço vinculado SFTP**</span><span class="sxs-lookup"><span data-stu-id="761cf-281">**SFTP linked service**</span></span>

<span data-ttu-id="761cf-282">Este exemplo usa a autenticação básica Olá com nome de usuário e senha em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="761cf-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="761cf-283">Você também pode usar uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="761cf-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="761cf-284">Autenticação básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="761cf-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="761cf-285">Autenticação de chave pública SSH</span><span class="sxs-lookup"><span data-stu-id="761cf-285">SSH public key authentication</span></span>

<span data-ttu-id="761cf-286">Confira a seção [Serviço FTP vinculado](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="761cf-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="761cf-287">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="761cf-287">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="761cf-288">**Conjunto de dados de entrada do SFTP**</span><span class="sxs-lookup"><span data-stu-id="761cf-288">**SFTP input dataset**</span></span>

<span data-ttu-id="761cf-289">Este conjunto de dados refere-se a pasta SFTP toohello `mysharedfolder` e o arquivo `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="761cf-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="761cf-290">pipeline de saudação copia o destino de toohello arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="761cf-291">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="761cf-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="761cf-292">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="761cf-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="761cf-293">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="761cf-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="761cf-294">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="761cf-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="761cf-295">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="761cf-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="761cf-296">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="761cf-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="761cf-297">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="761cf-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="761cf-298">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="761cf-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="761cf-299">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="761cf-299">Performance and Tuning</span></span>
<span data-ttu-id="761cf-300">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="761cf-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="761cf-301">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="761cf-301">Next Steps</span></span>
<span data-ttu-id="761cf-302">Consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="761cf-302">See hello following articles:</span></span>

* <span data-ttu-id="761cf-303">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="761cf-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
