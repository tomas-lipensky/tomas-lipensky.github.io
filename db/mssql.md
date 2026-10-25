# mssql

## MSSQL

### Externi odkazy

[SQL Server 2005 Waiting and Blocking Issues](http://www.informit.com/articles/article.aspx?p=686168&seqNum=5)  

### Klienti

#### Powershell

Import-Module Az.Sql -Force  
 Install-Module -Name SqlServer  
$Params = @{  
'ServerInstance' = 'atademo.database.windows.net';  
'Database' = 'ata-demo';  
'Username' = 'ataadmin';  
'Password' = 'Admin123';  
'Query' = 'select name from sys.database_principals;;'  
}  
Invoke-Sqlcmd @Params  
### Databaze

#### Prikazy - database master

select name,log_reuse_wait_desc from sys.databases ... seznam databazi a pocet ???  
alter login glob with password='HESLO123'; ... nastaveni hesla pro login na SQL server  
alter DATABASE [puvodni.nazev.databaze] modify name=[novy.nazev.databaze]; ... prejmenovani databaze  
DENY CONNECT TO account_name; ... zakaze pripojeni danemu uzivateli  
alter login USER disable; ... zakaze login daneho uzivatele  

#### Prikazy - hostovane databaze

select name from sys.database_principals; ... seznam uzivatelu v databazi  
alter user glob with login=glob;  ... propojeni uzivatele glob v databazi s loginem na SQL server - uprava SIDu  

#### Scenare

== Obsah aktualniho transakcniho logu: ==

```
    SELECT RTRIM(name) AS [Segment Name], groupid AS [Group Id], filename AS [File Name],
    CAST(size/128.0 AS DECIMAL(10,2)) AS [Allocated Size in MB],
    CAST(FILEPROPERTY(name, 'SpaceUsed')/128.0 AS DECIMAL(10,2)) AS [Space Used in MB],
    CAST([maxsize]/128.0 AS DECIMAL(10,2)) AS [Max in MB],
    CAST([maxsize]/128.0-(FILEPROPERTY(name, 'SpaceUsed')/128.0) AS DECIMAL(10,2)) AS [Available Space in MB],
    CAST((CAST(FILEPROPERTY(name, 'SpaceUsed')/128.0 AS DECIMAL(10,2))/CAST([maxsize]/128.0 AS DECIMAL(10,2)))*100 AS DECIMAL(10,2)) AS [Percent Used]
    FROM sys.sysfiles
    where name='log'
```

== Seznam session a jejich stav: ==

```
    SELECT
    R.SESSION_ID,
    R.REQUEST_ID AS SESSION_REQUEST_ID,
    R.STATUS,
    S.HOST_NAME,
    C.CLIENT_NET_ADDRESS,
    CASE WHEN S.LOGIN_NAME = S.ORIGINAL_LOGIN_NAME THEN S.LOGIN_NAME ELSE S.LOGIN_NAME + ' (' + S.ORIGINAL_LOGIN_NAME + ')' END AS LOGIN_NAME,
    S.PROGRAM_NAME,
    DB_NAME(R.DATABASE_ID) AS DATABASE_NAME,
    R.COMMAND,
    ST.TEXT AS QUERY_TEXT,
    QP.QUERY_PLAN AS XML_QUERY_PLAN,
    R.WAIT_TYPE AS CURRENT_WAIT_TYPE,
    R.LAST_WAIT_TYPE,
    R.BLOCKING_SESSION_ID,
    R.ROW_COUNT,
    R.GRANTED_QUERY_MEMORY,
    R.OPEN_TRANSACTION_COUNT,
    R.USER_ID,
    R.PERCENT_COMPLETE,
    CASE R.TRANSACTION_ISOLATION_LEVEL
          WHEN 0 THEN 'UNSPECIFIED'
          WHEN 1 THEN 'READUNCOMITTED'
          WHEN 2 THEN 'READCOMMITTED' 
          WHEN 3 THEN 'REPEATABLE'
          WHEN 4 THEN 'SERIALIZABLE'
          WHEN 5 THEN 'SNAPSHOT'
          ELSE CAST(R.TRANSACTION_ISOLATION_LEVEL AS VARCHAR(32))
    END AS TRANSACTION_ISOLATION_LEVEL_NAME

FROM
    SYS.DM_EXEC_REQUESTS R
    LEFT OUTER JOIN SYS.DM_EXEC_SESSIONS S ON S.SESSION_ID = R.SESSION_ID
    LEFT OUTER JOIN SYS.DM_EXEC_CONNECTIONS C ON C.CONNECTION_ID = R.CONNECTION_ID
    CROSS APPLY SYS.DM_EXEC_SQL_TEXT(R.SQL_HANDLE) ST
    CROSS APPLY SYS.DM_EXEC_QUERY_PLAN(R.PLAN_HANDLE) QP
--WHERE R.STATUS NOT IN ('BACKGROUND','SLEEPING')
```

== Seznam blokujicich a uzamykajicich sezeni: ==

```
    ;WITH Blockers AS
    (
              SELECT DISTINCT
                     blocking_session_id as session_id
              FROM sys.dm_exec_requests WITH(NOLOCK)
              WHERE blocking_session_id > 0
       )
SELECT
       'Blocker' as type_desc
       , ES.session_id
       , ES.transaction_isolation_level
       , ER.start_time
       , ER.[status]
       , ER.command
       , ER.wait_type
       , ER.wait_time
       , ER.blocking_session_id
       , '' AS stmt_text
FROM sys.dm_exec_sessions ES WITH(NOLOCK)
       LEFT JOIN sys.dm_exec_requests ER WITH(NOLOCK) ON ER.session_id = ES.session_id
       INNER JOIN Blockers ON Blockers.session_id = ES.session_id
UNION
SELECT
       'Victim' as type_desc
       , ES.session_id
       , ES.transaction_isolation_level
       , ER.start_time
       , ER.[status]
       , ER.command
       , ER.wait_type
       , ER.wait_time
       , ER.blocking_session_id
       , ST.[text] AS stmt_text
FROM sys.dm_exec_sessions ES WITH(NOLOCK)
       INNER JOIN sys.dm_exec_requests ER WITH(NOLOCK) ON ER.session_id = ES.session_id
       CROSS APPLY SYS.DM_EXEC_SQL_TEXT(ER.sql_handle) AS ST
WHERE blocking_session_id > 0
```
