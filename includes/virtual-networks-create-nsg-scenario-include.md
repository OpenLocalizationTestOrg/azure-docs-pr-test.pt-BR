## <a name="scenario"></a>Cenário
toobetter ilustram como toocreate NSGs, este documento usará cenário de saudação abaixo.

![Cenário de Rede Virtual](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Nesse cenário, você criará um NSG para cada sub-rede na Olá **TestVNet** rede virtual, conforme descrito abaixo: 

* **NSG-FrontEnd**. Olá front-end NSG será aplicado toohello *front-end* sub-rede e contêm duas regras:    
  * **rdp-rule**. Essa regra permitirá RDP tráfego toohello *front-end* sub-rede.
  * **web-rule**. Essa regra permitirá toohello de tráfego HTTP *front-end* sub-rede.
* **NSG-BackEnd**. back-end de saudação NSG será aplicado toohello *back-end* sub-rede e contêm duas regras:    
  * **sql-rule**. Essa regra permite o tráfego SQL apenas de saudação *front-end* sub-rede.
  * **web-rule**. Esta regra nega internet todos os tráfego de saída de hello *back-end* sub-rede.

a combinação dessas regras Hello criar um cenário como DMZ, onde sub-rede de back-end Olá só pode receber o tráfego de entrada para o SQL da sub-rede de front-end de saudação e tem toohello sem acesso à Internet, enquanto a sub-rede de front-end Olá pode se comunicar com hello da Internet, e receba solicitações HTTP de entrada apenas.

