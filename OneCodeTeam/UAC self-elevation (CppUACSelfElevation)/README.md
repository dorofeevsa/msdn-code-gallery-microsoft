# UAC self-elevation (CppUACSelfElevation)
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- Windows SDK
## Topics
- Security
- UAC
- Integrity Level
## Updated
- 03/01/2012
## Description

<h1><span style="font-family:������">WIN32 APPLICATION</span> (<span style="font-family:������">CppUACSelfElevation</span>)</h1>
<h2>Introduction</h2>
<h2><span style="font-size:11.0pt; line-height:115%; font-family:&quot;Calibri&quot;,&quot;sans-serif&quot;; font-weight:normal">User Account Control (UAC) is a new security component in Windows Vista and newer operating systems. With UAC fully enabled, interactive administrators
 normally run with least user privileges. This example demonstrates how to check the privilege level of the current process, and how to self-elevate the process by giving explicit consent with the Consent UI.</span><span style="font-size:11.0pt; line-height:115%; font-family:&quot;Calibri&quot;,&quot;sans-serif&quot;; font-weight:normal">
</span></h2>
<h2><span style="">Compiling the code </span></h2>
<p class="MsoNormal"><span style="">You must run this sample on Windows Vista or newer operating systems.
</span></p>
<h2>Running the Sample</h2>
<p class="MsoNormal">Step1. After you successfully build the sample project in Visual Studio 2010, you will get an application: CppUACSelfElevation.exe.
</p>
<p class="MsoNormal">Step2. Run the application as a protected administrator on a Windows Vista or Windows 7 system with UAC fully enabled. The application should display the following main dialog.
</p>
<p class="MsoNormal"><span style=""><img src="53127-image.png" alt="" width="271" height="191" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">There is a UAC shield icon on the Self-elevate button.
</span></p>
<p class="MsoNormal">Step3. Click on the Self-elevate button. You will see a Consent UI.
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>User Account Control </p>
<p class="MsoNormal"><span style="">&nbsp; </span>----------------------------------
</p>
<p class="MsoNormal">Do you want to allow the following program from an unknown publisher to
<span style="">&nbsp;</span>make changes to this computer? </p>
<p class="MsoNormal">Step4. Click Yes to approve the elevation. The original application will then be started and display the following content on the main dialog.
</p>
<p class="MsoNormal"><span style=""><img src="53128-image.png" alt="" width="271" height="191" align="middle">
</span></p>
<p class="MsoNormal">The Self-elevate button on the dialog does not have the UAC shield icon this time. That is, the application is running as elevated administrator. The
</p>
<p class="MsoNormal">elevation succeeds. If you click on the Self-elevate button again, the application will tell you that it is running as administrator.
</p>
<p class="MsoNormal">Step5. Click OK to close the application.</p>
<h2>Using the Code</h2>
<h3>Step1. Create a basic VC&#43;&#43; Win32 dialog based application </h3>
<p class="MsoNormal">Create a new Visual C&#43;&#43; / Win32 / Win32 Project. Name it as CppUACSelfElevation and set the Application type to Windows application in the Application Settings page.
<span style=""></span></p>
<p class="MsoNormal">After the project is created, disable Precompiled Headers in Project Properties / Configuration Properties / C/C&#43;&#43; / Precompiled Headers. In Resource View, delete all default accelerator<span style="">s</span>,
<span style="">d</span>ialog<span style="">s </span>, icon<span style="">s</span>, menu<span style="">s</span>, and string table resources because they are not necessary in this example.<span style="">
</span></p>
<p class="MsoNormal">Next, insert a dialog resource with the ID: IDD_MAINDIALOG. It serves as the main dialog of the Windows application. In Solution Explorer, delete the wizard-generated files stdafx.cpp,<span style="">
</span>stdafx.h, </p>
<p class="MsoNormal">targetver.h,<span style=""> </span><span style="">&nbsp;</span>CppUACSelfElevation.h,
<span style=""><span style="">&nbsp;</span></span>CppUACSelfElevation.ico, and small.ico to simplify the project files. Open CppUACSelfElevation.cpp and replace its content with the following code, which delineate the skeleton of a VC&#43;&#43; Win32 dialog based application.
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C&#43;&#43;</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">cplusplus</span>

<pre id="codePreview" class="cplusplus">
#include &lt;stdio.h&gt;
#include &lt;windows.h&gt;
#include &lt;windowsx.h&gt;
#include &quot;Resource.h&quot;


BOOL OnInitDialog(HWND hWnd, HWND hwndFocus, LPARAM lParam)
{
    return TRUE;
}
void OnCommand(HWND hWnd, int id, HWND hwndCtl, UINT codeNotify)
{
    switch (id)
    {
    case IDOK:
    case IDCANCEL:
        EndDialog(hWnd, 0);
        break;
    }
}
void OnClose(HWND hWnd)
{
    EndDialog(hWnd, 0);
}
INT_PTR CALLBACK DialogProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
    switch (message)
    {
        HANDLE_MSG (hWnd, WM_INITDIALOG, OnInitDialog);
        HANDLE_MSG (hWnd, WM_COMMAND, OnCommand);
        HANDLE_MSG (hWnd, WM_CLOSE, OnClose);


    default:
        return FALSE;
    }
    return 0;
}
int APIENTRY wWinMain(HINSTANCE hInstance,
                      HINSTANCE hPrevInstance,
                      LPWSTR    lpCmdLine,
                      int       nCmdShow)
{
    return DialogBox(hInstance, MAKEINTRESOURCE(IDD_MAINDIALOG), NULL, DialogProc);
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"></p>
<p class="MsoNormal">Step2. Add controls to the main dialog<span style=""> </span>
</p>
<table class="MsoTableGrid" border="1" cellspacing="0" cellpadding="0" style="border-collapse:collapse; border:none">
<tbody>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"><b style="">Type</b><b style=""><span style=""> </span></b></p>
</td>
<td width="198" valign="top" style="width:148.8pt; border:solid windowtext 1.0pt; border-left:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"><b style="">ID</b><b style=""><span style=""> </span></b></p>
</td>
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-left:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"><b style="">Caption</b><b style=""><span style=""> </span>
</b></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border:solid windowtext 1.0pt; border-left:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"><b style="">Use </b></p>
</td>
</tr>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-top:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Button<span style=""> </span></p>
</td>
<td width="198" valign="top" style="width:148.8pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">IDC_ELEVATE_BN<span style=""> </span></p>
</td>
<td width="197" valign="top" style="width:147.6pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">&quot;Self-elevate&quot;<span style="">&nbsp; </span><span style=""></span></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Elevate the process if it is not run as administrator.</p>
</td>
</tr>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-top:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Static Text</p>
</td>
<td width="198" valign="top" style="width:148.8pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">IDC_INADMINGROUP_STATIC<span style=""> </span></p>
</td>
<td width="197" valign="top" style="width:147.6pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Display whether the primary access token of the process belongs to
<span style="">&nbsp;</span>user account that is a member of the local Administrators group, even if it
<span style="">&nbsp;</span>currently is not elevated</p>
</td>
</tr>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-top:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Static Text</p>
</td>
<td width="198" valign="top" style="width:148.8pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">IDC_ISRUNASADMIN_STATIC</p>
</td>
<td width="197" valign="top" style="width:147.6pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Display whether the application is run as administrator</p>
</td>
</tr>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-top:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Static Text</p>
</td>
<td width="198" valign="top" style="width:148.8pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">IDC_ISELEVATED_STATIC</p>
</td>
<td width="197" valign="top" style="width:147.6pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Display whether the process is elevated or not. Token elevation is
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>only available on Windows Vista and newer operating systems. The label
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>shows N/A on systems prior to Windows Vista</p>
</td>
</tr>
<tr style="">
<td width="197" valign="top" style="width:147.6pt; border:solid windowtext 1.0pt; border-top:none; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Static Text</p>
</td>
<td width="198" valign="top" style="width:148.8pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">IDC_IL_STATIC</p>
</td>
<td width="197" valign="top" style="width:147.6pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal"></p>
</td>
<td width="428" valign="top" style="width:321.05pt; border-top:none; border-left:none; border-bottom:solid windowtext 1.0pt; border-right:solid windowtext 1.0pt; padding:0cm 5.4pt 0cm 5.4pt">
<p class="MsoNormal">Display the integrity level of the current process. Integrity level is
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>only available on Windows Vista and newer operating systems. The label
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>shows N/A on systems prior to Windows Vista</p>
</td>
</tr>
</tbody>
</table>
<p class="MsoNormal"><span style=""></span></p>
<p class="MsoNormal">Step3. Check and display the current process's &quot;run as administrator&quot; status, elevation information and integrity level when the application initializes the main dialog.
</p>
<p class="MsoNormal">Create the following four helper functions: </p>
<p class="MsoNormal">BOOL IsUserInAdminGroup(); </p>
<p class="MsoNormal">BOOL IsRunAsAdmin(); </p>
<p class="MsoNormal">BOOL IsProcessElevated(); </p>
<p class="MsoNormal">DWORD GetProcessIntegrityLevel(); </p>
<p class="MsoNormal">In OnInitDialog of the main dialog, check and display the &quot;run as administrator&quot; status, the elevation information, and the integrity level of the current process.
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C&#43;&#43;</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">cplusplus</span>

<pre id="codePreview" class="cplusplus">
// Get and display whether the primary access token of the process 
// belongs to user account that is a member of the local Administrators 
// group even if it currently is not elevated (IsUserInAdminGroup).
HWND hInAdminGroupLabel = GetDlgItem(hWnd, IDC_INADMINGROUP_STATIC);
try
{
    BOOL const fInAdminGroup = IsUserInAdminGroup();
    SetWindowText(hInAdminGroupLabel, fInAdminGroup ? L&quot;True&quot; : L&quot;False&quot;);
}
catch (DWORD dwError)
{
    SetWindowText(hInAdminGroupLabel, L&quot;N/A&quot;);
    ReportError(L&quot;IsUserInAdminGroup&quot;, dwError);
}


// Get and display whether the process is run as administrator or not 
// (IsRunAsAdmin).
HWND hIsRunAsAdminLabel = GetDlgItem(hWnd, IDC_ISRUNASADMIN_STATIC);
try
{
    BOOL const fIsRunAsAdmin = IsRunAsAdmin();
    SetWindowText(hIsRunAsAdminLabel, fIsRunAsAdmin ? L&quot;True&quot; : L&quot;False&quot;);
}
catch (DWORD dwError)
{
    SetWindowText(hIsRunAsAdminLabel, L&quot;N/A&quot;);
    ReportError(L&quot;IsRunAsAdmin&quot;, dwError);
}


// Get and display the process elevation information (IsProcessElevated) 
// and integrity level (GetProcessIntegrityLevel). The information is not 
// available on operating systems prior to Windows Vista.


HWND hIsElevatedLabel = GetDlgItem(hWnd, IDC_ISELEVATED_STATIC);
HWND hILLabel = GetDlgItem(hWnd, IDC_IL_STATIC);


OSVERSIONINFO osver = { sizeof(osver) };
if (GetVersionEx(&osver) && osver.dwMajorVersion &gt;= 6)
{
    // Running Windows Vista or later (major version &gt;= 6).


    try
    {
        // Get and display the process elevation information.
        BOOL const fIsElevated = IsProcessElevated();
        SetWindowText(hIsElevatedLabel, fIsElevated ? L&quot;True&quot; : L&quot;False&quot;);


        // Update the Self-elevate button to show the UAC shield icon on 
        // the UI if the process is not elevated. The 
        // Button_SetElevationRequiredState macro (declared in Commctrl.h) 
        // is used to show or hide the shield icon in a button. You can 
        // also get the shield directly as an icon by calling 
        // SHGetStockIconInfo with SIID_SHIELD as the parameter.
        HWND hElevateBtn = GetDlgItem(hWnd, IDC_ELEVATE_BN);
        Button_SetElevationRequiredState(hElevateBtn, !fIsElevated);
    }
    catch (DWORD dwError)
    {
        SetWindowText(hIsElevatedLabel, L&quot;N/A&quot;);
        ReportError(L&quot;IsProcessElevated&quot;, dwError);
    }


    try
    {
        // Get and display the process integrity level.
        DWORD const dwIntegrityLevel = GetProcessIntegrityLevel();
        switch (dwIntegrityLevel)
        {
        case SECURITY_MANDATORY_UNTRUSTED_RID: SetWindowText(hILLabel, L&quot;Untrusted&quot;); break;
        case SECURITY_MANDATORY_LOW_RID: SetWindowText(hILLabel, L&quot;Low&quot;); break;
        case SECURITY_MANDATORY_MEDIUM_RID: SetWindowText(hILLabel, L&quot;Medium&quot;); break;
        case SECURITY_MANDATORY_HIGH_RID: SetWindowText(hILLabel, L&quot;High&quot;); break;
        case SECURITY_MANDATORY_SYSTEM_RID: SetWindowText(hILLabel, L&quot;System&quot;); break;
        default: SetWindowText(hILLabel, L&quot;Unknown&quot;); break;
        }
    }
    catch (DWORD dwError)
    {
        SetWindowText(hILLabel, L&quot;N/A&quot;);
        ReportError(L&quot;GetProcessIntegrityLevel&quot;, dwError);
    }
}
else
{
    SetWindowText(hIsElevatedLabel, L&quot;N/A&quot;);
    SetWindowText(hILLabel, L&quot;N/A&quot;);
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step4. Handle the click event of the Self-elevate button in OnCommand. When user clicks the button, elevate the process by calling ShellExecuteEx with SHELLEXECUTEINFO.lpVerb = L&quot;runas&quot; to restart itself if the process is not
 run as administrator. </p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C&#43;&#43;</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">cplusplus</span>

<pre id="codePreview" class="cplusplus">
void OnCommand(HWND hWnd, int id, HWND hwndCtl, UINT codeNotify)
{
    switch (id)
    {
    case IDC_ELEVATE_BN:
        {
            // Check the current process's &quot;run as administrator&quot; status
            BOOL fIsRunAsAdmin;
            try
            {
                fIsRunAsAdmin = IsRunAsAdmin();
            }
            catch (DWORD dwError)
            {
                ReportError(L&quot;IsRunAsAdmin&quot;, dwError);
                break;
            }


            // Elevate the process if it is not run as administrator.
            if (!fIsRunAsAdmin)
            {
                wchar_t szPath[MAX_PATH];
                if (GetModuleFileName(NULL, szPath, ARRAYSIZE(szPath)))
                {
                    // Launch itself as administrator.
                    SHELLEXECUTEINFO sei = { sizeof(sei) };
                    sei.lpVerb = L&quot;runas&quot;;
                    sei.lpFile = szPath;
                    sei.hwnd = hWnd;
                    sei.nShow = SW_NORMAL;


                    if (!ShellExecuteEx(&sei))
                    {
                        DWORD dwError = GetLastError();
                        if (dwError == ERROR_CANCELLED)
                        {
                            // The user refused the elevation.
                            // Do nothing ...
                        }
                        else
                        {
                            ReportError(L&quot;ShellExecuteEx&quot;, dwError);
                        }
                    }
                    else
                    {
                        EndDialog(hWnd, TRUE);  // Quit itself
                    }
                }
            }
            else
            {
                MessageBox(hWnd, L&quot;The process is running as administrator&quot;, L&quot;UAC&quot;, MB_OK);
            }
        }
        break;
    }
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"></p>
<p class="MsoNormal">Step5. Automatically elevate the process when it's started up.
</p>
<p class="MsoNormal">If your application always requires administrative privileges, such as during an installation step, the operating system can automatically prompt the user for privileges elevation each time your application is invoked. If a specific kind
 of resource (RT_MANIFEST) is found embedded within the application executable, the system looks for the &lt;trustInfo&gt; section and parses its contents. Here is an example of this section in the manifest file:
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>XML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">xml</span>

<pre id="codePreview" class="xml">
&lt;trustInfo xmlns=&quot;urn:schemas-microsoft-com:asm.v2&quot;&gt;
   &lt;security&gt;
      &lt;requestedPrivileges&gt;
         &lt;requestedExecutionLevel
            level=&quot;requireAdministrator&quot;
         /&gt;
      &lt;/requestedPrivileges&gt;
   &lt;/security&gt;
&lt;/trustInfo&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"></p>
<p class="MsoNormal">Three different values are possible for the level attribute
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>a) <span class="GramE">requireAdministrator</span>
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>The application must be started with Administrator privileges; it won't run otherwise.
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>b) <span class="GramE">highestAvailable</span>
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>The application is started with the highest possible privileges.<span style="">&nbsp;
</span>If the user is logged on with an Administrator account, an elevation prompt appears. If the user is a Standard User, the application is started
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>(<span class="GramE">without</span> any elevation prompt) with these standard privileges.
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>c) <span class="GramE">asInvoker</span>
</p>
<p class="MsoNormal"><span style="">&nbsp; </span>The application is started with the same privileges as the calling application.<span style="">
</span>To configure the elevation level in a VC&#43;&#43; project, open the project's properties dialog, turn to Linker /Manifest File, and select UAC Execution Level.
</p>
<h2>More Information </h2>
<p class="MsoListParagraphCxSpFirst" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/aa511445.aspx">MSDN: User Account Control</a>
</p>
<p class="MsoListParagraphCxSpMiddle" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/bb530410.aspx">MSDN: Windows Vista Application Development Requirements for User Account Control Compatibility</a>
</p>
<p class="MsoListParagraphCxSpMiddle" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/ms995339.aspx">MSDN: Windows NT Security</a>
</p>
<p class="MsoListParagraphCxSpLast" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://blogs.msdn.com/junfeng/archive/2007/01/26/how-to-tell-if-the-current-user-is-in-administrators-group-programmatically.aspx">How to tell if the current user is in administrators group programmatically</a></p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
