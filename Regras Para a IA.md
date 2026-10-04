ARQUITETO DE SOFTWARE — PROJETO MODULAR E DOCUMENTADO
Você deverá desenvolver este projeto seguindo uma arquitetura altamente modular, legível, rastreável e amigável para manutenção por uma pessoa com conhecimento limitado de programação que utiliza IA como principal ferramenta de desenvolvimento.
O objetivo não é apenas fazer o projeto funcionar. O objetivo é fazer com que, depois de pronto, seja possível identificar rapidamente onde cada comportamento, componente, estilo, dado e configuração está localizado, permitindo alterações pontuais sem precisar compreender todo o sistema.

1. MODO CIRÚRGICO
Quando o usuário solicitar uma alteração localizada, opere estritamente em modo cirúrgico.
Exemplo:
 * PEDIDO: "Aumente o botão Entrar."
A IA deve:
 * Localizar o componente exato;
 * Localizar o seu arquivo de estilo;
 * Alterar somente o necessário para o pedido;
 * Não modificar o layout global;
 * Não alterar outros botões do sistema;
 * Não instalar novas dependências;
 * Não refatorar código não relacionado ao pedido.

2. PROIBIÇÃO DE "REFATORAÇÃO SILENCIOSA"
Não aproveite uma solicitação pequena para reorganizar o projeto inteiro.
Se o usuário pedir:
> "Mude a cor do botão."
> 
NÃO:
 * reorganize os componentes;
 * atualize dependências;
 * altere o sistema de temas;
 * renomeie arquivos;
 * reescreva o CSS inteiro.
Faça somente o necessário. Se uma alteração arquitetural realmente for necessária, explique antes.

3. PRINCÍPIO FUNDAMENTAL
Não construa uma aplicação monolítica.
Evite arquivos gigantes como:
 * "App.tsx" com centenas ou milhares de linhas;
 * um único CSS contendo todos os estilos;
 * componentes que concentram várias responsabilidades;
 * funções genéricas que fazem coisas demais;
 * lógica de negócio misturada com interface;
 * dados misturados com componentes visuais;
 * configurações espalhadas pelo projeto.
Cada módulo deve possuir uma responsabilidade claramente identificável. Utilize os princípios de Separation of Concerns, Single Responsibility, High Cohesion, Low Coupling, Componentização, Encapsulamento, Reutilização, Legibilidade e Rastreabilidade. Quando uma funcionalidade puder ser isolada em um módulo próprio, prefira isolá-la.

4. UMA FUNCIONALIDADE = UMA PASTA
Em vez de espalhar uma funcionalidade por diversos locais distantes no projeto, agrupe seus recursos em um único módulo funcional.
Exemplo:
funcionalidades/
└── favoritos/
    ├── Favoritos.tsx
    ├── favoritos.css
    ├── favoritos.service.ts
    ├── favoritos.types.ts
    └── README.md

Isso cria coesão funcional. Se você quiser remover ou alterar "Favoritos", saberá exatamente onde procurar.

5. COMPONENTES COM "CONTRATO" CLARO
Cada componente deve possuir um contrato explícito de responsabilidade.
Exemplo (CartaoPessoa):
 * Entrada (Props): nome (string), foto (string), idade (number)
 * Saída (Eventos): onClick()
 * Responsabilidade: Exibir informações visuais da pessoa.
 * NÃO É RESPONSÁVEL POR: Salvar pessoas, acessar API/banco de dados, buscar dados diretamente ou controlar rotas de navegação.

6. COMPONENTES AUTOCONTIDOS
Sempre que fizer sentido, organize componentes como módulos independentes.
Exemplo:
componentes/
└── cartao-pessoa/
    ├── CartaoPessoa.tsx
    ├── cartao-pessoa.css
    ├── tipos.ts
    └── README.md

O README.md deverá explicar: função do componente, arquivos relacionados, dados recebidos, eventos produzidos, dependências importantes, onde alterar sua aparência, onde alterar seu comportamento e o que este componente não deve fazer. Não crie arquivos desnecessários apenas para aumentar a quantidade de arquivos.

7. SEPARAÇÃO ENTRE INTERFACE E LÓGICA
Não misture indiscriminadamente: interface visual + estado + persistência + API + regras de negócio + configuração.
Separe essas responsabilidades. Por exemplo:
componentes/
    CartaoPessoa.tsx

servicos/
    pessoas.ts

dados/
    pessoas.ts

tipos/
    pessoa.ts

O componente visual não deve ser responsável por tudo.

8. ARQUITETURA ORIENTADA À LOCALIZAÇÃO
A estrutura de diretórios deve permitir que uma pessoa consiga responder rapidamente: «"Onde está aquilo que quero modificar?"»
Exemplos:
 * Quero alterar um botão → procurar em componentes/
 * Quero alterar uma página → procurar em paginas/
 * Quero alterar uma cor → procurar em estilos/
 * Quero alterar os dados → procurar em dados/
 * Quero alterar uma integração → procurar em servicos/
 * Quero alterar uma configuração → procurar em configuracao/
 * Quero alterar comportamento específico do Android → procurar em plataforma/
Não esconda funcionalidades importantes em arquivos com nomes genéricos como utils.ts, helpers.ts, misc.ts, common.ts, functions.ts ou stuff.ts quando for possível utilizar nomes semanticamente específicos.

9. REGRAS PARA ALTERAÇÕES FUTURAS
Quando receber uma solicitação de alteração:
 * Primeiro identifique o módulo responsável.
 * Consulte o MAPA_DO_PROJETO.md.
 * Consulte a documentação do módulo.
 * Modifique somente os arquivos necessários.
 * Evite alterações colaterais.
 * Não recrie componentes existentes.
 * Não duplicar lógica existente.
 * Não mover arquivos sem necessidade.
 * Não alterar a arquitetura apenas para resolver um problema pequeno.
 * Após modificar o projeto, informe exatamente quais arquivos foram alterados e por quê.
Se o pedido puder ser resolvido modificando um único arquivo, não altere cinco.

10. COMPATIBILIDADE COM IA
Este projeto será desenvolvido e mantido com auxílio frequente de inteligência artificial. Portanto, a arquitetura deve ser machine-readable e human-readable.
Os nomes devem ser semanticamente explícitos. Evite abstrações excessivamente sofisticadas quando uma implementação simples e explícita for suficiente. Não utilize padrões arquiteturais complexos apenas para demonstrar sofisticação técnica.
A melhor arquitetura para este projeto é aquela que permite:
LOCALIZAR → ENTENDER → ALTERAR → TESTAR com o menor número possível de etapas.

11. DOCUMENTAÇÃO CENTRAL
Crie obrigatoriamente o arquivo MAPA_DO_PROJETO.md na raiz da aplicação. Esse arquivo será o índice humano da aplicação.
Ele deverá explicar:
 * O propósito do projeto;
 * A estrutura de diretórios;
 * A função de cada diretório;
 * As páginas existentes;
 * Os principais componentes;
 * Onde ficam os estilos;
 * Onde ficam os dados;
 * Onde ficam os serviços;
 * Onde ficam as configurações;
 * Dependências importantes;
 * Fluxos principais;
 * Como adicionar uma nova funcionalidade;
 * Como alterar uma funcionalidade existente;
 * Quais arquivos NÃO devem ser modificados diretamente;
 * Relações importantes entre módulos.

12. DOCUMENTAÇÃO LOCAL
Cada módulo complexo deverá possuir documentação local (README.md).
A documentação deve responder:
 * «O que é isso?»
 * «Para que serve?»
 * «Quem utiliza isso?»
 * «Onde devo mexer se quiser alterar seu comportamento?»
 * «O que não devo alterar sem entender primeiro?»
Não escreva documentação ornamental. A documentação deve possuir utilidade prática.

13. MAPA DE DEPENDÊNCIAS
Sempre que houver relações importantes entre módulos, documente-as.
Exemplo:
Pessoas.tsx
    ↓
CartaoPessoa.tsx
    ↓
ModalEdicaoPessoa.tsx
    ↓
servicos/pessoas.ts
    ↓
servicos/armazenamento.ts

O objetivo é permitir rastrear: Interface → Componente → Regra → Serviço → Persistência.

14. IDIOMA E NOMENCLATURA
Toda a documentação criada especificamente para o projeto deverá estar em português brasileiro. Comentários importantes do código deverão estar em português brasileiro.
Nomes de arquivos, diretórios e componentes deverão ser claros e semanticamente descritivos.
Prefira: CartaoPessoa.tsx, ModalEdicaoPessoa.tsx, MenuLateral.tsx, armazenamento.ts, exportacao.ts, configuracaoTema.ts em vez de: Card.tsx, Modal2.tsx, Menu.tsx, utils.ts, data.ts, config.ts.
Evite abreviações desnecessárias. O nome de um arquivo deve ajudar uma pessoa a descobrir sua função sem precisar abrir o arquivo.

15. ESTILIZAÇÃO
Centralize valores globais de aparência.
Por exemplo:
estilos/
├── global.css
├── cores.css
├── tipografia.css
├── espacamento.css
└── componentes.css

Cores recorrentes, tamanhos, espaçamentos e outros tokens de design deverão ser centralizados quando isso melhorar a consistência. Não espalhe dezenas de valores arbitrários pelo projeto sem necessidade. Se uma cor principal estiver sendo utilizada em vinte lugares, deve existir uma forma simples de alterá-la globalmente.

16. CONFIGURAÇÕES
Configurações modificáveis deverão ficar em locais previsíveis.
Exemplo:
configuracao/
├── tema.ts
├── constantes.ts
├── ambiente.ts
└── funcionalidades.ts

Evite esconder configurações importantes dentro de componentes. Se existir algo que o usuário provavelmente desejará personalizar futuramente, considere isolá-lo.

17. DADOS
Dados estáticos, modelos e estruturas persistentes não devem ficar misturados indiscriminadamente à interface.
Utilize estruturas como:
dados/
├── pessoas.ts
├── categorias.ts
└── configuracoes.ts

tipos/
├── Pessoa.ts
├── Categoria.ts
└── Configuracao.ts

Quando houver persistência:
servicos/
└── armazenamento/
    ├── armazenamento.ts
    └── README.md

18. ANTES DE ESCREVER CÓDIGO
Antes de implementar a aplicação:
 * Analise os requisitos.
 * Proponha a arquitetura.
 * Crie a árvore de diretórios.
 * Explique a responsabilidade de cada módulo.
 * Identifique possíveis pontos de acoplamento.
 * Identifique funcionalidades que deverão ser isoladas.
 * Defina os padrões de nomenclatura.
 * Defina o sistema de documentação.
 * Crie o MAPA_DO_PROJETO.md.
 * Somente depois comece a implementação.
Não pule diretamente para um arquivo gigante.

19. CRITÉRIO DE QUALIDADE
Considere o projeto bem estruturado somente se uma pessoa que não conhece profundamente o código conseguir responder perguntas como:
 * «"Onde altero esta cor?"»
 * «"Onde está este botão?"»
 * «"Onde está esta página?"»
 * «"Onde os dados são armazenados?"»
 * «"Onde está a regra responsável por isso?"»
 * «"Qual arquivo controla esta configuração?"»
 * «"Se eu apagar este componente, o que quebra?"»
 * «"Como adiciono outro componente semelhante?"»
Se essas respostas não forem óbvias, melhore a organização.

20. REGRA FINAL E ENTREGÁVEIS
Não quero apenas um software funcional. Quero um software cuja arquitetura permita que eu continue trabalhando nele depois que você terminar. O projeto deve ser construído de forma que eu consiga usar a IA para fazer alterações específicas sem precisar compreender todo o código-fonte.
Priorize:
CLAREZA → LOCALIZAÇÃO → MODULARIDADE → DOCUMENTAÇÃO → MANUTENIBILIDADE → FUNCIONALIDADE
A funcionalidade continua sendo obrigatória, mas não sacrifique a legibilidade e a manutenibilidade para obtê-la.
Ao final de cada implementação, forneça obrigatoriamente:
 * Estrutura final dos arquivos;
 * Arquivos criados;
 * Arquivos modificados;
 * Responsabilidade de cada arquivo;
 * Como localizar as principais funcionalidades;
 * Possíveis pontos de manutenção futura;
 * Comandos necessários para executar, testar e gerar o projeto.