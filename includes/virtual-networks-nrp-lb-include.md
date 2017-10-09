## <a name="load-balancer"></a><span data-ttu-id="49f01-101">Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="49f01-101">Load Balancer</span></span>
<span data-ttu-id="49f01-102">Um balanceador de carga é usado quando você deseja tooscale seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="49f01-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="49f01-103">Cenários comuns de implantação envolvem aplicativos executados em várias instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="49f01-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="49f01-104">instâncias de VM Olá são apoiadas por um balanceador de carga que ajuda a toohello de tráfego de rede toodistribute várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="49f01-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![NICs em uma única VM](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="49f01-106">Propriedade</span><span class="sxs-lookup"><span data-stu-id="49f01-106">Property</span></span> | <span data-ttu-id="49f01-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="49f01-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49f01-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="49f01-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="49f01-109">um balanceador de carga pode incluir um ou mais endereços IP front-end, também conhecidos como VIPs (IPs virtuais).</span><span class="sxs-lookup"><span data-stu-id="49f01-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="49f01-110">Esses endereços IP servem como entrada para o tráfego de saudação e podem ser o IP público ou privado IP</span><span class="sxs-lookup"><span data-stu-id="49f01-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="49f01-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="49f01-111">*backendAddressPools*</span></span> |<span data-ttu-id="49f01-112">Estes são os endereços IP associados à saudação NICs de VM toowhich carga será distribuída</span><span class="sxs-lookup"><span data-stu-id="49f01-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="49f01-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="49f01-113">*loadBalancingRules*</span></span> |<span data-ttu-id="49f01-114">uma propriedade de regra mapeia um IP de front-end especificado e a porta do conjunto de tooa de combinação de endereços IP de back-end e combinação de porta.</span><span class="sxs-lookup"><span data-stu-id="49f01-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="49f01-115">Com uma única definição de um recurso de balanceador de carga, você pode definir várias regras de balanceamento de carga, cada regra refletindo uma combinação de um IP de front-end e porta e outra combinação de IP de back-end e porta, ambas associadas às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="49f01-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="49f01-116">regra de saudação é uma porta no pool do front-end de saudação toomany máquinas virtuais no pool de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="49f01-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="49f01-117">*Investigações*</span><span class="sxs-lookup"><span data-stu-id="49f01-117">*Probes*</span></span> |<span data-ttu-id="49f01-118">testes permitem que você controle tookeep da integridade de saudação de instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="49f01-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="49f01-119">Se um teste de integridade falhar, instância de máquina virtual hello será obtida da rotação automaticamente</span><span class="sxs-lookup"><span data-stu-id="49f01-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="49f01-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="49f01-120">*inboundNatRules*</span></span> |<span data-ttu-id="49f01-121">Regras NAT definindo Olá que passam por IP de front-end de saudação do tráfego de entrada e distribuídas instância de máquina virtual específica toohello back-end IP tooa.</span><span class="sxs-lookup"><span data-stu-id="49f01-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="49f01-122">Regra NAT é uma porta no pool do front-end de saudação tooone máquina virtual no pool de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="49f01-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="49f01-123">Exemplo de modelo de Balanceador de carga no formato Json:</span><span class="sxs-lookup"><span data-stu-id="49f01-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
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
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="49f01-124">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="49f01-124">Additional resources</span></span>
<span data-ttu-id="49f01-125">Para obter mais informações, leia [API REST do balanceador de carga](https://msdn.microsoft.com/library/azure/mt163651.aspx) .</span><span class="sxs-lookup"><span data-stu-id="49f01-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

