## Modethods to use
#### [back](../README.MD)

## How to use this library
You can use this api throwth your `DbConnection` delivers objects like `SqlConnection`, `MySqlConnection`, `SqliteConnection` ... etc, by calloing AddExcuteQuereySync(string query, int deviceid, int partid, SyncModeEnum syncMode = SyncModeEnum.INSERT) that in `Azad.SyncApp.Core.Extentions` namespace.

```csharp
// using Azad.SyncApp.Core.Extentions; You need to use this namespace

// [q]			is your query.
// [deviceid]	        is device id for this pc.
// [partid]		is part id for this center. 
// [connection]         is your SqlConnection object.

// this call add a new record to TSync Table of your database that [connection] object poits to it using your connectionstring.
connection.AddExcuteQuereySync(q, deviceid, partid);
```

## Extra methods
* long GetID() in `Azad.SyncApp.Core.Extentions` namespace, gets a uniqe id used to set in your id columns [NOT-RECOMMENDED]
```csharp
DateTime.Now.GetID();
```
* long GenerateID() in `Azad.SyncApp.Core.Extentions` namespace, gets a uniqe id used to set in your id columns [RECOMMENDED]; check if the id used before or not and bring new one.
```csharp
var id = Zync.GenerateID();
```

## Test Examples
### [DotNet Framework 4.8 Project](../Azad.SyncApp.Test.DotNetFrm)
+ This is example desktop application, it has one form called `Form1`, this form contains two textboxes one for connectionstring and one for query.
+ The query by default is `INSERT INTO TestTable VALUES(@ID@);`, in code behind you will see that `@ID@` just used to be replaced with generated id method ` Zync.GenerateID()`.
```csharp
// here replace "@ID@" with generated uniqe id, to be => INSERT INTO TestTable VALUES(2107021927291643693);
if (Query.Contains("@ID@"))
    Query = Query.Replace("@ID@", Zync.GenerateID().ToString() );

// Create new object of SqlConnection and then create command then assing a query
SqlConnection sqlConnection = new SqlConnection(Connectionstring);
var comm = sqlConnection.CreateCommand();
comm.CommandText = Query;

// open the connection then excute the real query first and save the status in `status` variable.
sqlConnection.Open();
var status = comm.ExecuteNonQuery() > 0;
            
// if the base insert query successed now we can regist it in sync table
if(status)
    // this method add new record in TSync table, MUST BE CREATED FIRST.
    sqlConnection.AddSQlExcuteQuerySync(Query, 0, 0, Core.Enums.SyncModeEnum.INSERT);

// close connection
sqlConnection.Close();
```
