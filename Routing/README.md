# Routing

Adobe Documentation: https://developer.adobe.com/commerce/php/development/components/routing/

## The routes.xml file

doc: https://developer.adobe.com/commerce/php/development/components/routing/#routesxml

Faz o mapeamento de qual modulo será acionado em uma determinada URL. O
 arquivo pode estar em etc/frontend ou em etc/adminhtml, o que especifica a área que a rota apontada.

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="%routerId%">
        <route id="%routeId%" frontName="%frontName%">
            <module name="%moduleName%"/>
        </route>
    </router>
</config>


        %routerId - Especifica o nome do router no Magento.
        %routeId% - Especifica o nó unico para essa rota no Magento é o segmento do XML filename (routeId_controller_action.xml)
        %frontName% - Especifica o primeiro segmento para a base URL da request.
        %moduleName% - Especifica o nome do módulo


Um exemplo pode ser encontrado em [aqui](http://link)

## Action class


