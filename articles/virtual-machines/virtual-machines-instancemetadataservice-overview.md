---
title: "Visão geral do serviço de metadados de instância de aaaAzure | Microsoft Docs"
description: "Interface rESTful tooget obter informações sobre computação, rede e eventos de manutenção futura da VM."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a>Serviço de metadados de instância do Azure 


saudação de serviço de metadados de instância do Azure fornece informações sobre instâncias de máquina virtual que podem ser usado toomanage e configurar as máquinas virtuais em execução.
Isso inclui informações como SKU, configuração de rede e eventos de manutenção futura. Para obter mais informações sobre o tipo de informação que está disponível, consulte [categorias de metadados](#instance-metadata-data-categories).

Serviço de metadados de instância do Azure é um ponto de extremidade REST tooall acessível IaaS VMs criada por meio do hello [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). ponto de extremidade Hello está disponível em um endereço IP não roteável conhecido (`169.254.169.254`) que podem ser acessados somente de dentro de saudação VM.

### <a name="important-information"></a>Informações importantes

Esse serviço é **disponível geralmente** em regiões do Azure globais. Ele está em visualização pública para o governo, China e em nuvem alemã do Azure. Regularmente, ele recebe atualizações tooexpose novas informações sobre instâncias de máquina virtual. Esta página reflete Olá atualizada [categorias de dados](#instance-metadata-data-categories) disponíveis.

## <a name="service-availability"></a>Disponibilidade do serviço
serviço de saudação está disponível em todas as regiões do Azure Global disponíveis. serviço de saudação está em visualização pública no hello governamentais, China, Alemanha regiões.

Regiões                                        | Disponibilidade?
-----------------------------------------------|-----------------------------------------------
[Todas as regiões globais do Azure disponíveis](https://azure.microsoft.com/en-us/regions/)     | Disponível 
[Azure Governamental](https://azure.microsoft.com/en-us/overview/clouds/government/)              | Na visualização 
[Azure China:](https://www.azure.cn/)                                                           | Na visualização
[Azure Alemanha](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | Na visualização

Esta tabela é atualizada quando o serviço Olá torna-se disponível em outras nuvens do Azure.

tootry out Olá instância metadados de serviço, criar uma VM do [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou hello [portal do Azure](http://portal.azure.com) em Olá acima regiões e siga Olá exemplos abaixo.

## <a name="usage"></a>Uso

### <a name="versioning"></a>Controle de versão
Olá serviço de metadados de instância é com controle de versão. As versões são obrigatórias e Olá a versão atual é `2017-04-02`.

> [!NOTE] 
> Versões anteriores de visualização de eventos agendados suportados {mais recente} como Olá api-version. Esse formato não é mais suportado e será substituído em Olá futuras.

Como adicionamos versões mais recentes, as versões mais antigas ainda podem ser acessadas para fins de compatibilidade se os scripts tiverem dependências de formatos de dados específicos. No entanto, observe que version(2017-03-01) de visualização atual Olá pode não estar disponível quando o serviço de saudação estiver disponível.

### <a name="using-headers"></a>Usando cabeçalhos
Quando você consulta Olá instância metadados de serviço, você deve fornecer o cabeçalho Olá `Metadata: true` solicitação de saudação tooensure não foi redirecionada acidentalmente.

### <a name="retrieving-metadata"></a>Configurando e recuperando os metadados

Os metadados de instância estão disponíveis para a execução de máquinas virtuais criadas/gerenciadas usando o [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Acesse todas as categorias de dados para uma instância de máquina virtual usando Olá solicitação a seguir:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.

### <a name="data-output"></a>Saída de dados
Por padrão, Olá instância metadados de serviço retorna dados em formato JSON (`Content-Type: application/json`). No entanto, diferentes APIs podem retornar dados em formatos diferentes, se solicitado.
Olá tabela a seguir é uma referência de outros formatos de dados que pode oferecer suporte a APIs.

API | Formato de dados padrão | Outros formatos
--------|---------------------|--------------
/instance | json | texto
/scheduledevents | json | nenhum

tooaccess um formato de resposta não padrão, especificar o formato solicitado hello como um parâmetro de querystring na solicitação de saudação. Por exemplo:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Segurança
ponto de extremidade de serviço de metadados de instância de saudação é acessível somente dentro Olá executando a instância de máquina virtual em um endereço IP não roteável. Além disso, qualquer solicitação com um `X-Forwarded-For` cabeçalho é rejeitado pelo serviço de saudação.
Também precisamos solicitações toocontain um `Metadata: true` tooensure de cabeçalho que Olá solicitação real diretamente foi pretendido e não faz parte do redirecionamento não intencional. 

### <a name="error"></a>Erro
Se houver um elemento de dados não encontrado ou uma solicitação incorreta, Olá instância metadados de serviço retorna erros HTTP padrão. Por exemplo:

Código de status HTTP | Motivo
----------------|-------
200 OK |
400 Solicitação Inválida | Faltando `Metadata: true` cabeçalho
404 Não Encontrado | Olá does't elemento solicitado existe 
405 método não permitido | Somente as solicitações `GET` e `POST` são suportadas
429 Número excessivo de solicitações | Olá API atualmente suporta um máximo de 5 consultas por segundo
500 Erro do serviço     | Aguarde um pouco e tente novamente

### <a name="examples"></a>Exemplos

> [!NOTE] 
> Todas as respostas de API são cadeias de caracteres JSON. Todas as respostas de exemplo a seguir são estilos de formatação para facilitar a leitura.

#### <a name="retrieving-network-information"></a>Recuperação das informações de rede

**Solicitação**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta de saudação é uma cadeia de caracteres JSON. saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Recuperação do endereço IP público

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Recuperação de todos os metadados para uma instância

**Solicitação**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta de saudação é uma cadeia de caracteres JSON. saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Recuperação de metadados na máquina virtual do Windows

**Solicitação**

Metadados de instância podem ser recuperados no Windows por meio de saudação do PowerShell utilitário `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Ou por meio de saudação `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Resposta**

> [!NOTE] 
> resposta de saudação é uma cadeia de caracteres JSON. saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Categorias de dados de metadados de instância
Olá categorias de dados a seguir está disponível por meio de saudação instância metadados de serviço:

Dados | Descrição
-----|------------
location | Saudação de região do Azure VM está em execução
name | Nome da saudação VM 
oferta | Oferece informações para a imagem VM hello. Esse valor só está presente para as imagens implantadas na Galeria de imagens do Azure.
publicador | Editor de imagem de VM Olá
sku | SKU específica para a imagem VM Olá  
version | Versão da imagem VM Olá 
osType | Linux ou Windows 
platformUpdateDomain |  [Domínio de atualização](virtual-machines-windows-manage-availability.md) Olá VM está em execução em
platformFaultDomain | [Domínio de falha](virtual-machines-windows-manage-availability.md) Olá VM está em execução em
vmId | [Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para Olá VM
vmSize | [Tamanho da VM](virtual-machines-windows-sizes.md)
IPv4/privateIpAddress | Endereço IPv4 local da saudação VM 
IPv4/privateIpAddress | Endereço IPv4 público da saudação VM
subnet/address | Endereço de sub-rede de saudação VM
subnet/prefix | Prefixo de sub-rede, exemplo 24
ipv6/ipAddress | Endereço IPv6 local da saudação VM
macAddress | Endereço mac da máquina virtual 
scheduledevents | No momento em Consulte de visualização pública [aventosagendados](virtual-machines-scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Cenários de exemplo para uso  

### <a name="tracking-vm-running-on-azure"></a>VM de controle em execução no Azure

Como um provedor de serviço, pode exigir o número de saudação do tootrack de VMs que executam o software ou tiver agentes que precisam tootrack exclusividade de saudação VM. toobe tooget capaz de uma ID exclusiva de uma VM, use Olá `vmId` campo do serviço de metadados de instância.

**Solicitação**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Resposta**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Posicionamento de contêineres, partições de dados com base em domínio de falha/atualização 

Para determinados cenários nos quais o posicionamento de réplicas diferentes é de vital importância. Por exemplo, [posicionamento de réplica do HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou a colocação de contêiner por meio de um [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) pode exigir o hello tooknow `platformFaultDomain` e `platformUpdateDomain` Olá VM está em execução no.
Você pode consultar esses dados diretamente por meio de saudação serviço de metadados de instância.

**Solicitação**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Resposta**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Obtendo mais informações sobre Olá VM durante o caso de suporte 

Como um provedor de serviço, você pode obter uma chamada de suporte em que você deseja tooknow mais informações sobre Olá VM. Solicitando Olá cliente tooshare Olá computação metadados podem fornecer informações básicas para tooknow profissional de suporte de saudação sobre o tipo de saudação do VM no Azure. 

**Solicitação**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta de saudação é uma cadeia de caracteres JSON. saudação de resposta de exemplo a seguir é impresso de formatação para facilitar a leitura.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Exemplos de como chamar o serviço de metadados usando linguagens diferentes dentro de saudação VM 

idioma | Exemplo 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Vá Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
JavaScript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
Powershell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>Perguntas frequentes
1. Estou recebendo o erro de saudação `400 Bad Request, Required metadata header not specified`. O que isso significa?
   * Olá instância metadados de serviço requer cabeçalho Olá `Metadata: true` toobe passado na solicitação de saudação. Passar esse cabeçalho na chamada REST Olá permite acesso toohello serviço de metadados de instância. 
2. Por que não estou obtendo informações de computação para minha máquina virtual?
   * Atualmente Olá instância metadados de serviço suporta apenas instâncias criadas com o Gerenciador de recursos do Azure. Olá futuras, podemos pode adicionar suporte para VMs de serviço de nuvem.
3. Criei minha máquina virtual com o Azure Resource Manager há algum tempo. Por que não consigo ver as informações de metadados de computação?
   * Para todas as máquinas virtuais criadas depois de setembro de 2016, adicione um [marca](../azure-resource-manager/resource-group-using-tags.md) toostart ver metadados de computação. Para VMs mais antigas (criadas antes de setembro de 2016), adicionar ou remover extensões ou dados discos toohello VM toorefresh metadados.
4. Por que estou recebendo o erro de saudação `500 Internal Server Error`?
   * Repita a solicitação com base no sistema de retirada exponencial. Se o problema de saudação persistir, contate o suporte do Azure.
5. Onde posso publicar comentários/perguntas adicionais?
   * Envie seus comentários em http://feedback.azure.com.
7. Isso funcionaria para Instância do Conjunto de Dimensionamento da Máquina Virtual?
   * Sim, o serviço de metadados está disponível para instâncias de conjunto de escala. 
6. Como obter suporte para o serviço Olá?
   * suporte tooget para serviço hello, criar um problema de suporte no portal do Azure para Olá VM em que não é capaz de tooget metadados resposta após várias tentativas longo 

   ![Serviço de Metadados de Instância](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre Olá [scheduledevents](virtual-machines-scheduled-events.md) API **na visualização pública** fornecida pelo Olá serviço de metadados de instância.
