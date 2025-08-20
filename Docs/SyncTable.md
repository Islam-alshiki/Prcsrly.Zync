## TSync Table
#### [back](../README.MD)

### Table creation script
```sql
CREATE TABLE [dbo].[TSync](
	[PartID] [int] NOT NULL,
--	[SyncID] [bigint] NOT NULL,
--	[ExtraSyncID] [int] NOT NULL,
	[JasonData] [nvarchar](max) NULL,
	[Target] [nvarchar](max) NULL,
	[TargetFullName] [nvarchar](max) NULL,
	[SyncType] [int] NOT NULL,
	[syncMode] [int] NOT NULL,
	[SyncStatus] [int] NOT NULL,
	[SyncDirection] [int] NOT NULL,
	[SyncNote] [nvarchar](max) NULL,
	[ReciveDate] [datetime] NULL,
	[AddDate] [datetime] NULL,
	[TargetID] [bigint] NOT NULL DEFAULT ((0)),
	[ID] [bigint] NOT NULL DEFAULT ((0)),
	[DeviceID] [int] NOT NULL DEFAULT ((0)),
	[IsDeleted] [bit] NOT NULL DEFAULT ((0)),
	[Note] [nvarchar](max) NULL,
 CONSTRAINT [PK_dbo.TSync] PRIMARY KEY CLUSTERED 
(
	[ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
```

### TConfiguration Table creation script
```sql
CREATE TABLE [dbo].[TConfiguration](
	[PartID] [bigint] NULL,
	[IsSync] [bit] NOT NULL DEFAULT ('FALSE');
	[IsDebug] [bit] NOT NULL DEFAULT ('FALSE');
	[EndPoint] [string] NOT NULL DEFAULT ('');
);
```

### TMigrations Table creation script
```sql
CREATE TABLE [TMigrations]( 
	[ID] BIGINT NOT NULL PRIMARY KEY ,
	[MigrationName] NVARCHAR(100) NOT NULL,
	[MigrationTimestamp] NVARCHAR(100) NOT NULL,
	[MigrationScript] TEXT NOT NULL,
);
```