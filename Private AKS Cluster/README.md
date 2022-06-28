# Publishing AKS with Application Gateway Ingress Controller  

## creating the resource group
```az group create -n <resourcegroupname> -l <location>```

## create public ip
```az network public-ip create -n <publicipname> -g <resourcegroupname> --allocation-method Static --sku Standard```

## create application gateway with WAF enabled.
```az network application-gateway create -n <appgwname> -l <location> -g <resourcegroupname> --sku WAF_v2 --public-ip-address <publicipname> --subnet /subscriptions/<subscriptionid>/resourceGroups/<aksvnetresourcegroupname>/providers/Microsoft.Network/virtualNetworks/<vnetname>/Subnets/<subnetname>```

## enable AGIC on an existing AKS cluster
appgwId=$(az network application-gateway show -n <appgwname> -g <resourcegroupname> -o tsv --query "id") 
az aks enable-addons -n <aksclustername> -g <aksresourcegroupname> -a ingress-appgw --appgw-id $appgwId  

