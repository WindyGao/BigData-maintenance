# Hbase无法drop table

Version:HDP3.1.0-78

Hbase2.1.6

## 报错

```shell
hbase(main):017:0* disable 'COC_CUSTOMER_GROUP_20201027'

ERROR: Table COC_CUSTOMER_GROUP_20201027 is disabled!

For usage try 'help "disable"'

Took 1.2053 seconds
hbase(main):018:0> drop  'COC_CUSTOMER_GROUP_20201027'

ERROR: Table org.apache.hadoop.hbase.TableNotDisabledException: Not DISABLED; tableName=COC_CUSTOMER_GROUP_20201027, state=ENABLING
        at org.apache.hadoop.hbase.master.HMaster.checkTableModifiable(HMaster.java:2644)
        at org.apache.hadoop.hbase.master.procedure.DeleteTableProcedure.prepareDelete(DeleteTableProcedure.java:238)
        at org.apache.hadoop.hbase.master.procedure.DeleteTableProcedure.executeFromState(DeleteTableProcedure.java:91)
        at org.apache.hadoop.hbase.master.procedure.DeleteTableProcedure.executeFromState(DeleteTableProcedure.java:58)
        at org.apache.hadoop.hbase.procedure2.StateMachineProcedure.execute(StateMachineProcedure.java:189)
        at org.apache.hadoop.hbase.procedure2.Procedure.doExecute(Procedure.java:965)
        at org.apache.hadoop.hbase.procedure2.ProcedureExecutor.execProcedure(ProcedureExecutor.java:1723)
        at org.apache.hadoop.hbase.procedure2.ProcedureExecutor.executeProcedure(ProcedureExecutor.java:1462)
        at org.apache.hadoop.hbase.procedure2.ProcedureExecutor.access$1200(ProcedureExecutor.java:78)
        at org.apache.hadoop.hbase.procedure2.ProcedureExecutor$WorkerThread.run(ProcedureExecutor.java:2039)
 should be disabled!

For usage try 'help "drop"'

Took 0.2507 seconds

```

## 解决办法

```Java
hbase hbck -j hbase-hbck2-1.0.0-SNAPSHOT.jar setTableState 'COC_CUSTOMER_GROUP_20201027' DISABLED
```



新版本hbase  setTableState 参数注释如下

```shell
 setTableState <TABLENAME> <STATE>
   Possible table states: ENABLED, DISABLED, DISABLING, ENABLING
   To read current table state, in the hbase shell run:
     hbase> get 'hbase:meta', '<TABLENAME>', 'table:state'
   A value of \x08\x00 == ENABLED, \x08\x01 == DISABLED, etc.
   An example making table name 'user' ENABLED:
     $ HBCK2 setTableState users ENABLED
   Returns whatever the previous table state was.

```

执行后，表状态正常，可以正常操作