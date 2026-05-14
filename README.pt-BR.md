# SAT-tableau

<p align="right">
  <a href="README.md">English</a> |
  <strong>Português (Brasil)</strong>
</p>

**SAT-tableau** é uma ferramenta educacional interativa, executada no navegador, para visualizar a prova por tableau por trás do **teorema de Cook-Levin**, isto é, que **SAT é NP-completo**.

A ferramenta foca na redução de uma computação aceitante de uma **Máquina de Turing não determinística em tempo polinomial (MTND)** para uma instância de satisfatibilidade booleana. Ela mostra como as variáveis do tableau, as transições da máquina e os componentes da fórmula SAT se conectam.

Ela foi projetada para uso em sala de aula em **Teoria da Computação**, especialmente no ensino do teorema de Cook-Levin por meio da construção padrão por histórico de computação/tableau.

🔗 **GitHub Pages:** https://brunogrisci.github.io/sat_tableau
🔗 **Repositório GitHub:** https://github.com/BrunoGrisci/SAT-tableau

---

## ✨ Funcionalidades

### Funcionalidade principal
- Visualização interativa da construção por tableau do teorema de Cook-Levin para SAT.
- Exemplo de MTND para múltiplos unários de **2 ou 3**:
  - o ramo `×2` verifica se o comprimento da entrada é par,
  - o ramo `×3` verifica se o comprimento da entrada é múltiplo de três.
- Comprimento configurável da entrada unária, representado pela quantidade de `1`s.
- Tratamento correto de ramos aceitantes e rejeitantes:
  - uma entrada como `1` não tem ramo aceitante,
  - uma entrada como `1111` é aceita pelo ramo `×2`, mas rejeitada pelo ramo `×3`,
  - ramos rejeitantes selecionados são destacados em vermelho para mostrar que sua atribuição não pode satisfazer `φaccept`.
- Controles dos ramos indicam se cada ramo não determinístico aceita ou rejeita a entrada atual.

### Visualização do tableau
- Tableau 3D de variáveis booleanas `x_{i,j,s}`:
  - linhas `t_i` representam passos de tempo/configurações,
  - colunas `j_i` representam posições da fita/configuração,
  - a profundidade representa os símbolos e estados possíveis.
- Variáveis verdadeiras são renderizadas como células legíveis; variáveis falsas aparecem como pequenos marcadores no modo 3D.
- Uma **visão 2D pelo eixo dos símbolos** achata o tableau numa projeção semelhante a uma matriz, útil para explicação em aula.
- No modo 2D, os marcadores das variáveis falsas são ocultados para não sobrepor os rótulos das células verdadeiras.
- Controles de visualização:
  - arrastar para rotacionar,
  - shift/botão do meio para mover a cena,
  - roda do mouse para zoom,
  - restaurar visão,
  - alinhar pelo eixo dos símbolos.

### Painéis da máquina e da fórmula
- **Painel da Máquina** com:
  - grafo da MTND,
  - transição ativa destacada,
  - cartões de transição para a escolha não determinística, varreduras, aceitações e rejeições,
  - controle da entrada unária.
- **Painel da Fórmula** com os componentes padrão da prova de Cook-Levin:
  - `φcell`: cada posição do tableau contém exatamente um símbolo,
  - `φstart`: a primeira linha é a configuração inicial,
  - `φaccept`: alguma célula do tableau contém `qA`,
  - `φmove`: toda janela local segue um movimento legal da máquina.
- Os blocos da fórmula mostram o esquema relevante, contagens de cláusulas/literais e a célula, unidade, literal aceitante ou janela legal atualmente selecionada.
- Seleções clicáveis no tableau:
  - escolha de uma célula para `φcell`,
  - escolha de uma unidade da linha inicial para `φstart`,
  - escolha de um literal de aceitação para `φaccept`,
  - escolha de uma janela local de duas linhas para `φmove`.
- Linhas de conexão ligam a explicação ativa da máquina/fórmula ao local correspondente no tableau.
- O painel lateral Máquina/Fórmula pode ser redimensionado arrastando seu separador esquerdo; a largura é persistida localmente.

### Referências e usabilidade
- Modal de **Referências** dentro da própria página explicando:
  - os papéis de Stephen Cook e Leonid Levin,
  - o estilo Karp/Sipser da prova por tableau usado pela ferramenta,
  - os 21 problemas NP-completos de Richard Karp,
  - a diferença entre a codificação pedagógica por tableau e codificações quasilineares posteriores,
  - a fonte teórica principal: Michael Sipser, *Introduction to the Theory of Computation*.
- Alternância entre modo claro/escuro 🌙 / ☀️.
- Alternância entre Inglês e Português do Brasil.
- Preferências persistentes via `localStorage`:
  - tema,
  - idioma,
  - largura do painel lateral.
- Totalmente client-side, sem backend e sem framework externo de UI.

---

## 🧠 Objetivos pedagógicos

Esta ferramenta foi construída para ajudar estudantes a:

- ver variáveis de SAT como posições de um tableau de computação, não apenas como símbolos abstratos,
- conectar o ramo aceitante existencial do não determinismo com a satisfatibilidade da fórmula,
- entender por que um ramo rejeitante não satisfaz `φaccept`,
- inspecionar separadamente as quatro restrições principais da prova de Cook-Levin,
- relacionar janelas locais do tableau com transições da Máquina de Turing,
- entender por que a consistência local basta para certificar um histórico global de computação,
- diferenciar a ideia da prova de detalhes de implementação ou codificações otimizadas.

Ela é adequada para:

- disciplinas de graduação em Teoria da Computação,
- demonstrações em sala com projetor,
- discussões guiadas sobre NP-completude e reduções,
- estudo individual da versão por tableau do teorema de Cook-Levin.

---

## 📄 Modelo de entrada

A versão atual da ferramenta não importa máquinas arbitrárias. Ela usa uma MTND pedagógica fixa derivada do material de aula:

- alfabeto de entrada: palavras unárias sobre `1`,
- valor de entrada: quantidade de `1`s, configurável no painel da Máquina,
- linguagem aceita: números unários cujo comprimento é múltiplo de `2` ou de `3`,
- escolha não determinística: a primeira transição escolhe o ramo `×2` ou o ramo `×3`.

O tamanho do tableau é derivado do comprimento atual da entrada. Para cada entrada, a ferramenta reconstrói a execução, atualiza o resultado dos dois ramos e renderiza novamente o tableau e as explicações da fórmula.

---

## 🌐 Internacionalização (i18n)

- Suporte completo a **Inglês** e **Português do Brasil**.
- Cabeçalho, controles, painéis, referências, mensagens de status, tooltips e explicações da fórmula são bilíngues.
- Trocar o idioma **não** reinicia a entrada selecionada, o ramo, o foco, a visão do tableau ou a largura do painel lateral.

---

## 🛠️ Stack tecnológica

- **HTML / CSS / JavaScript** puro
- Sem etapa de build
- Sem dependências externas
- Totalmente client-side
- Compatível com hospedagem estática, como **GitHub Pages**

Arquivos principais:

- `sat_tableau.html`
- `assetsSAT_tableau/styles.css`
- `assetsSAT_tableau/script.js`

Para executar localmente, abra `sat_tableau.html` diretamente no navegador ou sirva a pasta com qualquer servidor estático, por exemplo:

```bash
python3 -m http.server 4173
```

Então abra:

```text
http://127.0.0.1:4173/sat_tableau.html
```

---

## 🧪 Verificação

O projeto é estático e não exige framework de testes. Durante o desenvolvimento, a implementação foi verificada com:

```bash
node --check assetsSAT_tableau/script.js
```

Também foi usada validação no navegador para confirmar:

- aceitação/rejeição dos ramos para diferentes entradas unárias,
- destaques vermelhos para ramos rejeitantes selecionados,
- modos de foco da fórmula `φcell`, `φstart`, `φaccept` e `φmove`,
- seleção de células, unidades iniciais, literais de aceitação e janelas de movimento,
- linhas de conexão entre máquina/fórmula e tableau,
- rotação 3D, movimento, zoom, restauração e visão 2D pelo eixo dos símbolos,
- ocultação dos marcadores de variáveis falsas apenas no modo 2D,
- alternância entre tema claro/escuro,
- alternância entre Inglês e Português do Brasil,
- comportamento do modal de referências,
- redimensionamento e persistência do painel lateral.

---

## 🚀 Trabalhos futuros (ideias)

- Permitir importar ou editar Máquinas de Turing não determinísticas arbitrárias.
- Adicionar um modo guiado para os quatro componentes da fórmula.
- Exibir opcionalmente exemplos de cláusulas expandidas em mais posições do tableau.
- Adicionar uma legenda compacta para camadas de símbolos e classes estado/fita/delimitador.
- Exportar a atribuição atual do tableau ou o resumo da fórmula.
- Adicionar screenshots e exemplos animados curtos ao README.

---

## 🎓 Créditos

**Desenvolvido por**  
**Prof. Bruno Iochins Grisci**  
Departamento de Informática Teórica  
Instituto de Informática – Universidade Federal do Rio Grande do Sul (UFRGS)  
🔗 https://brunogrisci.github.io/  
🔗 https://www.inf.ufrgs.br/site/  
🔗 https://www.ufrgs.br/site/

**Principal referência teórica**
- Michael Sipser, *Introduction to the Theory of Computation*, especialmente o teorema de Cook-Levin e a construção por tableau/janelas locais.

**Contexto histórico e da prova**
- Stephen Cook e Leonid Levin: o teorema de Cook-Levin.
- Richard Karp: redutibilidade e os 21 problemas NP-completos.
- Prova por tableau no estilo Karp/Sipser usada como base para esta visualização.
- Codificações quasilineares posteriores são mencionadas no modal de referências, mas intencionalmente não são desenvolvidas nesta ferramenta didática.

**Nota de desenvolvimento**  
Esta ferramenta foi criada com assistência do **Codex GPT-5.5**.

---

## 📦 Licença

Este projeto está licenciado sob a **Licença MIT**.

Você pode usar, modificar e redistribuir para fins acadêmicos e educacionais, desde que haja a devida atribuição.

Veja o arquivo `LICENSE` para detalhes.

---

Se você usar esta ferramenta em ensino ou pesquisa, uma citação ou link para o repositório é bem-vindo.

## 📚 Citação

Se você usar esta ferramenta em trabalhos acadêmicos (artigos, teses, relatórios técnicos ou material didático), cite-a como:

```bibtex
@software{Grisci_SAT_tableau,
  author       = {Bruno Iochins Grisci},
  title        = {{SAT-tableau}: Um Visualizador Interativo para a Construção por Tableau de Cook-Levin},
  year         = {2026},
  url          = {https://github.com/BrunoGrisci/SAT-tableau},
  note         = {Software educacional baseado na web},
}
```

---

## 🔄 Veja também

- **Gerador de Dominós TM → PCP (tm2pcp)**  
  Webtool: https://brunogrisci.github.io/tm2pcp  
  Repositório: https://github.com/BrunoGrisci/tm2pcp-webtool

- **Webtool PCP → Ambiguidade de GLC**  
  Web app: https://brunogrisci.github.io/pcp2cfg  
  Repositório: https://github.com/BrunoGrisci/pcp2cfg-webtool

- **Reduções executáveis de computabilidade**  
  Repositório: https://github.com/BrunoGrisci/reductions-computability
