---
title: aaaSQL do Azure com o Azure RemoteApp | Microsoft Docs
description: Saiba como toouse SQL Azure com o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Muitas vezes, quando os clientes escolhem toohost seus aplicativos do Windows na nuvem Olá com o Azure RemoteApp também desejam toomigrate seus dados como servidores SQL em Olá de nuvem para uma implantação de nuvem inteira. Isso possibilita a solução hospedada de nuvem completa que pode ser acessada a qualquer momento por qualquer dispositivo em qualquer lugar usando o Azure RemoteApp. Abaixo estão os links e referências juntamente com diretrizes toohelp você com esse processo.  

## <a name="migrate-your-sql-data"></a>Migrar os dados SQL
Iniciar com [migrando um banco de dados de SQL Server tooAzure banco de dados SQL](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Configurar o Azure RemoteApp
Hospede seu aplicativo do Windows no Azure RemoteApp. A seguir, um passo a passo de nível muito alto:

1. Criar hello [modelo do RemoteApp do Azure VM](remoteapp-imageoptions.md). 
2. Instale o aplicativo hello necessárias em Olá VM.
3. Configurar aplicativo hello, de modo que ele se conecta toohello banco de dados SQL e confirme que ele funciona.
4. Olá Sysprep e desligue VM. Capture isso como uma imagem para usá-la com o Azure. **Observação:** tooensure aplicativo hello é tooretain capaz de informações de conectividade Olá DB por meio do processo do sysprep Olá será necessário. Se o aplicativo hello informações de conexão de saudação DB de tooretain não é possível, convém tooengage fornecedor Olá Olá aplicativo toocheck como podemos especificar cadeia de caracteres de conexão de saudação.
5. Importar imagem personalizada Olá na biblioteca do Azure RemoteApp selecionando Olá adequada localização geográfica que sua implantação do SQL Azure reside. 
6. Implante uma coleção do RemoteApp em Olá mesmo data center como sua implantação do SQL Azure usando Olá acima modelo e publica o aplicativo hello. Implantação do Azure RemoteApp em Olá mesmo data center da sua implantação do SQL Azure ajuda a garantir a velocidades de conexão mais rápidas hello e reduzir a latência. 

## <a name="app-and-sql-configuration-considerations"></a>Considerações sobre a configuração do aplicativo e do SQL:
Há alguns tooconsider de pontos ao usar o SQL Azure com o RemoteApp:

Saiba [como tooconfigure um SQL Azure banco de dados firewall](../sql-database/sql-database-firewall-configure.md). Um trecho de estados de artigo hello, "inicialmente, todos os servidores de banco de dados do SQL Azure tooyour de acesso está bloqueado por firewall hello. Toobegin ordem usando o servidor de banco de dados SQL, você deve ir toohello Portal clássico e especificar uma ou mais regras de firewall de nível de servidor que habilitar o acesso tooyour banco de dados SQL server. Use toospecify de regras de firewall Olá qual endereço IP varia de saudação Internet são permitidos, e se aplicativos do Azure podem tentar o servidor de banco de dados do Azure SQL tooyour tooconnect."

Além disso, quando um computador tenta tooconnect tooyour servidor de banco de dados de saudação da Internet, firewall de saudação verifica Olá endereços IP da solicitação Olá contra o conjunto completo de saudação de nível de servidor de origem e (se necessário) as regras de firewall de nível de banco de dados. "Se Olá endereço IP de saudação solicitação estiver dentro de um dos intervalos de saudação especificados nas regras de firewall de nível de servidor de saudação, conexão Olá será concedida tooyour servidor de banco de dados SQL." Portanto, podemos usar Intervalos de IP e não apenas os endereços IP de origem individuais.

Siga as instruções passo a passo de saudação em [como: definir configurações de firewall no banco de dados SQL usando hello Azure Portal](../sql-database/sql-database-configure-firewall-settings.md) toospecify intervalo IP de saudação. Quando você estiver configurando regras de Firewall do SQL hello, forneça o intervalo IP de saudação da sub-rede Olá especificado para Olá coleção do RemoteApp do Azure. Isso deve permitir servidores de ARA Olá tooconnect toohello banco de dados SQL mesmo que eles serão ter-endereços IP atribuídos dinamicamente.

## <a name="troubleshooting"></a>Solucionar problemas
Se tiver de saudação do uso de um aplicativo cliente hospedado no Azure RemoteApp que se conecta tooa SQL de banco de dados onde hospedados no Azure ou local está lento pode haver alguns motivos por que.  

* Latência de rede do seu dispositivo tooAzure é alta. Mova toohello conexão de rede melhor e mais rápido que possível para melhor desempenho. Use [azurespeed.com](http://azurespeed.com/) como uma ferramenta geral tootest seu dispositivos latência tooAzure do data center.  
* O aplicativo cliente hospedado no Azure RemoteApp está sob carga excessiva. Escolher um plano de cobrança diferente, como a cobrança Premium, melhorará o desempenho. Outro truque é toomonitor recursos de saudação seu aplicativo está consumindo: durante uma sessão ativa, executar uma sequência de teclas ctrl-alt-end que iniciará Olá SAS de tela, selecione o Gerenciador de tarefas e observar a utilização de recursos para seu aplicativo.
* O servidor SQL está sob carga excessiva ou não está otimizado. Siga as diretrizes do SQL para solução de problemas. 

