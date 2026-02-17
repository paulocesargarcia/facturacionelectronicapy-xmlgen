# /commit

Use modelo rápido e barato (gpt-4o-mini, gemini-flash, etc.).

Passos:

1. Pegue branch atual: `git rev-parse --abbrev-ref HEAD`

2. Encontre o .md que contém o nome do branch (ex: 042-fix-analise-envio-lote.md)

3. Se não achar → avise e pare

4. Analise mudanças: `git diff --staged` (ou `git diff` se nada staged)

5. Gere mensagem curta de commit + resumo das alterações

6. Anexe ao arquivo encontrado: adicione seção nova com data + resumo (use `date` para timestamp)

7. Adicione todos os arquivos ao staging: `git add .` (inclui arquivos novos, modificados e removidos)

8. Commit: `git commit --no-signoff -m "{mensagem}"`

9. Se o commit tiver co-autor adicionado automaticamente, remova com: `git commit --amend -m "{mensagem}"` (isso reescreve o commit sem trailers)

10. Confirme commit e mostre mensagem usada (verificar que não há "Co-authored-by" na mensagem)