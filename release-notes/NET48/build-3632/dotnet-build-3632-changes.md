# .NET Framework Build 3632 Release Notes

The following changes are included in .NET Framework 4.8 build 3632. You can view the full list of [.NET Framework 4.8 changes](/release-notes/NET48/dotnet-48-changes.md) up to and included build 3632.

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## BCL

* Fixed the serialization compatibility issue for CultureAwareComparer class [621387, mscorlib.dll , Bug, Build:3632]

## CLR

* The ‘shadowCopyVerifyByTimestamp’ setting is now configurable for individual appdomains, as opposed to being a process wide setting.  This helps in situations where you may not be the host process, but want to configure a new appdomain that verifys timestamps when shadow copying. [565570, clr.dll, Bug, Build:3632]

## SQL

* Fixed the following issue relevant to SQL: while connecting to Azure SQL DB using .NET 4.7.2, using MultipleActiveResultSets=true in the connection string with System.Data.SqlClient.SqlConnection, async query operations sometimes lead to a bad TDS protocol request stream to be sent from the client, causing the Async Query APIs to fail connection string [624283, System.Data.dll, Bug, Build:3632]

## Windows Forms

* Added support for UIA notification event to ProgressBar class. The feature is available starting with Windows 10, version 1709 (RS3). [581351, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed an issue where read-only Status for DataGridView TextBox column is not announced by Narrator. This change is effective in applications that were recompiled to target .NET framework 4.8 [599936, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed reliability issues in Graphics class when used in RDP sessions. [627739, System.Drawing.dll, Bug, Build:3632]

## WPF

* Addressed the issue of high CPU usage or hangs. This used to happen under certain conditions, where, WPF applications using WindowChromeWorker experience high CPU usage or hangs.  [437642, PresentationFramework.dll, Bug, Build:3632]
* Fixed a bug in the 4.7 algorithm for allocating sizes to *-rows in a Grid.  In some cases (e.g. Grid with Height="Auto" containing empty rows), rows were arranged at the wrong position, possibly outside the Grid altogether. [590061, PresentationFramework.dll, Bug, Build:3632]
* Fixed a potential deadlock in WPF Packaging APIs when multiple threads were both creating and closing large packages simultaneously. [609850, PresentationCore.dll, WindowsBase.dll, Bug, Build:3632]
