# JMeter

## Resumo geral da Ferramenta com Mind Maps

\MindMap-ResumoJmeter\ResumoJMeter.mm

## Exemplos de algumas estruturas

### 1 Obter Token Oauth2
Utilizando API's públicas do TDC para efeito de exemplo 

Informações: https://thedevconf.com/api
Para executar, obter suas credenciais para acessar a API e obter seu clientID e secret as instruções estão no início da página citada acima.
Substituir no script os valores em "Variáveis Definidas Pelo Usuário" para clientID e secret gerados para seu user no site https://www.globalcode.com.br/api

Foi utilizado o Base64 passando o clientID e secret, a chamada desse encodeBase64 é colocado numa váriavel chamada de auth no exemplo e ela é passada no Authorization para gerarmos o token.

Para ser utilizado em outros grupos de usuário foi utiliado o elemento JSON Extractor para buscar no JSON o valor do token para ser utilizado no header da chamada de outras API's

O Ouvinte "Ver Árvore de Resultado" foi Uitlizado somente para o exemplo ficar didático, para aplicar em disparos de volume não utilizar esses listeners que podem causar overhads nos disparos.

### 2 Variável Entre Grupos de Usuários com OAuth2

\Exemplos-JMX\2_VariavelEntreGruposDeUsuarios.jmx

Utilizando API's públicas do TDC para efeito de exemplo 

Informações: https://thedevconf.com/api
Para executar, obter suas credenciais para acessar a API e obter seu clientID e secret as instruções estão no início da página citada acima.
Substituir no script os valores em "Variáveis Definidas Pelo Usuário" para clientID e secret gerados para seu user no site https://www.globalcode.com.br/api

Obs: Esse é um exemplo meramente ilustrarivo para entender o formato, não utilize para fazer testes de performance no ambiente de produção do The Developers Conference.
Obrigada =)

No seUP Thread Group Acess Token usamos um JSON Extractor para obreter o valor do tken gerado e colocarmos em uma variável.
Para que ele seja interpretado como uma "variável global" no JMeter, ou seja, para que seja utilizado em outros grupos de usuários, foi utilizado o Pós-Processador BeanShell para setar uma propriedade de acordo com a variável criada no JSON Extractor.

Obs: Se for utilizar esse token dentro do grupo de usuário não tem necessidade de utilizar o Pós-Processador BeanShell.

O Ouvinte "Ver Árvore de Resultado" foi Uitlizado somente para o exemplo ficar didático, para aplicar em disparos de volume não utilizar esses listeners que podem causar overhads nos disparos.

