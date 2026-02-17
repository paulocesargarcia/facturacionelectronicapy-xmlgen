---
name: nf-xmlgen-overview
description: Ajuda o agente a entender e navegar o projeto facturacionelectronicapy-xmlgen, explicando módulos principais, fluxo de geração de XML SIFEN e como rodar/testar. Use ao explorar o projeto, responder dúvidas gerais ou propor mudanças estruturais.
---

# NF XMLGen – Visão geral do projeto

## Objetivo deste skill

Ensinar o agente a:

- entender rapidamente o que o projeto `facturacionelectronicapy-xmlgen` faz,
- saber onde estão os pontos de entrada e serviços principais,
- ter um resumo do fluxo de geração de XML para o SIFEN,
- lembrar como rodar, formatar, lintar e testar o projeto.

## Visão geral

- Biblioteca Node.js/TypeScript para:
  - gerar XML de Documento Eletrônico (DE) exigido pelo SIFEN a partir de JSON,
  - gerar XML de eventos SIFEN (cancelamento, inutilização, conformidade, etc.),
  - expor funções utilitárias e constantes de domínio (países, departamentos, etc.).
- Publicada como pacote npm com `main` apontando para `dist/index.js`.

## Estrutura principal

- `src/index.ts`
  - Ponto de entrada da API pública.
  - Expõe a classe/instância responsável por:
    - `generateXMLDE(params, data, config?)`,
    - geração de XML para eventos SIFEN (cancelación, inutilización, conformidad, disconformidad, etc.),
    - métodos auxiliares de consulta (países, departamentos, etc.).

- `src/services/`
  - Serviços especializados, por exemplo:
    - montagem do JSON que será transformado em XML para DE e eventos,
    - validações conforme manual técnico SIFEN (v150),
    - cálculo de CDC e dígito verificador,
    - montagem de itens, totais, transporte, complementos e documentos associados,
    - utilitários de datas e strings,
    - constantes de domínio (listas/códigos oficiais).

- `test/`
  - Testes em TypeScript usando Mocha/Chai.

## Fluxo de geração de XML (resumo)

1. **Chamada da API pública** via `generateXMLDE` ou métodos de evento.
2. **Normalização e validação** dos dados de entrada conforme regras do SIFEN.
3. **Cálculo de chaves/CDC** usando serviços de algoritmo dedicados.
4. **Montagem da estrutura JSON** do documento eletrônico ou evento.
5. **Conversão JSON → XML** com `xml2js`, produzindo o XML final.

## Como rodar e desenvolver

- **Instalação (como dependência)**:
  - `npm install facturacionelectronicapy-xmlgen`

- **Scripts principais do repositório**:
  - `npm run build` — compila TypeScript para `dist/`.
  - `npm test` — executa testes `test/**/*.test.ts` com Mocha/Chai.
  - `npm run format` — aplica Prettier em `src/**/*.ts`.
  - `npm run lint` — roda TSLint com as regras do projeto.

## Boas práticas ao usar este skill

- Quando o usuário pedir:
  - explicações de arquitetura,
  - ajuda para localizar onde implementar uma mudança,
  - orientações sobre como rodar/testar o projeto,
  - contexto sobre como é feito o XML do SIFEN,
  use este skill como ponto de partida antes de propor mudanças.

- Combine este skill com as regras em:
  - `.cursor/rules/project-overview.mdc` — visão geral e contexto,
  - `.cursor/rules/architecture.mdc` — organização de módulos,
  - `.cursor/rules/code-style-typescript.mdc` — estilo de código e ferramentas.

