# 🗄️ Política de Backups Automatizada - SQL Server

Este repositório contém os scripts e a configuração de uma rotina completa de backups (Completo, Diferencial e Log de Transações) desenvolvida para o Microsoft SQL Server. O objetivo deste projeto é demonstrar a implementação de uma política de contingência eficiente, minimizando a perda de dados e otimizando o espaço de armazenamento e tempo de restauração.

## 📌 Arquitetura do Projeto

O banco de dados utilizado na simulação é o `dbVendas`. Foram geradas notas fiscais e clientes simulados ao longo de um dia de trabalho para testar o crescimento do arquivo de backup e a integridade dos dados.

A política de backups foi estruturada da seguinte forma, sendo armazenada em um único arquivo `.BAK` diário:

| ID | Nome do Backup | Tipo | Horário | Notas Salvas (Simulação) |
|----|----------------|------|---------|--------------------------|
| 1  | BACKUP 1 AM | **FULL** | 01:00 | 3453 |
| 2  | BACKUP INCREMENTAL 4 AM | LOG | 04:00 | 3596 |
| 3  | BACKUP INCREMENTAL 6 AM | LOG | 06:00 | 3708 |
| 4  | BACKUP INCREMENTAL 8 AM | LOG | 08:00 | 3792 |
| 5  | BACKUP DIFFERENTIAL 9 AM | **DIFERENCIAL** | 09:00 | 3893 |
| 6  | BACKUP INCREMENTAL 10 AM | LOG | 10:00 | 3958 |
| 7  | BACKUP INCREMENTAL 12 PM | LOG | 12:00 | 4036 |
| 8  | BACKUP INCREMENTAL 2 PM | LOG | 14:00 | 4151 |
| 9  | BACKUP DIFFERENTIAL 2 PM | **DIFERENCIAL** | 14:00 | 4229 |
| 10 | BACKUP INCREMENTAL 3 PM | LOG | 15:00 | 4361 |
| 11 | BACKUP INCREMENTAL 5 PM | LOG | 17:00 | 4494 |
| 12 | BACKUP INCREMENTAL 7 PM | LOG | 19:00 | 4581 |
| 13 | BACKUP INCREMENTAL 9 PM | LOG | 21:00 | 4716 |

## 🚀 Estrutura dos Arquivos

* `01_DbVendas_Estrutura.sql`: Script de criação do banco de dados, tabelas, procedures (para geração de dados mockados) e configurações de instância.
* `02_Job_Backup_FULL.sql`: Script de automação (SQL Server Agent) que gera o arquivo base diário sobrescrevendo arquivos antigos (`WITH INIT`).
* `03_Job_Backup_DIFERENCIAL.sql`: Script de automação que salva os marcos intermediários do dia (`WITH DIFFERENTIAL`).
* `04_Job_Backup_INCREMENTAL.sql`: Script de automação que roda os backups de log de transações para garantir um Point-in-Time Restore (`WITH NOINIT`).

## 🛠️ Tecnologias Utilizadas
* Microsoft SQL Server
* T-SQL
* SQL Server Agent (Automação de Jobs)

