## ID: Breaking Change Title
Turn off call functionality to the JournalReader assembly from Microsoft.Ink namespace

### Scope
Microsoft.Ink Namespace that has Journal Reader assembly (.Net)

### Version Introduced


### Version Reverted


### Source Analyzer Status
Available

### Change Description
Description goes here.

Please refer to #3 below, we'd want to turn off call functionality to the JournalReader assembly from Microsoft.Ink namespace. The best would be to expose an error/ have this section ripped off and have all MSDN related documentation updated. You can also pick up the new note put up for #2 and the fact that the journalreader functionality has been broken since 03/18/2009 with no update or demand to fix (# 6) to aid with the current discussion 

Document Links :
The API that calls into Journal reader has been broken since 2009/03/18 22:46:33.

1)	Tablet PC API, using Journal Reader Component - https://msdn.microsoft.com/en-us/library/windows/desktop/ms700671(v=vs.85).aspx  
 
2)	IJournalReader Interface - https://msdn.microsoft.com/en-us/library/windows/desktop/ms704341(v=vs.85).aspx . A new note has been added to this article recently
Note - The Journal Reader component cannot read Windows Journal files created by machines running Windows 7 or later. The IJournalReader interface should be considered deprecated or obsolete and should not be used.
Requirements section – Minimum supported client - Windows XP Tablet PC Edition [desktop apps only]
 
3)	Microsoft.Ink Namespace that has Journal Reader assembly (.Net) - https://msdn.microsoft.com/en-us/library/microsoft.ink.journalreader(v=vs.90).aspx 

4)	Journal.dll is present on the system only when Ink Support (Desktop Experience) features are enabled. 
 
5)	Journal.dll is gone when Ink Support feature is disabled. 
NOTE : Desktop Experience depends on Ink Support. So if Desktop Experience is enabled, Ink Support is enabled, but if DesktopExperience is disabled, InkSupport will not be disabled automatically.  Users will have to manually disable Inksupport.
 
6)	Details around the Journal reader bug that has been broken since 2009.
 
This bug is introduced by  
BUG: 553636 ar-SA:3849:Windows 7 Client:S:120:Linguistic:Wrong date format 
 
BUG: 553636 
 
BUG 553636: 
Added a DATE_AUTOLAYOUT flag to GetDateFormat 
 
Code Reviewer: pradeem;amitkr 
Buddy Tester: amitsriv 
Change 352360 by FAREAST\sgopale@CHEXBLD045-3 on 2009/03/18 22:46:33 
 
Answer:  The root course is %SDXROOT%\drivers\tablet\Accessories\Journal\App\NBDocument\Stationery.cpp HRESULT CStationery::Date2W(const FILETIME *pfiletime, __deref_out LPWSTR* ppwszDate) 
 
 // call date format again to fill the buffer 
                if (0 == GetDateFormat(LOCALE_USER_DEFAULT, 
                              DATE_SHORTDATE | DATE_AUTOLAYOUT, 
                              &systemtimeLocal, 
                              NULL,           // use local format 
                              pwszTemp, 
                              nCount)) 
This function convert SystemTime to string, but it insert 0x200e(Unicode LeftToRight mark) in string, however OLE, ChangeType() can't recognize 0x200e.  
 


### Recommended Action
The best would be to expose an error/ have this section ripped off and have all MSDN related documentation updated

### Affected APIs
Microsoft.Ink Namespace that has Journal Reader assembly (.Net)

### Category


[More information](LinkForMoreInformation)

<!--
    ### Original Bug
    Bug link goes here
    ### Notes
    Source analyzer status: Not usefully detectable with an analyzer
-->


