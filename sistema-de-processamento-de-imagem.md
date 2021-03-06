---
description: Sistema de processamento de imagens.
---

# Processamento de imagens

O  MS³ é capaz de executar as operações necessárias através de dados de telemetria por satélite para gerar produtos de imagem de satélite. O sistema de processamento é responsável pela geração destes produtos, onde além dos produtos tradicionais existem os produtos especiais. Os produtos são gerados por um conjunto de módulos e ferramentas,  sendo que dentro do grupo de produtos tradicionais, estão as imagens produzidas em diferentes níveis de processamento.

### Nível 0

É um arquivo HDF \([GRALHA](http://enms3wiki.dpi.inpe.br/wiki/GRALHA)\), sem nenhum processamento, contendo a imagem de dados bruta, dados orbitais e auxiliares. Este produto é gerado pelo módulo de processamento D2G.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/9/95/Gralha.jpg/600px-Gralha.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Gralha.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Gralha.jpg)Level-0.

### Nível 1

É uma imagem com correção radiométrica , onde mesmo que nenhuma correção geométrica seja feita na imagem de nível 1, as coordenadas geográficas dos cantos são escritas nas tags Geotiff. Este produto é gerado pelo módulo de processamento G2T.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/7/71/Level1.jpg/400px-Level1.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Level1.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Level1.jpg)Level-1.

### Nível 2

É uma imagem Geotiff com correção radiométrica e geométrica do sistema. Este produto também é gerado pelo módulo de processamento G2T.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/8/83/Level2.jpg/400px-Level2.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Level2.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Level2.jpg)Level-2.

### Nível 3

É uma imagem GeoTiff com correção radiométrica e geométrica do sistema, refinada utilizando pontos de controle. Este produto também é gerado pelo módulo de processamento G2T. 

### Nível 4

É uma imagem GeoTiff com correção radiométrica e sistema geométrico, refinada utilizando pontos de controle e um DEM \(Digital Elevation Model\). Este produto também é gerado pelo módulo de processamento G2T.

### Quicklook

Imagem colorida de baixa resolução espacial no formato JPEG. As _quicklooks_ \(visualizações rápidas\) são as imagens mostradas pelo catálogo de imagens do MS³. Este produto é gerado pelo módulo de processamento G2Q.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/f/fd/Quicklook.jpg/400px-Quicklook.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Quicklook.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Quicklook.jpg)Quicklook.

### Outros produtos:

* **Imagem de encaixe**: mesmo que a imagem ortorretificada \(nível 4\) tenha alta precisão global, problemas pontuais de deslocamento ainda podem ser encontrados ao comparar a cena com uma referência. Podemos dizer que a mesma precisão não é garantida em diferentes pontos de cena. O pós-processamento da imagem ortorretificada corrige esses pequenos deslocamentos, resultando em uma imagem de alta precisão em toda a cena. Este produto é gerado pelo módulo de processamento _station\_image\_fit_. 
* **Imagens de refletância**: dois produtos são gerados aqui, refletância de ToA \(topo da atmosfera\) que é calculada por um modelo matemático, e _refletância de superfície_ que é calculada por 6S \(Segunda Simulação de um Sinal de Satélite no Código de Vetor de Espectro Solar\), que foi integrado ao MS³. Estes produtos são gerados pelo módulo de processamento T2R. 
* **Máscara de nuvem**_:_ imagem que indica se um pixel é nuvem. Este produto é gerado pelo módulo de processamento _station\_classifier_.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/5/56/Cloud_mask.jpg/400px-Cloud_mask.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Cloud_mask.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Cloud_mask.jpg)Cloud mask.

* **Máscara de sombra de nuvem**: imagem que indica se um pixel é sombra de nuvem. Este produto é gerado pelo módulo de processamento _station\_classifier_.

[![](http://enms3wiki.dpi.inpe.br/en.w/images/thumb/c/ca/Shadow_mask.jpg/400px-Shadow_mask.jpg)](http://enms3wiki.dpi.inpe.br/wiki/File:Shadow_mask.jpg)[![](http://enms3wiki.dpi.inpe.br/en.w/skins/common/images/magnify-clip.png)](http://enms3wiki.dpi.inpe.br/wiki/File:Shadow_mask.jpg)Cloud shadow mask.

* **Mosaico multi-temporal**: imagem resultante do mosaico de cenas multi-temporais. O mosaico é particionado levando em consideração uma grade de referência, onde cada célula da grade define um bloco. Este produto é gerado pelo módulo de processamento _station\_update\_mosaic_. 
* **Label mask**: imagem que indica a cena de origem de cada pixel de mosaico multi-temporal. Este produto é fornecido ao usuário junto com os mosaicos e também é gerado pelo módulo de processamento _station\_update\_mosaic_.

## Módulos de Processamento

Para a produção de imagens em diferentes níveis de processamento, o MS³ é composto por um conjunto de módulos. Estes módulos manipulam diferentes tipos de dados para gerar o produto desejado.

Os principais módulos de processamento do MS³ são: D2G, G2Q, G2T e H2T. Que vão desde o dado bruto até a imagem em nível 4 de processamento. Dados necessários para a realização destes procedimentos, de forma geral, se encontram armazenados em arquivos de calibração existentes para cada satélite e para cada sensor específico. 

### D2G

O módulo denominado **D2G** \(DRD to GRALHA\), utiliza o dado bruto do satélite para gerar o arquivo compatível com o sistema de processamento de imagens do MS³. Este processo envolve a decodificação de todos os dados da cena enviados pelos satélites e sua gravação num arquivo GRALHA. Uma vez gerado o GRALHA, o  MS³ está apto a gerar imagens em diferentes níveis de processamento. A gravação é feita agrupando as informações em conjuntos, que por sua vez, são subdivididos em grupos específicos de dados. 

Para melhor ilustrar esta hierarquia, sabe-se que cada cena possui dados de efemérides, atitude, tempo, valor de brilho de cada banda do sensor, entre outros. Cada um destes dados é armazenado em um conjunto separado. No caso do conjunto dos valores de brilho, é criado um grupo específico para cada banda, ou seja, os dados são subdivididos em grupos referentes a cada banda específica. Neste módulo, é gerado um ou mais GRALHAs para cada cena. 

### G2Q

O módulo denominado **G2Q** \(GRALHA to Quicklook\), produz, a partir do GRALHA, imagens denominadas _Quicklook_, que são de baixa resolução espacial e consistem em uma composição colorida de três bandas pré-determinadas no arquivo de configuração. Neste processo, é possível realizar algumas correções radiométricas e geométricas nas imagens, dependentes do tipo de sensor, tais como: correção de linhas perdidas, correção do tamanho da linha, do deslocamento entre as bandas, equalização de detectores, entre outras. Os Quicklooks gerados são gravados no formato [JPG](tipos-de-dados.md#jpg). Estes arquivos correspondem as imagens apresentadas pelo Catálogo de Imagens. 

### G2T

O principal módulo de geração de imagens denominado **G2T** \(GRALHA to Tiff\), é onde são geradas, a partir do GRALHA, as imagens de nível 1 a 4 de processamento citadas na explicação do [**Sistema de Processamento**](sobre-o-ms3.md#principais-sistemas)**.**

{% hint style="warning" %}
**ADICIONAR NOVOS MÓDULOS QUE SÃO UTILIZADOS AQUI NO INPE.**
{% endhint %}

