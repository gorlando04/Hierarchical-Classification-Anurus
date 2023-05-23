# Hierarchical-Classification-Anurus

O conjunto de dados que será analisado possui multirótulos para seus exemplos e cada um desses rótulos, pode ter mais de 2 valores, ou seja, as classes não são binárias. Logo, este conjunto de dados tem mais de uma coluna alvo, tendo portanto multi-saídas.

Após a contextualização de como é o formato do dataset, pode-se explicar quais são as informações que o conjunto tem.

Segundo o SBH em 2005, o Brasil abriga a maior riqueza de Anuros do planeta, com 747 espécies, só no estado de São Paulo, mais de 180 espécies de Anuros estão registradas. Anuros são caracterizados por terem cauda ausente e pernas curtas, adaptadas para saltar e nadar. Eles são animais geralmente terrestres, mas alguns grupos vivem em ambientes aquáticos.

O dataset que será analisado é derivado das gravações realizadas sobre o "cantar" de vários anfíbios da ordem dos Anuros. Para se obter uma boa especificação de qual animal é o responsável pelo ruído, é armazenado no conjunto a sua Família, Gênero e Espécie (3 atributos classe). Dito isso, cada exemplo de entrada é derivado de um Anuro específico. Logo, o objetivo deste trabalho é tentar descobrir pelo ruído que o animal produz, qual sua Família, Gênero e Espécie. É importante salientar que o conjunto de dados disponibilizado para uso não está em formato de aúdio, pois após a captura dos áudios os pesquisadores extraíram informações que são transformadas em atributos numéricos.

Os anfíbios da ordem Anura que destacam-se são: sapos, rãs e pererecas, um exemplo deste animal pode ser visualizado abaixo

![image](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/9d049e2a-f253-4371-8ddb-5cd0f7a86451)


O conjunto de dados pode ser obtido no seguinte link: https://archive.ics.uci.edu/ml/datasets/Anuran+Calls+%28MFCCs%29#


# Conjunto de dados

![Screenshot from 2023-05-22 18-37-19](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/5b297b02-7620-4dd0-9eb6-29d51e13d1ff)

Como podemos ver, os conjunto de dados tem 7195 exemplos com 26 atributos, sendo 3 deles as possíveis classes do exemplo
Deve-se atentar que como se trata de um problema de multirrótulo, é possível que um exemplo pertença a mais de uma classe.

O que está tentando se classificar é o seguinte:

Family: A Família do animal

Genus: O Genêro do animal

Species: A Espécie do animal

Esses 3 atributos devem ser classificados, sendo assim o problema é multi-classe, mas como essas classes possuem uma relação de hierarquia entre si, o problema se torna útil para ser enfrentado utilizando classificação hierárquica. Na imagem abaixo, podemos compreender como funciona esta relação

![image](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/a2f316a3-bce1-43de-9833-5fd8df43fe22)

## Análise do conjunto

A maioria dos atributos preditivios, ou seja, aqueles que serão usadaos para predizer o atributo alvo não eram tão facilmente explicativo, pois como o conjunto de dados era derivado de áudio, então os atributos também foram gerados a partir do áudio, e desta maneira, representam intensidades sonoras no momento específico do auido que foi dividido em mais de 20 separações.

Logo, o que resta é apenas analisar as classes e como elas estão dispsotas.


![Screenshot from 2023-05-22 18-42-23](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/4dd42665-d152-460d-9756-dadc3c1a1d9f)
![Screenshot from 2023-05-22 18-42-38](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/d658afae-2cbd-48cb-986d-e5f846ecf34b)
![Screenshot from 2023-05-22 18-42-51](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/e280a767-ae77-42a4-af27-df984031be26)


## Pré-Processamento

Após isso, foi realizado um breve processamento para deixar os valores em boa forma para serem utilizados no modelo. Além disso, no conjunto de treino e teste que eram referentes as classes foi realizado um One-Hot-Encoding.

# Classificação

Na classificação hierárquica é possível trabalhar com o problema de algumas formas. Neste trabalho será entendido três delas: Classificação Plana, Abordagem Global e Abordagem Local

Cada tipo de abordagem influencia no resultado de uma maneira

Estas abordagens podem ser melhor compreendidas em [1]

[1] CN Silla et al., "A survey of hierarchical classification across different application domains", 2011.

## Avaliação 
Para avaliar os modelos construídos algumas técnicas de avaliação serão utilizadas
Para a Classificação Plana serão calculados a: Perda de Hamming, Acurácia, Recall e F1-Score. Abaixo, pode-se visualizar como calcular cada uma dessas métricas

![image](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/99197f8e-dce6-4a7d-8fcd-50dcf9012c67)

Já para a classificação hierárquica utilizando a abordagem global/local, serão calculados o recall, precision e o f1-score. Abaixo, pode-se visualizar como calcular cada uma dessas métricas

![image](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/acee6daa-a838-41e5-9da4-0df57c5ab2ec)

## Classificação Plana

Esta abordagem consiste em ignorar a hierarquia entre as classes e tratar o problema como um problema multirrótulo. Assim, o classificador só prevê a classe nos nós folhas. Esta abordagem não se importa com hierarquia, e dessa maneira é uma solução indireta para este problema.

![image](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/135de7a1-e2f8-496a-8e83-bfa1cf587158)

## Abordagem Local

Esta abordagem utiliza um classificador local para cada "parte" da hierarquia, e com isso é possível utilizar informações locais das classes com o intuito de melhorar o resultado. Como é uma abordagem Top-Down, o teste começa pelas classes mais genéricas e desce para as mais especializadas.
Dentro dessa abordagem podemos utilizar 3 métodos diferentes: Classificador Local por Nó, Classificador Local por Nó Pai, Classificador Local por Nível

Todas as estratégias estão descritas no notebook.

# Resultados

No notebook uma comparação entre os resultados está descrita. Uma visão mais geral pode ser verificada aqui:



Abordagem Local - Classificação Por Nível

![Screenshot from 2023-05-22 19-10-54](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/67004c83-5e47-4e07-8662-99a19e4cd80b)

Abordagem Local -  Local por Nó Pai

![Screenshot from 2023-05-22 19-11-13](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/af25fd66-2293-4006-a443-27e96e46944f)

Abordagem Local - Local por Nó


![Screenshot from 2023-05-22 19-11-26](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/907fad27-5a69-4cda-82f2-ae495e7257de)

Classificação Plana

![Screenshot from 2023-05-22 19-11-43](https://github.com/gorlando04/Hierarchical-Classification-Anurus/assets/91696970/b98300b7-03c5-4fc3-b50d-479916714e1d)



# Conclusão




# Colaboradores

O projeto foi realizado em grupo:

Mateus Ferro
Eric Pereira
Gabriel Orlando


