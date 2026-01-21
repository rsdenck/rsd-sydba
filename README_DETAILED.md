# Oracle Database Scripts - Repositório Detalhado

Este repositório contém uma vasta coleção de scripts SQL e Shell para administração, monitoramento e ajuste de performance de bancos de dados Oracle. Os scripts estão organizados por categorias funcionais em diretórios simplificados e em letras minúsculas.

## Como Usar os Scripts

A maioria dos scripts são arquivos `.sql` que devem ser executados via **SQL*Plus** ou **SQL Developer**.

### Execução via SQL*Plus:
```sql
sqlplus / as sysdba
@sysdba/diretorio/nome_do_script.sql
```

---

## Categorias de Scripts

### 1. asm (Automatic Storage Management)
Scripts para gerenciamento de armazenamento e discos.
- **asm_diskdrop.sql**: Comandos para remover discos de um Diskgroup e monitorar o rebalanceamento.
- **asmdiskgroup.sql**: Consulta o status e espaço dos grupos de discos ASM.
- **asmfilevolinfo.sql**: Informações sobre volumes e arquivos no ASM.
- **asmspaceused.sql**: Detalhamento do espaço utilizado por arquivo no ASM.

### 2. admin (Administração Geral)
Scripts para tarefas do dia a dia do DBA, incluindo manutenção de dicionário e objetos.
- **archive.sql / archive_new.sql**: Consulta status de arquivamento e geração de logs.
- **blocking_local.sql.com**: Identifica sessões bloqueadoras e bloqueadas localmente.
- **columns_usage.sql**: Analisa o uso de colunas em predicados (útil para estatísticas).
- **dba_schedulerjobs.sql**: Monitora o status e histórico de execução de jobs do Scheduler.
- **dbgrowth_permonth.sql**: Relatório de crescimento mensal do banco de dados.
- **ddl_schema.sql**: Gera o DDL completo para um esquema.
- **flashback_main.sql**: Monitoramento e status do Flashback Database.
- **hidden_params.sql**: Consulta parâmetros ocultos (os famosos `_param`).
- **sessions_active.sql / sessions_main.sql**: Monitoramento detalhado de sessões.
- **tablespace_free-sum.sql**: Resumo do espaço livre em todas as tablespaces.

### 3. backup (Backup e Recuperação)
Scripts focados em RMAN e estratégias de proteção de dados.
- **rman_monitoring.sql**: Monitora o progresso de backups em execução.
- **rman_bkpdetails.sql**: Histórico detalhado de backups realizados.
- **rman_datafile_backup.sql**: Backup de datafiles específicos.
- **rman_everything.sql**: Script abrangente para checagem de RMAN.
- **rman_fulldb_backupscript.sql**: Exemplo de script completo para backup Full via RMAN.

### 4. datapump (Export/Import)
Monitoramento e execução de ferramentas de movimentação de dados.
- **data_pump_monitor_core.sql**: Monitoramento central de jobs Data Pump.
- **datampump_monitoring.sql**: Acompanha o progresso de jobs de exportação/importação.
- **datapump_cleanup_orphanedjobs.sql**: Limpeza de jobs do Data Pump órfãos.

### 5. exadata
Scripts específicos para hardware e software Exadata.
- **exadata_cellperf.sql**: Monitoramento de performance dos Cell Nodes (Storage Servers).

### 6. goldengate
Scripts para ambientes de replicação.
- **goldengate_healthcheck.sql**: Verificação rápida do estado dos processos Extract/Replicat.

### 7. tuning (Ajuste de Performance)
Uma das categorias mais ricas, com scripts para diagnóstico profundo e otimização.
- **activesessions_ash.sql**: Análise de sessões ativas baseada no ASH.
- **ash_event_trend.sql**: Tendência de eventos de espera via ASH.
- **ash_top_events.sql**: Top eventos de espera nos últimos minutos.
- **awr_manualsnap.sql**: Comandos para gerar snapshots manuais do AWR.
- **awretention.sql**: Consulta e altera a retenção de dados do AWR.
- **cursor_notsharing_reason.sql**: Explica falhas de compartilhamento de cursor.
- **find_sql.sql**: Localiza o SQL ID e detalhes na Shared Pool.
- **gather_stats.sql**: Comandos para coleta de estatísticas.
- **high_version_count.sql**: Identifica queries com alto número de versões.

### 8. rac (Real Application Clusters)
Administração de ambientes em cluster.
- **rac_diag.sql**: Diagnóstico geral do estado do cluster e instâncias.
- **rac_longops.sql**: Monitora operações de longa duração no RAC.
- **rac_main.sql**: Script principal de monitoramento RAC.
- **racdbstatus.sql**: Status consolidado de todas as instâncias RAC.

### 9. standby (Data Guard)
Scripts para monitoramento de bancos de contingência.
- **check_dataguard_config.sql**: Valida a configuração atual do Data Guard.
- **quick_gap_check.sql**: Checagem rápida de Gaps de archive.
- **standby_monitor.sql**: Monitora o Lag de aplicação de logs no standby.
- **standbygap.sql**: Verifica archives faltando no destino.

### 10. tools (Ferramentas de Terceiros e Monitoramento ASH)
- **ashtop.sql**: Script clássico para visualizar o top de sessões ASH.
- **dashtop.sql**: Versão para DASH (AWR History).
- **snapper.sql**: Script famoso para captura de performance em tempo real.

### 11. reports (Relatórios de Diagnóstico)
- **dba_snapshot_database.sql**: Motor de geração de relatórios HTML 360º. Localizado em `sysdba/reports/`.

---

## Notas de Segurança
*   **Sempre teste os scripts em ambiente de desenvolvimento** antes de executá-los em produção.
*   Muitos scripts requerem privilégios de **SYSDBA**.
*   Scripts que utilizam ASH/AWR exigem a licença **Oracle Diagnostic Pack**.

---
*Relatório atualizado conforme a nova estrutura de diretórios padronizada.*
