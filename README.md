# Guia Técnico de Scripts para Administração de Banco de Dados Oracle

Este repositório consolida ferramentas avançadas para DBAs (Database Administrators), focadas em monitoramento, diagnóstico de performance, auditoria de segurança e automação de tarefas em ambientes Oracle Database.

---

## 1. Relatório Consolidado de Saúde: `dba_snapshot_database.sql`

O script [dba_snapshot_database.sql](file:///c:/Users/ranlens.denck/Documents/trae_projects/ORAMON/sysdba/reports/dba_snapshot_database.sql) é um motor de geração de relatórios HTML que fornece uma visão 360º da instância.

### **Arquitetura Técnica**
- **Motor de Renderização:** Utiliza comandos `SET MARKUP HTML ON` do SQL*Plus para converter saídas de queries em tabelas HTML estruturadas com CSS inline.
- **Localização Padronizada:** Agora localizado em `sysdba/reports/`.
- **Compatibilidade:** Desenvolvido originalmente para Oracle 10g, mas compatível com 11g, 12c, 19c e 21c devido ao uso de visões de dicionário de dados estáveis (`V$`, `GV$`, `DBA_`).
- **Navegação:** Implementa um índice de âncoras internas no topo do documento para acesso rápido às seções.

---

## 2. Biblioteca de Scripts Especializados: `sysdba/`

O diretório [sysdba](file:///c:/Users/ranlens.denck/Documents/trae_projects/ORAMON/sysdba) contém uma coleção de mais de 500 scripts padronizados e categorizados por subsistemas do Oracle em diretórios simplificados e em letras minúsculas.

### **Categorias Técnicas e Funcionalidades**

#### **A. Gerenciamento de Memória e Performance (`tuning`)**
- **ASH (Active Session History):** Scripts como `ashtop.sql` permitem analisar o que as sessões estão fazendo *neste exato segundo*, decompondo o DB Time por eventos de espera, objetos e SQL IDs. Localizado em `sysdba/tools/` e `sysdba/tuning/`.
- **AWR (Automated Workload Repository):** Ferramentas para manipulação de retenção e geração manual de snapshots.
- **Optimizer & Statistics:** Scripts para identificar estatísticas obsoletas (`stale_stats`) e forçar planos de execução via SQL Plan Baselines ou Profiles.

#### **B. Armazenamento Avançado (`asm`)**
- Monitoramento de `REBALANCE` de discos em tempo real.
- Verificação de redundância e distribuição de extensões entre Failure Groups.
- Scripts para adição e remoção segura de discos físicos.

#### **C. Ambientes em Cluster (`rac`)**
- Diagnóstico de latência de interconectividade (Private Network).
- Status de recursos do Clusterware (CRS) e balanceamento de carga entre instâncias.
- Monitoramento de `GC` (Global Cache) waits, críticos para a escalabilidade do RAC.

#### **D. Continuidade de Negócios (`standby` / `backup`)**
- **Data Guard:** Scripts para cálculo de `Apply Lag` e `Transport Lag`.
- **RMAN:** Automação de purga de archives e validação de integridade física de backups.

#### **E. Relatórios Automáticos (`reports`)**
- Contém o `dba_snapshot_database.sql` e outros scripts de diagnóstico consolidado.

---

## 3. Instruções de Operação

### **Pré-requisitos**
1. **Privilégios:** A maioria dos scripts exige conexão `AS SYSDBA`.
2. **Licenciamento:** Scripts que acessam visões `V$ASH_...`, `V$AWR_...` ou `DBA_HIST_...` requerem as licenças **Diagnostic Pack** e **Tuning Pack**.
3. **Ambiente:** SQL*Plus (versão 10.2 ou superior).

### **Execução Padrão**
```bash
# Para scripts de relatório único (ex: Snapshot):
sqlplus -s / as sysdba @sysdba/reports/dba_snapshot_database.sql

# Para scripts da biblioteca especializada:
cd sysdba/tuning
sqlplus / as sysdba
SQL> @find_sql.sql  # Solicitará o SQL_ID como parâmetro
```

---

## 4. Melhores Práticas e Segurança

- **Ambiente de Teste:** Nunca execute scripts de "Shrink" ou "Kill Session" em produção sem antes validar em homologação.
- **Trace & Debug:** Scripts na pasta `datapump` e `admin` podem gerar arquivos de trace no servidor. Monitore o espaço em disco no `ADR_HOME`.
- **Customização:** Os scripts `+login.sql` e `+plusenv.sql` presentes nas subpastas configuram a formatação das colunas para evitar quebras de linha indesejadas.

---
*Este repositório é mantido como uma base de conhecimento técnica para operações de missão crítica em Oracle Database.*
