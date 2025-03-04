# Routing

Routing é o que permite ao Magento processar a URL de uma request e decidir qual classe acionar para execução.

Adobe Documentation: https://developer.adobe.com/commerce/php/development/components/routing/

## Como é uma URL no Magento

<store-url>/<store-code>/<front-name>/<controller-name>/<action-name>

A seguir vamos identificar parte por parte do que compoe essa URL

<store-url> - A instancia da aplicação web 
<store-code> - Especifica a loja
<front-name> - especifica qual frontName do FrontController será usado (por exemplo, [routesxml])
<controller-name> - especifica o controller
<action-name> - especifica a action class

Exemplo: {{base_url}/customer/account/login}
Executa a classe [Magento/Customer/Controller/Account/Login.php](https://github.com/magento/magento2/blob/2.4.7/app/code/Magento/Customer/Controller/Account/Login.php)

## Front Controller

O Front controler recebe todas as requests e a partir de uma lista com todos os routers identifica qual deve ser invocado. A partir daí, a requisição é despacahada para a action class retornada pelo router. Se nenhum for encontrado, então o router default é acionado.

## Routers

O Magento tem classes Routers que combinam requisições com 'action classes'

### Frontend routers

| NAME       | SORT ORDER | DESCRIPTION                                       |
|------------|------------|---------------------------------------------------|
| robots     | 10         | Matches request to the robots.txt file            |
| urlrewrite | 20         | Matches requests with URL defined in the database |
| standard   | 30         | The standard router                               |
| cms        | 60         | Matches requests for CMS pages                    |
| default    | 100        | The default router                                |

### Admin Area routers

| admin   | 10  | Matches requests in the Admin area    |
|---------|-----|---------------------------------------|
| default | 100 | The default router for the Admin area |

## Action Class

## O arquivo routes.xml

doc: https://developer.adobe.com/commerce/php/development/components/routing/#routesxml

Faz o mapeamento de qual modulo será acionado em uma determinada URL. O arquivo pode estar em etc/frontend ou em etc/adminhtml, o que especifica a área que a rota apontada.

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


