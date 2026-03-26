ADR-003 - JWT stateless em vez de sessions com Redis

DATA: 26-03-2026
STATUS: ACEITE

>>Contexto:

Sistema deve funcionar em LAN sem internet contínua. Sessões com Redis exigem infraestrutura adicional.


>>DECISÃO

JWT com accessToken (15min) e refreshToken (7 dias, guardado em DB). Stateless — o servidor não guarda estado de sessão.

>>CONSEQUÊNCIAS

Revogação de tokens mais complexa (exige blacklist na DB). Compensa pela simplicidade de deploy em ambiente LAN sem Redis.