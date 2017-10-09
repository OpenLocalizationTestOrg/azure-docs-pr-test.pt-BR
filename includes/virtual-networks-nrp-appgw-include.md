## <a name="application-gateway"></a><span data-ttu-id="953da-101">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="953da-101">Application Gateway</span></span>
<span data-ttu-id="953da-102">O Gateway de Aplicativo o fornece uma solução de balanceamento de carga HTTP gerenciada pelo Azure com base no balanceamento de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="953da-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="953da-103">Balanceamento de carga do aplicativo permite o uso de saudação de regras de roteamento de tráfego de rede com base em HTTP.</span><span class="sxs-lookup"><span data-stu-id="953da-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="953da-104">Propriedade</span><span class="sxs-lookup"><span data-stu-id="953da-104">Property</span></span> | <span data-ttu-id="953da-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="953da-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="953da-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="953da-106">**backendAddressPools**</span></span> |<span data-ttu-id="953da-107">lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="953da-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="953da-108">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP ou IP privado</span><span class="sxs-lookup"><span data-stu-id="953da-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="953da-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="953da-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="953da-110">Cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="953da-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="953da-111">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação</span><span class="sxs-lookup"><span data-stu-id="953da-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="953da-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="953da-112">**frontendPorts**</span></span> |<span data-ttu-id="953da-113">Essa porta é a porta pública de saudação aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="953da-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="953da-114">Tráfego chegue essa porta, e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="953da-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="953da-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="953da-115">**httpListeners**</span></span> |<span data-ttu-id="953da-116">Ouvinte tem uma porta de front-end, um protocolo (Http ou Https, eles diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento)</span><span class="sxs-lookup"><span data-stu-id="953da-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="953da-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="953da-117">**requestRoutingRules**</span></span> |<span data-ttu-id="953da-118">regra de saudação associa o pool de servidores de back-end de ouvinte e hello de saudação e define qual tráfego Olá pool do servidor de back-end deve ser direcionado.</span><span class="sxs-lookup"><span data-stu-id="953da-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="953da-119">Atualmente, funciona apenas como Round robin</span><span class="sxs-lookup"><span data-stu-id="953da-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="953da-120">Exemplo de um modelo Json de application gateway:</span><span class="sxs-lookup"><span data-stu-id="953da-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="953da-121">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="953da-121">Additional resources</span></span>
<span data-ttu-id="953da-122">Leitura de [ API REST do application gateway](https://msdn.microsoft.com/library/azure/mt299388.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="953da-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

