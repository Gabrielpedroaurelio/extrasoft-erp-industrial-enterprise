ADR-001 - Raw SQL com node-postgres (pg) em vez de Prisma

DATA: 26-03-2026
STATUS: ACEITE

>>Contexto:

O projecto usa PostgreSQL para persistência. A escolha do mecanismo de acesso à DB afecta performance, tipo-segurança e curva de aprendizagem.


>>DECISÃO

Usar node-postgres (pg) com Pool e queries SQL manuais parametrizadas. O desenvolvedor tem experiência em DBA e prefere controlo total sobre as queries.


>>CONSEQUÊNCIAS

Mais verboso que Prisma. Migrations manuais. Sem type-safety automática nas queries — compensado com TypeScript nas camadas de domínio.