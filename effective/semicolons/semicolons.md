1. GO与C一样，使用分号来结束语句。但是和C不同的是，分号并不会在源码中出现，词法分析器会使用一条简单的规则来自动插入分号

2. 词法分析器会在语句的末尾插入分号, 语句的末尾标识符可以概括为

   ```go
   break 
   continue 
   fallthrough 
   return 
   ++ 
   -- 
   ) 
   }
   ```

3. 在一行中写多个语句，也需要使用分号隔开

