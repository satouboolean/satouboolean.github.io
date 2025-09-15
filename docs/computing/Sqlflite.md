---
title: Sqlflite
tags:
  - Flutter
  - Sqlite
categories: programming
---
# Sqlflite
sqflite is a sqlite package for flutter, uses serveless database for flutter support

## Setting up
```
class DatabaseService {
  static Database? _db;
  static final DatabaseService instance = DatabaseService._constructor();
  
    

  Future<Database> get database async {
    if (_db != null) {
      return _db!;
    } else {
      _db = await getDatabase();
      return _db!;
    }
  }
  
    Future<Database> getDatabase() async {
    if (_db != null) return _db!;
    _db = await _initDb();
    return _db!;
  }
  
    Future<Database> _initDb() async {
    final databaseRootPath = await getDatabasesPath();
    final databasePath = join(databaseRootPath, "master_database.db");
    return await openDatabase(
      version: databaseVersion,
      databasePath,
      onCreate: (db, version) {
        createTable(db);
      },
      onUpgrade: (db, oldVersion, newVersion) async {
        if (oldVersion < databaseVersion) {
          // await db.execute("ALTER TABLE $_transactionTableName ADD COLUMN **new column** TEXT")
        }
      },
    );
  }
  
}
```

## Defining Table
```
  final String _reminderTableName = "dateItem";
  final String _reminderIdColumnName = "reminder_id";
  final String _reminderMonthColumnName = "month";
  final String _reminderDayColumnName = "day";
  final String _reminderClockColumnName = "Clock";
  final String _reminderEndTimeColumnName = "endTime";
  final String _reminderTitleColumnName = "title";
  final String _reminderContentColumnName = "content";
  final String _reminderFinishedColumnName = "finished";
  final String _reminderStartRemindDayColumnName = 'remindDay';

  void createReminderTable(Database db) async {
    await db.execute('''
          CREATE TABLE $_reminderTableName(
          $_reminderIdColumnName INTEGER PRIMARY KEY, 
          $_reminderMonthColumnName TEXT NOT NULL, 
          $_reminderDayColumnName TEXT NOT NULL, 
          $_reminderTitleColumnName TEXT NOT NULL,
          $_reminderContentColumnName TEXT, 
          $_reminderClockColumnName TEXT,
          $_reminderEndTimeColumnName TEXT,
          $_reminderStartRemindDayColumnName INTEGER, 
          $_reminderFinishedColumnName INTEGER
          )
          ''');
    viewTable(_reminderTableName);
  }
```