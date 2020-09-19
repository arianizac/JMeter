# JMeter

## Resumo geral da Ferramenta com Mind Maps

\MindMap-ResumoJmeter\ResumoJMeter.mm

## Exemplos de algumas estruturas

### 1 Obter Token Oauth2

\Exemplos-JMX\1_Obter_Token_Oauth2.jmx

Utilizando API's públicas do TDC para efeito de exemplo 

Informações: https://thedevconf.com/api

Para executar, obter suas credenciais para acessar a API e obter seu clientID e secret as instruções estão no início da página citada acima.
Substituir no script os valores em "Variáveis Definidas Pelo Usuário" para clientID e secret gerados para seu user no site https://www.globalcode.com.br/api

Nessa estrutura, em JSR223 PreProcessor, foi utilizado o Base64 passando o clientID e secret. A chamada desse encodeBase64 é colocado numa váriavel chamada de auth. No exemplo, essa variável é passada no Authorization para gerarmos o token.
Código:

import org.apache.commons.codec.binary.Base64;
byte[] encodedUsernamePassword = Base64.encodeBase64("${clientID}:${secret}".getBytes());
vars.put("auth",new String(encodedUsernamePassword));

Obs: Reforçando ${clientID}:${secret} foram passadas como variáveis que foram declaradas em "Variáveis Definidas Pelo Usuário"

Para ser utilizado em outros grupos de usuário foi utiliado o elemento JSON Extractor para buscar no JSON o valor do token para ser utilizado no header da chamada de outras API's.

Para obter o conteúdo do campo Access-Token do exemplo, passar o campo no formato usado para variável no JMeter $.NomeCampoNoBody

Exemplo:

JSON Path expressions: $.Access-Token

Para o body:

{"Access-Token":"XXX","token_type":"Bearer","expires_in":14400}

Para setar essa variável como uma propriedade foi usado o Pós-Processador BeanShell:

${__setProperty(nomePropriedade,${nomeVariavel})};

${__setProperty(token,${token})};

Por fim para passar o valor dessa propriedade atribuida para um campo no JMter usamos o formato   ${__property(token)}
Esse exemplo está em Gerenciador de Cabeçalhos HTTP

O Ouvinte "Ver Árvore de Resultado" foi Uitlizado somente para o exemplo ficar didático, para aplicar em disparos de volume não utilizar esses listeners que podem causar overhads nos disparos.

### 2 Variável Entre Grupos de Usuários com OAuth2

\Exemplos-JMX\2_VariavelEntreGruposDeUsuarios.jmx

Utilizando API's públicas do TDC para efeito de exemplo 

Informações: https://thedevconf.com/api

Para executar, obter suas credenciais para acessar a API e obter seu clientID e secret as instruções estão no início da página citada acima.
Substituir no script os valores em "Variáveis Definidas Pelo Usuário" para clientID e secret gerados para seu user no site https://www.globalcode.com.br/api

Obs: Esse é um exemplo meramente ilustrarivo para entender o formato, não utilize para fazer testes de performance no ambiente de produção do The Developers Conference.
Obrigada =)

No seUP Thread Group Acess Token usamos um JSON Extractor para obreter o valor do token gerado e colocarmos em uma variável.
Para que ele seja interpretado como uma "variável global" no JMeter, ou seja, para que seja utilizado em outros grupos de usuários, foi utilizado o Pós-Processador BeanShell para setar uma propriedade de acordo com a variável criada no JSON Extractor.

A mesma ideia do token pode ser utiliada entre API's que tem campos "dependentes".
Nesse exemplo, quer buscar um Evento Específico, mas para isso precisa passar o Id como parâmetro no endpoint.
Através da estrutura JSON Extractor e Pós-Processador BeanShell explicada no item 1 é possível obter esse valor em um grupo de usuário e utilizar essa propriedade em outro.

Obs: Se for utilizar esse token dentro do grupo de usuário não tem necessidade de utilizar o Pós-Processador BeanShell.

O Ouvinte "Ver Árvore de Resultado" foi Uitlizado somente para o exemplo ficar didático, para aplicar em disparos de volume não utilizar esses listeners que podem causar overhads nos disparos.

