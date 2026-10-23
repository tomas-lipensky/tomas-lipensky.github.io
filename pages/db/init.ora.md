control_files = (/lcg03/control.001.dbf, /lcg03/control.002.dbf, /lcg03/control.003.dbf)  
db_name = lcg03  

db_domain = lipnet.cz  

log_archive_dest_1 =  
"LOCATION=/log/lcg03/arch"  
log_archive_dest_state_1 = enable  

db_block_size = 8192  
pga_aggregate_target = 2500M  

processes = 1000  
sessions = 1200  
open_cursors = 1024  

undo_management = AUTO  

shared_servers = 3  
remote_listener = tnsfstlcg03  

undo_tablespace = smu_nd1  
compatible 10.1.0.0.0  

sga_target = 1500M  

nls_language = AMERICAN  
nls_territory = AMERICA  
db_recovery_dile_dest =  
/log/lcg03/arch  
db_recovery_file_dest_size = 100G
