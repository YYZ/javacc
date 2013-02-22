javacc
======

A Top-Down Parser with Semantic Analysis for javacc

grammar : 


program := ( decl )*
                    ( function )*
                    main_prog

decl := ( var_decl | const_decl )* 

var_decl := VAR ident_list:type ( , ident_list:type )* ; 

const_decl := CONSTANT identifier:type = expression ( , identifier:type = expression )* ;
              
function := type identifier (param_list)
                   {
                   ( decl )* 
                   ( statement ; )* 
                   return ( expression | ε  ) ;
                   }

param_list := ( identifier:type ( , identifier:type )* | ε  )

type := integer | boolean | real | string | void

main_prog := main
                   {
                   ( decl )* 
                   ( statement ; )* 
                   }

statement := identifier := expression
                | identifier := string
                | !expression
                | ?identifier
                | identifier ( arg_list ) 
                | { ( statement ; )* }
                | IF condition THEN statement
                | IF condition THEN statement ELSE statement
                | WHILE condition DO statement
                | ε 

expression := fragment ( ( + | - | * | / )  fragment )*

fragment := identifier | number | ( + | - ) fragment | expression

condition :=    NOTexpression
                | expression ( = | != | < | > | <= | >=  | AND | OR) expression
                | identifier 

ident_list := identifier ( , identifier )*

arg_list := ( identifier ( , identifier )* | ε  )
