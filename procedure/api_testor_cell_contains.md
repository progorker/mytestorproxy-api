```
===========_____=======_============
  _ __ _  |_   _|__ __| |_ ___ _ _ 
 | '  \ || || |/ -_|_-<  _/ _ \ '_|
 |_|_|_\_, ||_|\___/__/\__\___/_|  
=======|__/=========================
  API References of myTestorProxy
           ----- oOo -----
[procedure] api_testor_cell_contains
====================================


-------|__/-------------------------
               SYNTAX
------------------------------------

procedure mytestorproxy.api_testor_cell_contains ( 
  in p_token varchar(36), 
  out p_test_id bigint, 
  in p_suite_id bigint, 
  in p_case_id bigint, 
  in p_test_code varchar(640), 
  in p_table varchar(8192), 
  in p_field varchar(8192), 
  in p_where varchar(8192), 
  in p_order varchar(8192), 
  in p_limit varchar(8192), 
  in p_value varchar(8192) 
)


-------|__/-------------------------
               USAGE
------------------------------------

$) set @v_token = '_'; call mytestorproxy.api_testor_login( @v_token, 'mytestor', 'rzutomqahegpnyx' ); select @v_token;

    ----------------------------

+----------------------------------+
| @v_token                         |
+----------------------------------+
| d01d121b34651750aa7d6a7e97c358cf |
+----------------------------------+

    ----------------------------

$) set @v_suite_id = -1; call mytestorproxy.api_testor_suite( @v_token, @v_suite_id, 'sterry' );

$) call mytestorproxy.api_testor_clean( @v_token, @v_suite_id );

$) set @v_case_id = -1; set @v_suite_id = -1; call mytestorproxy.api_testor_suite_case( @v_token, @v_suite_id, @v_case_id, 'sterry', 'table-users' ); select @v_case_id, @v_suite_id;

    ----------------------------

+------------+-------------+
| @v_case_id | @v_suite_id |
+------------+-------------+
|        180 |           3 |
+------------+-------------+

    ----------------------------

$) set @v_tested_db = 'mytestortested'; 

$) set @v_sql = concat( 'drop temporary table if exists `', trim(@v_tested_db), '`.`temp_vars`;' );
set @v_sql_testor_test_cells = @v_sql;
prepare stmt_testor_test_cells from @v_sql_testor_test_cells;
execute stmt_testor_test_cells;
deallocate prepare stmt_testor_test_cells;

$) set @v_sql = concat( 'create temporary table `', trim(@v_tested_db), '`.`temp_vars` (`id` bigint not null auto_increment primary key, `str_val` varchar(8192) not null default '''', `num_val` double not null default 0);' );
set @v_sql_testor_test_cells = @v_sql;
prepare stmt_testor_test_cells from @v_sql_testor_test_cells;
execute stmt_testor_test_cells;
deallocate prepare stmt_testor_test_cells;

$) set @v_table = concat( '`', trim(@v_tested_db), '`.`temp_vars`' );
set @v_field = '`str_val`';
set @v_where = '';
set @v_order = 'order by `id` asc';
set @v_idx = 0;
set @v_str_a = 'Hello world!';
set @v_str_b = 'world';
set @v_limit = concat( 'limit ', @v_idx, ', 1' );
set @v_sql = concat( 'insert into `', trim(@v_tested_db), '`.`temp_vars` ( `str_val` ) values ( mytestorproxy.api_testor_unescape(''', mytestorproxy.api_testor_escape( @v_str_a ), ''') );' );
set @v_sql_testor_test_cells = @v_sql;
prepare stmt_testor_test_cells from @v_sql_testor_test_cells;
execute stmt_testor_test_cells;
deallocate prepare stmt_testor_test_cells;
call mytestorproxy.api_testor_cell_contains( @v_token, @v_test_id, @v_suite_id, @v_case_id, 'str.contains.1', @v_table, @v_field, @v_where, @v_order, @v_limit, @v_str_b ); select @v_test_id as `test_id`, @v_suite_id as `suite_id`, @v_case_id as `case_id`;

    ----------------------------

+---------+----------+---------+
| test_id | suite_id | case_id |
+---------+----------+---------+
|    2609 |        3 |     180 |
+---------+----------+---------+

    ----------------------------

$) call mytestorproxy.api_testor_finish( @v_token, @v_suite_id );

    ----------------------------

+---------+--------+--------+------+---------------+--------------+------------+------------+
| version | status | code   | id   | success_count | failed_count | test_count | case_count |
+---------+--------+--------+------+---------------+--------------+------------+------------+
| 10      | GREEN  | sterry | 3    | 1             | 0            | 1          | 1          |
+---------+--------+--------+------+---------------+--------------+------------+------------+
1 row in set (0.81 sec)

+------------------------------------------+-----------------------------------------------+
| To re-print:                             | To get source file of [a] test case:          |
+------------------------------------------+-----------------------------------------------+
| $) call api_testor_result('_token_', 3); | $) call api_testor_source('_token_', 3, 'a'); |
+------------------------------------------+-----------------------------------------------+
1 row in set (0.82 sec)

    ----------------------------

$) call mytestorproxy.api_testor_success( @v_token, @v_suite_id, 1 );

    ----------------------------

+-------------+----------------+-------------------------------------------------------------------------------------------+
| case        | test           | message                                                                                   |
+-------------+----------------+-------------------------------------------------------------------------------------------+
| table-users | str.contains.1 | [str.contains.1] test (cell_contains) is success. \nOperand: Hello world!\nValue: world\n |
+-------------+----------------+-------------------------------------------------------------------------------------------+

    ----------------------------

```