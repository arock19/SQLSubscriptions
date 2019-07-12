USE AlertManagerDB;
GO
/*
CREATE TABLE AlertInfoTable (
	ErrorID INT IDENTITY(1,1) PRIMARY KEY,
	ErrorCode VARCHAR(20),
	Benchmark DECIMAL(3,2)
)
GO

CREATE TABLE DeviceInfoTable (
	MachineID INT IDENTITY(1,1) PRIMARY KEY,
	MachineSerial VARCHAR(20)
	--other data
)
GO

CREATE TABLE AlertEntryTable (
	MachineID INT,
	ErrorID INT,
	EventDate DATE,
	FOREIGN KEY(ErrorID) REFERENCES AlertInfoTable(ErrorID),
	FOREIGN KEY(MachineID) REFERENCES DeviceInfoTable(MachineID)
)
GO

DROP PROCEDURE checkAlert;
GO

CREATE PROCEDURE checkAlert 
@errorID INT,
@machineID INT,
@dateStart DATE,
@dateEnd DATE
AS
DECLARE @errorCount DECIMAL, @benchmark DECIMAL(3,2);

SELECT @errorCount = COUNT(ErrorID) 
FROM AlertEntryTable 
WHERE MachineID = @machineID AND ErrorID = @errorID AND EventDate > @dateStart AND EventDate < @dateEnd;

SELECT @benchmark = Benchmark 
FROM AlertInfoTable
WHERE ErrorID = @errorID;

IF(@errorCount/90 > @benchmark) 
BEGIN
	PRINT @errorCount
	PRINT @machineID
	PRINT @errorID
	PRINT @benchmark
END
GO

DROP PROCEDURE checkAllDevices;
GO
CREATE PROCEDURE checkAllDevices 
@dateStart DATE,
@dateEnd DATE
AS

DECLARE @errorID INT, @machineID INT;

SELECT @machineID = COUNT(MachineID) 
FROM DeviceInfoTable;

WHILE @machineID > 0
BEGIN 

	SELECT @errorID = COUNT(ErrorID)
	FROM AlertInfoTable;

	WHILE @errorID > 0
	BEGIN

		EXEC checkAlert @errorID, @machineID, @dateStart, @dateEnd;

		SET @errorID = @errorID - 1;
		
	END

	SET @machineID = @machineID - 1;

END
GO
*/
--SELECT * FROM AlertInfoTable;
--SELECT * FROM DeviceInfoTable;
--SELECT * FROM AlertEntryTable
/*
INSERT INTO AlertEntryTable VALUES(3, 4, '2019-02-05')
INSERT INTO AlertEntryTable VALUES(1, 3, '2019-01-20')
INSERT INTO AlertEntryTable VALUES(1, 4, '2019-02-21')
INSERT INTO AlertEntryTable VALUES(2, 4, '2019-02-13')
INSERT INTO AlertEntryTable VALUES(3, 2, '2019-01-01')
INSERT INTO AlertEntryTable VALUES(3, 3, '2019-01-15')
*/
EXEC checkAllDevices '2018-01-01' , '2019-03-01'



