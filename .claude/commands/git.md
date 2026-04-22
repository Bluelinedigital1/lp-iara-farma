Faça o deploy para produção seguindo estes passos:

1. Execute `git status` para ver os arquivos modificados
2. Execute `git diff --stat` para entender o que mudou
3. Execute `git log --oneline -3` para ver o estilo das mensagens de commit anteriores
4. Adicione os arquivos modificados com `git add` (apenas os arquivos relevantes, nunca use `git add .` de forma irresponsável — verifique antes)
5. Crie um commit com mensagem descritiva em português, resumindo o que foi alterado
6. Faça `git push origin main`
7. Execute `npx vercel --prod` para fazer o deploy direto no ambiente de produção do Vercel
8. Informe ao usuário que o deploy foi iniciado via Vercel CLI
