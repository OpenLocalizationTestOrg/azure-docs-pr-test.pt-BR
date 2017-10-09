## <a name="sample-scenario"></a>Cenário de exemplo
toobetter ilustram como toomanage NSGs, este artigo usa o cenário de saudação abaixo.

![Cenário de Rede Virtual](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Nesse cenário, você criará um NSG para cada sub-rede na Olá **TestVNet** rede virtual, conforme descrito abaixo: 

* **NSG-FrontEnd**. Olá front-end NSG será aplicado toohello *front-end* sub-rede e contêm duas regras:    
  * **rdp-rule**. Essa regra permitirá RDP tráfego toohello *front-end* sub-rede.
  * **web-rule**. Essa regra permitirá toohello de tráfego HTTP *front-end* sub-rede.
* **NSG-BackEnd**. back-end de saudação NSG será aplicado toohello *back-end* sub-rede e contêm duas regras:    
  * **sql-rule**. Essa regra permite o tráfego SQL apenas de saudação *front-end* sub-rede.
  * **web-rule**. Esta regra nega internet todos os tráfego de saída de hello *back-end* sub-rede.

combinação de saudação dessas regras criar um cenário como DMZ, onde sub-rede de back-end Olá só pode receber o tráfego de entrada para o tráfego SQL da sub-rede de front-end hello e tem toohello sem acesso à Internet, enquanto a sub-rede de front-end Olá pode se comunicar com hello Internet e receber solicitações HTTP de entrada apenas.

cenário de saudação toodeploy descrito acima, execute [este link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação. Instruções de exemplo hello abaixo, o modelo de saudação foi toodeploy usado um recurso de nomes de grupo **NSG RG**. 

