ADR-004 - UUID em vez de IDs sequenciais (SERIAL/INTEGER)

DATA: 26-03-2026
STATUS: ACEITE

>>Contexto:

IDs sequenciais expõem o volume de dados da empresa (ex: a factura 0043 revela que há menos de 50 facturas). Risco de segurança e de scraping.


>>DECISÃO
 
Usar UUID v4 gerado pelo PostgreSQL (gen_random_uuid()) como PK em todas as tabelas.

>>CONSEQUÊNCIAS
 
UUIDs são maiores (16 bytes vs 4). Índices ligeiramente maiores. Sem impacto perceptível para o volume de dados deste ERP.