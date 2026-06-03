```
===========_____=======_============
  _ __ _  |_   _|__ __| |_ ___ _ _ 
 | '  \ || || |/ -_|_-<  _/ _ \ '_|
 |_|_|_\_, ||_|\___/__/\__\___/_|  
=======|__/=========================
  API References of myTestorProxy
           ----- oOo -----
  [procedure] api_testor_pattern
====================================


-------|__/-------------------------
               SYNTAX
------------------------------------

procedure mytestorproxy.api_testor_pattern (
  in p_module varchar(64),
  in p_kind varchar(36),
  in p_code varchar(600),
  in p_variant varchar(40)
  out p_pattern longtext
)


    ----------------------------
             p_module
    ----------------------------

+ 'mytestor'
+ 'mytestorproxy'


    ----------------------------
              p_kind
    ----------------------------

+ 'table'
+ 'function'
+ 'procedure'


    ----------------------------
             p_variant
    ----------------------------

+ 'scrp'
+ 'proc'
+ '_'


-------|__/-------------------------
               USAGE
------------------------------------


$) set @v_pattern = '_'; call mytestorproxy.api_testor_pattern( 'mytestor', 'procedure', 'api_testor_login', 'scrp', @v_pattern ); select @v_pattern as `pattern`\G

    ----------------------------

*************************** 1. row ***************************
pattern: 
set @v_token = '_';
set @v_username = 'mytestor';
set @v_password = 'rzutomqahegpnyx';
call api_testor_login( @v_token, @v_username, @v_password ); select @v_token as `Token`;
call api_testor_logout( @v_token );

    ----------------------------
```
