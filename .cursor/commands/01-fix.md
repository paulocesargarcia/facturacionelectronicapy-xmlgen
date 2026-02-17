# /fix {descrição}

Use um modelo rápido e barato para esta tarefa (ex: gpt-4o-mini, gemini-flash, grok-fast, deepseek ou composer se disponível).

Passos exatos:

1. Converta "{descrição}" em kebab-case (minúsculas, hifens, sem acentos/caracteres especiais). Ex: "analise de envio do lote" → "001-chore-analise-envio-lote".

2. Liste arquivos: `ls docs/changelog/*.md 2>/dev/null || true`

3. Extraia o maior número do prefixo (formato XXX-*.md). Se nenhum → 000. Senão incremente.  
   Use lógica simples ou peça para calcular: seq=$(printf "%03d" $((maior + 1)))

4. Nome do branch e arquivo: ${seq}-fix-${kebab}

5. Crie branch: `git checkout -b ${nome}`

6. Crie arquivo: `mkdir -p docs/changelog && touch docs/changelog/${nome}.md`

7. Mostre o nome criado e confirme que o branch está ativo.

8. Tipos
- `feat`: nova funcionalidade
- `fix`: correção de bug
- `refactor`: refatoração sem mudança de comportamento
- `docs`: documentação
- `chore`: tarefas de manutenção
- `style`: formatação